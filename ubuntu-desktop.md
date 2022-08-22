# Logiciel a install

## Via apt
```bash
sudo add-apt-repository universe
sudo apt install git make apt-transport-https curl libfuse2 exa bat

# Changement dans les nouvelles versions de gnome
sudo apt install chrome-gnome-shell -> gnome-browser-connector

# PHP
sudo apt install php8.1 php8.1-zip php8.1-intl php8.1-xml php8.1-dom php8.1-curl
```

## Autre
- [go](https://go.dev/doc/install || https://www.digitalocean.com/community/tutorials/how-to-install-go-on-ubuntu-20-04)
- [brave](https://brave.com/fr/download/)
- [sshs](https://github.com/quantumsheep/sshs)
- [slack](https://slack.com/intl/fr-fr/downloads/linux)
- [jetbrains-tools](https://www.jetbrains.com/fr-fr/toolbox-app/ || https://thirddriver.medium.com/jetbrains-toolbox-the-best-way-to-install-intellij-idea-on-linux-53c1070cd03b)
- [GitKraken](https://help.gitkraken.com/gitkraken-client/how-to-install/#deb)
- [Spotify](https://www.spotify.com/fr/download/linux/)
- [nvm - node et npm](https://github.com/nvm-sh/nvm)
- [yarn](https://classic.yarnpkg.com/lang/en/docs/install/#debian-stable)
- [composer](https://getcomposer.org/download/)

# Config

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
