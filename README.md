# Référence des commandes essentielles — Windows, Linux et macOS

Ce document a pour objectif de fournir un guide de référence clair, pratique et structuré des commandes les plus utiles sur **Windows**, **Linux** et **macOS**. Il couvre les opérations courantes, quelques usages avancés, ainsi que des outils indispensables pour les développeurs et les administrateurs système.

> Les exemples ci-dessous utilisent les shells les plus courants : **PowerShell** sur Windows, **Bash/Zsh** sur Linux et macOS. Certaines commandes peuvent aussi exister sous d’autres formes selon le terminal utilisé.

---

## Vue d’ensemble rapide des équivalents

| Action                       | Windows                     | Linux               | macOS                            |
| ---------------------------- | --------------------------- | ------------------- | -------------------------------- |
| Lister un dossier            | `Get-ChildItem` / `dir`     | `ls`                | `ls`                             |
| Changer de dossier           | `Set-Location` / `cd`       | `cd`                | `cd`                             |
| Copier un fichier            | `Copy-Item` / `copy`        | `cp`                | `cp`                             |
| Déplacer / renommer          | `Move-Item` / `move`        | `mv`                | `mv`                             |
| Supprimer                    | `Remove-Item` / `del`       | `rm`                | `rm`                             |
| Lire le contenu d’un fichier | `Get-Content` / `type`      | `cat`, `less`       | `cat`, `less`                    |
| Voir les processus           | `Get-Process` / `tasklist`  | `ps`, `top`, `htop` | `ps`, `top`, `htop`              |
| Vérifier l’adresse IP        | `ipconfig`                  | `ip addr`, `ip a`   | `ifconfig`, `ipconfig getifaddr` |
| Télécharger un fichier       | `Invoke-WebRequest`, `curl` | `curl`, `wget`      | `curl`, `wget`                   |

---

# Windows

## Gestion des fichiers

### `dir` / `Get-ChildItem`

Liste les fichiers et dossiers d’un répertoire.

```powershell
dir
Get-ChildItem -Force
```

### `cd` / `Set-Location`

Change de répertoire courant.

```powershell
cd C:\Users\Public
Set-Location C:\Temp
```

### `mkdir` / `New-Item -ItemType Directory`

Crée un dossier.

```powershell
mkdir Projet
New-Item -ItemType Directory -Path C:\Temp\Logs
```

### `copy` / `Copy-Item`

Copie un fichier ou un dossier.

```powershell
copy fichier.txt C:\Backup\
Copy-Item .\rapport.pdf C:\Archives\
```

### `move` / `Move-Item`

Déplace ou renomme un fichier ou un dossier.

```powershell
move ancien.txt nouveau.txt
Move-Item .\notes.txt C:\Docs\
```

### `del` / `Remove-Item`

Supprime un fichier.

```powershell
del fichier.log
Remove-Item .\temp.txt
```

### `rmdir` / `Remove-Item -Recurse`

Supprime un dossier, avec son contenu si nécessaire.

```powershell
rmdir /s /q AncienDossier
Remove-Item .\Cache -Recurse -Force
```

### `type` / `Get-Content`

Affiche le contenu d’un fichier texte.

```powershell
type readme.txt
Get-Content .\journal.log
```

### `more`

Affiche un fichier page par page.

```powershell
more fichier.txt
```

### `findstr`

Recherche une chaîne dans un fichier ou une sortie de commande.

```powershell
findstr "erreur" log.txt
```

### `where` / `Get-Command`

Localise un exécutable ou une commande.

```powershell
where git
Get-Command python
```

### `robocopy`

Copie robuste de dossiers, très utile pour les sauvegardes et synchronisations.

```powershell
robocopy C:\Source C:\Backup /MIR /R:2 /W:2
```

**Remarque :** commande intégrée à Windows, aucune installation requise.

### `xcopy`

Copie de fichiers et dossiers, plus ancien que `robocopy`.

```powershell
xcopy C:\Source C:\Backup /E /I /Y
```

**Conseil :** privilégier `robocopy` pour un usage moderne.

### `attrib`

Modifie les attributs d’un fichier.

```powershell
attrib +h secret.txt
attrib -h secret.txt
```

### `mklink`

Crée un lien symbolique ou un lien physique.

```powershell
mklink lien.txt cible.txt
mklink /D MonLien C:\Dossier\Cible
```

---

## Système

### `systeminfo`

