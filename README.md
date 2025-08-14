# Curso: Produção de PDFs Bonitos com Pandoc + XeLaTeX (macOS)

[![CI](https://github.com/prof-ramos/pandoc-xelatex-curso/actions/workflows/ci.yml/badge.svg)](https://github.com/prof-ramos/pandoc-xelatex-curso/actions/workflows/ci.yml)

Este curso em Markdown ensina, passo a passo, a gerar PDFs elegantes a partir de Markdown usando Pandoc com o engine XeLaTeX no macOS. Foi pensado para um MacBook Air M3 com 8GB de RAM, priorizando leveza e comandos confiáveis.

## O que você vai aprender
- Instalar e configurar Pandoc e (Xe)LaTeX no macOS
- Converter Markdown em PDF, HTML e DOCX
- Usar recursos avançados: sumário, numeração, fontes do sistema, cores de links
- Inserir imagens, tabelas, citações e códigos com destaque de sintaxe
- Personalizar o visual com templates e variáveis
- Automatizar builds com Makefile e garantir reprodutibilidade

## Pré‑requisitos
- macOS atualizado (Apple Silicon OK)
- Homebrew instalado (https://brew.sh)
- Acesso de administrador para instalar TeX

## Estrutura do curso
- `01-instalacao.md`: Instalação no macOS (Pandoc + TeX)
- `02-primeira-conversao.md`: Primeiro PDF com recursos básicos
- `03-fontes-e-idioma.md`: Fontes, acentuação e PT‑BR
- `04-figuras-tabelas-codigos.md`: Imagens, tabelas e código
- `05-citacoes-e-bibliografia.md`: Citações e bibliografia (citeproc)
- `06-templates-e-estilo.md`: Templates, cabeçalhos e cores
- `07-automacao-makefile.md`: Makefile, variáveis e perfis
- `08-troubleshooting.md`: Erros comuns e soluções no macOS
- `09-formatos-adicionais.md`: HTML, DOCX e ePub
- `exemplos/relatorio-simples`: Projeto exemplo completo

## Como usar
1) Abra o diretório `exemplos/relatorio-simples`.
2) Edite `conteudo.md` e `metadata.yaml`.
3) Rode `make pdf` para gerar `build/relatorio.pdf`.
4) Explore as aulas para customizar.

Se preferir, rode diretamente com Pandoc:

```
pandoc conteudo.md \
  --from=gfm \
  --pdf-engine=xelatex \
  --metadata-file=metadata.yaml \
  --toc --toc-depth=3 \
  -o build/relatorio.pdf
```

---

Dica: Se o PDF não renderizar corretamente, verifique se `xelatex` está no `PATH` com `which xelatex`. Caso use BasicTeX, instale pacotes faltantes com `tlmgr` (veja `01-instalacao.md`).
