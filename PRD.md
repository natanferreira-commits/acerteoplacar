# PRD — Gol do Rayo (Brasil x Haiti)

> **Status:** Rascunho para execução imediata
> **Owner:** Natan (estratégia) + Claude (build)
> **Afiliado:** Rayo (especialidade: ao vivo)
> **Data do documento:** 18/06/2026
> **Jogo-alvo:** Brasil x Haiti — 19/06/2026 (amanhã)
> **Prazo de publicação:** até a manhã de 19/06, com captação aberta antes do apito inicial

---

## 1. Visão geral

Site promocional de palpite. O usuário tenta acertar o **placar exato** e o **primeiro jogador a marcar** em Brasil x Haiti. Quem acertar os dois leva **R$500 no Pix**. A participação é **condicionada ao registro em uma casa de aposta** através do link de afiliado do Rayo — comprovado por print do e-mail de boas-vindas.

O site é, na prática, uma **máquina de captação de registros** disfarçada de bolão. O palpite é a isca; o registro na casa é o resultado de negócio.

## 2. Objetivo e métrica de sucesso

- **Objetivo de negócio:** captar o maior número possível de **novos registros qualificados** nas casas parceiras, atribuídos ao Rayo.
- **Métrica primária (North Star):** nº de registros válidos comprovados (print de boas-vindas + cruzamento no painel de afiliado).
- **Métricas secundárias:**
  - Taxa de conversão visitante → palpite enviado
  - Taxa palpite enviado → registro comprovado
  - Distribuição de registros por casa (qual casa converteu melhor)
  - Custo por registro (se houver mídia paga por trás)

## 3. Mecânica da promoção (regra oficial)

- **Como ganhar:** acertar **placar exato** (gols Brasil x gols Haiti) **E** o **primeiro jogador a marcar** no jogo.
- **Prêmio:** R$500 via Pix.
- **Critério de desempate / vencedor único:** entre todos que acertarem os dois itens **e tiverem registro válido comprovado**, vence **quem enviou o palpite primeiro** (menor timestamp do servidor). Prêmio único.
- **Encerramento das participações:** no **apito inicial** do jogo. Palpites enviados após o início não valem.
- **Edge cases do "1º marcador" (definir na regra escrita):**
  - Gol contra: mercado normalmente **anulado** nas casas → sugerimos que, se o 1º gol for contra, vale o **primeiro gol marcado por jogador** (não-contra). Decisão final do Natan.
  - 0x0 / jogo sem gols: ninguém acerta "1º marcador" → prêmio não é distribuído (ou rola pra "quem chegou mais perto" — **decisão aberta**, ver §13).
- **Elegibilidade:** maiores de 18 anos; registro feito pelo link de afiliado do Rayo; um palpite por pessoa (deduplicar por WhatsApp/CPF).

## 4. Fluxo do usuário

1. Cai na landing (vindo de story/grupo/anúncio do Rayo).
2. Vê o prêmio (R$500 Pix) e a regra em uma frase.
3. **Escolhe a casa** e clica no botão → abre o **link de afiliado do Rayo** daquela casa (nova aba).
4. Faz o cadastro na casa, recebe o **e-mail de boas-vindas**.
5. Volta ao site, preenche o palpite e **sobe o print do e-mail**.
6. Envia → tela de confirmação ("Palpite registrado às HH:MM. Boa sorte!").
7. Pós-jogo: equipe valida e contata o vencedor pelo WhatsApp.

## 5. Escopo do site (páginas / seções)

Single page (landing) + página de confirmação + página de regulamento.

**Landing:**
- Hero: marca "Gol do Rayo", jogo Brasil x Haiti, prêmio R$500 Pix, CTA.
- "Como funciona" em 3 passos (registra → palpita → comprova).
- Seletor de casas (cards com logo + botão "Quero me cadastrar").
- Formulário de palpite (ver §6).
- FAQ curto + link pro regulamento.
- Selo "+18 | Jogue com responsabilidade".

**Confirmação:** resumo do palpite + horário do envio.
**Regulamento:** regra completa, prazos, LGPD, contato.

## 6. Formulário de palpite — campos

| Campo | Tipo | Obrigatório | Observação |
|---|---|---|---|
| Nome completo | texto | sim | |
| WhatsApp | tel (máscara BR) | sim | chave de contato do vencedor + dedupe |
| Casa escolhida | select | sim | lista das casas parceiras |
| Placar Brasil | número (0–20) | sim | |
| Placar Haiti | número (0–20) | sim | |
| 1º marcador | texto OU select do elenco | sim | select reduz erro de digitação na validação |
| Print do e-mail de boas-vindas | upload imagem (jpg/png/pdf, máx ~5MB) | sim | comprovação |
| Aceite regulamento + 18 | checkbox | sim | LGPD/idade |