Affiche des informations détaillées sur la machine.

```powershell
systeminfo
```

### `ver`

Affiche la version de Windows.

```powershell
ver
```

### `hostname`

Affiche le nom de l’ordinateur.

```powershell
hostname
```

### `wmic`

Interroge des composants système via WMI. Utile mais plus ancien.

```powershell
wmic cpu get name
wmic os get caption,version
```

**Remarque :** `wmic` est considéré comme obsolète dans de nombreux contextes ; privilégier PowerShell (`Get-CimInstance`).

### `Get-CimInstance`

Récupère des informations système de manière moderne.

```powershell
Get-CimInstance Win32_OperatingSystem
Get-CimInstance Win32_Processor
```

### `sfc /scannow`

Vérifie et répare les fichiers système Windows.

```powershell
sfc /scannow
```

### `DISM`

Répare l’image Windows et les composants système.

```powershell
DISM /Online /Cleanup-Image /RestoreHealth
```

### `shutdown`

Éteint, redémarre ou programme une extinction.

```powershell
shutdown /s /t 0
shutdown /r /t 60
shutdown /l
```

### `powercfg`

Gère les options d’alimentation et les rapports énergie.

```powershell
powercfg /batteryreport
powercfg /energy
```

### `taskschd.msc`

Ouvre le Planificateur de tâches.

```powershell
start taskschd.msc
```

### `reg`

Manipule le registre Windows.

```powershell
reg query HKLM\Software\Microsoft\Windows\CurrentVersion
```

**Attention :** commande puissante, à utiliser avec prudence.

### `msinfo32`

Ouvre les Informations système.

```powershell
start msinfo32
```

### `services.msc`

Ouvre la console des services.

```powershell
start services.msc
```

---

## Réseau

### `ipconfig`

Affiche la configuration réseau.

```powershell
ipconfig
ipconfig /all
ipconfig /flushdns
```

### `ping`

Teste la connectivité réseau.

```powershell
ping 8.8.8.8
ping google.com
```

### `tracert`

Affiche le chemin réseau vers une destination.

```powershell
tracert google.com
```

### `pathping`

Combine `ping` et `tracert` avec des statistiques.

```powershell
pathping google.com
```

### `nslookup`

Interroge DNS.

```powershell
nslookup github.com
```

### `netstat`

Affiche connexions, ports et statistiques réseau.

```powershell
netstat -ano
```

### `arp`

Affiche le cache ARP.

```powershell
arp -a
```

### `netsh`

Configure le réseau avancé.

```powershell
netsh interface show interface
netsh wlan show profiles
```

### `Test-NetConnection`

Commande PowerShell très utile pour diagnostiquer les ports et la connectivité.

```powershell
Test-NetConnection google.com -Port 443
```

### `curl`

Télécharge ou interroge une ressource HTTP.

```powershell
curl https://example.com
curl -O https://example.com/fichier.zip
```

**Remarque :** intégré aux versions récentes de Windows.

### `Invoke-WebRequest`

Alternative PowerShell pour les requêtes web et téléchargements.

```powershell
Invoke-WebRequest https://example.com -OutFile page.html
```

---

## Processus

### `tasklist`

Liste les processus en cours.

```powershell
tasklist
```

### `taskkill`

Termine un processus.

```powershell
taskkill /IM notepad.exe /F
taskkill /PID 1234 /F
```

### `Get-Process`

Affiche et filtre les processus de façon plus moderne.

```powershell
Get-Process
Get-Process chrome
```

### `Stop-Process`

Arrête un processus.

```powershell
Stop-Process -Name notepad -Force
```

### `Start-Process`

Lance un programme avec des options.

```powershell
Start-Process notepad.exe
Start-Process "C:\Program Files\Git\bin\git-bash.exe"
```

### `schtasks`

Gère les tâches planifiées en ligne de commande.

```powershell
schtasks /query
```

---

## Utilitaires

### `powershell`

Ouvre PowerShell ou exécute des scripts.

```powershell
powershell
```

### `cmd`

Ouvre l’invite de commandes classique.

```powershell
cmd
```

### `echo`

Affiche une chaîne ou crée des sorties simples.

```powershell
echo Bonjour
```

### `set`

Affiche les variables d’environnement dans `cmd`.

```powershell
set PATH
```

### `Get-ChildItem Env:`

Affiche les variables d’environnement dans PowerShell.

```powershell
Get-ChildItem Env:
```

