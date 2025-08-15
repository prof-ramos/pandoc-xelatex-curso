# Figuras, Tabelas e Código-Fonte

Esta aula ensina como inserir e formatar imagens, tabelas e blocos de código com destaque de sintaxe em seus documentos.

## 🖼️ Inserindo Imagens

### Sintaxe básica
```markdown
![Descrição da imagem](caminho/para/imagem.png)
```

### Com dimensionamento
```markdown
![Diagrama do sistema](figs/diagrama.png){ width=60% }
![Logo da empresa](logo.png){ width=3cm height=2cm }
```

### Posicionamento e legendas
```markdown
![Arquitetura do sistema. Fonte: Equipe de desenvolvimento](figs/arquitetura.png){ width=80% }
```

!!! tip "Organização de arquivos"
    **Estrutura recomendada:**
    ```
    projeto/
    ├── documento.md
    ├── figs/
    │   ├── diagrama.png
    │   ├── fluxograma.svg
    │   └── grafico.pdf
    └── build/
        └── documento.pdf
    ```

### Formatos suportados
| Formato | Recomendação | Observações |
|---------|--------------|-------------|
| **PNG** | ✅ Ótimo | Ideal para screenshots |
| **PDF** | ✅ Ótimo | Vetorial, escalável |
| **SVG** | ⚠️ Condicional | Pode precisar conversão |
| **JPG** | ✅ Bom | Para fotos |

!!! warning "SVG no XeLaTeX"
    Se encontrar erros com SVG, converta para PDF:
    ```bash
    # macOS com librsvg
    brew install librsvg
    rsvg-convert -f pdf input.svg > output.pdf
    ```

## 📊 Tabelas Eficazes

### Tabela simples com pipes
```markdown
| Componente | Função | Status |
|------------|--------:|:------:|
| API Gateway | Roteamento | ✅ Ativo |
| Database | Persistência | ✅ Ativo |
| Cache | Performance | ⚠️ Manutenção |
```

### Tabela com alinhamento
```markdown
| Item          | Preço     | Quantidade |
|:--------------|----------:|-----------:|
| Licença Pro   | R$ 299,00 |         10 |
| Suporte       | R$ 150,00 |          1 |
| **Total**     | **R$ 449,00** |     **11** |
```

!!! info "Alinhamento de colunas"
    - `:---` = Esquerda (padrão)
    - `---:` = Direita (números)
    - `:---:` = Centro

### Tabelas complexas
Para tabelas muito complexas, use HTML:

```html
<table>
<thead>
<tr><th rowspan="2">Produto</th><th colspan="2">Vendas</th></tr>
<tr><th>Q1</th><th>Q2</th></tr>
</thead>
<tbody>
<tr><td>Software A</td><td>1000</td><td>1200</td></tr>
<tr><td>Software B</td><td>800</td><td>950</td></tr>
</tbody>
</table>
```

## 💻 Código-Fonte com Destaque

### Bloco de código básico
\`\`\`python
def calcular_media(valores):
    """Calcula a média de uma lista de valores."""
    if not valores:
        return 0
    return sum(valores) / len(valores)

# Exemplo de uso
numeros = [10, 20, 30, 40, 50]
media = calcular_media(numeros)
print(f"Média: {media}")
\`\`\`

### Linguagens suportadas
- **Python, JavaScript, Java, C++, Go**
- **Bash, PowerShell, SQL**
- **HTML, CSS, XML, JSON**
- **Markdown, YAML, LaTeX**

### Código inline
Use \`código inline\` para comandos curtos como \`npm install\` ou \`git commit\`.

### Configurações avançadas

#### Numeração de linhas
```bash
pandoc documento.md \
  --pdf-engine=xelatex \
  --highlight-style=tango \
  --listings \
  -V listings-no-page-break \
  -o documento.pdf
```

#### Estilos de destaque disponíveis
- `pygments` (padrão)
- `tango`
- `github`
- `zenburn`
- `breezedark`

Teste diferentes estilos:
```bash
pandoc --list-highlight-styles
```

## 🎨 Exemplos Práticos Completos

### Documento com figuras e tabelas
```markdown
---
title: "Relatório de Performance"
author: "Equipe DevOps"
lang: pt-BR
colorlinks: true
---

# Análise de Performance

## Arquitetura Atual

O sistema segue a arquitetura mostrada na figura abaixo:

![Arquitetura do sistema em produção](figs/arquitetura.png){ width=70% }

## Métricas de Performance

| Métrica | Valor Atual | Meta | Status |
|---------|-------------|------|--------|
| Latência média | 120ms | < 100ms | ⚠️ |
| Throughput | 1000 req/s | > 800 req/s | ✅ |
| Uptime | 99.9% | > 99.5% | ✅ |

## Script de Monitoramento

\`\`\`bash
#!/bin/bash
# Script para monitorar APIs

API_URL="https://api.exemplo.com/health"
LOG_FILE="/var/log/monitoring.log"

while true; do
    response=$(curl -s -w "%{http_code}" "$API_URL")
    timestamp=$(date '+%Y-%m-%d %H:%M:%S')
    
    if [[ $response == *"200" ]]; then
        echo "$timestamp - API OK" >> "$LOG_FILE"
    else
        echo "$timestamp - API ERROR: $response" >> "$LOG_FILE"
    fi
    
    sleep 60
done
\`\`\`
```

## 🚨 Solução de Problemas

!!! bug "Imagem não aparece"
    **Causas comuns:**
    - Caminho incorreto
    - Arquivo não existe
    - Formato não suportado
    
    **Soluções:**
    ```bash
    # Verificar se arquivo existe
    ls -la figs/
    
    # Converter SVG para PDF
    rsvg-convert -f pdf diagrama.svg > diagrama.pdf
    ```

!!! bug "Tabela mal formatada"
    **Problema:** Colunas desalinhadas
    
    **Solução:** Verifique pipes `|` e espaços:
    ```markdown
    # ❌ Incorreto
    |Nome|Idade |
    |João| 25|
    
    # ✅ Correto
    | Nome | Idade |
    |------|-------|
    | João |    25 |
    ```

!!! bug "Código sem destaque"
    **Causa:** Linguagem não reconhecida
    
    **Solução:** Use linguagem válida ou `text`:
    ```markdown
    # ❌ Incorreto
    \`\`\`pseudocode
    
    # ✅ Correto  
    \`\`\`text
    ```

## 🚀 Próximo Passo

Agora que você domina a inserção de elementos visuais, vamos aprender sobre [Citações e Bibliografia](05-citacoes-e-bibliografia.md) para adicionar referências acadêmicas e profissionais aos seus documentos.