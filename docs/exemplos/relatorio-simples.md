# 📄 Exemplo: Relatório Simples

Um projeto prático completo demonstrando como usar Pandoc + XeLaTeX para gerar documentos profissionais a partir de Markdown.

## 🎯 Estrutura do Projeto

```
exemplos/relatorio-simples/
├── conteudo.md          # Conteúdo principal em Markdown
├── metadata.yaml        # Configurações e metadados
├── template.latex       # Template LaTeX personalizado
├── Makefile            # Automação de build
├── figs/               # Imagens e diagramas
│   └── diagrama.png
└── build/              # Arquivos gerados
    ├── relatorio.pdf
    └── relatorio.html
```

## 📝 Conteúdo Principal

O arquivo `conteudo.md` demonstra elementos essenciais:

```markdown
---
title: "Relatório de Exemplo"
author: "Estudante Pandoc"
lang: pt-BR
date: today
---

# Capa e Sumário

Este documento demonstra como gerar PDFs bonitos a partir 
de Markdown usando Pandoc + XeLaTeX.

## Objetivos

- Configurar fontes do macOS
- Inserir imagens, tabelas e código
- Produzir um PDF com sumário e estilo leve

# Introdução

O Pandoc converte Markdown em diversos formatos. Com 
`--pdf-engine=xelatex`, conseguimos usar fontes do sistema 
e recursos avançados do LaTeX.

## Links

Consulte o site oficial do [Pandoc](https://pandoc.org).

# Imagens

![Diagrama do sistema](figs/diagrama.png){ width=60% }

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
```

!!! tip "Estrutura Recomendada"
    O exemplo segue boas práticas:
    - Metadados no cabeçalho YAML
    - Seções hierárquicas bem organizadas
    - Exemplos de todos os elementos principais
    - Caminhos relativos para imagens

## ⚙️ Configuração de Metadados

O arquivo `metadata.yaml` centraliza todas as configurações:

```yaml
title: "Relatório de Exemplo"
author: "Estudante Pandoc"
lang: pt-BR
date: today

# Estilo e tipografia
mainfont: "Helvetica Neue"
monofont: "Menlo"
colorlinks: true
linkcolor: MidnightBlue
geometry: margin=2.5cm
number-sections: true
```

### Personalizações Incluídas

| Configuração | Efeito |
|--------------|--------|
| `mainfont: "Helvetica Neue"` | Fonte principal moderna |
| `monofont: "Menlo"` | Fonte para código |
| `colorlinks: true` | Links coloridos (não bordas) |
| `linkcolor: MidnightBlue` | Cor azul elegante |
| `geometry: margin=2.5cm` | Margens equilibradas |
| `number-sections: true` | Numeração automática |

## 🎨 Template LaTeX

Template mínimo mas funcional que personaliza:

- Configuração de idioma português
- Fontes do sistema macOS
- Layout de página otimizado
- Suporte a links coloridos

```latex
\documentclass[12pt,a4paper]{article}

% Pacotes essenciais
\usepackage{fontspec}
\usepackage{polyglossia}
\setdefaultlanguage{portuguese}

% Configuração de fontes
\setmainfont{$mainfont$}
\setmonofont{$monofont$}

% Resto do template...
```

## 🔨 Automação com Makefile

O Makefile permite builds simples e reprodutíveis:

```makefile
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

### Comandos Disponíveis

```bash
# Gerar PDF
make pdf

# Gerar HTML
make html

# Gerar ambos
make all

# Limpar arquivos gerados
make clean
```

## 🖼️ Recursos Visuais

### Imagens

O exemplo inclui uma imagem de diagrama que demonstra:

- Uso de caminhos relativos (`figs/diagrama.png`)
- Controle de tamanho (`{ width=60% }`)
- Legenda automática
- Numeração sequencial

### Tabelas

Tabela exemplo com alinhamento customizado:

```markdown
| Componente | Função         |
|-----------:|:---------------|
| API        | Comunicação    |
| DB         | Persistência   |
```

- Coluna direita: alinhada à direita (`-----------:`)
- Coluna esquerda: alinhada à esquerda (`:---------------`)

### Código

Blocos de código com syntax highlighting:

```python
def soma(a, b):
    return a + b
