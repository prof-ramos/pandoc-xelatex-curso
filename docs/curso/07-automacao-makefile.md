# ⚙️ Automação com Makefile

Automatize suas conversões de documentos com Makefile para garantir reprodutibilidade, reduzir erros e agilizar seu fluxo de trabalho.

## 🎯 Por que Usar Makefile?

### Vantagens

- **Reprodutibilidade**: Comandos sempre iguais
- **Eficiência**: Rebuild apenas quando necessário
- **Padronização**: Fluxo de trabalho consistente
- **Facilidade**: Um comando para múltiplas operações
- **Colaboração**: Equipe usa os mesmos comandos

!!! tip "Ideal para Projetos"
    Makefile é especialmente útil quando você tem:
    - Múltiplos formatos de saída (PDF, HTML, DOCX)
    - Dependências complexas (imagens, bibliografias)
    - Diferentes perfis de build (draft, final)
    - Trabalho em equipe

## 📝 Makefile Básico

```makefile
# Variáveis de configuração
PDF = build/relatorio.pdf
HTML = build/relatorio.html
DOCX = build/relatorio.docx
MD = conteudo.md
META = metadata.yaml
TEMPLATE = template.latex
BIB = referencias.bib
CSL = estilo.csl

# Alvos especiais
.PHONY: all pdf html docx clean dirs help

# Alvo padrão
all: pdf html

# Criar diretórios necessários
dirs:
	mkdir -p build

# Gerar PDF
pdf: dirs $(PDF)

$(PDF): $(MD) $(META) $(TEMPLATE)
	pandoc $(MD) \
	  --pdf-engine=xelatex \
	  --metadata-file=$(META) \
	  --template=$(TEMPLATE) \
	  --toc --toc-depth=3 \
	  --number-sections \
	  -o $(PDF)

# Gerar HTML
html: dirs $(HTML)

$(HTML): $(MD) $(META)
	pandoc $(MD) \
	  --from=gfm \
	  --metadata-file=$(META) \
	  --standalone \
	  --toc \
	  -o $(HTML)

# Gerar DOCX
docx: dirs $(DOCX)

$(DOCX): $(MD) $(META)
	pandoc $(MD) \
	  --from=gfm \
	  --metadata-file=$(META) \
	  --toc \
	  -o $(DOCX)

# Limpeza
clean:
	rm -rf build

# Ajuda
help:
	@echo "Comandos disponíveis:"
	@echo "  make pdf    - Gera PDF"
	@echo "  make html   - Gera HTML"  
	@echo "  make docx   - Gera DOCX"
	@echo "  make all    - Gera PDF e HTML"
	@echo "  make clean  - Remove arquivos gerados"
```

## 🔄 Makefile com Bibliografia

```makefile
# Variáveis
PDF = build/relatorio.pdf
HTML = build/relatorio.html
MD = conteudo.md
META = metadata.yaml
TEMPLATE = template.latex
BIB = referencias.bib
CSL = estilo.csl

.PHONY: all pdf html clean dirs

all: pdf html

dirs:
	mkdir -p build

# PDF com citações
pdf: dirs $(PDF)

$(PDF): $(MD) $(META) $(TEMPLATE) $(BIB) $(CSL)
	pandoc $(MD) \
	  --pdf-engine=xelatex \
	  --metadata-file=$(META) \
	  --template=$(TEMPLATE) \
	  --citeproc \
	  --bibliography=$(BIB) \
	  --csl=$(CSL) \
	  --toc --toc-depth=3 \
	  --number-sections \
	  -o $(PDF)

# HTML com citações
html: dirs $(HTML)

$(HTML): $(MD) $(META) $(BIB) $(CSL)
	pandoc $(MD) \
	  --from=gfm \
	  --metadata-file=$(META) \
	  --citeproc \
	  --bibliography=$(BIB) \
	  --csl=$(CSL) \
	  --standalone \
	  --toc \
	  -o $(HTML)

clean:
	rm -rf build
```

## 🎨 Perfis de Build Diferentes

### Makefile com Múltiplos Perfis

