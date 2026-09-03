# Componentes

Catálogo do que existe em [`../assets/deck.css`](../assets/deck.css). Cada entrada
diz **quando usar** e **quando não usar** — a segunda pergunta é a que evita o
deck virar colcha de retalhos. Veja tudo renderizado em `index.html`.

---

## 1. Estrutura do slide

Todo slide é uma `<section class="slide">` dentro de `#stage`.

```html
<section class="slide slide--dark slide--center" data-hud="Bloco 2 · Ciclo e evidências">
  <!-- conteúdo -->
  <aside class="notes">
    <p>Nota que só o docente vê (tecla P).</p>
  </aside>
</section>
```

| Atributo | Obrigatório | Papel |
|---|---|---|
| `data-hud` | sim | Texto do rodapé. Padrão: `Bloco N · Nome do bloco`. |
| `class="slide"` | sim | Modificadores: `--soft`, `--dark`, `--ink`, `--center`. |
| `<aside class="notes">` | quando houver o que dizer | Nota do docente. Fica oculta; `P` abre a gaveta. |

O deck é indexado pela ordem no HTML. `#12` na URL salta para o slide 12.

---

## 2. Blocos de texto

### `.eyebrow` — rótulo acima do título

```html
<p class="eyebrow">Onde estamos</p>
<p class="eyebrow eyebrow--accent">A regra de ouro da disciplina</p>
```

Sempre o primeiro elemento do slide. `--accent` reserva-se ao que a turma precisa
levar para casa; se todo eyebrow for vermelho, nenhum é.

### `h1` / `h2` / `h3`

`h1` só na capa e no encerramento. `h2` é o título do slide. `h3` vive dentro de
card ou coluna. Não pule níveis para conseguir um tamanho — se precisar de outro
tamanho, o componente é outro.

### `.lead` — subtítulo explicativo

```html
<p class="lead lead--wide">
  Processo iterativo que começa na necessidade real do usuário, formula
  hipóteses, prototipa, testa e só então consolida.
</p>
```

Vem depois do `h2`. `--wide` sobe a largura de 24ch para 40ch. Sem o modificador
para frase curta; com ele para definição.

### `.statement` — a afirmação da aula

```html
<p class="statement">
  O "baseadas em evidências" do nome é o que impede o design de virar
  <span class="accent">achismo criativo</span>.
</p>
```

Ocupa o slide sozinha. Quase sempre em `.slide--dark .slide--center`. Uma ou
duas palavras em `.accent`, nunca a frase toda.

**Não use** para explicar um conceito — para isso é `h2` + `.lead`.

### `.consigna` — a fala literal do instrutor

```html
<p class="consigna">O problema é do cidadão, não do CBMDF.</p>
<p class="consigna-note">
  "Falta de viatura" não é problema elegível; "o idoso que cai em casa e fica
  horas sem socorro" é.
</p>
```

Barra vermelha à esquerda. É o que o docente **diz**, não o que a turma lê.
`.consigna--center` remove a barra para uso em `.slide--center`.
`.consigna-note` é a glosa abaixo (52ch).

**Diferença para `.statement`:** statement é conclusão; consigna é instrução.

### `.quote` — citação de fonte externa

```html
<p class="quote">"A confiança moderna no desenho sistemático não foi confirmada pela experiência."</p>
<p class="quote-src">Colebatch, H. K. (2018). <em>The idea of policy design.</em></p>
```

Só para palavra de terceiro, com aspas e atribuição. Fala do docente é `.consigna`.

### `.footnote` — ressalva abaixo do conteúdo

```html
<p class="footnote">Escala de peso, não ranking fixo: o próximo slide mostra por quê.</p>
```

Último elemento do slide. Serve para a cautela, o "mas", o "não confundir com".

### `.display` — número ou palavra isolada

104px. Um dado que deve chocar. Se houver mais de um, use `.figures`.

---

## 3. Slides especiais

### Capa

```html
<section class="slide" data-hud="Abertura">
  <div class="rule"></div>
  <p class="eyebrow">Aula 1</p>
  <h1>Design de Políticas Públicas Baseadas em Evidências</h1>
  <p class="cover-meta">Ten-Cel. Muniz</p>
</section>
```

`.rule` é o traço vermelho de 76×4px. Em `.slide--center` ele se centraliza sozinho.

### Divisor de bloco

