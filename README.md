# Desafio Criativo DIO: Alerta de garantia com N8N

Automação planejada a partir de um prompt estruturado em três passos: definir a automação, adicionar contexto e regras, e montar o prompt final.


## Passo 1: Automação desejada
```text
Quero criar uma automação no N8N para avisar o cliente quando a garantia de um produto estiver perto de vencer.
Público ou responsável:
Pessoas que cadastraram seus produtos em uma planilha de controle de garantias.
Resultado esperado:
A pessoa recebe um e-mail 30 dias e 7 dias antes do fim da garantia, e a planilha registra que o aviso foi enviado.
```

## Passo 2: Contexto e regras
```text
Ferramentas envolvidas:
Google Sheets (cadastro de produtos), Gmail e Google Calendar.
Fluxo desejado:
1. Todos os dias às 8h, ler a planilha de produtos cadastrados.
2. Calcular quantos dias faltam para o fim da garantia (data da compra + meses de garantia).
3. Se faltarem 30 ou 7 dias, enviar um e-mail com nome do produto, loja e data final da garantia.
4. Criar um evento no Google Calendar na data final da garantia.
5. Marcar na planilha a coluna "aviso_30" ou "aviso_7" como enviado.
Regras importantes:
Ignorar linhas sem e-mail válido ou sem data de compra.
Não enviar o mesmo aviso duas vezes (checar as colunas de controle).
Garantias já vencidas recebem status "vencida" e não geram e-mail.
```

## Passo 3: Prompt final
```text
Atue como um especialista em N8N.
Crie uma automação para avisar quando a garantia de um produto estiver perto de vencer.
Público:
Pessoas que cadastraram seus produtos em uma planilha de controle de garantias.
Ferramentas envolvidas:
Google Sheets, Gmail e Google Calendar.
Fluxo:
1. Todos os dias às 8h, ler a planilha de produtos (colunas: produto, loja, email, data_compra, meses_garantia, aviso_30, aviso_7, status).
2. Calcular a data final da garantia (data_compra + meses_garantia) e os dias restantes.
3. Quando faltarem 30 ou 7 dias, enviar um e-mail com produto, loja e data final.
4. Criar um evento no Google Calendar na data final da garantia (apenas no aviso de 30 dias).
5. Atualizar a planilha marcando aviso_30 ou aviso_7 como "enviado".
Regras:
- Ignorar linhas sem e-mail válido ou sem data de compra.
- Não repetir avisos já marcados como "enviado".
- Garantias já vencidas recebem status "vencida" e não geram e-mail.
Explique quais nós do N8N devem ser utilizados e a lógica de funcionamento do workflow.
```

## Bônus: workflow N8N gerado a partir do prompt

| Nó | Função |
|---|---|
| Schedule Trigger | Dispara todos os dias às 8h |
| Google Sheets (ler) | Lê os produtos cadastrados |
| Code | Valida os dados, calcula a data final e os dias restantes |
| Switch | Separa aviso de 30 dias, aviso de 7 dias e garantia vencida |
| Gmail | Envia o e-mail de aviso |
| Google Calendar | Cria o evento na data final da garantia |
| Google Sheets (atualizar) | Marca o aviso como enviado ou a garantia como vencida |
