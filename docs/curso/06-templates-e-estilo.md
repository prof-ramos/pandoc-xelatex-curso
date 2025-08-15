# 🎨 Templates e Estilo Personalizado

O Pandoc oferece flexibilidade total para personalizar a aparência dos seus documentos através de variáveis de template e templates LaTeX customizados.

## 🔧 Variáveis de Template

### Via Linha de Comando

```bash
pandoc documento.md \
  --pdf-engine=xelatex \
  -V geometry:margin=2.5cm \
  -V mainfont:"Helvetica Neue" \
  -V colorlinks:true \
  -V linkcolor:blue \
  -o documento.pdf
```

### Via Metadata YAML

```yaml
title: "Relatório Técnico"
author: "Seu Nome"
lang: pt-BR
date: today

# Fontes
mainfont: "Helvetica Neue"
sansfont: "Arial"
monofont: "Menlo"

# Layout
geometry: margin=2.5cm
fontsize: 12pt
linestretch: 1.2

# Cores e Links
colorlinks: true
linkcolor: MidnightBlue
urlcolor: DarkBlue
citecolor: DarkGreen

# Numeração
number-sections: true
secnumdepth: 3

# Sumário
toc: true
toc-depth: 3
```

## 📋 Variáveis Mais Utilizadas

### Layout e Geometria

| Variável | Descrição | Exemplo |
|----------|-----------|---------|
| `geometry` | Margens da página | `margin=2.5cm` |
| `fontsize` | Tamanho da fonte | `12pt` |
| `linestretch` | Espaçamento entre linhas | `1.5` |
| `papersize` | Tamanho do papel | `a4` |

### Tipografia

| Variável | Descrição | Exemplo |
|----------|-----------|---------|
| `mainfont` | Fonte principal | `"Times New Roman"` |
| `sansfont` | Fonte sem serifa | `"Arial"` |
| `monofont` | Fonte monoespaçada | `"Courier New"` |

### Cores e Links

| Variável | Descrição | Exemplo |
|----------|-----------|---------|
| `colorlinks` | Ativa links coloridos | `true` |
| `linkcolor` | Cor dos links internos | `MidnightBlue` |
| `urlcolor` | Cor das URLs | `DarkBlue` |
| `citecolor` | Cor das citações | `DarkGreen` |

!!! tip "Fontes no macOS"
    Fontes recomendadas que já vêm instaladas:
    - **Serif**: "Times New Roman", "Georgia"
    - **Sans-serif**: "Helvetica Neue", "Arial"
    - **Monospace**: "Menlo", "Monaco", "Courier New"

## 🏗️ Template LaTeX Customizado

Para controle total sobre o layout, crie seu próprio `template.latex`:

```latex
\documentclass[12pt,a4paper]{article}

% Pacotes essenciais
\usepackage{fontspec}
\usepackage{polyglossia}
\usepackage{geometry}
\usepackage{fancyhdr}
\usepackage{xcolor}

% Configuração do idioma
\setdefaultlanguage{portuguese}

% Configuração das fontes
\setmainfont{$mainfont$}
\setmonofont{$monofont$}

% Configuração da página
\geometry{$geometry$}

% Cabeçalho e rodapé
\pagestyle{fancy}
\fancyhead[L]{$title$}
\fancyhead[R]{\thepage}
\fancyfoot[C]{$author$}

% Título personalizado
\title{$title$}
\author{$author$}
\date{$date$}

\begin{document}

% Capa personalizada
\begin{titlepage}
\centering
{\Huge\bfseries $title$ \par}
\vspace{1cm}
{\Large $author$ \par}
\vspace{2cm}
{\large $date$ \par}
\end{titlepage}

% Sumário (se solicitado)
$if(toc)$
\tableofcontents
\newpage
$endif$

% Conteúdo do documento
$body$

\end{document}
```

### Usando o Template

```bash
pandoc conteudo.md \
  --pdf-engine=xelatex \
  --template=template.latex \
  --metadata-file=metadata.yaml \
  --toc \
  -o build/relatorio.pdf
```

## 🎯 Templates Pré-configurados

### Template Acadêmico

