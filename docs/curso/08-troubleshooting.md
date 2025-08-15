# 🔧 Troubleshooting (macOS)

Guia completo para resolver problemas comuns ao gerar PDFs com Pandoc + XeLaTeX em ambiente macOS, especialmente testado em MacBook Air M3 8GB.

## 🚨 Problemas de Instalação

### `xelatex: command not found`

!!! bug "XeLaTeX não encontrado no PATH"
    **Sintomas**: 
    ```
    pandoc: xelatex not found. xelatex is needed for pdf output.
    ```
    
    **Diagnóstico**:
    ```bash
    which xelatex
    echo $PATH | grep tex
    ```
    
    **Soluções**:
    
    1. **Adicionar ao PATH temporariamente**:
    ```bash
    export PATH="/Library/TeX/texbin:$PATH"
    pandoc documento.md --pdf-engine=xelatex -o saida.pdf
    ```
    
    2. **Adicionar permanentemente** (~/.zshrc ou ~/.bash_profile):
    ```bash
    echo 'export PATH="/Library/TeX/texbin:$PATH"' >> ~/.zshrc
    source ~/.zshrc
    ```
    
    3. **Verificar instalação do TeX**:
    ```bash
    # Para MacTeX completo
    ls -la /Library/TeX/texbin/
    
    # Para BasicTeX
    sudo tlmgr update --self
    ```

### Pandoc não instalado ou versão antiga

!!! warning "Versão incompatível do Pandoc"
    **Verificar versão**:
    ```bash
    pandoc --version
    ```
    
    **Instalar/atualizar via Homebrew**:
    ```bash
    brew install pandoc
    # ou
    brew upgrade pandoc
    ```

## 📦 Problemas de Pacotes LaTeX

### Pacotes ausentes (LaTeX Error: File not found)

