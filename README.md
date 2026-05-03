# ⚡ Commands4OS — Cheat Sheet

> Commandes essentielles pour **Windows** (CMD / PowerShell), **Linux** (Bash) et **macOS** (Zsh/Bash)

---

## 📁 Navigation & Fichiers

| Action | Windows CMD | PowerShell | Linux | macOS |
|---|---|---|---|---|
| Répertoire courant | `cd` | `pwd` | `pwd` | `pwd` |
| Lister fichiers | `dir` | `ls` / `Get-ChildItem` | `ls -la` | `ls -la` |
| Changer répertoire | `cd dossier` | `cd dossier` | `cd dossier` | `cd dossier` |
| Remonter d'un niveau | `cd ..` | `cd ..` | `cd ..` | `cd ..` |
| Créer dossier | `mkdir nom` | `mkdir nom` | `mkdir nom` | `mkdir nom` |
| Supprimer fichier | `del fichier` | `rm fichier` | `rm fichier` | `rm fichier` |
| Supprimer dossier | `rmdir /s nom` | `rm -r nom` | `rm -r nom` | `rm -r nom` |
| Copier fichier | `copy src dest` | `cp src dest` | `cp src dest` | `cp src dest` |
| Déplacer/Renommer | `move src dest` | `mv src dest` | `mv src dest` | `mv src dest` |
| Afficher contenu fichier | `type fichier` | `cat fichier` | `cat fichier` | `cat fichier` |
| Créer fichier vide | `echo. > fichier` | `New-Item fichier` | `touch fichier` | `touch fichier` |
| Chercher fichier | `where fichier` | `Get-ChildItem -r fichier` | `find / -name fichier` | `find / -name fichier` |
| Chercher dans fichier | `findstr "texte" fichier` | `Select-String "texte"` | `grep "texte" fichier` | `grep "texte" fichier` |
| Taille dossier | — | `du -sh` | `du -sh dossier` | `du -sh dossier` |
| Lien symbolique | `mklink lien cible` | `New-Item -ItemType SymbolicLink` | `ln -s cible lien` | `ln -s cible lien` |

---

## 🖥️ Système & Informations

| Action | Windows CMD | PowerShell | Linux | macOS |
|---|---|---|---|---|
| Version OS | `ver` | `$PSVersionTable` | `uname -a` | `sw_vers` |
| Infos CPU | `wmic cpu get name` | `Get-CimInstance Win32_Processor` | `lscpu` | `sysctl -n machdep.cpu.brand_string` |
| RAM utilisée | `wmic OS get FreePhysicalMemory` | `Get-CimInstance Win32_OS` | `free -h` | `vm_stat` |
| Espace disque | `wmic logicaldisk get size,freespace` | `Get-PSDrive` | `df -h` | `df -h` |
| Processus actifs | `tasklist` | `Get-Process` | `ps aux` | `ps aux` |
| Tuer un processus | `taskkill /PID 1234` | `Stop-Process -Id 1234` | `kill -9 1234` | `kill -9 1234` |
| Tuer par nom | `taskkill /IM nom.exe` | `Stop-Process -Name nom` | `pkill nom` | `pkill nom` |
| Uptime | `systeminfo \| find "Boot"` | `(Get-Date) - (gcim Win32_OS).LastBootUpTime` | `uptime` | `uptime` |
| Nom de la machine | `hostname` | `hostname` | `hostname` | `hostname` |
| Utilisateur courant | `whoami` | `whoami` | `whoami` | `whoami` |
| Variables d'env | `set` | `Get-ChildItem Env:` | `env` | `env` |
| Var d'env spécifique | `echo %VAR%` | `$env:VAR` | `echo $VAR` | `echo $VAR` |
| Définir var d'env | `set VAR=val` | `$env:VAR="val"` | `export VAR=val` | `export VAR=val` |
| Historique commandes | `doskey /history` | `Get-History` | `history` | `history` |
| Infos matériel détaillées | `msinfo32` | `Get-ComputerInfo` | `lshw` | `system_profiler` |
| Moniteur ressources | `resmon` | — | `htop` / `top` | `top` / Activity Monitor |

