# Primeira Conversão: Markdown para PDF

Nesta aula, você criará seu primeiro PDF usando Pandoc com XeLaTeX, incluindo sumário automático e numeração de seções.

## 📝 Criando o Arquivo de Exemplo

Crie um arquivo chamado `hello.md` com o seguinte conteúdo:

```markdown
---
title: "Meu Primeiro PDF com Pandoc"
author: "Seu Nome"
date: "2025-01-01"
lang: pt-BR
---

# Introdução

Este é um PDF gerado a partir de Markdown usando Pandoc e XeLaTeX.

O **XeLaTeX** oferece vantagens como:
- Suporte nativo ao Unicode
- Acesso a fontes do sistema
- Melhor tipografia

## Objetivos

- [x] Demonstrar instalação funcional
- [x] Gerar PDF com sumário automático
- [ ] Explorar recursos avançados

# Conteúdo Principal

Este é o conteúdo principal do documento. Aqui você pode usar toda a sintaxe Markdown padrão.

## Recursos Markdown

### Formatação de texto
Você pode usar *itálico*, **negrito** e `código inline`.

### Listas
1. Item numerado
2. Outro item
   - Subitem
   - Outro subitem

### Links
Visite a [documentação oficial do Pandoc](https://pandoc.org) para mais informações.

# Conclusão

Este exemplo demonstra como é simples gerar PDFs profissionais com Pandoc.
```

## 🔧 Comando de Conversão

Execute o seguinte comando para gerar o PDF:

```bash
pandoc hello.md \
  --from=gfm \
  --pdf-engine=xelatex \
  --toc --toc-depth=3 \
  --number-sections \
  -V geometry:margin=1in \
  -o hello.pdf
```

!!! info "Explicação dos Parâmetros"
    - **`--from=gfm`**: Interpreta Markdown no estilo GitHub (GitHub Flavored Markdown)
    - **`--pdf-engine=xelatex`**: Usa XeLaTeX para melhor suporte Unicode e fontes
    - **`--toc`**: Inclui sumário automático
    - **`--toc-depth=3`**: Limita sumário até nível 3 (`###`)
    - **`--number-sections`**: Numera seções automaticamente
    - **`-V geometry:margin=1in`**: Define margens de 1 polegada

## 📋 Estrutura dos Metadados

O cabeçalho YAML (entre `---`) define metadados importantes:

| Campo | Descrição | Exemplo |
|-------|-----------|---------|
| `title` | Título do documento | "Meu Relatório" |
| `author` | Autor(es) | "João Silva" |
| `date` | Data | "2025-01-01" ou "today" |
| `lang` | Idioma principal | "pt-BR" |

!!! tip "Data automática"
    Use `date: today` para data atual automática.

## 🎨 Personalizações Básicas

### Margens customizadas
```bash
-V geometry:margin=2.5cm
# ou
-V geometry:"top=3cm,bottom=3cm,left=2cm,right=2cm"
```

### Tamanho de papel
```bash
-V papersize:a4
# ou
-V papersize:letter
```

### Quebras de página
Para forçar quebra de página no Markdown:
```markdown
# Nova Seção

\newpage

# Esta seção começará em nova página
```

## ✅ Verificando o Resultado

Abra o arquivo `hello.pdf` gerado. Você deve ver:

- ✅ Sumário automático no início
- ✅ Seções numeradas (1, 1.1, 1.2, etc.)
- ✅ Formatação profissional
- ✅ Links clicáveis (azul)
- ✅ Acentos e caracteres brasileiros corretos

## 🚨 Problemas Comuns

!!! bug "PDF não abre"
    **Causa:** Erro na compilação XeLaTeX
    
    **Solução:** Execute sem `-o` para ver erros:
    ```bash
    pandoc hello.md --pdf-engine=xelatex --toc
    ```

!!! bug "Acentos incorretos"
    **Causa:** Codificação ou falta do `lang: pt-BR`
    
    **Solução:** 
    - Salve o arquivo como UTF-8
    - Confirme `lang: pt-BR` nos metadados

!!! bug "Sumário não aparece"
    **Causa:** Documento muito simples ou sem seções
    
    **Solução:** Adicione pelo menos duas seções `#` ou `##`

## 🎯 Exercício Prático

Crie um documento próprio com:

1. Título personalizado
2. Pelo menos 3 seções principais
3. Uma lista numerada e uma com marcadores
4. Um link externo
5. Texto em **negrito** e *itálico*

Execute a conversão e compare com o exemplo.

## 🚀 Próximo Passo

Agora que você fez sua primeira conversão, vamos personalizar [Fontes e Idioma](03-fontes-e-idioma.md) para criar documentos com aparência profissional e adequada ao português brasileiro.