# Placar Certo — Brasil x Haiti

Landing page de palpite premiado. Acerte o **placar exato** e o **1º jogador a marcar** em Brasil x Haiti (19/06/2026) e leve **R$500 no Pix**. A participação é condicionada ao cadastro em uma casa de aposta pelo link de afiliado do **Rayo**, comprovado pelo print do e-mail de boas-vindas.

Campanha da **Arena / Dupla**.

## Arquivos

- `index.html` — landing page autocontida (abre direto no navegador, sem build).
- `img/placarcerto.png` — criativo de herói (story Brasil x Haiti).
- `apps-script/Code.gs` — back-end de uma linha (grava os leads na planilha Google).
- `SETUP-PLANILHA.md` — passo a passo pra ligar a planilha.
- `PRD.md` — documento de produto (mecânica, fluxo, stack, decisões abertas).

## Como rodar

Abra `index.html` no navegador. Não precisa de build nem servidor.

## Pendências (antes de ir ao ar)

1. **Links de afiliado** das casas — editar o array `CASAS` no `<script>` do `index.html`.
2. **Elencos** — conferir os arrays `BRASIL` e `HAITI`.
3. **Planilha de leads** — seguir o `SETUP-PLANILHA.md` e colar a URL em `SCRIPT_URL`. Sem isso, o envio fica em modo demo (não grava). O timestamp do vencedor é carimbado pelo servidor do Google.
4. **Regra do 0x0** — definir no regulamento/FAQ.

## Regra do prêmio

R$500 no Pix para o **primeiro** participante que acertar placar + 1º marcador **e** tiver cadastro comprovado. Desempate = ordem de envio (timestamp do servidor). Participações encerram no apito inicial.