### `clip`

Envoie une sortie vers le presse-papiers.

```powershell
echo hello | clip
```

### `tree`

Affiche l’arborescence des dossiers.

```powershell
tree /F
```

### `choco`

Gestionnaire de paquets tiers pour Windows.

```powershell
choco install git -y
```

**Installation préalable :** Chocolatey.

### `winget`

Gestionnaire de paquets officiel Windows.

```powershell
winget install Git.Git
winget upgrade --all
```

**Remarque :** présent sur de nombreuses versions récentes de Windows.

### `scoop`

Gestionnaire de paquets populaire orienté développeurs.

```powershell
scoop install git
```

**Installation préalable :** Scoop.

### `git`

Gestion de versions, indispensable pour le développement.

```powershell
git clone https://github.com/user/repo.git
git status
git log --oneline --graph
```

**Installation préalable :** `winget install Git.Git`, `choco install git`, ou installation manuelle.

### `curl` et `wget`

Téléchargement et requêtes HTTP.

```powershell
curl -L -o fichier.zip https://example.com/fichier.zip
```

**Installation préalable :** `wget` n’est pas toujours natif sur Windows ; privilégier `curl` ou installer via `winget`/`choco`.

### `docker`

Conteneurisation pour développeurs et administrateurs.

```powershell
docker version
docker ps
docker run hello-world
```

**Installation préalable :** Docker Desktop ou Docker Engine selon le contexte.

---

# Linux

## Gestion des fichiers

### `ls`

Liste les fichiers et dossiers.

```bash
ls
ls -la
```

### `cd`

Change de répertoire.

```bash
cd /var/log
```

### `pwd`

Affiche le répertoire courant.

```bash
pwd
```

### `mkdir`

Crée un dossier.

```bash
mkdir projet
mkdir -p src/app/config
```

### `touch`

Crée un fichier vide ou met à jour son horodatage.

```bash
touch notes.txt
```

### `cp`

Copie des fichiers ou dossiers.

```bash
cp fichier.txt /tmp/
cp -r dossier1 dossier2
```

### `mv`

Déplace ou renomme.

```bash
mv ancien.txt nouveau.txt
mv rapport.pdf /backup/
```

### `rm`

Supprime des fichiers ou dossiers.

```bash
rm fichier.log
rm -r dossier_temp
rm -rf cache
```

**Attention :** `-rf` est destructif.

### `cat`

Affiche le contenu d’un fichier.

```bash
cat fichier.txt
```

### `less`

Lecture paginée très pratique pour les gros fichiers.

```bash
less /var/log/syslog
```

### `head` et `tail`

Affichent le début ou la fin d’un fichier.

```bash
head fichier.txt
tail -n 50 journal.log
tail -f journal.log
```

### `grep`

Recherche dans un texte ou une sortie.

```bash
grep "erreur" journal.log
grep -R "TODO" .
```

### `find`

Recherche des fichiers selon plusieurs critères.

```bash
find . -name "*.log"
find /var -type f -mtime -7
```

### `locate`

Recherche rapide dans une base indexée.

```bash
locate nginx.conf
```

**Installation préalable :** `mlocate` ou `plocate` selon la distribution.

### `tree`

Affiche une arborescence.

```bash
tree
```

**Installation préalable :** souvent `sudo apt install tree`, `sudo dnf install tree`, ou équivalent.

### `ln`

Crée des liens symboliques ou physiques.

```bash
ln -s /opt/app/config.yml config.yml
```

---

## Système

### `uname`

Affiche des informations système.

```bash
uname -a
```

### `hostnamectl`

Affiche et gère le nom d’hôte et certaines infos système.

```bash
hostnamectl
```

### `lsb_release`

Donne des informations sur la distribution.

```bash
lsb_release -a
```

**Installation préalable :** `lsb-release` peut être nécessaire selon la distribution.

### `cat /etc/os-release`

Affiche l’identité de la distribution.

```bash
cat /etc/os-release
```

### `df`

Affiche l’espace disque utilisé.

```bash
df -h
```

### `du`

Mesure l’espace occupé par les fichiers et dossiers.

```bash
du -sh .
du -sh *
```

### `free`

Affiche l’utilisation mémoire.

```bash
free -h
```

### `uptime`

Montre depuis combien de temps la machine tourne.

```bash
uptime
```

### `date`

Affiche ou règle la date.

```bash
date
```

### `timedatectl`