---

## 🌐 Réseau

| Action | Windows CMD | PowerShell | Linux | macOS |
|---|---|---|---|---|
| Adresse IP | `ipconfig` | `Get-NetIPAddress` | `ip a` / `ifconfig` | `ifconfig` / `ipconfig getifaddr en0` |
| Ping | `ping hôte` | `ping hôte` | `ping -c 4 hôte` | `ping -c 4 hôte` |
| Traceroute | `tracert hôte` | `tracert hôte` | `traceroute hôte` | `traceroute hôte` |
| DNS lookup | `nslookup domaine` | `Resolve-DnsName domaine` | `nslookup domaine` / `dig domaine` | `nslookup domaine` / `dig domaine` |
| Connexions actives | `netstat -an` | `Get-NetTCPConnection` | `ss -tuln` / `netstat -an` | `netstat -an` |
| Ports ouverts | `netstat -ano` | `Get-NetTCPConnection` | `ss -tlnp` | `lsof -i -P -n` |
| Table ARP | `arp -a` | `Get-NetNeighbor` | `arp -a` | `arp -a` |
| Route par défaut | `route print` | `Get-NetRoute` | `ip route` | `netstat -rn` |
| Télécharger fichier | — | `Invoke-WebRequest -Uri url -OutFile f` | `wget url` / `curl -O url` | `curl -O url` / `wget url` |
| Requête HTTP | — | `Invoke-RestMethod url` | `curl url` | `curl url` |
| Flush DNS | `ipconfig /flushdns` | `Clear-DnsClientCache` | `systemd-resolve --flush-caches` | `dscacheutil -flushcache` |
| Firewall statut | — | `Get-NetFirewallProfile` | `ufw status` | `pfctl -s info` |

---

## 👤 Utilisateurs & Permissions

| Action | Windows CMD | PowerShell | Linux | macOS |
|---|---|---|---|---|
| Lister utilisateurs | `net user` | `Get-LocalUser` | `cat /etc/passwd` | `dscl . list /Users` |
| Créer utilisateur | `net user nom pass /add` | `New-LocalUser nom` | `useradd nom` | `dscl . create /Users/nom` |
| Supprimer utilisateur | `net user nom /delete` | `Remove-LocalUser nom` | `userdel nom` | `dscl . delete /Users/nom` |
| Changer mot de passe | `net user nom newpass` | `Set-LocalUser nom` | `passwd nom` | `passwd nom` |
| Groupes d'un user | `net user nom` | `Get-LocalGroupMember` | `groups nom` | `id nom` |
| Ajouter à un groupe | `net localgroup grp user /add` | `Add-LocalGroupMember` | `usermod -aG grp user` | `dseditgroup -o edit -a user -t user grp` |
| Permissions fichier | `icacls fichier` | `Get-Acl fichier` | `ls -l fichier` | `ls -l fichier` |
| Modifier permissions | `icacls fichier /grant user:F` | `Set-Acl` | `chmod 755 fichier` | `chmod 755 fichier` |
| Changer propriétaire | `takeown /f fichier` | `Set-Acl` | `chown user:grp fichier` | `chown user:grp fichier` |
| Exécuter en admin | `runas /user:Administrator cmd` | `Start-Process -Verb RunAs` | `sudo commande` | `sudo commande` |

---

## 📦 Gestion de Paquets

### Windows — Winget
```powershell
winget search nom          # Chercher
winget install nom         # Installer
winget uninstall nom       # Désinstaller
winget upgrade             # Lister mises à jour
winget upgrade --all       # Tout mettre à jour
winget list                # Paquets installés
```

### Windows — Chocolatey
```powershell
choco install nom          # Installer
choco uninstall nom        # Désinstaller
choco upgrade all          # Tout mettre à jour
choco list --local-only    # Paquets installés
choco search nom           # Chercher
```

