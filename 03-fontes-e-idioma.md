# 03 — Fontes do Sistema e Idioma PT‑BR

Com XeLaTeX você pode usar fontes do macOS com `fontspec`, e configurar idioma para hifenização e datas.

## Configurar idioma

Em metadata adicionamos `lang: pt-BR`. Com XeLaTeX, Pandoc usa `polyglossia` por padrão para tratar o idioma.

Exemplo em `metadata.yaml`:

```
title: "Relatório Demo"
author: "Seu Nome"
lang: pt-BR
date: today
```

## Escolher fontes do sistema

Defina variáveis de fonte (XeLaTeX) no metadata ou na linha de comando:

```
mainfont: "Helvetica Neue"
monofont: "Menlo"
sansfont: "Helvetica Neue"
```

Pandoc (XeLaTeX) adiciona automaticamente `\setmainfont{Helvetica Neue}` no preâmbulo via `fontspec`.

## Cores de links e ajustes finos

Para links coloridos e sem caixas, use variáveis do `hyperref` via `-V` ou `metadata`:

```
colorlinks: true
linkcolor: blue
urlcolor: teal
toccolor: black
```

## Comando completo (exemplo)

```
pandoc conteudo.md \
  --pdf-engine=xelatex \
  --metadata-file=metadata.yaml \
  --toc --number-sections \
  -V geometry:margin=2.5cm \
  -o build/relatorio.pdf
```

Teste variações de fontes até encontrar um visual consistente com seu projeto.

