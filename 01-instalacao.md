# 01 — Instalação (Pandoc + XeLaTeX) no macOS

Este guia cobre opções leves e completas para ter Pandoc e um engine LaTeX (XeLaTeX) funcionando no macOS.

## 1. Instalar o Pandoc

Requer Homebrew:

```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
brew install pandoc
pandoc --version
```

## 2. Instalar um TeX (recomendação para M3 Air 8GB)

Você tem duas opções principais:

- Completo (maior, mais simples):
  - `brew install --cask mactex-no-gui`
  - Inclui `xelatex`, milhares de pacotes e utilitários.

- Leve (menor, mais manual):
  - `brew install --cask basictex`
  - Depois, use `tlmgr` para instalar pacotes conforme necessário.

Após a instalação, garanta o `PATH` do TeX:

```
echo 'export PATH="/Library/TeX/texbin:$PATH"' >> ~/.zshrc
source ~/.zshrc
which xelatex
```

## 3. Pacotes úteis (se usar BasicTeX)

Atualize o gerenciador e instale pacotes comuns:

```
sudo tlmgr update --self --all
sudo tlmgr install xetex fontspec polyglossia biblatex csquotes geometry hyperref setspace microtype titlesec fancyhdr upquote listings
```

Notas:
- `xetex` fornece `xelatex`.
- `fontspec` habilita fontes do sistema (recurso do XeLaTeX).
- `polyglossia` lida com idioma (PT‑BR) no XeLaTeX.

## 4. Verificação rápida

```
xelatex --version
pandoc --version
```

Se ambos responderem, prossiga para a próxima aula.

