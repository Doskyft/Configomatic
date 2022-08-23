# Logiciel a installer

## Via apt
```bash
sudo add-apt-repository universe
sudo apt install git make apt-transport-https curl libfuse2 exa bat zsh tmux

# Changement dans les nouvelles versions de gnome
sudo apt install chrome-gnome-shell -> gnome-browser-connector

# PHP
sudo apt install php8.1 php8.1-zip php8.1-intl php8.1-xml php8.1-dom php8.1-curl php8.1-mysql

# Mysql
sudo apt install mysql-server
sudo mysql_secure_installation
```

- [exa => ls plus moderne](https://the.exa.website/)
- [bat => cat plus moderne](https://github.com/sharkdp/bat)
- [zsh => bash plus moderne](https://doc.ubuntu-fr.org/zsh)
- [tmux](https://doc.ubuntu-fr.org/tmux)

## Autre
- [go](https://go.dev/doc/install) || [doc non officiel](https://www.digitalocean.com/community/tutorials/how-to-install-go-on-ubuntu-20-04) <!-- language, dépendance pour d'autre app) -->
- [brave](https://brave.com/fr/download/) <!-- Navigateur web -->
- [sshs](https://github.com/quantumsheep/sshs) <!-- Gestionnaire de connexion ssh -->
- [slack](https://slack.com/intl/fr-fr/downloads/linux) <!-- Méssagerie pro -->
- [jetbrains-tools](https://www.jetbrains.com/fr-fr/toolbox-app/) || [doc non officiel](https://thirddriver.medium.com/jetbrains-toolbox-the-best-way-to-install-intellij-idea-on-linux-53c1070cd03b) # Pour installer tous les outils Jetbrains (PhpStorm, WebStorm, etc.)
- [GitKraken](https://help.gitkraken.com/gitkraken-client/how-to-install/#deb) <!-- GUI pour git -->
- [Spotify](https://www.spotify.com/fr/download/linux/) <!-- # Musique -->
- [nvm - node et npm](https://github.com/nvm-sh/nvm) <!-- Gestionnaire de paquet javascript -->
- [yarn](https://classic.yarnpkg.com/lang/en/docs/install/#debian-stable) <!-- Gestionnaire de paquet javascript -->
- [composer](https://getcomposer.org/download/) <!-- Gestionnaire de paquet PHP -->
- [OhMyZsh](https://github.com/ohmyzsh/ohmyzsh/wiki) <!-- Amélioration à Zsh -->
- [Antigen](https://github.com/zsh-users/antigen) <!-- Amélioration à Zsh -->

# Config

## Fichier de config utilisateur
Renommer les fichiers suivants:
- `.bash_profile` en `.profile`
- `.bash_aliases` en `.aliases`
ce qui permet de les utiliser pour plusieurs shell

## Remplir ce fichier avec les hosts connu ce qui permettra a sshs de l'afficher
```
# ~/.ssh/config
Host *
  AddKeysToAgent yes
  UseKeychain yes
  IdentityFile ~/.ssh/id_rsa

Host "My server"
  HostName server1.example.com
  User root
  Port 22

Host "Go through Proxy"
  HostName server2.example.com
  User someone
  Port 22
  ProxyCommand ssh -W %h:%p proxy.example.com
```

## Générer des clés SSH
```bash
ssh-keygen
```

## Envoyer les clés sur le serveur
```bash
ssh-copy-id -i ~/.ssh/key_file user@ip
```

## Pour ne pas a avoir à lancer le serveur php en root
```bash
sudo iptables -t nat -I OUTPUT -p tcp -d 127.0.0.1 --dport 80 -j REDIRECT --to-ports 8080
sudo apt install iptables-persistent # Pour rendre la règle précédente persistente
```
plus de détail [ici](https://serverfault.com/questions/112795/how-to-run-a-server-on-port-80-as-a-normal-user-on-linux)

## Mysql
```mysql
CREATE USER damien@localhost IDENTIFIED BY 'Pwd123';
GRANT ALL PRIVILEGES ON *.* TO damien@localhost;
FLUSH PRIVILEGES;
```

## ZSH
```bash
chsh # Pour changer le shell par defaut répondre /bin/zsh
nano ~/.zshrc # ajouter: source ~/.aliases
source ~/.zshrc
```

## Antigen
```bash
source /path-to-antigen/antigen.zsh

# Load the oh-my-zsh's library.
antigen use oh-my-zsh

# Bundles from the default repo (robbyrussell's oh-my-zsh).
antigen bundle git
antigen bundle heroku
antigen bundle pip
antigen bundle lein
antigen bundle command-not-found

antigen bundle zsh-users/zsh-completions
antigen bundle zsh-users/zsh-autosuggestions
antigen bundle zsh-users/zsh-syntax-highlighting
antigen bundle zsh-users/zsh-history-substring-search
antigen bundle lukechilds/zsh-nvm

# Syntax highlighting bundle.
antigen bundle zsh-users/zsh-syntax-highlighting

# Load the theme.
antigen theme robbyrussell

# Tell Antigen that you're done.
antigen apply
```

## Tmux
Ajouter dans le fichier .profile
```bash
if command -v tmux &> /dev/null && [ -z "$TMUX" ]; then
    tmux attach -t default || tmux new -s default
fi
```

# Gnome extension
- [Bluetooth Quick Connect](https://extensions.gnome.org/extension/1401/bluetooth-quick-connect/)
- [User Themes](https://extensions.gnome.org/extension/19/user-themes/)
- [Clipboard Indicator](https://extensions.gnome.org/extension/779/clipboard-indicator/)
- [Color Picker](https://extensions.gnome.org/extension/3396/color-picker/)
- [Dash to Panel](https://extensions.gnome.org/extension/1160/dash-to-panel/)

# Structuration dossier home
```bash
mkdir ~/Projects ~/Data
```

# Autre

## Numlock automatique
[source](https://www.numetopia.fr/activer-la-touche-verr-num-au-demarrage-sur-ubuntu/)
```bash
sudo apt install dbus-x11 # Corrige en bug leurs du gsettings
sudo -i # Pour passer en root
xhost +SI:localuser:gdm # Donnez les droits de faire des connexions avec le serveur X à l’utilisateur gdm
su gdm -s /bin/bash # Passez à l’utilisateur gdm
gsettings set org.gnome.desktop.peripherals.keyboard numlock-state true
exit
```

## Clavier Microsoft
[source](https://askubuntu.com/questions/57079/xubuntu-make-shiftnumpad-work-like-windows)
```bash
sudo nano /etc/default/keyboard

# Modifier XKBOPTIONS="" vers XKBOPTIONS="numpad:microsoft"
```

## Alias
```bash
nano ~/.bash_aliases
```

```bash
alias ls="exa -lah"
alias cat="batcat"
alias restart="reboot"
```

## Theme pour ubuntu
```bash
sudo apt install gnome-tweaks
mkdir ~/.icons ~/.themes
```
- [WhiteSur-icon-theme](https://github.com/vinceliuice/WhiteSur-icon-theme)
```bash
./install.sh
```
- [WhiteSur-gtk-theme](https://github.com/vinceliuice/WhiteSur-gtk-theme)
```bash
./install.sh -c Dark -c Light -t all -s default -i ubuntu -N default
sudo ./tweaks.sh -g -b "/path/my-picture.jpg" 
```
Ouvrire tweaks et modifier les themes par WhiteSur
