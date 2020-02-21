# Terminal

## cURL

**cURL (Client URL)** - pisane także jako `curl`, to narzędzie wiersza poleceń do transferowania plików z użyciem syntaxu URL. Wspiera wiele protokołów, w tym HTTP, HTTPS, FTP.

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

## build-essential

```bash
sudo apt install build-essential
```
## Git Credentials Manager

Instalacja i konfiguracja Git Credentials Manager dla WSL Windows 10:
1. Sprawdzić czy jest zainstlowany `Git` na WIndows 10: w `cmd.exe` wpisać komendę `where git.exe`. Jeśli nie zwórci ścieżki do pliku należy zainstalować `Git` z adresu: https://git-scm.com/

2. Sprawdzić czy jest zainstalowany `Credential Manager`: w `cmd.exe` wpisać komendę ` where git-credential-manager.exe`. Jeśli nie zwróci ścieżki, sprawdzić na dysku czy plik managera znajduje się w ścieżce `C:\Program Files\Git\mingw64\libexec\git-core\git-credential-manager.exe`. Jeśli nie zainstalować `Credential Manager` z repozytorium: https://github.com/Microsoft/Git-Credential-Manager-for-Windows/releases/tag/1.20.0

3. Po instalacji `Credential Manager` przekonwertować ścieżkę do pliku 

```bash
# Z DOSowej
C:\Program Files\Git\mingw64\libexec\git-core\git-credential-manager.exe

# Na linuxową
/mnt/c/Program\ Files/Git/mingw64/libexec/git-core/git-credential-manager.exe
```
Konwersja polega na:
- Zamiana `C:\` na `/mnt/c/`
- Zamiana slashy z `\` na `/`
- Wstawienie znaku ucieczki przed spacjami i nawiasami

4. W konsoli `bash` (`Ubuntu`) konfigurujemy `Git` poleceniem:

```bash
In bash call git config --global credential.helper "<converted/path>"

```bash
git config --global credential.helper "/mnt/c/Program\ Files/Git/mingw64/libexec/git-core/git-credential-manager.exe"
```