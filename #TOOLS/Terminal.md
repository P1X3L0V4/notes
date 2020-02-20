# Terminal

## nvm

**nvm** - Node Version Manager

Repozytorium: https://github.com/nvm-sh/nvm

```bash
# curl
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.2/install.sh | bash

# wget
wget -qO- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.2/install.sh | bash
```

Do właściwego pliku profilu `~/.bash_profile, ~/.zshrc, ~/.profile,` lub `~/.bashrc` należy dodać kod:

```bash
# This loads nvm

export NVM_DIR="$([ -z "${XDG_CONFIG_HOME-}" ] && printf %s "${HOME}/.nvm" || printf %s "${XDG_CONFIG_HOME}/nvm")"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"
```

### Komendy

```bash
# Lista wszystkich zainstalowanych wersji node'a
nvm ls

# Instalacja aktualnej najnowszej wersji (Current release)
nvm install node

# Instalacja aktualnej najnowszej wersji (Stable LTS)
# nvm install --lts
```
