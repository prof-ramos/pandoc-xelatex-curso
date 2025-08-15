# 🌐 Formatos Adicionais: HTML, DOCX e ePub

Além de PDFs, o Pandoc pode gerar múltiplos formatos de alta qualidade a partir do mesmo conteúdo Markdown, mantendo consistência e economizando tempo.

## 🎯 Vantagens dos Múltiplos Formatos

### Casos de Uso

| Formato | Ideal Para | Vantagens |
|---------|------------|-----------|
| **PDF** | Documentos finais, impressão | Layout fixo, tipografia profissional |
| **HTML** | Web, compartilhamento online | Interativo, responsivo, SEO |
| **DOCX** | Colaboração, revisão | Editável, comentários, controle de alterações |
| **ePub** | E-books, leitura digital | Reflowable, suporte a e-readers |

!!! tip "Estratégia Multi-formato"
    Mantenha um único arquivo Markdown como fonte da verdade e gere todos os formatos necessários para diferentes audiências e propósitos.

## 🌍 HTML Standalone

### Comando Básico

```bash
pandoc conteudo.md \
  --from=gfm \
  --metadata-file=metadata.yaml \
  --standalone \
  --toc \
  -o build/relatorio.html
```

### Opções Avançadas

```bash
pandoc conteudo.md \
  --from=gfm \
  --metadata-file=metadata.yaml \
  --standalone \
  --toc --toc-depth=3 \
  --css=estilo.css \
  --self-contained \
  --highlight-style=github \
  --number-sections \
  -o build/relatorio.html
```

### Parâmetros HTML

| Parâmetro | Descrição |
|-----------|-----------|
| `--standalone` | Gera HTML completo com `<head>` e `<body>` |
| `--self-contained` | Inclui CSS e imagens no próprio arquivo |
| `--css=arquivo.css` | Aplica folha de estilo personalizada |
| `--highlight-style` | Estilo de syntax highlighting |
| `--mathjax` | Suporte a fórmulas matemáticas |

### CSS Personalizado

```css
/* estilo.css */
body {
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
    line-height: 1.6;
    max-width: 800px;
    margin: 0 auto;
    padding: 2rem;
    color: #333;
}

h1, h2, h3 {
    color: #2c3e50;
    border-bottom: 2px solid #3498db;
    padding-bottom: 0.3rem;
}

code {
    background-color: #f8f9fa;
    padding: 0.2rem 0.4rem;
    border-radius: 3px;
    font-size: 0.9em;
}

pre {
    background-color: #f8f9fa;
    padding: 1rem;
    border-radius: 5px;
    overflow-x: auto;
}

blockquote {
    border-left: 4px solid #3498db;
    margin: 0;
    padding-left: 1rem;
    color: #7f8c8d;
}

table {
    border-collapse: collapse;
    width: 100%;
    margin: 1rem 0;
}

th, td {
    border: 1px solid #ddd;
    padding: 0.5rem;
    text-align: left;
}

th {
    background-color: #f2f2f2;
}
```

### Template HTML Customizado

```html
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml" lang="$lang$" xml:lang="$lang$">
<head>
  <meta charset="utf-8" />
  <meta name="generator" content="pandoc" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>$if(title-prefix)$$title-prefix$ – $endif$$pagetitle$</title>
  
  <style>
  $styles.html()$
  </style>
  
  $for(css)$
  <link rel="stylesheet" href="$css$" />
  $endfor$
</head>
<body>
  $if(title)$
  <header>
    <h1 class="title">$title$</h1>
    $if(subtitle)$
    <p class="subtitle">$subtitle$</p>
    $endif$
    $if(author)$
    <p class="author">$for(author)$$author$$sep$, $endfor$</p>
    $endif$
    $if(date)$
    <p class="date">$date$</p>
    $endif$
  </header>
  $endif$
  
  $if(toc)$
  <nav id="TOC">
    <h2>Sumário</h2>
    $table-of-contents$
  </nav>
  $endif$
  
  <main>
    $body$
  </main>
  
  <footer>
    <p>Gerado com <a href="https://pandoc.org">Pandoc</a></p>
  </footer>
</body>
</html>
```

## 📝 DOCX (Microsoft Word)

### Comando Básico

```bash
pandoc conteudo.md \
  --from=gfm \
  --metadata-file=metadata.yaml \
  --toc \
  -o build/relatorio.docx
```

### Com Template Personalizado

```bash
pandoc conteudo.md \
  --from=gfm \
  --metadata-file=metadata.yaml \
  --reference-doc=template.docx \
  --toc \
  -o build/relatorio.docx
```

