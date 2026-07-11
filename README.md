# 🍕 Controle Pizza

Sistema de gestão financeira do delivery de pizza. Simples de propósito.

**Acesse:** https://orodrigao.github.io/controle-pizza/

**Login:** e-mail `rodrigao@gmail.com` com a mesma senha do ERP da Pane&Salute (o login é o mesmo Supabase).

## O que dá pra fazer

- **💵 Lançar** — registrar as vendas do dia, separadas em **Loja/Balcão** e **iFood**.
- **📋 Contas** — cadastrar contas a pagar com categoria e vencimento, marcar como pagas com um toque. Contas vencidas ficam destacadas em vermelho.
- **📊 DRE** — resultado do mês calculado automaticamente: receita bruta, taxas, CMV (insumos + embalagens), pessoal, contas fixas e o lucro/prejuízo final com margem.
- **🏷️ Categorias** — criar novas categorias de gasto; cada uma diz em qual linha do DRE ela entra.

## Como o DRE é montado

```
  Vendas Loja + Vendas iFood        = RECEITA BRUTA
  (–) Taxas e impostos              = RECEITA LÍQUIDA
  (–) Ingredientes e embalagens     = LUCRO BRUTO
  (–) Pessoal
  (–) Contas fixas
  (–) Outras despesas               = RESULTADO DO MÊS
```

As despesas entram no mês do **vencimento** (regime de competência). Contas ainda não pagas do mês já são descontadas do resultado, e o DRE avisa quanto ainda está pendente.

## Infraestrutura

- **Hospedagem:** GitHub Pages (este repositório, arquivo único `index.html`).
- **Banco e login:** Supabase, projeto `PanePedidosLojas` (`gohluceldchoitihrimw`), tabelas com prefixo `pizza_` isoladas do ERP.
- **Segurança:** Row Level Security em todas as tabelas — só e-mails cadastrados em `pizza_usuarios` acessam os dados. Para dar acesso a outra pessoa, insira o e-mail dela nessa tabela (a pessoa também precisa ter login no Supabase Auth do projeto).

## Tabelas

| Tabela | O que guarda |
|---|---|
| `pizza_vendas` | entradas de dinheiro por dia e canal (`loja` / `ifood`) |
| `pizza_despesas` | contas a pagar: descrição, categoria, valor, vencimento, pago |
| `pizza_categorias` | categorias de gasto e o grupo do DRE (`cmv`, `taxas`, `pessoal`, `fixas`, `outros`) |
| `pizza_usuarios` | e-mails autorizados a usar o sistema |
