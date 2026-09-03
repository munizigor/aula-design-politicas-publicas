# Tokens

Definidos em [`../assets/deck.css`](../assets/deck.css). Esta página descreve o
que cada um significa e quando ele muda. Veja renderizado em `index.html`.

## Cor

### Globais (`:root`)

| Token | Valor | Papel |
|---|---|---|
| `--accent` | `#b22222` | Vermelho bombeiro. Ênfase única por slide. |
| `--gold` | `#c99700` | Só o aviso do cronômetro (último minuto). Não use em conteúdo. |

### Por variante de fundo

Cada variante reescreve os cinco tokens de superfície. É por isso que um
componente que só usa tokens funciona nas quatro sem regra extra.

| Token | `.slide` (claro) | `.slide--soft` | `.slide--dark` | `.slide--ink` |
|---|---|---|---|---|
| `--bg` | `#ffffff` | `#fbfbfd` | `#000000` | `#1d1d1f` |
| `--ink` | `#1d1d1f` | herda | `#f5f5f7` | `#f5f5f7` |
| `--mute` | `#6e6e73` | herda | `#86868b` | `#98989d` |
| `--hair` | `#d2d2d7` | herda | `#333336` | `#3a3a3c` |
| `--chip` | `#f5f5f7` | herda | `#1c1c1e` | `#2c2c2e` |
| `--accent` | `#b22222` | herda | `#e2564d` | `#e2564d` |

**Por que o accent muda no escuro:** #b22222 sobre preto não passa contraste em
projetor de sala de aula. #e2564d é a mesma família clareada. Está no CSS de
propósito — não "corrija".

### Quando usar cada variante

| Variante | Uso |
|---|---|
| `.slide` (padrão) | Conteúdo comum: quadros, listas, cards, dados. |
| `.slide--soft` | Conteúdo comum quando o slide anterior era branco puro e você quer respiro. Diferença sutil e intencional. |
| `.slide--dark` | Divisores de bloco e afirmações que devem parar a sala. Alto contraste, ruptura de ritmo. |
| `.slide--ink` | Consigna (fala literal do instrutor) e atividades. Escuro sem ser preto: sinaliza "agora é com vocês" sem o peso do divisor. |

`.slide--center` é ortogonal: centraliza e alinha ao centro, combinável com qualquer uma.

## Tipografia

Uma família só: pilha de fontes de sistema (`--font`), sem webfont, sem rede.

```
-apple-system, BlinkMacSystemFont, "SF Pro Display", "SF Pro Text",
"Segoe UI Variable Display", "Segoe UI", Inter, Roboto, "Helvetica Neue", Arial, sans-serif
```

### Escala

Tamanhos em px do palco 1280×720 (o `#stage` inteiro é escalado depois).

| Classe | px | Peso | Tracking | Largura máx. | Papel |
|---|---|---|---|---|---|
| `.divider-num` | 210 | 700 | −.05em | — | Número do bloco no divisor |
| `.display` | 104 | 700 | −.04em | — | Número ou palavra isolada |
| `.timer__time` | 96 | 600 | −.035em | — | Cronômetro |
| `h1` | 92 | 700 | −.035em | — | Título de capa |
| `.figure__n` | 88 | 700 | −.04em | — | Número grande em série |
| `.divider-title` | 74 | 700 | −.035em | — | Título do bloco no divisor |
| `.statement` | 68 | 650 | −.032em | 21ch | Afirmação que a turma deve levar |
| `h2` | 60 | 700 | −.03em | — | Título de slide |
| `.quote` | 58 | 600 | −.028em | 24ch | Citação literal de fonte |
| `.consigna` | 50 | 600 | −.025em | 26ch | Fala literal do instrutor |
| `.cluster__n` | 44 | 700 | −.035em | — | Número do cluster |
| `h3`, `.matrix__verb` | 34 | 600/700 | −.02em | — | Título de card / célula |
| `.lead` | 33 | 400 | — | 24ch (`--wide`: 40ch) | Subtítulo explicativo |
| `.card h3` | 30 | 600 | — | — | Título dentro de card |
| `p`, `.row__key` | 27 | 400/620 | — | — | Corpo |
| `.divider-time`, `.cover-meta`, `.quote-src`, `.consigna-note` | 23–25 | 400 | — | 46–52ch | Metadados e apoio |
| `.compare__cell`, `.arc__t`, `.agenda__i`, `.row__val`, `.weight__label` | 23–24 | 400–600 | — | — | Conteúdo de componente |
| `.card p`, `.figure__l`, `.footnote` | 21–22 | 400 | — | 16ch (`.figure__l`) | Apoio secundário |
| `.src`, `.why__tag`, `.weight__note` | 19 | 400 | — | 62ch (`.src`) | Fonte e nota fina |
| `.eyebrow` | 19 | 600 | **+.14em**, maiúsculas | — | Rótulo acima do título |
| `.tag`, `.arc__n`, `.cluster__unit`, `.grade` | 15 | 650–700 | +.09–.12em, maiúsculas | — | Micro-rótulo |
| `.timer__hint` | 16 | 400 | +.1em, maiúsculas | — | Dica do cronômetro |

**Regra do tracking:** texto grande fecha o espacejamento (valores negativos);
micro-rótulo em maiúsculas abre (valores positivos). O corpo do slide herda
`letter-spacing: -.011em` de `.slide`.

**As larguras máximas não são sugestão.** Se `.statement` estourar 21ch, o slide
tem duas ideias — quebre em dois, não aumente a largura.

## Espaço

Não há escala de espaçamento nomeada; os valores são fixos por componente.
Os que importam:

| Medida | Valor | Onde |
|---|---|---|
| Padding do slide | `76px 104px` | `.slide` — a margem de segurança da projeção |
| Âncora do cronômetro | `right: 104px; bottom: 76px` | Alinha com o padding do slide |
| Gap de grade | `30px` | `.cols` |
| Gap de lista | `20px` (`.stack`), `14px` (`.weights`, `.why`) | |
| Raio | `18px` cards e células · `16px` arc/cluster · `12px` overview · `999px` `.grade` | |
| Fio | `1px solid var(--hair)` · `2px` só no cabeçalho do comparativo e em destaque `is-hot`/`is-now` | |

**Nunca reduza o padding de 76×104 para caber mais conteúdo.** É a margem que
garante que nada seja cortado no projetor.

## Movimento

| Token / regra | Valor | Papel |
|---|---|---|
| `--ease` | `cubic-bezier(.16, 1, .3, 1)` | Curva única do sistema |
| `.slide` → `.current` | `opacity .38s` | Troca de slide |
| `@keyframes rise` | `.78s`, `translateY(18px)` → 0 | Entrada dos filhos diretos do slide |
| Escalonamento | `.02s` + `.07s` por filho, até o 6º | Ordem de leitura |
| `[data-step]` → `.shown` | `.5s`, `translateY(14px)` → 0 | Revelação progressiva |
| `@keyframes blink` | `1.1s steps(2)` | Cronômetro esgotado |

Filhos com `[data-step]` ficam fora da animação `rise` — o `.shown` os controla.
Na impressão, todo movimento é desligado e todo `[data-step]` é revelado.