Gère l’heure système et le fuseau horaire.

```bash
timedatectl
```

### `journalctl`

Consulte les journaux systemd.

```bash
journalctl
journalctl -xe
journalctl -u ssh
```

### `systemctl`

Gère les services systemd.

```bash
systemctl status nginx
sudo systemctl restart ssh
sudo systemctl enable docker
```

### `service`

Commande plus ancienne pour gérer les services.

```bash
service ssh status
```

### `mount` / `umount`

Monte ou démonte un système de fichiers.

```bash
mount
sudo mount /dev/sdb1 /mnt/usb
sudo umount /mnt/usb
```

### `blkid`

Affiche les identifiants des périphériques de blocs.

```bash
sudo blkid
```

### `fdisk` / `lsblk`

Inspecte les partitions et périphériques.

```bash
lsblk
sudo fdisk -l
```

### `dmesg`

Affiche les messages du noyau.

```bash
dmesg | less
```

### `reboot` / `shutdown`

Redémarre ou éteint la machine.

```bash
sudo reboot
sudo shutdown -h now
sudo shutdown -r now
```

---

## Réseau

### `ip`

Commande moderne de gestion réseau.

```bash
ip addr
ip route
ip link
```

### `ifconfig`

Commande historique, encore présente sur certains systèmes.

```bash
ifconfig
```

**Remarque :** souvent fournie par le paquet `net-tools`.

### `ping`

Teste la connectivité.

```bash
ping -c 4 google.com
```

### `traceroute`

Affiche le chemin réseau.

```bash
traceroute google.com
```

**Installation préalable :** `sudo apt install traceroute` ou équivalent.

### `ss`

Remplace souvent `netstat` pour voir sockets et connexions.

```bash
ss -tulpen
```

### `netstat`

Affiche les connexions réseau et ports.

```bash
netstat -tulpen
```

**Installation préalable :** `net-tools`.

### `nslookup`

Interroge le DNS.

```bash
nslookup github.com
```

### `dig`

Outil DNS plus avancé que `nslookup`.

```bash
dig github.com
dig +short github.com
```

**Installation préalable :** `dnsutils` ou `bind-tools` selon la distribution.

### `host`

Interroge rapidement le DNS.

```bash
host github.com
```

### `curl`

Télécharge ou appelle des API HTTP.

```bash
curl -I https://example.com
curl -L -o fichier.zip https://example.com/fichier.zip
```

### `wget`

Téléchargement fiable depuis le terminal.

```bash
wget https://example.com/fichier.zip
wget -c https://example.com/fichier.zip
```

### `mtr`

Combine `ping` et `traceroute`.

```bash
mtr google.com
```

**Installation préalable :** `sudo apt install mtr` ou équivalent.

### `arp`

Affiche le cache ARP.

```bash
arp -a
```

### `nmcli`

Gère NetworkManager en ligne de commande.

```bash
nmcli device status
nmcli connection show
```

**Installation préalable :** généralement présent si NetworkManager est utilisé.

---

## Processus

### `ps`

Affiche les processus actifs.

```bash
ps aux
ps -ef
```

### `top`

Vue dynamique des processus.

```bash
top
```

### `htop`

Version améliorée et interactive de `top`.

```bash
htop
```

**Installation préalable :** `sudo apt install htop`, `sudo dnf install htop`, etc.

### `pgrep`

Recherche un processus par nom.

```bash
pgrep nginx
```

### `pkill`

Termine des processus par nom.

```bash
pkill nginx
pkill -f "python app.py"
```

### `kill`

Termine un processus par PID.

```bash
kill 1234
kill -9 1234
```

### `nice` / `renice`

Ajuste la priorité d’un processus.

```bash
nice -n 10 commande
sudo renice -n 5 -p 1234
```

### `jobs`, `bg`, `fg`

Gère les tâches en arrière-plan du shell.

```bash
sleep 100 &
jobs
bg
fg %1
```

### `nohup`

Lance une commande qui continue après déconnexion.

```bash
nohup ./script.sh &
```

---

## Utilitaires

### `sudo`

Exécute une commande avec privilèges administrateur.

```bash
sudo apt update
```

### `su`

Bascule vers un autre utilisateur, souvent `root`.

```bash
su -
```

### `man`

Affiche les pages de manuel.

```bash
man ls
```

### `which`

Localise une commande dans le PATH.

```bash
which python3
```

### `whereis`

