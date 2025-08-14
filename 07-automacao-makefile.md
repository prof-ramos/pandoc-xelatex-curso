# 07 — Automação com Makefile

Automatize conversões com Makefile para garantir reprodutibilidade e menos digitação.

## Makefile básico

```
PDF=build/relatorio.pdf
HTML=build/relatorio.html
MD=conteudo.md
META=metadata.yaml
TEMPLATE=template.latex

.PHONY: all pdf html clean dirs

all: pdf html

dirs:
	mkdir -p build

pdf: dirs
	pandoc $(MD) \
	  --pdf-engine=xelatex \
	  --metadata-file=$(META) \
	  --template=$(TEMPLATE) \
	  --toc --toc-depth=3 \
	  -o $(PDF)

html: dirs
	pandoc $(MD) \
	  --from=gfm \
	  --metadata-file=$(META) \
	  --standalone \
	  -o $(HTML)

clean:
	rm -rf build
```

## Perfis (alvos) diferentes

- `make pdf`: PDF com XeLaTeX
- `make html`: HTML standalone
- `make clean`: limpa `build/`

Integre com CI posteriormente, se desejar.

