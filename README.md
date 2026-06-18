# Placar Certo — Brasil x Haiti

Landing page de palpite premiado. Acerte o **placar exato** e o **1º jogador a marcar** em Brasil x Haiti (19/06/2026) e leve **R$500 no Pix**. A participação é condicionada ao cadastro em uma casa de aposta pelo link de afiliado do **Rayo**, comprovado pelo print do e-mail de boas-vindas.

Campanha da **Arena / Dupla**.

## Arquivos

- `index.html` — landing page autocontida (abre direto no navegador, sem build).
- `placarcerto.png` — criativo de herói (story Brasil x Haiti).
- `PRD.md` — documento de produto (mecânica, fluxo, stack, decisões abertas).

## Como rodar

Abra `index.html` no navegador. Não precisa de build nem servidor.

## Pendências (antes de ir ao ar)

1. **Links de afiliado** das casas — editar o array `CASAS` no `<script>` do `index.html`.
2. **Elenco do Brasil** — conferir o array `PLAYERS`.
3. **Back-end** — o envio ainda é só front-end. Falta a rota que grava o `created_at` do **servidor** (decide o vencedor) e sobe o print pro storage. Stack alvo: Next 15 + Vercel + Supabase.
4. **Regra do 0x0** — definir no regulamento/FAQ.

## Regra do prêmio

R$500 no Pix para o **primeiro** participante que acertar placar + 1º marcador **e** tiver cadastro comprovado. Desempate = ordem de envio (timestamp do servidor). Participações encerram no apito inicial.
