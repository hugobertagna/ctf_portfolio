# Gobuster (Directory Bruteforcer)

!!! info "Qu'est-ce que Gobuster ?"
Gobuster est un outil de force brute écrit en Go. Il est conçu pour être rapide et efficace, et est utilisé pour énumérer :

* Les **répertoires** et **fichiers** cachés d'un serveur web.
* Les **sous-domaines** à partir d'une liste (wordlist).
* Les **Virtual Hosts** sur un serveur.


## 1. La Commande "Royale" (CTF) 

Si tu cherches des chemins cachés sur un site, c'est la commande standard à retenir :
```bash
gobuster dir -u [http://cible.thm](http://cible.thm) -w /usr/share/wordlists/dirb/common.txt -t 50 -x php,txt,html
```
| **Option** | **Description**                                                                                                                         |
| ---------- | --------------------------------------------------------------------------------------------------------------------------------------- |
| **`dir`**  | Spécifie le **mode de fonctionnement** de Gobuster : la recherche de **répertoires** et de fichiers sur la cible.                       |
| **`-u`**   | Définit l'**URL de la cible** (le site web) à scanner.                                                                                  |
| **`-w`**   | Indique le chemin vers la **wordlist** (liste de mots) contenant les noms de répertoires/fichiers à tester.                             |
| **`-t`**   | Fixe le nombre de **threads** concurrents à utiliser, influençant la **vitesse** du scan.                                               |
| **`-x`**   | Ajoute des **extensions de fichiers** spécifiques (par exemple, `.php`, `.html`, `.bak`) à essayer pour chaque entrée de la _wordlist_. |



## 2. Les Modes de Scan (Types d'attaque)

Gobuster fonctionne selon plusieurs modes, que tu définis immédiatement après gobuster :

| **Mode**  | **Nom**        | **Description**                                                                                           |
| --------- | -------------- | --------------------------------------------------------------------------------------------------------- |
| **dir**   | Directory/File | Mode standard. Recherche les **répertoires et fichiers cachés**.                                          |
| **dns**   | DNS Subdomains | **Force brute** pour trouver des **sous-domaines** (ex: `https://www.google.com/search?q=dev.cible.com`). |
| **vhost** | Virtual Hosts  | Recherche des **noms de serveurs virtuels** (utile sur des serveurs partagés).                            |


## 3. Options de Filtrage et de Performance

| **Option** | **Nom**    | **Description**                                                          |
| ---------- | ---------- | ------------------------------------------------------------------------ |
| **-w**     | Wordlist   | Le fichier contenant la **liste de mots à tester**.                      |
| **-t**     | Threads    | **Augmente la vitesse** du scan (attention à ne pas saturer la cible !). |
| **-x**     | Extensions | Ajoute une **liste d'extensions à tester** (ex: `.php`, `.bak`, `.zip`). |
| **-k**     | Insecure   | **Ignorer les erreurs de certificats SSL** (pour les sites en HTTPS).    |

!!! warning "Codes de Statut à surveiller"
* 200 (OK) : Fichier ou répertoire trouvé.
* 301 / 302 (Redirection) : Chemin trouvé, mais redirige ailleurs.
* 403 (Forbidden) : Chemin trouvé, mais l'accès est interdit (souvent intéressant !).
* 404 (Not Found) : Non trouvé (comportement normal).

## 4. Cheat Sheet Récapitulatif 

| **Catégorie**   | **Commande** | **Description**                                                           |
| --------------- | ------------ | ------------------------------------------------------------------------- |
| **Mode**        | `dir`        | Lance le scan de **chemins** (directories/files).                         |
|                 | `vhost`      | Lance le scan de **serveurs virtuels** (Virtual Hosts).                   |
|                 | `dns`        | Lance le scan de **sous-domaines** (DNS Subdomains).                      |
| **Ciblage**     | `-u`         | **URL de la cible**.                                                      |
|                 | `-w`         | Indique le chemin de la **wordlist**.                                     |
|                 | `-x`         | Liste des **extensions à tester** (ex: `php`, `bak`).                     |
| **Performance** | `-t`         | **Nombre de threads**.                                                    |
|                 | `-r`         | **Suivre les redirections** (Follow redirects).                           |
| **Filtrage**    | `-s`         | **Afficher** uniquement les codes de statut spécifiés (ex: `200`, `301`). |
|                 | `-b`         | **Masquer** les codes de statut spécifiques (ex: `404`).                  |
|                 | `-k`         | **Ignorer les certificats SSL non valides** (Insecure).                   |
