# John the Ripper 

 ### info "C'est quoi ?"
    **John the Ripper** (JtR) est l'un des outils de cassage de mots de passe les plus célèbres. Il fonctionne **hors ligne** (offline), c'est-à-dire qu'il tente de trouver le mot de passe correspondant à une empreinte chiffrée (hash) que vous avez récupérée.

### failure "Attention"
    L'utilisation de cet outil est strictement réservée aux environnements de test (CTF, Pentest autorisé).

---

## 1. L'Attaque par Dictionnaire (Wordlist)

C'est la méthode la plus utilisée en CTF. On fournit une liste de mots probables (comme `rockyou.txt`) et John teste chaque mot.

### Prérequis : La Wordlist Rockyou
Sur Kali Linux, si c'est la première fois, décompressez la liste :
```bash
sudo gzip -d /usr/share/wordlists/rockyou.txt.gz

```

### La commande de base 

```bash
# Syntaxe : john --wordlist=[CheminWordlist] [FichierHash]
john --wordlist=/usr/share/wordlists/rockyou.txt hash.txt
```

## 2. Identifier et Forcer un Format

Par défaut, John essaie de deviner le type de hash (MD5, SHA1...). Parfois, il se trompe ou vous demande d'être plus précis.

*Lister les formats disponibles*

```Bash
john --list=formats
```

*Forcer un format spécifique*

Si vous savez que c'est du MD5 brut :
```Bash

john --format=Raw-MD5 --wordlist=/usr/share/wordlists/rockyou.txt hash.txt
```
## 3. Craquer des mots de passe Linux (/etc/shadow)

Sur Linux, pour cracker un compte utilisateur, il faut combiner le fichier /etc/passwd et /etc/shadow. John possède un outil pour ça : unshadow.

Procédure :

    Fusionner les fichiers :
```Bash

unshadow passwd.txt shadow.txt > unshadowed.txt
```

Lancer l'attaque :

```Bash

    john --wordlist=/usr/share/wordlists/rockyou.txt unshadowed.txt
```
## 4. Voir les mots de passe trouvés

Une fois un mot de passe trouvé, John ne le réaffiche pas si vous relancez la commande (il le sauvegarde dans ~/.john/john.pot).

Pour afficher ce qui a déjà été craqué :
```Bash

john --show hash.txt
```

## 5. Utilitaires de conversion (Les "*2john")

Souvent en CTF, vous récupérez un fichier ZIP protégé ou une clé SSH, pas un simple hash. Il faut les convertir dans un format que John comprend.
```
Fichier source	Outil de conversion	Commande
Fichier ZIP	zip2john	zip2john protected.zip > hash.txt
Clé SSH (id_rsa)	ssh2john	ssh2john id_rsa > hash.txt
Fichier RAR	rar2john	rar2john archive.rar > hash.txt
Fichier Keepass	keepass2john	keepass2john database.kdbx > hash.txt
```