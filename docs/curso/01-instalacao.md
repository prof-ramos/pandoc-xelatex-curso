# Instalação (Pandoc + XeLaTeX) no macOS

Este guia apresenta opções completas e otimizadas para configurar Pandoc e XeLaTeX no macOS, com foco em eficiência para MacBook Air M3.

## 🍺 1. Instalar o Pandoc

O Pandoc é a ferramenta principal para conversão de documentos. Instale via Homebrew:

!!! tip "Instalação do Homebrew"
    Se ainda não possui o Homebrew:
    ```bash
    /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
    ```

```bash
brew install pandoc
pandoc --version
```

!!! success "Verificação"
    Você deve ver a versão do Pandoc (ex: `pandoc 3.1.8`)

## 📄 2. Escolher uma Distribuição TeX

Para gerar PDFs, você precisa de um engine LaTeX. Temos duas opções principais:

### Opção 1: MacTeX (Completa)
Recomendada para usuários que querem simplicidade:

```bash
brew install --cask mactex-no-gui
```

**Vantagens:**
- ✅ Inclui XeLaTeX e milhares de pacotes
- ✅ Funcionamento imediato
- ✅ Suporte completo a recursos avançados

**Desvantagens:**
- ❌ ~4GB de espaço em disco
- ❌ Download mais longo

### Opção 2: BasicTeX (Minimalista)
Ideal para instalações leves:

```bash
brew install --cask basictex
```

**Vantagens:**
- ✅ Instalação rápida (~100MB)
- ✅ Controle granular de pacotes

**Desvantagens:**
- ❌ Requer instalação manual de pacotes
- ❌ Possíveis erros iniciais

!!! warning "Configuração do PATH"
    Após qualquer instalação TeX, configure o PATH:
    ```bash
    echo 'export PATH="/Library/TeX/texbin:$PATH"' >> ~/.zshrc
    source ~/.zshrc
    which xelatex
    ```

## 📦 3. Pacotes Essenciais (BasicTeX apenas)

Se escolheu BasicTeX, instale os pacotes fundamentais:

```bash
# Atualizar o gerenciador
sudo tlmgr update --self --all

# Pacotes essenciais para este curso
sudo tlmgr install \
  xetex fontspec polyglossia \
  biblatex csquotes geometry \
  hyperref setspace microtype \
  titlesec fancyhdr upquote listings
```

!!! info "Explicação dos Pacotes"
    - **`xetex`**: Fornece o engine XeLaTeX
    - **`fontspec`**: Habilita uso de fontes do sistema
    - **`polyglossia`**: Suporte a idiomas (PT-BR) no XeLaTeX
    - **`biblatex`**: Sistema moderno de citações
    - **`geometry`**: Controle de margens e layout
    - **`hyperref`**: Links clicáveis no PDF

## ✅ 4. Verificação Final

Confirme que tudo está funcionando:

```bash
# Verificar XeLaTeX
xelatex --version

# Verificar Pandoc
pandoc --version

# Teste rápido
echo "# Teste" | pandoc --pdf-engine=xelatex -o teste.pdf
```

!!! success "Resultado esperado"
    - Ambos comandos devem mostrar informações de versão
    - O arquivo `teste.pdf` deve ser criado sem erros

## 🚨 Solução de Problemas Comuns

!!! bug "Comando não encontrado"
    **Problema:** `xelatex: command not found`
    
    **Solução:** Adicione o PATH do TeX:
    ```bash
    export PATH="/Library/TeX/texbin:$PATH"
    ```

!!! bug "Pacote não encontrado (BasicTeX)"
    **Problema:** `! LaTeX Error: File 'fontspec.sty' not found`
    
    **Solução:** Instale o pacote específico:
    ```bash
    sudo tlmgr install fontspec
    ```

!!! bug "Erro de permissão"
    **Problema:** `tlmgr: permission denied`
    
    **Solução:** Use `sudo` com tlmgr:
    ```bash
    sudo tlmgr install [pacote]
    ```

## 🚀 Próximo Passo

Com tudo instalado e funcionando, vamos fazer nossa [Primeira Conversão](02-primeira-conversao.md) de Markdown para PDF e ver o Pandoc em ação!