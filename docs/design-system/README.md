# Design system dos decks

Disciplina **Design de Políticas Públicas Baseadas em Evidências** · CAEO · CEPED/CBMDF

Este é o sistema visual e de comportamento comum aos decks das seis aulas. Ele
não foi inventado aqui: foi **extraído** do que já está em produção em
[`../assets/deck.css`](../assets/deck.css) e [`../assets/deck.js`](../assets/deck.js),
a partir do deck da Aula 1.

## O que é e o que não é

| É | Não é |
|---|---|
| Referência visual navegável dos tokens e componentes | Uma nova biblioteca de CSS |
| Catálogo do markup exato que os decks usam | Um framework com build |
| Regras de uso e limites do sistema | Um documento de marca institucional |

**A fonte da verdade continua sendo `../assets/deck.css`.** Esta pasta documenta e
demonstra; não redefine. Se um componente mudar no CSS, atualize o styleguide.

## Estrutura

```
docs/design-system/
  index.html          styleguide vivo — renderiza cada componente em tamanho de projeção
  README.md           este arquivo: princípios e como criar uma aula
  tokens.md           cores, tipografia, espaço, movimento
  componentes.md      catálogo: markup, quando usar, quando não usar
  template-aula.html  esqueleto de deck pronto para copiar
```

Abra `index.html` direto no navegador (`file://` funciona — sem servidor, sem build).

## Princípios

Estes princípios estão codificados no CSS; não são preferências avulsas.

1. **Palco fixo de 1280×720, escalado para caber.** Você desenha para a projeção,
   não para a tela do notebook. `deck.js` calcula `min(largura/1280, altura/720)`
   e aplica no `#stage`. Nada é responsivo: um slide que só cabe se a fonte
   diminuir está errado.

2. **Um slide, uma ideia.** As larguras máximas são deliberadas — `.statement`
   trava em 21ch, `.lead` em 24ch, `.consigna` em 26ch. Se o texto não coube,
   o slide tem duas ideias.

3. **Nunca escreva uma cor literal.** Cada variante de fundo (`.slide`,
   `--soft`, `--dark`, `--ink`) reescreve `--bg`, `--ink`, `--mute`, `--hair`,
   `--chip` e, no escuro, o próprio `--accent`. Componente que usa só tokens
   funciona nas quatro sem regra adicional. Componente com `#hex` quebra em uma delas.

4. **Vermelho com parcimônia.** `--accent` (#b22222) marca *uma* coisa por slide:
   o número do bloco, a coluna que importa no comparativo, uma palavra na
   afirmação. Slide com quatro elementos vermelhos não tem ênfase nenhuma.

5. **Contraste na projeção vence fidelidade de marca.** Em fundo escuro o
   #b22222 fica ilegível no projetor, então as variantes `--dark` e `--ink`
   trocam o accent por #e2564d — mesma família, clareada até passar. Isso já
   está no CSS; não desfaça.

6. **A nota do docente mora no slide.** `<aside class="notes">` dentro da própria
   `<section>`, exibida com a tecla `P`. Nada de roteiro em arquivo à parte que
   dessincroniza do deck.

7. **Sem build, sem rede, sem dependências.** Dois arquivos estáticos e HTML.
   Qualquer coisa que exija `npm install` para projetar uma aula está fora.

8. **Rastreabilidade da afirmação.** Comentários `<!-- R:105 -->` e `<!-- P:30 -->`
   ligam o slide à linha do roteiro docente e da pesquisa; `<!-- LACUNA: ... -->`
   marca o que falta. Afirmação citada em sala leva `.src` com a fonte, e
   `.grade` quando o grau de sustentação importa. Ver `componentes.md`.

## Como criar a aula seguinte

1. `cp docs/design-system/template-aula.html docs/aula-0N/index.html`
2. Ajuste `<title>`, `<meta name="description">` e o slide de capa.
3. No slide "Onde estamos", mova a classe `is-now` para o `.arc__step` da aula.
4. Monte a agenda com `.agenda` e um `.agenda__i` por bloco.
5. Para cada bloco: um slide `.slide--dark` de divisor (`.divider-num` /
   `.divider-title` / `.divider-time`), depois os slides de conteúdo.
6. Escolha os componentes em `index.html` (styleguide) e copie o markup.
7. Toda atividade cronometrada ganha `<div class="timer" data-t="5">`.
8. Toda `<section>` ganha `data-hud="Bloco N · Nome"` e, quando houver algo a
   dizer, `<aside class="notes">`.
9. Rode o checklist abaixo antes de projetar.

## Checklist antes de projetar

- [ ] Todo slide tem `data-hud` preenchido.
- [ ] Nenhum texto passa da borda em 1280×720 (abra em tela cheia com `F`).
- [ ] Nenhuma cor literal no HTML — só tokens ou classes do sistema.
- [ ] No máximo um elemento em `--accent` por slide.
- [ ] Toda afirmação citável tem `.src`.
- [ ] Cronômetros com `data-t` no valor certo; a soma bate com a carga horária.
- [ ] `Ctrl+P` gera um slide por página, paisagem, com gráficos de fundo ativados.
- [ ] Tecla `O` (visão geral) mostra títulos legíveis — se um slide aparece como
      "—", falta nele um `h1`, `h2`, `.statement`, `.quote`, `.consigna`,
      `.display` ou `.divider-title`.

## Dívidas conhecidas

- Os tokens estão duplicados entre `deck.css` e o `<style>` inline de
  `../index.html` (a página da disciplina). Mudança de cor precisa ser feita nos
  dois lugares. A página do site está fora do escopo deste sistema.
- `.matrix` (matriz 2×2) e `.cols-2` / `.card--fill` existem no CSS mas nenhum
  deck os usa ainda. Estão documentados aqui como disponíveis.
- O comentário de `.clusters` no CSS diz "clusters da aula 3", mas a regra vive
  no arquivo comum às seis aulas. O componente é genérico; o comentário é que
  está estreito.
- `../aula-01/index.html:339-352` tem um slide "comentado" que na verdade vaza
  para o DOM: comentário HTML não aninha, e o `-->` interno fecha o externo. Fica
  invisível (pintado atrás dos slides), mas é markup solto. Ver a armadilha em
  `componentes.md`.