Localise binaires, sources et manuels.

```bash
whereis git
```

### `alias`

Crée des raccourcis de commande.

```bash
alias ll='ls -la'
```

### `env` / `printenv`

Affiche les variables d’environnement.

```bash
env
printenv PATH
```

### `export`

Définit une variable d’environnement pour la session.

```bash
export EDITOR=vim
```

### `tar`

Archive et compresse des fichiers.

```bash
tar -cvf archive.tar dossier/
tar -xvf archive.tar
tar -czvf archive.tar.gz dossier/
```

### `zip` / `unzip`

Compression et extraction ZIP.

```bash
zip -r archive.zip dossier/
unzip archive.zip
```

**Installation préalable :** `zip` et `unzip` peuvent nécessiter une installation.

### `chmod`

Change les permissions.

```bash
chmod +x script.sh
chmod 644 fichier.txt
```

### `chown`

Change le propriétaire.

```bash
sudo chown user:user fichier.txt
```

### `getfacl` / `setfacl`

Gère les ACL.

```bash
getfacl fichier.txt
sudo setfacl -m u:alice:rwx fichier.txt
```

**Installation préalable :** paquet `acl` selon la distribution.

### `rsync`

Synchronisation efficace de fichiers et sauvegardes.

```bash
rsync -avh source/ destination/
rsync -avh --delete source/ destination/
```

### `cron` / `crontab`

Planifie des tâches récurrentes.

```bash
crontab -e
crontab -l
```

### `at`

Planifie une commande ponctuelle.

```bash
echo "backup.sh" | at now + 1 hour
```

**Installation préalable :** paquet `at`.

### `git`

Indispensable en développement.

```bash
git init
git clone https://github.com/user/repo.git
git status
git diff
git branch
git log --oneline --graph --decorate
```

### `docker`

Conteneurisation pour développement et exploitation.

```bash
docker ps
docker images
docker run -it ubuntu bash
```

**Installation préalable :** Docker Engine ou Docker Desktop selon l’environnement.

### `kubectl`

Gestion de clusters Kubernetes.

```bash
kubectl get pods
kubectl get nodes
```

**Installation préalable :** binaire `kubectl`.

### `ssh`

Connexion distante sécurisée.

```bash
ssh user@serveur
```

### `scp`

Copie sécurisée via SSH.

```bash
scp fichier.txt user@serveur:/tmp/
```

### `sftp`

Transfert de fichiers via SSH.

```bash
sftp user@serveur
```

---

## Gestion des paquets

### Debian / Ubuntu : `apt`

```bash
sudo apt update
sudo apt install curl git htop
sudo apt upgrade
```

### Fedora / RHEL / CentOS : `dnf` ou `yum`

```bash
sudo dnf install curl git htop
sudo dnf update
```

### Arch Linux : `pacman`

```bash
sudo pacman -S curl git htop
sudo pacman -Syu
```

### openSUSE : `zypper`

```bash
sudo zypper install curl git htop
sudo zypper refresh
```

---

# macOS

## Gestion des fichiers

### `ls`

Liste les fichiers et dossiers.

```bash
ls
ls -la
```

### `cd`

Change de répertoire.

```bash
cd ~/Documents
```

### `pwd`

Affiche le répertoire courant.

```bash
pwd
```

### `mkdir`

Crée un dossier.

```bash
mkdir Projet
mkdir -p ~/Sites/mon-app
```

### `cp`

Copie des fichiers ou dossiers.

```bash
cp fichier.txt /tmp/
cp -R dossier1 dossier2
```

### `mv`

Déplace ou renomme.

```bash
mv ancien.txt nouveau.txt
```

### `rm`

Supprime un fichier ou un dossier.

```bash
rm fichier.txt
rm -rf dossier_temp
```

### `cat`, `less`, `head`, `tail`

Lecture de fichiers texte.

```bash
cat fichier.txt
less /var/log/system.log
head -n 20 fichier.txt
tail -f /var/log/system.log
```

### `find`

Recherche avancée de fichiers.

```bash
find . -name "*.log"
```

### `grep`

Recherche textuelle.

```bash
grep "fail" system.log
```

### `ln -s`

Crée un lien symbolique.

```bash
ln -s /Applications/MonApp.app/Contents/MacOS/app app
```

### `open`

Ouvre un fichier, dossier ou application avec l’interface graphique.

```bash
open .
open document.pdf
open -a Safari https://example.com
```

