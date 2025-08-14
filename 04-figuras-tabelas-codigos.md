# 04 — Imagens, Tabelas e Código-Fonte

Esta aula mostra como inserir imagens, tabelas simples e blocos de código com destaque.

## Imagens

Markdown padrão:

```
![Diagrama do sistema](figs/diagrama.png){ width=60% }
```

Recomendações:
- Use caminhos relativos e mantenha as figuras dentro de `figs/`.
- Ajuste tamanho com `{ width=60% }` (pandoc attribute syntax).

## Tabelas simples (pipes)

```
| Componente | Função         |
|-----------:|:---------------|
| API        | Comunicação    |
| DB         | Persistência   |
```

## Código-fonte com destaque

Pandoc oferece destaque integrado sem depender do LaTeX `minted`.

```
```python
def soma(a, b):
    return a + b
```
```

Para LaTeX, você pode ativar `listings` com `-V listings`, mas o destaque interno do Pandoc é normalmente suficiente e mais simples (evita `-shell-escape`).

## Dicas de compatibilidade

- Prefira formatos de imagem PDF/PNG/SVG. Para PDF final, SVG pode ser convertido ou renderizado via LaTeX.
- Se usar SVG e houver erro, converta para PDF/PNG antes: `rsvg-convert` ou exporte como PDF no editor.