!!! bug "Pacotes básicos ausentes"
    **Sintomas comuns**:
    ```
    ! LaTeX Error: File `polyglossia.sty' not found.
    ! LaTeX Error: File `fontspec.sty' not found.
    ! LaTeX Error: File `geometry.sty' not found.
    ```
    
    **Para BasicTeX (instalação mínima)**:
    ```bash
    # Atualizar o gerenciador primeiro
    sudo tlmgr update --self --all
    
    # Instalar pacotes essenciais
    sudo tlmgr install polyglossia fontspec geometry
    sudo tlmgr install babel babel-portuguese
    sudo tlmgr install fancyhdr lastpage
    sudo tlmgr install xcolor titlesec
    ```
    
    **Pacotes frequentemente necessários**:
    ```bash
    sudo tlmgr install collection-fontsrecommended
    sudo tlmgr install collection-langportuguese  
    sudo tlmgr install xeCJK # Para caracteres CJK se necessário
    ```

### Erro de permissões do tlmgr

!!! warning "Permission denied"
    **Sintomas**:
    ```
    tlmgr: action install: package already present: ...
    tlmgr: Cannot access TeX Live root directory
    ```
    
    **Soluções**:
    ```bash
    # Verificar permissões
    ls -la /usr/local/texlive/
    
    # Executar com sudo
    sudo tlmgr install <pacote>
    
    # Ou reinstalar completamente
    sudo tlmgr update --self --all --reinstall-forcibly-removed
    ```

## 🔤 Problemas de Encoding e Fontes

### Caracteres acentuados quebrados

!!! bug "Acentos não aparecem corretamente"
    **Sintomas**: 
    - Acentos aparecem como símbolos estranhos
    - Caracteres UTF-8 não renderizam
    
    **Diagnóstico**:
    ```bash
    # Verificar encoding do arquivo
    file -I documento.md
    # Deve mostrar: charset=utf-8
    ```
    
    **Soluções**:
    
    1. **Use sempre XeLaTeX** (não pdflatex):
    ```bash
    pandoc documento.md --pdf-engine=xelatex -o saida.pdf
    ```
    
    2. **Configure fontes no metadata**:
    ```yaml
    lang: pt-BR
    mainfont: "Times New Roman"
    # ou
    mainfont: "Helvetica Neue"
    ```
    
    3. **Salve arquivos em UTF-8**:
    ```bash
    # Converter se necessário
    iconv -f ISO-8859-1 -t UTF-8 arquivo.md > arquivo_utf8.md
    ```

### Fonte não encontrada

!!! bug "Font not found error"
    **Sintomas**:
    ```
    fontspec error: "font-not-found"
    The font "MinhaFonte" cannot be found.
    ```
    
    **Diagnóstico**:
    ```bash
    # Listar fontes disponíveis no sistema
    fc-list | grep -i "nome da fonte"
    
    # Para macOS especificamente
    system_profiler SPFontsDataType | grep -i "nome"
    ```
    
    **Soluções**:
    
    1. **Use nomes exatos das fontes**:
    ```yaml
    # Correto
    mainfont: "Helvetica Neue"
    
    # Incorreto
    mainfont: helvetica
    ```
    
    2. **Fontes seguras para macOS**:
    ```yaml
    mainfont: "Times New Roman"      # Serif
    sansfont: "Helvetica Neue"      # Sans-serif  
    monofont: "Menlo"               # Monospace
    ```
    
    3. **Instalar fontes se necessário**:
    ```bash
    # Abrir Font Book e instalar manualmente
    open /Applications/Font\ Book.app
    ```

## 🖼️ Problemas com Imagens

### Imagens SVG não aparecem

!!! bug "SVG não suportado pelo XeLaTeX"
    **Sintomas**: Imagens SVG não renderizam no PDF
    
    **Soluções**:
    
    1. **Converter SVG para PDF** (recomendado):
    ```bash
    # Usando rsvg-convert (instalar via Homebrew)
    brew install librsvg
    rsvg-convert -f pdf -o imagem.pdf imagem.svg
    ```
    
    2. **Converter para PNG**:
    ```bash
    rsvg-convert -f png -w 1200 -o imagem.png imagem.svg
    ```
    
    3. **Atualizar referências no Markdown**:
    ```markdown
    # Antes
    ![Diagrama](imagem.svg)
    
    # Depois  
    ![Diagrama](imagem.pdf)
    ```

### Problemas de caminho de imagens

!!! warning "Image not found"
    **Sintomas**: `! Package pdftex.def Error: File 'imagem.png' not found`
    
    **Soluções**:
    
    1. **Usar caminhos relativos corretos**:
    ```markdown
    # Se executando na raiz do projeto
    ![Figura](figs/diagrama.png)
    
    # Verificar estrutura
    projeto/
    ├── documento.md
    └── figs/
        └── diagrama.png
    ```
    
    2. **Verificar se arquivo existe**:
    ```bash
    ls -la figs/diagrama.png
    file figs/diagrama.png  # Verificar formato
    ```

## 💾 Problemas de Performance

### Memória insuficiente (8GB RAM)

!!! warning "Compilation too slow"
    **Sintomas**: 
    - Compilação muito lenta
    - Sistema trava durante build
    - Erros de memória do XeLaTeX
    
    **Soluções**:
    
    1. **Fechar aplicações pesadas**:
    ```bash
    # Verificar uso de memória
    top -o mem
    
    # Fechar Chrome, VS Code, etc. durante build
    ```
    
    2. **Otimizar imagens**:
    ```bash
    # Comprimir PNGs
    brew install pngquant
    pngquant --quality=65-80 imagem.png
    
    # Redimensionar se muito grandes
    sips -Z 1200 imagem.png  # Máximo 1200px
    ```
    
    3. **Build incremental**:
    ```makefile
    # No Makefile, usar dependências corretas
    relatorio.pdf: documento.md metadata.yaml
        pandoc documento.md --pdf-engine=xelatex -o relatorio.pdf
    ```

### Compilação lenta

!!! tip "Otimizar performance"
    **Estratégias**:
    
    1. **Template mais simples durante desenvolvimento**:
    ```yaml
    # metadata-draft.yaml (para desenvolvimento)
    title: "Draft"
    author: "Você"
    # Sem fontes customizadas, sem bibliografia
    ```
    
    2. **Build em duas etapas**:
    ```bash
    # Draft rápido
    pandoc documento.md -o draft.pdf
    
    # Final completo  
    pandoc documento.md --template=template.latex --citeproc -o final.pdf
    ```

## 🔍 Ferramentas de Diagnóstico

### Verificação completa do ambiente

```bash
#!/bin/bash
# script: check-pandoc-env.sh