```makefile
# Configurações
BUILD_DIR = build
SOURCE = conteudo.md
BASE_META = metadata.yaml

.PHONY: all draft final presentation clean

all: draft final

# Build rápido para desenvolvimento
draft:
	mkdir -p $(BUILD_DIR)
	pandoc $(SOURCE) \
	  --metadata-file=$(BASE_META) \
	  --metadata draft:true \
	  --pdf-engine=xelatex \
	  -o $(BUILD_DIR)/draft.pdf

# Build completo para entrega
final:
	mkdir -p $(BUILD_DIR)
	pandoc $(SOURCE) \
	  --metadata-file=$(BASE_META) \
	  --template=template.latex \
	  --citeproc \
	  --bibliography=referencias.bib \
	  --csl=abnt.csl \
	  --pdf-engine=xelatex \
	  --toc --toc-depth=3 \
	  --number-sections \
	  -o $(BUILD_DIR)/final.pdf

# Slides para apresentação
presentation:
	mkdir -p $(BUILD_DIR)
	pandoc $(SOURCE) \
	  --to=beamer \
	  --metadata-file=$(BASE_META) \
	  --pdf-engine=xelatex \
	  -o $(BUILD_DIR)/slides.pdf

clean:
	rm -rf $(BUILD_DIR)
```

## 📊 Makefile Avançado com Dependências

```makefile
# Configuração
BUILD_DIR = build
FIGS_DIR = figs
SOURCE_FILES = $(wildcard *.md)
FIGURE_FILES = $(wildcard $(FIGS_DIR)/*.png) $(wildcard $(FIGS_DIR)/*.jpg)

# Outputs
PDF_FILE = $(BUILD_DIR)/relatorio.pdf
HTML_FILE = $(BUILD_DIR)/relatorio.html

# Configurações
PANDOC_PDF_OPTIONS = --pdf-engine=xelatex \
                     --metadata-file=metadata.yaml \
                     --template=template.latex \
                     --citeproc \
                     --bibliography=referencias.bib \
                     --csl=abnt.csl \
                     --toc --toc-depth=3 \
                     --number-sections

PANDOC_HTML_OPTIONS = --standalone \
                      --metadata-file=metadata.yaml \
                      --citeproc \
                      --bibliography=referencias.bib \
                      --csl=abnt.csl \
                      --toc \
                      --css=estilo.css

.PHONY: all pdf html watch clean install-deps

# Alvo padrão
all: pdf html

# Criar diretórios
$(BUILD_DIR):
	mkdir -p $(BUILD_DIR)

# PDF (depende de todos os arquivos relevantes)
pdf: $(PDF_FILE)

$(PDF_FILE): $(SOURCE_FILES) metadata.yaml template.latex referencias.bib | $(BUILD_DIR)
	pandoc $(SOURCE_FILES) $(PANDOC_PDF_OPTIONS) -o $@

# HTML
html: $(HTML_FILE)

$(HTML_FILE): $(SOURCE_FILES) metadata.yaml referencias.bib estilo.css | $(BUILD_DIR)
	pandoc $(SOURCE_FILES) $(PANDOC_HTML_OPTIONS) -o $@

# Watch mode para desenvolvimento
watch:
	@echo "Monitorando arquivos para mudanças..."
	@while true; do \
		make pdf; \
		echo "PDF atualizado: $$(date)"; \
		sleep 2; \
	done

# Instalar dependências
install-deps:
	@echo "Verificando dependências..."
	@command -v pandoc >/dev/null || { echo "Pandoc não encontrado!"; exit 1; }
	@command -v xelatex >/dev/null || { echo "XeLaTeX não encontrado!"; exit 1; }
	@echo "Dependências OK!"

# Limpeza
clean:
	rm -rf $(BUILD_DIR)

# Status do projeto
status:
	@echo "=== Status do Projeto ==="
	@echo "Arquivos fonte: $(SOURCE_FILES)"
	@echo "Figuras: $(FIGURE_FILES)"
	@echo "Build dir: $(BUILD_DIR)"
	@ls -la $(BUILD_DIR) 2>/dev/null || echo "Nenhum arquivo gerado ainda"
```

## 🚀 Comandos Úteis

### Uso Básico

