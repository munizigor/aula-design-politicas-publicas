# Design de Políticas Públicas Baseadas em Evidências

Material da disciplina **Design de Políticas Públicas Baseadas em Evidências** do CAEO — Curso de Altos Estudos para Oficiais (CEPED/CBMDF).

A disciplina reformula o antigo "Desenho de Políticas Públicas Baseado em Evidências" em um **sprint prático de Design Thinking**: em 6 aulas (30 h/a), grupos de Oficiais Superiores partem de um **problema real do cidadão** que o CBMDF pode ajudar a resolver e chegam a uma **solução prototipada, testada com o cidadão e encaminhada para implementação** — com evidências fundamentando cada etapa, inteligência artificial como copiloto do início ao fim e monitoramento embutido no próprio design da solução.

## Arquivos

O que o **aluno** acessa fica em `docs/` — é a pasta que o GitHub Pages publica:

- [`docs/index.html`](docs/index.html) — página da disciplina: identificação, objetivo, ementa, competências, conteúdo programático das 6 unidades, material e referências. É a porta de entrada.
- [`docs/aula-01/index.html`](docs/aula-01/index.html) — slides da Aula 1: apresentação HTML navegável (setas ← → avançam/voltam, F = tela cheia).
- [`docs/anexos/`](docs/anexos/) — materiais de apoio, cada um em `.md` (fonte editável) e `.docx` (versão distribuída aos alunos):
  - **Canvas do Problema** (A3 paisagem, 1 por grupo);
  - **Critérios de elegibilidade do problema** (com quadro de triagem);
  - **Roteiro do participante da oficina de IA** (prompts e verificação de fontes);
  - **Briefing do campo de empatia** da Aula 2.

O que é de uso **docente ou institucional** fica na raiz:

- [`plano-de-ensino.md`](plano-de-ensino.md) — Plano de Ensino completo, no padrão CEPED (10 seções), versão editável.
- `plano-de-ensino.docx` — versão Word para tramitação institucional (SEI/boletim).
- [`roteiro-docente.md`](roteiro-docente.md) — roteiro do docente da Aula 1 (cronograma minuto a minuto, oficina de IA, dinâmica de escolha do problema). Fora de `docs/` de propósito: não é material do aluno.

## Estrutura do curso

| Aula | Modalidade | Etapa |
|---|---|---|
| 1 | Presencial | Enquadrar: desenho × design, evidências, IA, escolha do problema do cidadão |
| 2 | A distância | Campo de empatia: imersão com o cidadão afetado |
| 3 | Presencial | Definir e idear: da evidência à solução + design da retroalimentação |
| 4 | A distância | Campo de experimentação: prototipar e testar com o cidadão |
| 5 | Presencial | Iterar e encaminhar: implementação, monitoramento, pitch |
| 6 | Presencial | Apresentação das soluções à banca |

## Publicar no GitHub Pages

Tudo o que o aluno vê está em `docs/`, já no formato que o GitHub Pages serve. Para ativar (uma única vez, após o merge na `main`):

1. No repositório, acesse **Settings → Pages**;
2. Em *Build and deployment*, escolha **Deploy from a branch**, branch **`main`**, pasta **`/docs`** e salve;
3. Em alguns minutos a disciplina estará em `https://munizigor.github.io/aula-design-politicas-publicas/`, e os slides da Aula 1 em `.../aula-01/`.

Cada nova aula publicada em `docs/aula-NN/index.html` ganha automaticamente sua URL; para aparecer aos alunos, acrescente o cartão correspondente na seção **Material** de `docs/index.html`.

Para conferir localmente antes de publicar, sirva a pasta como o Pages faria:

```
cd docs && python -m http.server 8000
```

e abra `http://127.0.0.1:8000/`.

## Como evoluir este material

Edite o `plano-de-ensino.md` e regenere o `.docx` a partir dele. Alterações relevantes devem ser feitas em branches e revisadas antes de ir para a versão que tramita institucionalmente.