- **Timestamp do servidor** gravado no envio (não confiar no relógio do cliente — é o que decide o vencedor).
- Validação client-side básica + bloqueio de envio após o apito.

## 7. Comprovação e antifraude

- **Comprovação aceita:** print do e-mail de boas-vindas da casa (mostra que o cadastro foi concluído).
- **Atribuição ao Rayo:** registro deve sair do link de afiliado do site. Validação final cruza o print com o **painel de afiliado da casa** (nome/e-mail aparecendo como novo registro do Rayo).
- **Antifraude mínimo:**
  - Dedupe por WhatsApp (e idealmente por e-mail do print).
  - 1 palpite válido por pessoa.
  - Validação **manual** dos prints só dos candidatos a vencedor (não precisa validar todo mundo no envio — só ranquear por timestamp e validar de cima pra baixo).
  - (Opcional/futuro) plugar o **SaaS de verificação OCR + IA** de vocês pra ler o print automaticamente. Fora de escopo pra amanhã.

## 8. Validação e escolha do vencedor (operacional)

1. Após o jogo, filtrar palpites com **placar exato + 1º marcador corretos**.
2. Ordenar por **timestamp** (mais antigo primeiro).
3. Validar de cima pra baixo: print de boas-vindas válido + registro confere no painel de afiliado.
4. Primeiro candidato válido = vencedor. Pagar R$500 no Pix e pedir autorização de divulgação.
5. Registrar o resultado pra prova social ("Fulano levou os R$500").

## 9. Stack técnico e arquitetura de dados

- **Front/app:** Next 15 (App Router) + Tailwind. Deploy na **Vercel** (padrão Dupla).
- **Persistência (recomendado pelo prazo):** **Supabase** (Postgres + Storage) — grava o registro do palpite e guarda o arquivo do print em um bucket. Alternativa equivalente: **Vercel Postgres + Vercel Blob**.
- **Tabela `palpites`:** id, nome, whatsapp, casa, placar_brasil, placar_haiti, primeiro_marcador, print_url, created_at (server), ip/user-agent (antifraude), status_validacao.
- **Links de afiliado:** config simples (array de `{ casa, logo, url_afiliado_rayo }`) — fácil de editar sem deploy se possível.
- **Fechamento automático:** flag/horário de kickoff que bloqueia novos envios server-side.
- **Observação:** seguir a regra de não rodar dev server pesado localmente quando arriscar travar a máquina — validar via deploy de preview na Vercel.

## 10. LGPD / legal

- Coleta mínima (nome, WhatsApp, print). Finalidade declarada no regulamento.
- Checkbox de consentimento + idade (+18).
- Regulamento com: período, critério de vitória, desempato, forma de pagamento, prazo de pagamento, política de contato e divulgação do vencedor.
- Disclaimer de jogo responsável (+18) visível.
- Promoção do tipo "concurso de palpite" — revisar se precisa de qualquer formalidade adicional conforme as casas envolvidas.

## 11. Fora de escopo (não fazer pra amanhã)

- Verificação OCR automática do print (manual por enquanto).
- Login/conta de usuário.
- Painel administrativo bonito (basta consultar a tabela / export CSV).
- Multi-jogo / recorrência (esse é one-shot pro Brasil x Haiti).

## 12. Cronograma sugerido (hoje → amanhã)

- **Hoje (18/06):**
  - Travar decisões abertas (§13): casas + links, valor/regra de empate de gol contra e 0x0, elenco pro select.
  - Build da landing + form + persistência + upload.
  - Escrever regulamento.
- **Amanhã (19/06), antes do jogo:**
  - Deploy final + smoke test (envio real + print chegando no storage).
  - Divulgar pelos canais do Rayo.
  - Fechamento automático no apito.
- **Pós-jogo:** validação e pagamento do vencedor.

## 13. Decisões abertas (precisam do Natan)

1. **Casas parceiras + links de afiliado do Rayo** (quais e as URLs).
2. **Regra do "1º marcador"** em gol contra e cenário **0x0** (prêmio anula? vai pra "mais perto"?).
3. **Elenco do Brasil** pra montar o select do 1º marcador (ou deixar texto livre).
4. **Datas/horário exato do kickoff** pra travar o fechamento.
5. Quem opera a **validação manual** e o **Pix** do prêmio.