### `pbcopy` / `pbpaste`

Copie vers et depuis le presse-papiers.

```bash
echo "texte" | pbcopy
pbpaste
```

### `mdfind`

Recherche via Spotlight.

```bash
mdfind "nom:Terminal"
```

---

## Système

### `uname`

Affiche des informations système.

```bash
uname -a
```

### `sw_vers`

Affiche la version de macOS.

```bash
sw_vers
```

### `system_profiler`

Donne des informations détaillées sur le matériel et le système.

```bash
system_profiler SPHardwareDataType
```

### `diskutil`

Gère les disques et volumes.

```bash
diskutil list
diskutil info /Volumes/Macintosh\ HD
```

### `df`

Affiche l’espace disque.

```bash
df -h
```

### `du`

Affiche l’espace utilisé.

```bash
du -sh ~/Downloads
```

### `launchctl`

Gère les services et agents launchd.

```bash
launchctl list
```

### `scutil`

Interroge la configuration système et réseau.

```bash
scutil --get ComputerName
scutil --get HostName
```

### `spctl`

Gère Gatekeeper et les politiques de sécurité.

```bash
spctl --status
```

### `softwareupdate`

Recherche et installe les mises à jour macOS.

```bash
softwareupdate -l
sudo softwareupdate -ia
```

### `csrutil`

Utilitaire lié à la protection d’intégrité système.

```bash
csrutil status
```

**Remarque :** commande utilisée depuis Recovery Mode.

### `killall`

Termine des processus par nom.

```bash
killall Safari
```

### `shutdown`

Éteint ou redémarre la machine.

```bash
sudo shutdown -h now
sudo shutdown -r now
```

### `reboot`

Redémarre la machine.

```bash
sudo reboot
```

---

## Réseau

### `ifconfig`

Affiche et configure les interfaces réseau.

```bash
ifconfig
```

### `ipconfig`

Commande macOS utile pour certaines requêtes réseau.

```bash
ipconfig getifaddr en0
ipconfig getpacket en0
```

### `networksetup`

Gère les paramètres réseau.

```bash
networksetup -listallnetworkservices
networksetup -getinfo Wi-Fi
```

### `ping`

Teste la connectivité.

```bash
ping -c 4 google.com
```

### `traceroute`

Suit le chemin réseau.

```bash
traceroute google.com
```

### `netstat`

Affiche connexions et ports.

```bash
netstat -an
```

### `lsof -i`

Affiche les processus utilisant le réseau.

```bash
lsof -i :80
```

### `nslookup`

Interroge le DNS.

```bash
nslookup github.com
```

### `dig`

Outil DNS avancé.

```bash
dig github.com
```

### `curl`

Requêtes HTTP et téléchargements.

```bash
curl -I https://example.com
curl -L -o fichier.zip https://example.com/fichier.zip
```

### `wget`

Téléchargement en ligne de commande.

```bash
wget https://example.com/fichier.zip
```

**Installation préalable :** souvent via Homebrew.

---

## Processus

### `ps`

Liste les processus.

```bash
ps aux
```

### `top`

Vue dynamique des processus.

```bash
top
```

### `htop`

Version améliorée de `top`.

```bash
htop
```

**Installation préalable :** `brew install htop`.

### `pgrep`

Recherche un PID par nom.

```bash
pgrep Safari
```

### `pkill`

Termine des processus.

```bash
pkill Safari
```

### `kill`

Termine un processus par PID.

```bash
kill 1234
kill -9 1234
```

### `nice` / `renice`

Ajuste la priorité d’un processus.

```bash
nice -n 10 commande
sudo renice -n 5 -p 1234
```

---

## Utilitaires

### `sudo`

Exécute une commande avec élévation de privilèges.

```bash
sudo rm -rf /tmp/test
```

### `man`

Affiche le manuel.

```bash
man ls
```

### `which`

Localise une commande.

```bash
which python3
```

### `whereis`

Localise binaires et documentation.

```bash
whereis git
```

### `env` / `printenv`

Affiche les variables d’environnement.

```bash
env
printenv PATH
```

### `export`

Définit une variable d’environnement.

```bash
export EDITOR=nano
```

### `alias`

Crée un raccourci.

```bash
alias ll='ls -la'
```

### `tar`, `zip`, `unzip`

Gestion des archives.

```bash
tar -czvf archive.tar.gz dossier/
unzip archive.zip
```

