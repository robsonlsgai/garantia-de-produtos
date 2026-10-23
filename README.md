# 🛡️ Garantia de Produtos: nunca mais perca uma garantia! ⏰

> 🎯 **Desafio Criativo DIO** · Planejando automações com N8N usando apenas bons prompts

Sabe aquela geladeira que deu defeito **uma semana depois** de a garantia acabar? 😩
Pois é... esse projeto nasceu para que isso **nunca mais** aconteça! 💚

A ideia é simples: uma automação no **N8N** que fica de olho na data de compra dos seus produtos e te avisa **antes** de a garantia vencer. Assim dá tempo de acionar a loja ou o fabricante com tranquilidade. 😌✨

---

## 🧭 Como cheguei até aqui

Um bom prompt nasce de **intenção clara + contexto + instruções específicas**. Por isso, construí o prompt em três passos, peça por peça 🧩:

| Passo | O que defini |
|:---:|---|
| 1️⃣ | 💡 **O quê** automatizar e **para quem** |
| 2️⃣ | 🔧 **Ferramentas**, **fluxo** e **regras** |
| 3️⃣ | 🚀 O **prompt final**, juntando tudo |

---

## 1️⃣ Passo 1: A automação dos sonhos 💡

🎯 **Qual tarefa repetitiva?** Lembrar quando a garantia de cada produto vai acabar (ninguém merece ficar caçando nota fiscal! 🧾).
👥 **Quem se beneficia?** Qualquer pessoa que cadastra seus produtos em uma planilha.
🏁 **Resultado esperado?** Um e-mail amigável 30 e 7 dias antes do fim da garantia 📬, e a planilha atualizada sozinha ✅.

```text
Quero criar uma automação no N8N para avisar o cliente quando a garantia de um produto estiver perto de vencer.
Público ou responsável:
Pessoas que cadastraram seus produtos em uma planilha de controle de garantias.
Resultado esperado:
A pessoa recebe um e-mail 30 dias e 7 dias antes do fim da garantia, e a planilha registra que o aviso foi enviado.
```

---

## 2️⃣ Passo 2: Contexto e regras do jogo 🔧

🧰 **Ferramentas:** 📊 Google Sheets · 📧 Gmail · 📅 Google Calendar

🔄 **O fluxo, passo a passo:**

1. ☀️ Todo dia às 8h, a automação acorda e lê a planilha.
2. 🧮 Calcula quantos dias faltam para a garantia acabar.
3. 📬 Faltando 30 ou 7 dias? Manda um e-mail com produto, loja e data final.
4. 📅 Cria um lembrete no Google Calendar no dia em que a garantia termina.
5. ✅ Marca na planilha que o aviso foi enviado.

🚦 **Regras importantes:**

- 🚫 Sem e-mail válido ou sem data de compra? A linha é ignorada.
- 🔁 Nada de spam: cada aviso é enviado **uma única vez**.
- ⌛ Garantia já vencida? Recebe o status "vencida" e não gera e-mail.

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

---

## 3️⃣ Passo 3: O prompt final 🚀

Chegou a hora de juntar todas as peças! 🧩➡️🖼️
É só copiar, colar na sua IA favorita 🤖 e ver a mágica acontecer ✨

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

---

## 🎁 Bônus: o workflow pronto para usar!

Fui além do prompt e montei o workflow completo 😎. Ele está na pasta [`workflow/`](workflow/), com um [guia de importação](workflow/como-usar-workflow-garantia.md) passo a passo.

```
⏰ Agenda (8h) ➜ 📊 Lê a planilha ➜ 🧮 Calcula ➜ 🔀 Decide o aviso
                                                   ├─ 📬 30 dias ➜ 📅 Calendar ➜ ✅ Marca
                                                   ├─ ⚠️ 7 dias  ➜ ✅ Marca
                                                   └─ ⌛ Vencida ➜ 🏷️ Marca status
```

| Nó do N8N | O que ele faz |
|---|---|
| ⏰ Schedule Trigger | Dispara todos os dias às 8h |
| 📊 Google Sheets (ler) | Lê os produtos cadastrados |
| 🧮 Code | Valida os dados e calcula os dias restantes |
| 🔀 Switch | Separa aviso de 30 dias, de 7 dias e garantia vencida |
| 📧 Gmail | Envia o e-mail de aviso |
| 📅 Google Calendar | Cria o lembrete na data final |
| ✅ Google Sheets (atualizar) | Marca o aviso como enviado |

---

## 💭 O que aprendi

✨ Um prompt bem estruturado faz toda a diferença: quanto mais **claro** o objetivo, o **contexto** e as **regras**, mais certeira é a resposta da IA.
🧠 Pensar nas exceções antes (e-mail inválido, aviso repetido, garantia vencida) evita dor de cabeça depois!

---

<p align="center">
Feito com 💚 e muito ☕ para o <b>Desafio Criativo da DIO</b> 🚀
</p>
