# 09 — Formatos Adicionais: HTML, DOCX e ePub

Além de PDF, o Pandoc gera HTML, DOCX e ePub com alta qualidade.

## HTML standalone

```
pandoc conteudo.md \
  --from=gfm \
  --metadata-file=metadata.yaml \
  --standalone \
  -o build/relatorio.html
```

Dicas:
- Adicione `--css estilo.css` para estilização customizada.
- Use `--toc` também em HTML, se quiser sumário navegável.

## DOCX (Word)

```
pandoc conteudo.md \
  --from=gfm \
  --metadata-file=metadata.yaml \
  -o build/relatorio.docx
```

Template DOCX customizado (opcional): Gere um modelo a partir de um DOCX estilizado e use `--reference-doc=meu-modelo.docx`.

## ePub

```
pandoc conteudo.md \
  --from=gfm \
  --metadata-file=metadata.yaml \
  -o build/relatorio.epub
```

Para um eBook mais rico, inclua capa (`--epub-cover-image=capa.jpg`) e CSS específico.

