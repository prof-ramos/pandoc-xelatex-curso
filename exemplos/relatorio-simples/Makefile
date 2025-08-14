# Makefile simples para Pandoc + XeLaTeX

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
	  --from=gfm \
	  --pdf-engine=xelatex \
	  --metadata-file=$(META) \
	  --template=$(TEMPLATE) \
	  --no-highlight \
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