```html
<section class="slide slide--dark" data-hud="Bloco 1 · Desenho × design">
  <p class="divider-num">01</p>
  <p class="divider-title">Desenho × design<br />de políticas públicas</p>
  <p class="divider-time">40 min</p>
  <p class="divider-goal">Formato: exercício provocador (15 min) + exposição dialogada (25 min).</p>
</section>
```

Um por bloco, sempre `.slide--dark`. Número com dois dígitos (`00`, `01`…).
`.divider-goal` é opcional e traz um fio acima.

---

## 4. Componentes de conteúdo

### `.arc` — arco das seis aulas

```html
<div class="arc">
  <div class="arc__step is-now">
    <div class="arc__n">Aula 1</div>
    <div class="arc__t">Enquadrar: do desenho ao design</div>
    <div class="arc__mode">hoje · presencial</div>
  </div>
  <!-- ... demais aulas sem is-now -->
</div>
```

Slide "onde estamos", uma vez por aula. `is-now` marca a aula corrente (borda
accent, fundo `--chip`); as demais ficam a 55% de opacidade. **Exatamente um `is-now`.**

### `.agenda` — roteiro do dia

```html
<div class="agenda">
  <div class="agenda__i">
    <div class="agenda__n">0</div>
    <div class="agenda__t">Abertura e contrato do curso</div>
    <div class="agenda__d">15 min</div>
  </div>
  <div class="agenda__i agenda__i--break">
    <div class="agenda__n">☕</div>
    <div class="agenda__t">Intervalo</div>
    <div class="agenda__d">15 min</div>
  </div>
</div>
```

Grade de **duas colunas**: o navegador preenche coluna a coluna, então a ordem no
HTML não é a ordem visual de leitura de cima para baixo. Confira o resultado.
`--break` esmaece o intervalo.

### `.compare` — quadro comparativo de duas colunas

```html
<div class="compare">
  <div class="compare__row compare__row--head">
    <div class="compare__head">Desenho (tradicional)</div>
    <div class="compare__head compare__head--now">Design (abordagem da disciplina)</div>
  </div>
  <div class="compare__row" data-step>
    <div class="compare__cell">Parte do gabinete</div>
    <div class="compare__cell compare__cell--now">Parte do cidadão</div>
  </div>
</div>
```

Sempre com `data-step` nas linhas: o quadro é construído **com** a turma, linha a
linha. `--now` marca a coluna da disciplina (accent no cabeçalho, tinta cheia na
célula); a outra fica em `--mute`.

**Não use** para chave/valor — para isso é `.stack` + `.row`.

### `.weights` — escala de peso da evidência

```html
<div class="weights">
  <div class="weight">
    <div class="weight__bar" style="width:420px"></div>
    <div class="weight__label">Revisões sistemáticas e experimentos</div>
  </div>
</div>
```

Largura da barra em px = peso relativo. É o único lugar do sistema onde `style`
inline é esperado. Deliberadamente **não** é pirâmide: não há ranking fixo de
desenhos de estudo.

### `.stack` / `.row` — lista chave-valor

```html
<div class="stack">
  <div class="row">
    <div class="row__key">40%</div>
    <div class="row__val">Solução + pitch</div>
  </div>
  <div class="row row--hot">
    <div class="row__key">Empatia</div>
    <div class="row__val">Evidência qualitativa, não achismo</div>
  </div>
</div>
```

Chave em coluna fixa de 300px. `--hot` pinta a chave de accent. O último `.row`
perde o fio automaticamente.

### `.cols` + `.card` — grade de cards

```html
<div class="cols cols-3">
  <div class="card" data-step>
    <span class="tag">Fase 1</span>
    <h3>Agenda</h3>
    <p>Onde a maioria pula direto para a solução.</p>
  </div>
  <div class="card card--accent">…</div>
  <div class="card card--fill">…</div>
</div>
```

`.cols-2` / `-3` / `-4` para colunas iguais; para outra contagem use
`style="grid-template-columns:repeat(5,1fr)"` no `.cols`. `--accent` marca borda,
`--fill` troca borda por fundo `--chip`.

Acima de 4 colunas, o card fica só com `.tag` + `h3` — não cabe parágrafo.

### `.clusters` / `.cluster` — agrupamento numerado

```html
<div class="clusters">
  <div class="cluster">
    <div class="cluster__n">01</div>
    <div class="cluster__name">Definir</div>
    <div class="cluster__unit">Etapas 1–2 · 48 min</div>
  </div>
</div>
```