```

## 🚀 Como Usar Este Exemplo

### 1. Copiar Estrutura

```bash
# Copiar para seu projeto
cp -r exemplos/relatorio-simples/ meu-projeto/
cd meu-projeto/
```

### 2. Personalizar Conteúdo

Edite os arquivos principais:

- `conteudo.md` - Seu conteúdo
- `metadata.yaml` - Seus dados
- `template.latex` - Seu estilo (opcional)

### 3. Gerar Documentos

```bash
# Build completo
make all

# Verificar resultados
ls -la build/
```

### 4. Iterar e Melhorar

- Adicione suas imagens em `figs/`
- Ajuste estilos no `metadata.yaml`
- Personalize template conforme necessário

## 🎨 Variações e Extensões

### Para Trabalho Acadêmico

```yaml
# metadata-academico.yaml
title: "Trabalho de Conclusão"
subtitle: "Análise de Algoritmos"
author: "Seu Nome"
institution: "Universidade"
advisor: "Prof. Orientador"
date: today

# Bibliografia
bibliography: referencias.bib
csl: abnt.csl

# Formatação acadêmica
fontsize: 12pt
linestretch: 1.5
geometry: "top=3cm,bottom=2cm,left=3cm,right=2cm"
number-sections: true
```

### Para Relatório Corporativo

```yaml
# metadata-corporativo.yaml
title: "Relatório Executivo"
subtitle: "Resultados Q4 2024"
author: "Equipe Analytics"
company: "TechCorp"
date: today

# Estilo corporativo
mainfont: "Arial"
fontsize: 11pt
geometry: margin=2cm
colorlinks: true
linkcolor: "#0066CC"
```

## 📊 Resultados Esperados

### PDF Final

- ✅ Sumário automático numerado
- ✅ Fontes elegantes (Helvetica Neue + Menlo)
- ✅ Links coloridos funcionais
- ✅ Imagens bem posicionadas
- ✅ Código com syntax highlighting
- ✅ Numeração de seções automática

### HTML Complementar

- ✅ Versão web responsiva
- ✅ Navegação por links
- ✅ Compatível com todos os browsers
- ✅ Ideal para compartilhamento online

## 🛠️ Troubleshooting

### Problema: Imagem não aparece

!!! bug "Figura não renderizada"
    **Sintomas**: Espaço em branco onde deveria ter imagem
    
    **Soluções**:
    - Verificar se `figs/diagrama.png` existe
    - Usar caminho relativo correto
    - Converter SVG para PNG/PDF se necessário

### Problema: Fonte não encontrada

!!! warning "Font not found"
    **Sintomas**: Erro sobre "Helvetica Neue" não encontrada
    
    **Soluções**:
    - Trocar por "Arial" ou "Times New Roman"
    - Verificar fontes instaladas: `fc-list | grep Helvetica`
    - Usar fontes padrão do macOS

### Problema: Make não funciona

!!! bug "Command not found"
    **Sintomas**: `make: command not found`
    
    **Soluções**:
    - Instalar Xcode Command Line Tools
    - Executar comandos pandoc diretamente
    - Usar script shell alternativo

## 📚 Aprendizados

Este exemplo ensina na prática:

1. **Organização**: Estrutura clara de projeto
2. **Automatização**: Build reprodutível com Make
3. **Flexibilidade**: Múltiplos formatos de saída
4. **Manutenibilidade**: Separação de conteúdo e configuração
5. **Profissionalismo**: Resultado final de alta qualidade

## 🎯 Próximos Passos

Depois de dominar este exemplo:

1. **Expanda o conteúdo** com mais seções
2. **Adicione bibliografia** com arquivos `.bib`
3. **Customize o template** para suas necessidades
4. **Integre com Git** para versionamento
5. **Automatize com CI/CD** para builds automáticos

Este exemplo serve como base sólida para qualquer projeto de documentação profissional com Pandoc!