### Criando Template DOCX

1. **Crie um documento base**:
   ```bash
   # Gerar DOCX inicial
   pandoc exemplo.md -o base.docx
   ```

2. **Personalize no Word**:
   - Abra `base.docx` no Microsoft Word
   - Modifique estilos: Título 1, Título 2, Normal, etc.
   - Configure cabeçalho/rodapé
   - Ajuste fontes e cores
   - Salve como `template.docx`

3. **Use como referência**:
   ```bash
   pandoc documento.md --reference-doc=template.docx -o saida.docx
   ```

### Metadados para DOCX

```yaml
# metadata-docx.yaml
title: "Relatório Técnico"
subtitle: "Análise Detalhada Q4 2024"
author: 
  - "João Silva"
  - "Maria Santos"
date: "Janeiro 2025"
abstract: |
  Este relatório apresenta uma análise detalhada dos resultados
  obtidos durante o quarto trimestre de 2024, incluindo métricas
  de performance e recomendações estratégicas.
keywords: 
  - análise
  - performance
  - relatório
subject: "Relatório Corporativo"
category: "Análise de Dados"
```

## 📚 ePub (E-books)

### Comando Básico

```bash
pandoc conteudo.md \
  --from=gfm \
  --metadata-file=metadata.yaml \
  --toc --toc-depth=2 \
  -o build/livro.epub
```

### ePub Completo

```bash
pandoc conteudo.md \
  --from=gfm \
  --metadata-file=metadata-epub.yaml \
  --epub-cover-image=capa.jpg \
  --epub-metadata=metadata.xml \
  --css=estilo-epub.css \
  --toc --toc-depth=3 \
  -o build/livro.epub
```

### Metadados para ePub

```yaml
# metadata-epub.yaml
title: "Guia Completo do Pandoc"
subtitle: "Do Markdown ao PDF Profissional"
author: "Seu Nome"
date: "2025"
lang: pt-BR
publisher: "Editora Tech"
rights: "© 2025 Seu Nome. Todos os direitos reservados."
description: |
  Um guia completo e prático para dominar o Pandoc e criar 
  documentos profissionais a partir de Markdown.
subject: "Tecnologia, Documentação"
```

### CSS para ePub

```css
/* estilo-epub.css */
body {
    font-family: "Georgia", serif;
    line-height: 1.6;
    text-align: justify;
    hyphens: auto;
}

h1, h2, h3 {
    font-family: "Helvetica", sans-serif;
    page-break-after: avoid;
    color: #2c3e50;
}

h1 {
    font-size: 1.8em;
    margin-top: 1.5em;
    margin-bottom: 1em;
    page-break-before: always;
}

h2 {
    font-size: 1.4em;
    margin-top: 1.2em;
    margin-bottom: 0.8em;
}

p {
    margin-bottom: 1em;
    text-indent: 1.2em;
}

blockquote {
    font-style: italic;
    margin: 1em 2em;
    border-left: 3px solid #ccc;
    padding-left: 1em;
}

code {
    font-family: "Courier New", monospace;
    background-color: #f5f5f5;
    padding: 0.2em;
    border-radius: 2px;
}

pre {
    background-color: #f5f5f5;
    padding: 1em;
    border-radius: 5px;
    overflow-x: auto;
    font-size: 0.9em;
}

/* Quebras de página */
.chapter {
    page-break-before: always;
}
```

## 🔄 Makefile Multi-formato