echo "=== Verificação do Ambiente Pandoc + XeLaTeX ==="

# Versões
echo "## Versões"
pandoc --version | head -1
xelatex --version | head -1

# PATH
echo -e "\n## PATH do TeX"
echo $PATH | grep -o '[^:]*tex[^:]*'

# Pacotes LaTeX essenciais
echo -e "\n## Pacotes LaTeX"
for pkg in polyglossia fontspec geometry fancyhdr; do
    if kpsewhich $pkg.sty >/dev/null 2>&1; then
        echo "✅ $pkg.sty"
    else
        echo "❌ $pkg.sty (instalar: sudo tlmgr install $pkg)"
    fi
done

# Fontes do sistema
echo -e "\n## Fontes do Sistema"
for font in "Times New Roman" "Helvetica Neue" "Menlo"; do
    if fc-list : family | grep -q "$font"; then
        echo "✅ $font"
    else
        echo "❌ $font"
    fi
done

# Teste básico
echo -e "\n## Teste de Conversão"
echo "# Teste" | pandoc --pdf-engine=xelatex -o /tmp/teste.pdf 2>&1 && echo "✅ Conversão básica OK" || echo "❌ Erro na conversão"
```

### Log de debugging

```bash
# Habilitar logs verbosos
pandoc documento.md \
  --pdf-engine=xelatex \
  --verbose \
  -o documento.pdf 2>&1 | tee pandoc.log

# Verificar log do XeLaTeX  
ls -la documento.log  # Arquivo gerado pelo XeLaTeX
```

## 📋 Checklist de Troubleshooting

### Antes de reportar problemas

- [ ] ✅ Pandoc e XeLaTeX estão no PATH
- [ ] ✅ Arquivos em UTF-8
- [ ] ✅ Fontes existem no sistema
- [ ] ✅ Imagens existem nos caminhos corretos
- [ ] ✅ Pacotes LaTeX necessários instalados
- [ ] ✅ Comando funciona com arquivo mínimo
- [ ] ✅ Testado em terminal limpo

### Arquivo de teste mínimo

```markdown
---
title: "Teste"
author: "Teste"
lang: pt-BR
---

# Título

Texto com acentuação: ção, não, coração.

## Subtítulo

Lista:
- Item 1
- Item 2

Fim.
```

Comando de teste:
```bash
pandoc teste.md --pdf-engine=xelatex -o teste.pdf
```

## 🆘 Quando Pedir Ajuda

### Informações para incluir

1. **Ambiente**:
   - Versão do macOS
   - Modelo do Mac
   - Versão do Pandoc: `pandoc --version`
   - Versão do XeLaTeX: `xelatex --version`

2. **Comando exato que falhou**

3. **Mensagem de erro completa**

4. **Arquivo mínimo que reproduz o problema**

5. **Logs relevantes**:
   ```bash
   pandoc --verbose documento.md --pdf-engine=xelatex -o saida.pdf > debug.log 2>&1
   ```

## 🚀 Próximo Passo

Agora que você sabe resolver os problemas mais comuns, vamos explorar [Formatos Adicionais](09-formatos-adicionais.md) para expandir suas possibilidades além do PDF e gerar HTML, DOCX e ePub de alta qualidade.