```yaml
# metadata-academico.yaml
title: "Trabalho de Conclusão de Curso"
subtitle: "Análise de Algoritmos de Machine Learning"
author: "João Silva"
institution: "Universidade Federal"
course: "Ciência da Computação"
advisor: "Prof. Dr. Maria Santos"
lang: pt-BR
date: today

mainfont: "Times New Roman"
fontsize: 12pt
linestretch: 1.5
geometry: "top=3cm,bottom=2cm,left=3cm,right=2cm"

number-sections: true
secnumdepth: 4
toc: true
toc-depth: 4

colorlinks: true
linkcolor: black
urlcolor: blue
citecolor: blue
```

### Template Corporativo

```yaml
# metadata-corporativo.yaml
title: "Relatório Técnico"
subtitle: "Análise de Performance Q3 2024"
author: "Equipe de Desenvolvimento"
company: "TechCorp Solutions"
lang: pt-BR
date: today

mainfont: "Helvetica Neue"
fontsize: 11pt
geometry: margin=2cm

colorlinks: true
linkcolor: "#0066CC"
urlcolor: "#0066CC"

number-sections: true
toc: true
```

## 🎨 Estilização Avançada

### Cabeçalho e Rodapé com fancyhdr

No seu template LaTeX, adicione:

```latex
\usepackage{fancyhdr}
\usepackage{lastpage}

\pagestyle{fancy}
\fancyhf{} % Limpa cabeçalho e rodapé

% Cabeçalho
\fancyhead[L]{\leftmark}
\fancyhead[R]{\thepage\ de \pageref{LastPage}}

% Rodapé
\fancyfoot[L]{$author$}
\fancyfoot[C]{$title$}
\fancyfoot[R]{\today}

% Linha no cabeçalho
\renewcommand{\headrulewidth}{0.4pt}
\renewcommand{\footrulewidth}{0.4pt}
```

### Cores Personalizadas

```latex
\usepackage{xcolor}

% Definir cores personalizadas
\definecolor{azulcorp}{HTML}{0066CC}
\definecolor{cinzatitulo}{HTML}{333333}

% Aplicar nas seções
\usepackage{titlesec}
\titleformat{\section}
  {\normalfont\Large\bfseries\color{azulcorp}}
  {\thesection}{1em}{}
```

## 🛠️ Troubleshooting

### Problema: Fonte não encontrada

!!! bug "LaTeX Error: font-not-found"
    **Sintomas**: Erro sobre fonte não encontrada durante compilação
    
    **Soluções**:
    - Use `fc-list | grep "Nome da Fonte"` para verificar se está instalada
    - Use nomes exatos das fontes (com aspas)
    - Teste com fontes padrão primeiro

### Problema: Template muito complexo

!!! warning "Conflitos de Pacotes"
    **Sintomas**: Erros de compilação com templates elaborados
    
    **Soluções**:
    - Comece com um template minimal e adicione complexidade gradualmente
    - Evite redefinir comandos já definidos pelo Pandoc
    - Use `\usepackage{ifxetex}` para condicionais

### Problema: Encoding de caracteres

!!! bug "Caracteres especiais quebrados"
    **Sintomas**: Acentos e caracteres especiais não aparecem corretamente
    
    **Soluções**:
    - Use sempre `--pdf-engine=xelatex`
    - Configure `\usepackage{fontspec}` no template
    - Defina `lang: pt-BR` no metadata

## 📝 Boas Práticas

1. **Simplicidade**: Mantenha templates simples para evitar conflitos
2. **Reutilização**: Crie uma biblioteca de templates para diferentes tipos de documento
3. **Versionamento**: Versione seus templates junto com o projeto
4. **Teste**: Sempre teste templates com conteúdo real antes de usar
5. **Documentação**: Documente variáveis personalizadas nos seus templates

## 📊 Exemplo Completo

Estrutura de projeto com template personalizado:

```
projeto/
├── conteudo.md
├── metadata.yaml
├── template.latex
├── assets/
│   ├── logo.png
│   └── estilo.css
└── build/
    └── relatorio.pdf
```

Comando de build:

```bash
pandoc conteudo.md \
  --pdf-engine=xelatex \
  --template=template.latex \
  --metadata-file=metadata.yaml \
  --toc --toc-depth=3 \
  --number-sections \
  -o build/relatorio.pdf
```

## 🚀 Próximo Passo

Agora que você domina a personalização de templates, vamos aprender sobre [Automação com Makefile](07-automacao-makefile.md) para otimizar seu fluxo de trabalho e tornar o processo de build mais eficiente.