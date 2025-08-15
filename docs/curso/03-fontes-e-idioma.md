# Fontes do Sistema e Configuração de Idioma

Com XeLaTeX, você pode usar qualquer fonte instalada no macOS e configurar adequadamente o idioma português brasileiro para hifenização e formatação de datas.

## 🌐 Configuração de Idioma PT-BR

### Metadados básicos
A configuração de idioma é feita através dos metadados YAML:

```yaml
title: "Relatório Técnico"
author: "João Silva"
lang: pt-BR
date: today
```

!!! info "Como funciona"
    Com `lang: pt-BR`, o Pandoc automaticamente:
    - Configura hifenização em português
    - Formata datas no padrão brasileiro
    - Usa o pacote `polyglossia` para XeLaTeX
    - Define "Sumário" como título do índice

### Arquivo metadata.yaml separado
Para projetos maiores, crie um arquivo `metadata.yaml`:

```yaml
title: "Manual do Sistema"
subtitle: "Versão 2.1"
author: 
  - "João Silva"
  - "Maria Santos"
lang: pt-BR
date: today
subject: "Documentação Técnica"
keywords: [manual, sistema, documentação]
```

Use com:
```bash
pandoc conteudo.md --metadata-file=metadata.yaml -o documento.pdf
```

## 🖋️ Configuração de Fontes

### Fontes disponíveis no macOS
Veja fontes instaladas:
```bash
# Listar fontes do sistema
fc-list : family | grep -i helvetica
# ou use Font Book.app
```

### Definindo fontes nos metadados

```yaml
title: "Documento Elegante"
lang: pt-BR
mainfont: "Helvetica Neue"     # Fonte principal (texto)
sansfont: "Arial"              # Fonte sans-serif
monofont: "Menlo"              # Fonte monoespaçada (código)
mathfont: "Latin Modern Math"  # Fonte para matemática
```

!!! tip "Fontes recomendadas para macOS"
    **Elegantes e legíveis:**
    - **Helvetica Neue** - Moderna e limpa
    - **SF Pro Text** - Fonte padrão do macOS
    - **Avenir** - Geométrica e profissional
    
    **Para código:**
    - **Menlo** - Padrão do Terminal/Xcode
    - **Monaco** - Clássica do macOS
    - **SF Mono** - Monoespaçada da Apple

### Configurações avançadas de fonte

```yaml
# Tamanhos de fonte
fontsize: 12pt
linestretch: 1.2  # Espaçamento entre linhas

# Configurações específicas do XeLaTeX
mainfont: "Helvetica Neue"
mainfontoptions: 
  - "Scale=1.0"
  - "Ligatures=TeX"
```

## 🎨 Cores e Aparência de Links

### Configuração básica de cores
```yaml
colorlinks: true
linkcolor: blue
urlcolor: teal
citecolor: green
toccolor: black
```

### Cores personalizadas (hexadecimal)
```yaml
colorlinks: true
linkcolor: "#2E86AB"      # Azul escuro
urlcolor: "#A23B72"       # Rosa escuro  
citecolor: "#F18F01"      # Laranja
```

### Removendo caixas coloridas
```yaml
# Evita caixas coloridas ao redor dos links
colorlinks: true
# ou, para remover completamente:
hidelinks: true
```

## 📐 Layout e Formatação

### Margens e geometria
```yaml
geometry:
  - margin=2.5cm
  - a4paper
  - heightrounded

# ou mais específico:
geometry:
  - top=3cm
  - bottom=3cm
  - left=2.5cm
  - right=2.5cm
```

### Numeração e sumário
```yaml
toc: true
toc-depth: 3
number-sections: true
secnumdepth: 3
```

## 🔧 Comando Completo com Exemplo

Crie um arquivo `exemplo.md`:

```markdown
---
title: "Relatório de Projeto"
subtitle: "Análise Técnica Detalhada"
author: "Equipe de Desenvolvimento"
date: today
lang: pt-BR
mainfont: "Helvetica Neue"
monofont: "Menlo"
fontsize: 11pt
linestretch: 1.15
colorlinks: true
linkcolor: "#2E86AB"
urlcolor: "#A23B72"
geometry: margin=2.5cm
toc: true
number-sections: true
---

# Introdução

Este relatório apresenta os resultados da análise técnica realizada em dezembro de 2024.

## Objetivos do Projeto

- Implementar novo sistema de autenticação
- Melhorar performance da aplicação
- Documentar APIs existentes

Para mais informações, consulte a [documentação oficial](https://exemplo.com).

# Metodologia

Nossa abordagem seguiu as melhores práticas da indústria...
```

Execute:
```bash
pandoc exemplo.md \
  --pdf-engine=xelatex \
  --toc --number-sections \
  -o exemplo.pdf
```

## ✅ Resultado Esperado

Seu PDF deve apresentar:

- ✅ **Texto em português** com hifenização correta
- ✅ **Data formatada** no padrão brasileiro  
- ✅ **Fonte Helvetica Neue** como principal
- ✅ **Código em Menlo** (monospace)
- ✅ **Links coloridos** conforme especificado
- ✅ **"Sumário"** como título do índice

## 🎯 Exercício Prático

1. **Teste diferentes fontes:** SF Pro Text, Avenir, Times New Roman
2. **Experimente cores:** Defina um esquema de cores próprio
3. **Varie layouts:** Teste margens diferentes (1.5cm, 3cm)
4. **Compare idiomas:** Teste com `lang: en-US` para ver diferenças

## 🚀 Próximo Passo

Com a tipografia bem configurada, vamos aprender sobre [Figuras, Tabelas e Códigos](04-figuras-tabelas-codigos.md) para enriquecer seus documentos com elementos visuais e técnicos.