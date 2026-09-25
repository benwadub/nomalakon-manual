# NOMALAKON — manuel et logiciel

Deux choses à télécharger :

1. **Le manuel** de la machine (PDF)
2. **Nomalakon Flasher** — pour mettre à jour le firmware, voir la carte SD, et envoyer des samples

Rien d’autre à installer (pas de pilote, pas de Node, pas de ligne de commande de développeur).

---

## 1. Manuel d’utilisation

**[Télécharger le PDF](./NOMALAKON-Manuel-utilisateur.pdf)**

---

## 2. Télécharger Nomalakon Flasher

Ouvrez la page **[Releases](https://github.com/benwadub/nomalakon-manual/releases/latest)** et prenez **un seul** fichier, selon votre ordinateur :

| Vous êtes sur… | Fichier à télécharger |
|---|---|
| Mac avec puce Apple (M1, M2, M3, M4…) | `Nomalakon Flasher-1.0.0-mac-arm64.dmg` |
| Mac Intel | `Nomalakon Flasher-1.0.0-mac-x64.dmg` |
| Windows 10 ou 11 | `Nomalakon Flasher-1.0.0-win-x64.exe` |

Pour savoir quel Mac : menu Pomme → **À propos de ce Mac**.  
« Puce Apple » = fichier **arm64**. « Processeur Intel » = fichier **x64**.

Le fichier arrive en général dans le dossier **Téléchargements**.

Le logiciel n’est pas signé par Apple ni Microsoft. C’est normal. macOS et Windows affichent un avertissement : suivez exactement les étapes ci-dessous, surtout les commandes Terminal / PowerShell.

---

## 3. Installer sur Mac (Terminal)

Ouvrez **Terminal** : Applications → Utilitaires → Terminal  
(ou Spotlight : Cmd+Espace, tapez `Terminal`, Entrée).

### Étape A — copier l’application dans Applications

**Si vous avez un Mac Apple Silicon (M1 / M2 / M3 / M4),** collez ces 3 lignes, puis Entrée :

```bash
hdiutil attach -nobrowse "$HOME/Downloads/Nomalakon Flasher-1.0.0-mac-arm64.dmg"
rm -rf "/Applications/Nomalakon Flasher.app"
cp -R "/Volumes/Nomalakon Flasher 1.0.0-arm64/Nomalakon Flasher.app" /Applications/
```

**Si vous avez un Mac Intel,** collez plutôt :

```bash
hdiutil attach -nobrowse "$HOME/Downloads/Nomalakon Flasher-1.0.0-mac-x64.dmg"
rm -rf "/Applications/Nomalakon Flasher.app"
cp -R "/Volumes/Nomalakon Flasher 1.0.0/Nomalakon Flasher.app" /Applications/
```

Si Terminal dit que le fichier est introuvable : le `.dmg` n’est pas dans Téléchargements, ou le nom ne correspond pas. Vérifiez avec :

```bash
ls "$HOME/Downloads/" | grep -i Nomalakon
```

### Étape B — éjecter le disque

**Apple Silicon :**

```bash
hdiutil detach "/Volumes/Nomalakon Flasher 1.0.0-arm64"
```

**Intel :**

```bash
hdiutil detach "/Volumes/Nomalakon Flasher 1.0.0"
```

### Étape C — autoriser l’ouverture (obligatoire)

macOS bloque souvent l’app ou la met à la corbeille. Ces deux commandes lèvent le blocage. Copiez-les **telles quelles**, une après l’autre :

```bash
xattr -cr "/Applications/Nomalakon Flasher.app"
```

```bash
codesign --force --deep --sign - "/Applications/Nomalakon Flasher.app"
```

La deuxième peut afficher quelques lignes. Tant qu’il n’y a pas `error`, c’est bon.

### Étape D — lancer

```bash
open -a "Nomalakon Flasher"
```

Si macOS demande encore confirmation : clic droit sur **Nomalakon Flasher** dans Applications → **Ouvrir** → **Ouvrir**.  
Ou : Réglages système → Confidentialité et sécurité → **Autoriser quand même**.

Vous refaites les étapes C et D seulement après une mise à jour du logiciel.

---

## 4. Installer sur Windows (PowerShell)

1. Téléchargez `Nomalakon Flasher-1.0.0-win-x64.exe` (voir le tableau plus haut).
2. Ouvrez **PowerShell** : cliquez le menu Démarrer, tapez `PowerShell`, Entrée.

Collez **cette ligne**, puis Entrée (elle retire le verrou « fichier Internet ») :

```powershell
Unblock-File -Path "$env:USERPROFILE\Downloads\Nomalakon Flasher-1.0.0-win-x64.exe"
```

Puis lancez l’installeur :

```powershell
Start-Process "$env:USERPROFILE\Downloads\Nomalakon Flasher-1.0.0-win-x64.exe"
```

Si Windows affiche **« Windows a protégé votre PC »** :

1. cliquez **Informations complémentaires** ;
2. cliquez **Exécuter quand même**.

Suivez l’installeur. Un raccourci bureau est proposé. Ensuite, ouvrez **Nomalakon Flasher**.

Si PowerShell dit que le fichier est introuvable, listez Téléchargements :

```powershell
Get-ChildItem "$env:USERPROFILE\Downloads" | Where-Object { $_.Name -like "*Nomalakon*" }
```

---

## 5. Première utilisation

1. Allumez le Nomalakon.
2. Branchez-le en **USB** à l’ordinateur (évitez un petit hub sans alimentation).
3. Ouvrez **Nomalakon Flasher**.
4. Choisissez :
   - **Firmware Updater** — envoyer une mise à jour ;
   - **Folder Explorer** — voir la carte SD à côté de vos dossiers ;
   - **Sample Transfer** — préparer des samples et les envoyer sur la carte.

Ne débranchez pas le câble pendant un flash ou un transfert.

---

## En cas de blocage

**Mac — « logiciel malveillant » ou l’icône part à la corbeille**  
Ce n’est pas un virus. Refaites les deux commandes de l’étape C, puis `open -a "Nomalakon Flasher"`.

**Windows — SmartScreen**  
L’éditeur est inconnu (pas de certificat payant). Informations complémentaires → Exécuter quand même.

**La carte SD n’apparaît pas**  
Câble USB, machine allumée, relancez le logiciel.

---

MidiBen / Nomalakon. Ce dépôt public contient le manuel, le guide d’installation et les installeurs. Le code source n’est pas ici.
