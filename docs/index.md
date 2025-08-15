# Curso: Produção de PDFs Bonitos com Pandoc + XeLaTeX

[![CI](https://github.com/prof-ramos/pandoc-xelatex-curso/actions/workflows/ci.yml/badge.svg)](https://github.com/prof-ramos/pandoc-xelatex-curso/actions/workflows/ci.yml)

Bem-vindo ao curso completo para gerar PDFs elegantes a partir de Markdown usando Pandoc com o engine XeLaTeX no macOS. Este curso foi especialmente desenvolvido para MacBook Air M3 com 8GB de RAM, priorizando leveza e comandos confiáveis.

## 🎯 O que você vai aprender

- **Instalação e configuração** do Pandoc e (Xe)LaTeX no macOS
- **Conversão avançada** de Markdown para PDF, HTML e DOCX
- **Recursos profissionais**: sumário automático, numeração, fontes do sistema, cores de links
- **Elementos complexos**: imagens, tabelas, citações e códigos com destaque de sintaxe
- **Personalização visual** com templates e variáveis
- **Automação de builds** com Makefile para garantir reprodutibilidade

## 📋 Pré-requisitos

!!! tip "Requisitos do sistema"
    - macOS atualizado (Apple Silicon suportado)
    - [Homebrew](https://brew.sh) instalado
    - Acesso de administrador para instalar TeX

## 📚 Estrutura do Curso

Este curso está organizado em módulos progressivos:

1. **[Instalação](curso/01-instalacao.md)** - Setup completo no macOS
2. **[Primeira Conversão](curso/02-primeira-conversao.md)** - Seu primeiro PDF
3. **[Fontes e Idioma](curso/03-fontes-e-idioma.md)** - Configuração PT-BR
4. **[Figuras, Tabelas e Códigos](curso/04-figuras-tabelas-codigos.md)** - Elementos visuais
5. **[Citações e Bibliografia](curso/05-citacoes-e-bibliografia.md)** - Referências acadêmicas
6. **[Templates e Estilo](curso/06-templates-e-estilo.md)** - Personalização avançada
7. **[Automação com Makefile](curso/07-automacao-makefile.md)** - Workflows eficientes
8. **[Troubleshooting](curso/08-troubleshooting.md)** - Resolução de problemas
9. **[Formatos Adicionais](curso/09-formatos-adicionais.md)** - HTML, DOCX e ePub

## 🚀 Início Rápido

Para começar imediatamente:

1. Clone este repositório
2. Navegue até `exemplos/relatorio-simples`
3. Execute `make pdf` para gerar seu primeiro PDF
4. Explore as aulas para personalizar conforme sua necessidade

!!! example "Comando direto com Pandoc"
    ```bash
    pandoc conteudo.md \
      --from=gfm \
      --pdf-engine=xelatex \
      --metadata-file=metadata.yaml \
      --toc --toc-depth=3 \
      -o build/relatorio.pdf
    ```

## 💡 Dicas Importantes

!!! warning "Verificação de instalação"
    Se o PDF não renderizar corretamente, verifique se `xelatex` está no `PATH` com:
    ```bash
    which xelatex
    ```
    
    Para usuários do BasicTeX, instale pacotes faltantes com `tlmgr` (veja o módulo de instalação).

## 🤝 Contribuições

Este projeto é open source! Sinta-se à vontade para contribuir com melhorias, correções ou novos exemplos.

---

*Desenvolvido com ❤️ para a comunidade brasileira de documentação técnica*