### Linux — APT (Debian/Ubuntu)
```bash
apt update                 # Mettre à jour les sources
apt upgrade                # Mettre à jour les paquets
apt install nom            # Installer
apt remove nom             # Désinstaller
apt purge nom              # Désinstaller + configs
apt autoremove             # Nettoyer inutilisés
apt list --installed       # Paquets installés
apt search nom             # Chercher
```

### Linux — DNF (Fedora/RHEL)
```bash
dnf update                 # Mettre à jour
dnf install nom            # Installer
dnf remove nom             # Désinstaller
dnf search nom             # Chercher
dnf list installed         # Paquets installés
```

### Linux — Pacman (Arch)
```bash
pacman -Syu                # Mettre à jour tout
pacman -S nom              # Installer
pacman -R nom              # Désinstaller
pacman -Rs nom             # Désinstaller + dépendances
pacman -Ss nom             # Chercher
pacman -Q                  # Paquets installés
```

### macOS — Homebrew
```bash
brew update                # Mettre à jour Homebrew
brew upgrade               # Mettre à jour les paquets
brew install nom           # Installer
brew uninstall nom         # Désinstaller
brew search nom            # Chercher
brew list                  # Paquets installés
brew cleanup               # Nettoyer
brew doctor                # Diagnostiquer
```

---

## ⚙️ Services & Démarrage

| Action | Windows CMD | PowerShell | Linux (systemd) | macOS (launchctl) |
|---|---|---|---|---|
| Lister services | `sc query` | `Get-Service` | `systemctl list-units` | `launchctl list` |
| Statut service | `sc query nom` | `Get-Service nom` | `systemctl status nom` | `launchctl list \| grep nom` |
| Démarrer service | `net start nom` | `Start-Service nom` | `systemctl start nom` | `launchctl start nom` |
| Arrêter service | `net stop nom` | `Stop-Service nom` | `systemctl stop nom` | `launchctl stop nom` |
| Redémarrer service | — | `Restart-Service nom` | `systemctl restart nom` | `launchctl kickstart -k nom` |
| Activer au démarrage | `sc config nom start=auto` | `Set-Service nom -StartupType Automatic` | `systemctl enable nom` | `launchctl enable nom` |
| Désactiver au démarrage | `sc config nom start=disabled` | `Set-Service nom -StartupType Disabled` | `systemctl disable nom` | `launchctl disable nom` |
| Logs service | `eventvwr` | `Get-EventLog` | `journalctl -u nom` | `log show --predicate 'processImagePath contains "nom"'` |

---

## 💾 Disques & Partitions

| Action | Windows CMD | PowerShell | Linux | macOS |
|---|---|---|---|---|
| Lister disques | `diskpart` → `list disk` | `Get-Disk` | `lsblk` | `diskutil list` |
| Lister partitions | `diskpart` → `list partition` | `Get-Partition` | `fdisk -l` | `diskutil list` |
| Monter partition | — | `Mount-DiskImage` | `mount /dev/sdb1 /mnt` | `diskutil mount /dev/disk2s1` |
| Démonter partition | — | `Dismount-DiskImage` | `umount /mnt` | `diskutil unmount /dev/disk2s1` |
| Formater partition | `format X: /fs:NTFS` | `Format-Volume -DriveLetter X` | `mkfs.ext4 /dev/sdb1` | `diskutil eraseDisk APFS nom /dev/disk2` |
| Vérifier disque | `chkdsk C:` | `Repair-Volume C` | `fsck /dev/sdb1` | `diskutil verifyDisk /dev/disk2` |
| Réparer disque | `chkdsk C: /f` | `Repair-Volume C -Scan` | `fsck -y /dev/sdb1` | `diskutil repairDisk /dev/disk2` |

---

## 🔐 Sécurité & Chiffrement

