---
title: "Relatório de Exemplo"
author: "Estudante Pandoc"
lang: pt-BR
date: today
---

# Capa e Sumário

Este documento demonstra como gerar PDFs bonitos a partir de Markdown usando Pandoc + XeLaTeX.

## Objetivos

- Configurar fontes do macOS
- Inserir imagens, tabelas e código
- Produzir um PDF com sumário e estilo leve

# Introdução

O Pandoc converte Markdown em diversos formatos. Com `--pdf-engine=xelatex`, conseguimos usar fontes do sistema e recursos avançados do LaTeX.

## Links

Consulte o site oficial do [Pandoc](https://pandoc.org).

# Imagens

Exemplo (adicione sua imagem em `figs/diagrama.png`).

<!--
Descomente a linha abaixo após adicionar a imagem:
![Diagrama do sistema](figs/diagrama.png){ width=60% }
-->

# Tabelas

| Componente | Função         |
|-----------:|:---------------|
| API        | Comunicação    |
| DB         | Persistência   |

# Código

```python
def soma(a, b):
    return a + b
```

# Conclusão

Com poucos comandos, obtemos um PDF elegante e reprodutível.

# Referências

Coloque suas referências aqui, ou use `--citeproc` + `.bib`.
