# 📚 Citações, Bibliografia e Formatos de Referência

O Pandoc oferece um sistema robusto para gerenciar citações e bibliografias através do `--citeproc`, que pode processar arquivos BibTeX/BibLaTeX junto com estilos CSL (Citation Style Language).

## 🏗️ Estrutura do Projeto

Para trabalhar com citações, você precisará organizar seu projeto com os seguintes arquivos:

| Arquivo | Descrição | Exemplo |
|---------|-----------|---------|
| `conteudo.md` | Texto com citações | `[@chomsky1957]` |
| `referencias.bib` | Base BibTeX | Entradas bibliográficas |
| `estilo.csl` | Estilo de citação | ABNT, APA, IEEE |

!!! tip "Organização Recomendada"
    ```
    projeto/
    ├── conteudo.md
    ├── referencias.bib
    ├── estilo.csl
    ├── metadata.yaml
    └── build/
        └── relatorio.pdf
    ```

## ✍️ Exemplo de Conteúdo com Citações

```markdown
# Introdução

Este argumento foi proposto originalmente em [@knuth1992]. 
Trabalhos posteriores [@dijkstra1968; @lamport1994] expandiram 
essa abordagem.

Segundo @turing1936, a computabilidade pode ser definida...

# Múltiplas citações

A evolução dos algoritmos [@knuth1992; @dijkstra1968] 
demonstrou a importância da estruturação adequada.

# Referências
```

!!! info "Formatos de Citação"
    - `[@autor2020]` - Citação entre parênteses: (Autor, 2020)
    - `@autor2020` - Citação textual: Autor (2020)
    - `[@autor2020; @outro2021]` - Múltiplas citações
    - `[@autor2020, p. 42]` - Com página específica

## 📖 Exemplo de Arquivo BibTeX

```bibtex
@book{knuth1992,
  title={The Art of Computer Programming},
  author={Knuth, Donald E.},
  year={1992},
  publisher={Addison-Wesley},
  volume={1},
  edition={3}
}

@article{dijkstra1968,
  title={Go To Statement Considered Harmful},
  author={Dijkstra, Edsger W.},
  journal={Communications of the ACM},
  volume={11},
  number={3},
  pages={147--148},
  year={1968},
  publisher={ACM}
}

@book{lamport1994,
  title={LaTeX: A Document Preparation System},
  author={Lamport, Leslie},
  year={1994},
  publisher={Addison-Wesley},
  edition={2}
}
```

## 🎨 Obtendo Estilos CSL

### Repositório Oficial Zotero

Baixe estilos prontos do [repositório oficial Zotero](https://www.zotero.org/styles):

- **ABNT**: Para trabalhos acadêmicos brasileiros
- **APA**: Padrão da American Psychological Association  
- **IEEE**: Para trabalhos técnicos e de engenharia
- **Chicago**: Estilo Chicago Manual
- **Vancouver**: Para trabalhos médicos

!!! tip "Busca de Estilos"
    Use a busca no site para encontrar estilos específicos:
    - "ABNT" para padrão brasileiro
    - "IEEE" para engenharia
    - Nome da revista/conferência específica

### Estilos Customizados

Você também pode criar estilos personalizados usando o [CSL Editor](https://editor.citationstyles.org/).

## ⚙️ Comando de Compilação

```bash
pandoc conteudo.md \
  --pdf-engine=xelatex \
  --citeproc \
  --bibliography=referencias.bib \
  --csl=estilo.csl \
  --metadata-file=metadata.yaml \
  --toc \
  -o build/relatorio.pdf
```

### Parâmetros das Citações

| Parâmetro | Descrição |
|-----------|-----------|
| `--citeproc` | Ativa o processamento de citações |
| `--bibliography` | Especifica o arquivo .bib |
| `--csl` | Define o estilo de citação |
| `--metadata-file` | Arquivo com metadados adicionais |

## 🔧 Configuração no Metadata

Você pode definir as configurações de bibliografia diretamente no `metadata.yaml`:

```yaml
title: "Meu Trabalho Acadêmico"
author: "Seu Nome"
bibliography: referencias.bib
csl: abnt.csl
lang: pt-BR
reference-section-title: "Referências Bibliográficas"
```

!!! warning "Seção de Referências"
    Sempre inclua um cabeçalho `# Referências` no final do documento para que a lista de referências seja inserida corretamente.

## 🛠️ Troubleshooting

### Problema: Citações não aparecem

!!! bug "Citações não processadas"
    **Sintomas**: Citações aparecem como `[@autor2020]` no PDF final
    
    **Soluções**:
    - Verifique se `--citeproc` está no comando
    - Confirme que o arquivo `.bib` existe e está no caminho correto
    - Verifique se as chaves no `.bib` correspondem às citações

### Problema: Estilo de citação incorreto

!!! bug "Formato ABNT não aplicado"
    **Sintomas**: Citações no formato errado (ex: APA em vez de ABNT)
    
    **Soluções**:
    - Baixe o arquivo CSL correto do Zotero
    - Verifique o caminho do arquivo `--csl`
    - Teste com um estilo padrão primeiro

### Problema: Caracteres especiais nas referências

!!! bug "Acentos quebrados na bibliografia"
    **Sintomas**: Nomes com acentos aparecem incorretamente
    
    **Soluções**:
    - Use `--pdf-engine=xelatex` (não `pdflatex`)
    - Salve o arquivo `.bib` em UTF-8
    - Configure `lang: pt-BR` no metadata

## 📝 Boas Práticas

1. **Chaves únicas**: Use chaves descritivas como `@silva2023metodologia`
2. **Organização**: Mantenha um arquivo `.bib` por projeto ou tema
3. **Backup**: Versione seus arquivos `.bib` junto com o código
4. **Validação**: Use ferramentas como `biber --tool` para validar o BibTeX
5. **Gerenciadores**: Considere usar Zotero ou Mendeley para gerenciar referências

## 📈 Próximo Passo

Agora que você domina citações e bibliografia, vamos aprender sobre [Templates e Estilo Personalizado](06-templates-e-estilo.md) para customizar completamente a aparência dos seus documentos.