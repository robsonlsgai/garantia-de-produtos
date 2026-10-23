# Workflow "Garantia": como importar e usar

Arquivo do workflow: `workflow-garantia.json`

## 1. Preparar a planilha (Google Sheets)

Crie uma planilha com uma aba chamada **Produtos** e esta primeira linha de cabeçalho:

| produto | loja | email | data_compra | meses_garantia | aviso_30 | aviso_7 | status |
|---|---|---|---|---|---|---|---|
| Geladeira | Loja Exemplo | cliente@email.com | 15/11/2025 | 12 | | | |

- `data_compra` no formato **dd/mm/aaaa** (formate a coluna como texto simples para evitar conversões).
- As colunas `aviso_30`, `aviso_7` e `status` começam vazias; o workflow preenche.

## 2. Importar no N8N

1. No N8N, crie um workflow novo, clique nos três pontinhos e escolha **Import from File** (ou cole o conteúdo do JSON na tela).
2. Crie as credenciais **Google Sheets**, **Gmail** e **Google Calendar** (OAuth2 da sua conta Google) e selecione-as em cada nó.
3. Nos nós **Ler produtos**, **Marcar aviso 30**, **Marcar aviso 7** e **Marcar vencida**, troque `COLE_AQUI_O_ID_DA_PLANILHA` pelo ID da sua planilha (o trecho da URL entre `/d/` e `/edit`).
4. Clique em **Test workflow** para rodar uma vez e, depois, ative o workflow.

## 3. Nós e lógica do workflow

| Nó | Tipo | O que faz |
|---|---|---|
| Todo dia às 8h | Schedule Trigger | Dispara diariamente às 8h (fuso America/Sao_Paulo). |
| Ler produtos | Google Sheets | Lê todas as linhas da aba Produtos. |
| Calcular garantia | Code | Valida e-mail e data, calcula data final (compra + meses) e dias restantes, e define a ação: `aviso_30`, `aviso_7` ou `vencida`. |
| Qual aviso? | Switch | Separa os itens pelos três caminhos. |
| E-mail 30 dias / E-mail 7 dias | Gmail | Envia o aviso com produto, loja e data final. |
| Evento no Calendar | Google Calendar | Cria um evento na data final da garantia e convida o cliente (só no aviso de 30 dias). |
| Marcar aviso 30 / 7 / vencida | Google Sheets (update) | Grava "enviado" ou "vencida" na linha, usando `row_number`, para não repetir avisos. |

**Regras aplicadas no nó Code:**
- Linhas sem e-mail válido ou sem data de compra são ignoradas.
- Avisos já marcados como "enviado" não são reenviados.
- O aviso de 30 dias vale para quem está entre 8 e 30 dias do fim, e o de 7 dias para quem está a 7 dias ou menos. Assim, se o workflow ficar um dia sem rodar, o aviso não se perde.
- Garantias vencidas recebem status "vencida" e não geram e-mail.
