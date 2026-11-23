# Rubrica de teardown — criativo de concorrente (Meta Ads)

> Fonte: `.claude/skills/copy-review/SKILL.md` + `.claude/agents/creative-director.md`.
> O prompt de visão da automação injeta este arquivo como parte do system.
> É rubrica de **análise** (dissecar um anúncio que já roda), não de criação.

O criativo analisado pode ser imagem estática, carrossel ou vídeo. No MVP a automação
manda pro modelo as **imagens + capas** (não a timeline do vídeo) + a copy do anúncio
(`headline`, `primary_text`, `cta`) e a metadata (`formato`, `dias_no_ar`, `ads_ativos`).

## 1. Hook — primeiros 3 segundos / primeira linha — peso 40

- Para o scroll? (surpreendente, provocador, ou ultra-relevante pro alvo)
- Promessa clara **ou** loop de curiosidade aberto?
- Específico (número, situação concreta) ou genérico?
- Funciona **sem som e sem contexto**? (a maioria vê no mudo)
- Não abre com logo / institucional / "Você sabia que..." sem tensão?
- Nota 1-10 + o que exatamente carrega ou derruba.

## 2. Desenvolvimento — peso 30

- Sustenta a promessa do hook?
- Tem prova, dado ou exemplo concreto?
- Flui natural pro CTA?
- **Staircase error:** introduz marca/produto antes de estabelecer o problema? (queda de
  retenção ~15s). Se sim, sinalizar.
- Nota 1-10.

## 3. CTA — peso 30

- Claro e específico (o que fazer + por quê agora)?
- Urgência ou benefício imediato?
- Único (não três pedidos)?
- Nota 1-10.

## 4. Estágio de consciência (1-5)

Qual estágio o criativo ataca — e se é o certo pra público frio de Meta Ads:
1. **Unaware** — não sabe do problema → pattern interrupt, reframe
2. **Problem Aware** — sente a dor → agitação + educação da causa
3. **Solution Aware** — conhece soluções → Mecanismo Único diferenciador
4. **Product Aware** — conhece a marca → prova social + reversão de risco
5. **Most Aware** — pronto pra comprar → oferta direta + urgência

Regra 80/10/10: ~80% dos criativos frios devem falar com estágios 1-2. Se o anúncio já
presume que o espectador conhece a marca → marcar como **retargeting-only**.

## 5. Framework e ângulo

- **Framework:** PAS / AIDA / HSO / BAB / BITE — qual está em uso e se está bem executado.
- **Ângulo psicológico:** prova social / curiosidade / escassez-FOMO / status / segurança /
  economia / transformação / autoridade — qual é o principal.
- **Criativo nativo?** Parece conteúdo orgânico do feed ou parece propaganda? (UGC, câmera
  de celular, demo, antes/depois, pessoa real = nativo).

## 6. Risco de compliance Meta

Sinalizar se o anúncio: afirma conhecer atributo pessoal do usuário ("Você está acima do
peso?"), usa antes/depois explícito em saúde/estética/finanças, ou faz claim sem lastro
("cura", "100% garantido", "resultado imediato").

## 7. O gap — o que a Perseo faria diferente

- Qual ângulo/hook/formato a Perseo testaria contra este criativo, e a hipótese que valida.
- 1 frase, concreta.

---

## Formato de saída (`teardown.txt`)

```
TEARDOWN — <marca> · <nicho> · coletado <data>
Meta: <N> ads ativos · <D> dias no ar · formato dominante <formato>

NOTA GERAL: <média ponderada>/10

Hook (40%): <nota>/10 — <1-2 frases>
Desenvolvimento (30%): <nota>/10 — <1-2 frases>
CTA (30%): <nota>/10 — <1-2 frases>

Estágio de consciência: <n> (<nome>) — <cold-ok / retargeting-only>
Framework: <nome> · Ângulo: <nome>
Nativo: <sim/não> — <por quê>
Compliance: <ok / ponto de atenção>

O QUE ESTÁ FUNCIONANDO
- <bullet>
- <bullet>

O GAP (o que a Perseo faria diferente)
<1-3 frases: ângulo + hook + hipótese de teste>

ABERTURA SUGERIDA (rascunho — reescrever à mão antes de enviar)
"<primeira linha de e-mail/DM frio, cita a marca + 1 escolha concreta do criativo>"
```