| Action | Windows | Linux | macOS |
|---|---|---|---|
| Générer clé SSH | `ssh-keygen -t ed25519` | `ssh-keygen -t ed25519` | `ssh-keygen -t ed25519` |
| Se connecter SSH | `ssh user@hôte` | `ssh user@hôte` | `ssh user@hôte` |
| Copier clé SSH | — | `ssh-copy-id user@hôte` | `ssh-copy-id user@hôte` |
| Hash MD5 | `certutil -hashfile fichier MD5` | `md5sum fichier` | `md5 fichier` |
| Hash SHA256 | `certutil -hashfile fichier SHA256` | `sha256sum fichier` | `shasum -a 256 fichier` |
| Chiffrer fichier | `cipher /e fichier` | `gpg -c fichier` | `openssl enc -aes-256-cbc -in f -out f.enc` |
| Lister certificats | `certmgr` | `openssl s_client -connect host:443` | `security find-certificate -a` |
| Pare-feu — bloquer port | `netsh advfirewall firewall add rule ...` | `ufw deny port` | `pfctl` |

---

## 🔄 Processus & Tâches Planifiées

| Action | Windows CMD | PowerShell | Linux | macOS |
|---|---|---|---|---|
| Lister tâches planifiées | `schtasks /query` | `Get-ScheduledTask` | `crontab -l` | `crontab -l` |
| Créer tâche planifiée | `schtasks /create ...` | `Register-ScheduledTask` | `crontab -e` | `crontab -e` |
| Supprimer tâche | `schtasks /delete /tn nom` | `Unregister-ScheduledTask` | `crontab -r` | `crontab -r` |
| Processus en arrière-plan | `start /b commande` | `Start-Job { commande }` | `commande &` | `commande &` |
| Jobs en cours | — | `Get-Job` | `jobs` | `jobs` |
| Priorité processus | `wmic process ... priority` | `Set-Process -Priority` | `nice -n val cmd` / `renice` | `renice -n val -p PID` |

---

## 📝 Texte & Redirections

| Action | Windows CMD | PowerShell | Linux/macOS |
|---|---|---|---|
| Rediriger sortie vers fichier | `cmd > fichier` | `cmd > fichier` | `cmd > fichier` |
| Ajouter à fichier | `cmd >> fichier` | `cmd >> fichier` | `cmd >> fichier` |
| Rediriger erreurs | `cmd 2> erreurs` | `cmd 2> erreurs` | `cmd 2> erreurs` |
| Pipe | `cmd1 \| cmd2` | `cmd1 \| cmd2` | `cmd1 \| cmd2` |
| Compter lignes | `find /c /v "" fichier` | `(Get-Content fichier).Count` | `wc -l fichier` |
| Trier | `sort fichier` | `Sort-Object` | `sort fichier` |
| Dédoublonner | — | `Select-Object -Unique` | `sort -u fichier` / `uniq` |
| Chercher et remplacer | — | `(Get-Content f) -replace "a","b"` | `sed -i 's/a/b/g' fichier` |
| Afficher début | — | `Get-Content -Head 10` | `head -n 10 fichier` |
| Afficher fin | — | `Get-Content -Tail 10` | `tail -n 10 fichier` |
| Suivi temps réel | — | `Get-Content -Wait` | `tail -f fichier` |

---

## 🔧 Divers & Utilitaires

| Action | Windows | Linux | macOS |
|---|---|---|---|
| Redémarrer | `shutdown /r /t 0` | `reboot` | `sudo reboot` |
| Éteindre | `shutdown /s /t 0` | `poweroff` | `sudo shutdown -h now` |
| Verrouiller session | `rundll32 user32.dll,LockWorkStation` | `loginctl lock-session` | `pmset displaysleepnow` |
| Calendrier | `cal` (si installé) | `cal` | `cal` |
| Heure système | `time` | `Get-Date` | `date` |
| Date système | `date` | `Get-Date` | `date` |
| Calculatrice CLI | — | — | `bc` |
| Compression ZIP | `compact` / `Compress-Archive` | `Compress-Archive src dest.zip` | `zip -r dest.zip src` |
| Extraction ZIP | `expand` | `Expand-Archive dest.zip` | `unzip fichier.zip` |
| Compression TAR | — | `tar -czf archive.tar.gz src` | `tar -czf archive.tar.gz src` |
| Extraction TAR | — | `tar -xzf archive.tar.gz` | `tar -xzf archive.tar.gz` |
| Effacer l'écran | `cls` | `Clear-Host` / `cls` | `clear` |
| Aide commande | `commande /?` | `Get-Help commande` | `man commande` |
| Chemin d'un binaire | `where commande` | `Get-Command commande` | `which commande` |
| Alias | `doskey alias=cmd` | `Set-Alias alias cmd` | `alias alias='cmd'` |
| Variables système | `systeminfo` | `Get-ComputerInfo` | `system_profiler SPSoftwareDataType` |

