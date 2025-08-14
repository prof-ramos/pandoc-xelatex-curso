# 08 — Troubleshooting (macOS)

Problemas comuns ao gerar PDFs com Pandoc + XeLaTeX e como resolver em um MacBook Air M3 8GB.

## `xelatex: command not found`

- Garanta o PATH do TeX: `export PATH="/Library/TeX/texbin:$PATH"`
- Verifique instalação do TeX (MacTeX/BasicTeX).

## Pacotes ausentes (LaTeX Error: File `...` not found)

- Se usa BasicTeX: `sudo tlmgr install <pacote>` (ex.: `polyglossia`, `fontspec`, `geometry`).
- Rode `sudo tlmgr update --self --all` para atualizar o gerenciador e índices.

## Caracteres acentuados quebrados

- Use `--pdf-engine=xelatex` e defina fontes via `fontspec` (ex.: `mainfont: "Helvetica Neue"`).
- Evite `pdflatex` para textos com muitos acentos/Unicode.

## Erros com SVG

- Converta para PDF/PNG ou exporte do editor como PDF.

## Memória/tempo de compilação

- Feche apps pesadas antes do build.
- Prefira imagens compactadas (PNG Otimizado, PDF vetorial).
- Evite templates muito complexos; mantenha o preâmbulo enxuto.

## Depuração

- Rode `pandoc -v` para conferir versões.
- Use `--verbose` no Pandoc e inspecione o `.log` do XeLaTeX em caso de falhas.