Quatro colunas fixas. Para fases de uma oficina com tempo. Mais compacto que
`.card`; use quando não houver texto corrido.

### `.figures` — números grandes em série

```html
<div class="figures">
  <div><div class="figure__n">6</div><div class="figure__l">aulas</div></div>
  <div><div class="figure__n">2</div><div class="figure__l">a distância, que são campo</div></div>
</div>
```

Dois a quatro números lado a lado. Rótulo trava em 16ch.

### `.why` — cascata escalonada

```html
<div class="why">
  <div class="why__row">
    <div class="why__q">Usuário específico</div>
    <div class="why__line"></div>
    <div class="why__tag">idosos que moram sozinhos em Ceilândia, não a população do DF</div>
  </div>
  <!-- até 5 linhas -->
</div>
```

Cada linha recua 54px a mais que a anterior. **Máximo 5 linhas** — o CSS só
define recuo até a quinta. Serve para 5 porquês, encadeamento se-então, ou
qualquer estrutura em que cada passo depende do anterior.

### `.matrix` — matriz 2×2

```html
<div class="matrix">
  <div class="matrix__ylab">Impacto</div>
  <div class="matrix__cell is-hot">
    <div class="matrix__verb">Fazer agora</div>
    <div class="matrix__desc">Alto impacto, baixo esforço.</div>
  </div>
  <div class="matrix__cell">…</div>
  <div class="matrix__ylab"></div>
  <div class="matrix__cell">…</div>
  <div class="matrix__cell">…</div>
  <div class="matrix__corner"></div>
  <div class="matrix__xlab">Baixo esforço</div>
  <div class="matrix__xlab">Alto esforço</div>
</div>
```

Grade de 3 colunas × 3 linhas, altura fixa 430px. `is-hot` destaca o quadrante
que a turma deve buscar. **Nenhum deck usa ainda** — disponível.

### `.cycle` — diagrama SVG

```html
<svg class="cycle" viewBox="0 0 900 470" role="img" aria-label="Descrição do diagrama">
  <path class="box" d="M 30,190 L 215,80 L 400,190 L 215,300 Z" />
  <path class="arrow" d="M 560,90 C 650,110 690,160 700,195" />
  <text x="127" y="196" font-size="19" font-weight="650" text-anchor="middle">DESCOBRIR</text>
  <text x="127" y="332" font-size="16" text-anchor="middle" fill="var(--mute)">abrir</text>
</svg>
```

SVG inline, máx. 1000px, centralizado. As classes fazem o diagrama seguir a
variante de fundo:

| Classe / atributo | Efeito |
|---|---|
| `.box` | Preenche `--chip`, contorna `--hair` |
| `.arrow` | Traço `--accent` 2.5px, sem preenchimento |
| `.rlab` | Rótulo de reforço em `--accent`, peso 700 |
| `fill` padrão de `text` | Texto na tinta do slide (`--ink`) |
| `fill="var(--mute)"` | Texto secundário |

**Sempre** `role="img"` + `aria-label` descrevendo o diagrama. Cores literais no
SVG quebram nas variantes escuras — use `var(--token)`.

---

## 5. Fonte e sustentação

### `.src` — linha de fonte

```html
<p class="src">
  <span class="grade grade--forte">FORTE · 3/3 votos</span>
  Howlett, M. &amp; Lejano, R. P. (2013). <em>Tales From the Crypt.</em>
  Administration &amp; Society.
</p>
```

Fio acima, 62ch, `--mute`. Vai em **toda** afirmação que a turma possa citar
depois. `<strong>` dentro dela volta à tinta cheia.

### `.grade` — grau de sustentação

| Classe | Cor | Significado |
|---|---|---|
| `.grade--forte` | `--ink` | Verificado, sem refutação |
| `.grade--moderado` | `--mute` | Confirma o tema, não o argumento |
| `.grade--fraco` | `--accent` | Fonte fraca — cautela ao citar |
| `.grade--nao` | `--accent` | Atribuição não confere com a fonte |

**O vermelho aqui sinaliza cautela, não força.** É a inversão deliberada do
significado usual: o que precisa de atenção em sala é o frágil, não o sólido.

### Convenções de comentário no HTML

