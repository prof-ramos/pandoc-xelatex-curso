# 02 — Primeiro PDF com Pandoc + XeLaTeX

Objetivo: converter um arquivo Markdown simples em PDF com sumário e numeração de seções.

## Arquivo de exemplo (hello.md)

Crie `hello.md` com o conteúdo:

```
---
title: "Meu Primeiro PDF com Pandoc"
author: "Seu Nome"
date: "2025-01-01"
lang: pt-BR
---

# Introdução

Este é um PDF gerado a partir de Markdown.

## Objetivos

- Demonstrar instalação
- Gerar um PDF com sumário

# Conteúdo

Texto de exemplo. Veja [link externo](https://pandoc.org).
```

## Converter para PDF

```
pandoc hello.md \
  --from=gfm \
  --pdf-engine=xelatex \
  --toc --toc-depth=3 \
  -V geometry:margin=1in \
  -o hello.pdf
```

Parâmetros principais:
- `--from=gfm`: interpreta Markdown estilo GitHub.
- `--pdf-engine=xelatex`: usa XeLaTeX (fontes do sistema e Unicode).
- `--toc`: inclui sumário; `--toc-depth=3` limita profundidade.
- `-V geometry:margin=1in`: define margens via pacote geometry.

Abra o `hello.pdf` e confirme o sumário e a numeração.