### `chmod`

Change les permissions.

```bash
chmod +x script.sh
chmod 644 fichier.txt
```

### `chown`

Change le propriétaire.

```bash
sudo chown user:staff fichier.txt
```

### `rsync`

Synchronisation efficace.

```bash
rsync -avh ~/Documents/ /Volumes/Backup/Documents/
```

### `cron` / `crontab`

Planifie des tâches répétitives.

```bash
crontab -e
crontab -l
```

### `ssh`, `scp`, `sftp`

Administration distante et transferts.

```bash
ssh user@serveur
scp fichier.txt user@serveur:/tmp/
sftp user@serveur
```

### `git`

Gestion de versions.

```bash
git status
git pull
git log --oneline --graph
```

### `docker`

Conteneurisation.

```bash
docker ps
docker compose up -d
```

**Installation préalable :** Docker Desktop ou Docker Engine.

### `brew`

Gestionnaire de paquets macOS indispensable pour les outils développeurs.

```bash
brew update
brew install git htop wget
brew upgrade
```

**Installation préalable :** Homebrew.

### `mas`

Gestionnaire en ligne de commande du Mac App Store.

```bash
mas search Xcode
mas install 497799835
```

**Installation préalable :** `brew install mas`.

### `xcode-select`

Gère les outils en ligne de commande Xcode.

```bash
xcode-select --install
xcode-select -p
```

---

## Installation des outils utiles sur macOS

```bash
brew install git curl wget htop jq tree rsync docker kubectl
```

---

# Outils externes populaires

## `git`

Indispensable pour le contrôle de version.

```bash
git clone https://github.com/organisation/projet.git
git branch
git rebase main
```

## `curl`

Très utile pour tester des API, télécharger des ressources et automatiser des requêtes.

```bash
curl -X POST https://api.example.com/data
```

## `wget`

Pratique pour télécharger des fichiers de manière répétable.

```bash
wget -r https://example.com
```

## `jq`

Analyse et transforme du JSON depuis le terminal.

```bash
jq '.name' fichier.json
```

**Installation préalable :** `sudo apt install jq`, `brew install jq`, `winget install jqlang.jq` ou équivalent.

## `docker`

Permet de lancer des environnements isolés.

```bash
docker run --rm hello-world
```

## `kubectl`

Gère les ressources Kubernetes.

```bash
kubectl get pods -A
```

## `rsync`

Synchronisation fiable, idéale pour sauvegardes.

```bash
rsync -avh source/ backup/
```

---

# Astuces & raccourcis importants

* `Tab` : auto-complétion des chemins et commandes dans la plupart des shells.
* `Ctrl + C` : interrompre une commande en cours.
* `Ctrl + L` : effacer l’écran du terminal.
* `Ctrl + R` : rechercher dans l’historique du shell.
* `!!` : relancer la dernière commande, très pratique avec `sudo`.
* `sudo !!` : réexécuter la commande précédente avec privilèges administrateur.
* `history` : afficher l’historique des commandes.
* `|` : chaîner des commandes avec un pipe.
* `>` / `>>` : rediriger la sortie vers un fichier, en écrasant ou en ajoutant.
* `&` : lancer une commande en arrière-plan sur les shells Unix.
* `man commande` : consulter rapidement l’aide intégrée.
* `Get-Help` / `Get-Command` : équivalents PowerShell très utiles.
* `winget`, `choco`, `scoop` : gestionnaires de paquets Windows pratiques pour automatiser l’installation.
* `brew` : standard de facto sur macOS pour installer des outils de ligne de commande.
* `apt`, `dnf`, `pacman`, `zypper` : principaux gestionnaires de paquets Linux.
* Utiliser `--help` ou `-h` sur la majorité des commandes pour obtenir l’aide intégrée.

---

## Bonnes pratiques

* Préférer les commandes modernes quand elles existent : `systemctl` plutôt que scripts maison, `ip` plutôt que `ifconfig`, `ss` plutôt que `netstat` sur Linux.
* Éviter les suppressions agressives sans vérification, notamment `rm -rf`, `Remove-Item -Recurse -Force` et `del /s /q`.
* Tester les commandes avec des chemins temporaires avant de les utiliser en production.
* Documenter les commandes répétitives dans des scripts ou des alias.
* Pour les tâches administratives récurrentes, privilégier l’automatisation via scripts, tâches planifiées et configuration as code.

---

j'ai envie de dodo