---

## 🐧 Commandes Linux/macOS exclusives

```bash
# Permissions avancées
chmod u+x fichier          # Rendre exécutable
chmod 644 fichier          # rw-r--r--
chmod 755 dossier          # rwxr-xr-x
chown -R user:groupe doss  # Récursif

# Recherche avancée
find . -name "*.log" -mtime -7    # Fichiers .log < 7 jours
find . -size +100M                 # Fichiers > 100 Mo
grep -r "texte" /chemin            # Recherche récursive

# Monitoring
watch -n 2 commande        # Répéter toutes les 2s
strace commande            # Tracer appels système (Linux)
lsof -p PID                # Fichiers ouverts par un PID
vmstat 1                   # Stats VM chaque seconde
iostat                     # Stats I/O disque

# Réseau avancé
nmap -sV hôte              # Scanner ports + versions
tcpdump -i eth0            # Capturer trafic réseau
nc -zv hôte port           # Tester connectivité port
ssh -L 8080:localhost:80 user@hôte   # Tunnel SSH local
rsync -avz src/ user@hôte:dest/      # Synchronisation

# Environnement
source ~/.bashrc           # Recharger config shell
echo $PATH                 # Afficher le PATH
export PATH="$PATH:/nouveau/chemin"  # Ajouter au PATH
```

---

## 💻 Commandes Windows exclusives (CMD/PowerShell)

```powershell
# Registre
reg query HKLM\Software\nom
reg add HKLM\Software\nom /v Valeur /t REG_SZ /d "data"
reg delete HKLM\Software\nom /v Valeur

# Réseau Windows
netsh wlan show profiles               # Profils WiFi
netsh wlan show profile "nom" key=clear # Mot de passe WiFi
netsh interface ip set address "Ethernet" static 192.168.1.10 255.255.255.0

# Active Directory (PowerShell)
Get-ADUser -Identity nom
Get-ADComputer -Filter *
New-ADUser -Name "nom" -AccountPassword (Read-Host -AsSecureString)

# WMI / CIM
Get-CimInstance Win32_BIOS
Get-CimInstance Win32_LogicalDisk
Get-CimInstance Win32_NetworkAdapterConfiguration

# Gestion modules PowerShell
Install-Module -Name NomModule
Get-Module -ListAvailable
Import-Module NomModule

# BitLocker
Enable-BitLocker -MountPoint "C:" -RecoveryPasswordProtector
Get-BitLockerVolume
```

---

## 🍎 Commandes macOS exclusives

```bash
# Spotlight / mdfind
mdfind "kMDItemDisplayName == '*.pdf'"   # Recherche Spotlight
mdutil -s /                               # Statut indexation

# Defaults (préférences système)
defaults read com.apple.finder           # Lire prefs Finder
defaults write com.apple.finder AppleShowAllFiles true
defaults delete com.apple.finder         # Réinitialiser

# Gestion apps
open -a "Nom App"                        # Ouvrir une app
osascript -e 'tell app "Finder" to quit'  # AppleScript
spctl --status                            # Statut Gatekeeper
spctl --master-disable                    # Désactiver Gatekeeper

# Réseau macOS
networksetup -listallnetworkservices
networksetup -setdnsservers Wi-Fi 8.8.8.8 8.8.4.4
airport -s                               # Scanner réseaux WiFi (/System/Library/PrivateFrameworks/...)

# TimeMachine
tmutil startbackup
tmutil listbackups
tmutil status

# Keychain
security find-generic-password -a user -s service -w
security add-generic-password -a user -s service -w pass

# Homebrew Cask (apps GUI)
brew install --cask nom-app
brew list --cask
