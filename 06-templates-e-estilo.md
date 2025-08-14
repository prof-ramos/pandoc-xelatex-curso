# 06 — Templates e Estilo Personalizado

Você pode usar as variáveis do template padrão do Pandoc ou criar seu próprio `template.latex`.

## Variáveis úteis (linha de comando ou metadata)

- `geometry:margin=2.5cm`
- `mainfont: "Helvetica Neue"`
- `monofont: "Menlo"`
- `colorlinks: true`
- `linkcolor: blue`
- `number-sections: true`

Exemplo (metadata):

```
title: "Relatório"
author: "Seu Nome"
lang: pt-BR
date: today
mainfont: "Helvetica Neue"
monofont: "Menlo"
colorlinks: true
linkcolor: MidnightBlue
geometry: margin=2.5cm
number-sections: true
```

## Template LaTeX customizado

Crie um `template.latex` mínimo para controlar a capa e cabeçalhos. Exemplo no projeto `exemplos/relatorio-simples/template.latex`.

Use com:

```
pandoc conteudo.md \
  --pdf-engine=xelatex \
  --template=template.latex \
  --metadata-file=metadata.yaml \
  --toc \
  -o build/relatorio.pdf
```

## Cabeçalho/rodapé (fancyhdr)

No template, inclua `\usepackage{fancyhdr}` e configure:

```
\pagestyle{fancy}
\fancyhead[L]{\leftmark}
\fancyhead[R]{\thepage}
\fancyfoot{}
```

Mantenha o template simples para evitar conflitos com o preâmbulo do Pandoc.