```makefile
# Configuração
BUILD_DIR = build
SOURCE = conteudo.md
METADATA = metadata.yaml
CSS_WEB = assets/estilo-web.css
CSS_EPUB = assets/estilo-epub.css
TEMPLATE_DOCX = assets/template.docx
COVER = assets/capa.jpg

# Saídas
PDF = $(BUILD_DIR)/documento.pdf
HTML = $(BUILD_DIR)/documento.html
DOCX = $(BUILD_DIR)/documento.docx
EPUB = $(BUILD_DIR)/documento.epub

.PHONY: all pdf html docx epub clean

# Gerar todos os formatos
all: pdf html docx epub

# Criar diretório de build
$(BUILD_DIR):
	mkdir -p $(BUILD_DIR)

# PDF
pdf: $(PDF)
$(PDF): $(SOURCE) $(METADATA) | $(BUILD_DIR)
	pandoc $(SOURCE) \
	  --pdf-engine=xelatex \
	  --metadata-file=$(METADATA) \
	  --template=template.latex \
	  --toc --toc-depth=3 \
	  --number-sections \
	  -o $@

# HTML
html: $(HTML)
$(HTML): $(SOURCE) $(METADATA) $(CSS_WEB) | $(BUILD_DIR)
	pandoc $(SOURCE) \
	  --from=gfm \
	  --metadata-file=$(METADATA) \
	  --standalone \
	  --toc --toc-depth=3 \
	  --css=$(CSS_WEB) \
	  --self-contained \
	  --highlight-style=github \
	  -o $@

# DOCX
docx: $(DOCX)
$(DOCX): $(SOURCE) $(METADATA) $(TEMPLATE_DOCX) | $(BUILD_DIR)
	pandoc $(SOURCE) \
	  --from=gfm \
	  --metadata-file=$(METADATA) \
	  --reference-doc=$(TEMPLATE_DOCX) \
	  --toc \
	  -o $@

# ePub
epub: $(EPUB)
$(EPUB): $(SOURCE) $(METADATA) $(CSS_EPUB) $(COVER) | $(BUILD_DIR)
	pandoc $(SOURCE) \
	  --from=gfm \
	  --metadata-file=$(METADATA) \
	  --epub-cover-image=$(COVER) \
	  --css=$(CSS_EPUB) \
	  --toc --toc-depth=2 \
	  -o $@

# Limpeza
clean:
	rm -rf $(BUILD_DIR)

# Status
status:
	@echo "=== Status dos Formatos ==="
	@ls -la $(BUILD_DIR) 2>/dev/null || echo "Nenhum arquivo gerado"
```

## 🛠️ Troubleshooting Multi-formato

### Problemas com HTML

!!! bug "CSS não aplicado"
    **Sintomas**: HTML sem estilização
    
    **Soluções**:
    - Use `--self-contained` para incluir CSS no arquivo
    - Verifique caminho do arquivo CSS
    - Teste CSS válido em validador online

### Problemas com DOCX

!!! warning "Template não aplicado"
    **Sintomas**: Documento DOCX com formatação padrão
    
    **Soluções**:
    - Verifique se `template.docx` existe
    - Recrie template a partir de DOCX gerado pelo Pandoc
    - Use estilos padrão do Word (Título 1, Título 2, etc.)

### Problemas com ePub

!!! bug "ePub não abre em e-reader"
    **Sintomas**: Arquivo corrompido ou não reconhecido
    
    **Soluções**:
    - Valide com [EpubCheck](https://github.com/w3c/epubcheck)
    - Simplifique CSS (evite propriedades não suportadas)
    - Teste em múltiplos e-readers

## 📊 Comparação de Formatos

| Recurso | PDF | HTML | DOCX | ePub |
|---------|-----|------|------|------|
| **Layout fixo** | ✅ | ❌ | ❌ | ❌ |
| **Editável** | ❌ | ❌ | ✅ | ❌ |
| **Interativo** | ❌ | ✅ | ❌ | ✅ |
| **Offline** | ✅ | ✅ | ✅ | ✅ |
| **Responsivo** | ❌ | ✅ | ❌ | ✅ |
| **Print-ready** | ✅ | ❌ | ✅ | ❌ |
| **Cross-platform** | ✅ | ✅ | ⚠️ | ✅ |

## 📝 Boas Práticas Multi-formato

1. **Markdown limpo**: Evite HTML específico
2. **Imagens otimizadas**: Use formatos suportados por todos
3. **Metadados consistentes**: Mesmo `metadata.yaml` para todos
4. **Teste regular**: Valide saídas em cada formato
5. **Versionamento**: Mantenha templates junto com código

## 🎉 Conclusão do Curso

Parabéns! Você completou o curso de Pandoc + XeLaTeX. Agora você domina:

- ✅ Instalação e configuração completa
- ✅ Conversão de Markdown para PDF profissional  
- ✅ Configuração de fontes e idiomas
- ✅ Inserção de figuras, tabelas e códigos
- ✅ Sistema de citações e bibliografia
- ✅ Templates e estilos personalizados
- ✅ Automação com Makefile
- ✅ Troubleshooting de problemas comuns
- ✅ Geração de múltiplos formatos

### Próximos Passos

- Explore o [exemplo prático](../exemplos/relatorio-simples.md)
- Crie seus próprios templates
- Integre com seu fluxo de trabalho
- Automatize com CI/CD
- Compartilhe seus projetos com a comunidade

**Continue praticando e boa sorte com seus projetos!** 🚀