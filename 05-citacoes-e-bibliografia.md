# 05 — Citações, Bibliografia e Formatos de Referência

Pandoc pode processar citações via `--citeproc` lendo um `.bib` (BibTeX/BibLaTeX) e um estilo CSL.

## Estrutura mínima

- `conteudo.md`: texto com citações `[@chomsky1957]`.
- `referencias.bib`: sua base BibTeX.
- `estilo.csl`: estilo de citação (ex.: ABNT, APA, IEEE).

## Exemplo de conteúdo

```
Este argumento foi proposto em [@knuth1992].

# Referências
```

> Dica: Coloque um cabeçalho `# Referências` no final para a lista.

## Comando

```
pandoc conteudo.md \
  --pdf-engine=xelatex \
  --citeproc \
  --bibliography=referencias.bib \
  --csl=estilo.csl \
  -o build/relatorio.pdf
```

## Obtendo estilos CSL

Baixe de https://www.zotero.org/styles (estilos CSL). Procure por “ABNT” para o padrão brasileiro.

## Notas

- `--citeproc` substitui o antigo `pandoc-citeproc` (agora interno).
- Mantenha as chaves únicas em `referencias.bib` (ex.: `@livro2020autor`).