```html
<!-- R:105 -->            liga o slide à linha do roteiro docente
<!-- P:30 -->             liga a afirmação à linha do arquivo de pesquisa
<!-- R:87-93 -->          intervalo de linhas
<!-- LACUNA: ... -->      informação que falta e por quê
```

**Armadilha: comentário não aninha em HTML.** Comentar um slide inteiro que já
contém um comentário `R:`/`P:` **não** comenta o slide: o primeiro `-->` interno
fecha o comentário externo e o resto do bloco vaza para o DOM como markup real.

```html
<!-- <section class="slide">
  <p class="src">
    <!-- <span class="grade">FORTE</span> -->   ← fecha o comentário AQUI
    Colebatch, H. K. (2018).                    ← a partir daqui, vaza
  </p>
</section> -->                                  ← este "-->" fica órfão
```

Isso acontece hoje em `../aula-01/index.html:339-352`. O texto vazado cai como
filho direto de `#stage`, fora de qualquer `.slide`, e fica pintado **atrás** dos
slides (que são `position:absolute`) — por isso passa despercebido. Não quebra a
projeção, mas é markup solto no documento.

Antes de comentar um bloco, remova os comentários internos — ou apague o bloco de
vez e confie no histórico do git.

---

## 6. Comportamento

### `[data-step]` — revelação progressiva

```html
<div class="compare__row" data-step> … </div>
```

Atributo sem valor, em elementos irmãos. `→` / `espaço` revela um por vez antes
de trocar de slide; `←` desfaz. Elementos com `data-step` ficam fora da animação
de entrada do slide.

Use para: quadro construído com a turma, listas em que a ordem importa, revelação
de resposta. **Não use** em tudo — três ou quatro passos por slide é o teto útil.

### `.timer` — cronômetro de atividade

```html
<div class="timer" data-t="5">
  <div class="timer__time">05:00</div>
  <div class="timer__hint">T inicia · R zera</div>
</div>
```

`data-t` em **minutos**. Ancorado no canto inferior direito, alinhado ao padding
do slide. `.timer__time` inicial é só o que se vê antes do JS montar; o texto
real vem do `data-t`.

| Estado | Classe (automática) | Cor |
|---|---|---|
| Parado | — | `--mute` |
| Correndo | `.is-running` | `--ink` |
| Último minuto | `.is-warning` | `--gold` |
| Esgotado | `.is-done` | `--accent`, piscando |

Teclas: `T` inicia/pausa, `R` zera, `+`/`−` ajustam 30s (ajustam o total também,
para que `R` volte ao valor corrigido em sala). O estado é por slide e sobrevive
à navegação.

### `<aside class="notes">` — nota do docente

Oculta (`display:none`) e injetada na gaveta que a tecla `P` abre. Aceita
`<p>`, `<strong>` e `<span class="accent">`.

### Chrome fixo do deck

Estes blocos ficam **fora** do `#stage` e são idênticos em todo deck — copie do
`template-aula.html`:

| Elemento | Papel |
|---|---|
| `#progress` | Barra de progresso no topo (2px, accent) — vai **antes** do `#stage` |
| `#hud` | Rodapé: bloco corrente e contagem |
| `#notes` | Gaveta das notas do docente (`P`) |
| `#overview` | Grade de todos os slides, clicável (`O`) |
| `#help` | Tabela de atalhos (`?`) |
| `#blackout` | Tela preta para prender a atenção (`B`) |

Os `id` são lidos por `deck.js` na carga. Faltando um, o motor quebra.

### Atalhos

| Tecla | Ação |
|---|---|
| `→` `espaço` `PgDn` `↓` | Avançar passo ou slide |
| `←` `PgUp` `↑` `Backspace` | Voltar |
| `Home` / `End` | Primeiro / último slide |
| `T` / `R` / `+` `−` | Cronômetro: inicia-pausa / zera / ±30s |
| `P` | Notas do docente |
| `O` | Visão geral |
| `B` | Tela preta |
| `F` | Tela cheia |
| `?` ou `H` | Ajuda |
| `Esc` | Fecha overlays |

Clique na metade direita avança, na esquerda volta. Deslize horizontal funciona
em toque (limiar de 46px).

### Impressão

`Ctrl+P` → um slide por página, paisagem, gráficos de fundo ativados. O
`beforeprint` revela todos os `[data-step]`; o `@media print` desliga animações,
esconde o chrome e fixa cada `.slide` em 1280×720 com quebra de página. O
cronômetro sai a 40% de opacidade.