```bash
# Gerar todos os formatos
make all

# Gerar apenas PDF
make pdf

# Gerar apenas HTML
make html

# Limpar arquivos gerados
make clean

# Ver ajuda
make help
```

### Build Condicional

```bash
# Verificar se precisa rebuild
make -n pdf

# Rebuild forçado
make -B pdf

# Build paralelo (mais rápido)
make -j4 all
```

## 🛠️ Troubleshooting

### Problema: "make: command not found"

!!! bug "Make não instalado"
    **No macOS**: 
    ```bash
    xcode-select --install
    ```
    
    **No Linux**:
    ```bash
    sudo apt install build-essential  # Ubuntu/Debian
    sudo yum install make            # CentOS/RHEL
    ```

### Problema: Tabs vs Espaços

!!! warning "Erro de indentação"
    **Sintomas**: `Makefile:10: *** missing separator`
    
    **Solução**: Use TABs (não espaços) para indentar comandos no Makefile
    
    ```makefile
    pdf: dirs
    [TAB]pandoc conteudo.md -o build/doc.pdf
    ```

### Problema: Dependências não detectadas

!!! bug "Arquivo não atualiza"
    **Sintomas**: Mudanças no source não geram rebuild
    
    **Solução**: Verifique se todas as dependências estão listadas:
    ```makefile
    $(PDF): $(MD) $(META) $(TEMPLATE) $(BIB)
    	pandoc...
    ```

## 📋 Templates de Makefile

### Para TCC/Dissertação

```makefile
# Makefile para trabalho acadêmico
MAIN = dissertacao
CHAPTERS = cap01.md cap02.md cap03.md cap04.md conclusao.md
APPENDIX = apendiceA.md apendiceB.md

.PHONY: all tcc presentation clean

all: tcc

tcc:
	pandoc $(CHAPTERS) $(APPENDIX) \
	  --metadata-file=metadata.yaml \
	  --template=template-abnt.latex \
	  --citeproc \
	  --bibliography=referencias.bib \
	  --csl=abnt.csl \
	  --pdf-engine=xelatex \
	  --number-sections \
	  --toc --toc-depth=4 \
	  -o build/$(MAIN).pdf

presentation:
	pandoc $(CHAPTERS) \
	  --to=beamer \
	  --template=template-slides.latex \
	  --pdf-engine=xelatex \
	  -o build/apresentacao.pdf
```

### Para Relatórios Corporativos

```makefile
# Makefile para relatórios corporativos
COMPANY = techcorp
PROJECT = analise-q4

.PHONY: all report dashboard clean

all: report dashboard

report:
	pandoc relatorio.md \
	  --metadata-file=metadata-$(COMPANY).yaml \
	  --template=template-$(COMPANY).latex \
	  --pdf-engine=xelatex \
	  --toc \
	  -o build/$(PROJECT)-relatorio.pdf

dashboard:
	pandoc dashboard.md \
	  --to=html5 \
	  --template=template-web.html \
	  --css=assets/$(COMPANY).css \
	  --self-contained \
	  -o build/$(PROJECT)-dashboard.html
```

## 🎯 Integração com CI/CD

### GitHub Actions

```yaml
# .github/workflows/build-docs.yml
name: Build Documentation
on: [push, pull_request]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - name: Install Pandoc
        run: sudo apt-get install pandoc texlive-xetex
      - name: Build Documents
        run: make all
      - name: Upload Artifacts
        uses: actions/upload-artifact@v2
        with:
          name: documents
          path: build/
```

## 📝 Boas Práticas

1. **Variáveis**: Use variáveis para paths e configurações
2. **Dependências**: Liste todas as dependências corretamente
3. **Alvos .PHONY**: Marque alvos que não geram arquivos
4. **Comentários**: Documente seções complexas
5. **Modularidade**: Separe lógica em alvos específicos
6. **Validação**: Inclua checks de dependências

## 🔧 Próximo Passo

Com seu fluxo de trabalho automatizado, vamos aprender sobre [Troubleshooting](08-troubleshooting.md) para resolver problemas comuns que podem aparecer durante o desenvolvimento dos seus documentos.