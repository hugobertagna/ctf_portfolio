# Nmap (Network Mapper)

!!! info "C'est quoi Nmap ?"
    **Nmap** est l'outil indispensable du pentester. Il permet de scanner un réseau pour découvrir :
    
    * Les machines actives.
    * Les ports ouverts.
    * Les services qui tournent dessus (et leur version).
    * Le système d'exploitation de la cible.

---

## 1. La Commande "Royale" (CTF) 👑

Si tu ne dois retenir qu'une seule commande pour tes challenges Root-Me ou TryHackMe, c'est celle-ci :

```bash
sudo nmap -sS -sC -sV -p- -T4 -oA scan_result <IP_CIBLE>
``` 

Décorticage de la commande :

    sudo : Nécessaire pour le scan SYN (-sS) et la détection d'OS.

    -sS : SYN Scan. Rapide et discret (ne termine pas la connexion TCP).

    -sC : Scripts par défaut. Lance des scripts basiques (titre HTML, clés SSH...).

    -sV : Version. Affiche la version précise des services (ex: Apache 2.4.1).

    -p- : Tout. Scanne les 65535 ports (pas juste les 1000 premiers).

    -T4 : Vitesse. Mode "Agressif" pour gagner du temps.

    -oA : Output All. Sauvegarde les résultats dans 3 formats différents.

## 2.Les Types de Scans

| Flag | Nom | Description |
| :--- | :--- | :--- |
| `-sS` | **SYN Scan** (Stealth) | Le scan par défaut en root. Rapide, il n'établit pas la connexion complète. |
| `-sT` | **Connect Scan** | Utilisé si on n'a pas les droits root. Plus lent et plus visible dans les logs. |
| `-sU` | **UDP Scan** | Scanne les ports UDP (DNS, SNMP...). Très lent mais crucial pour un audit complet. |

!!! warning "Attention au scan UDP" Scanner tous les ports UDP (-sU -p-) peut prendre des heures. Préférez scanner les ports connus : nmap -sU --top-ports 100 <IP>

## 3. Découverte de Services & OS

Savoir qu'un port est ouvert (Open), c'est bien. Savoir ce qui tourne derrière, c'est mieux.

    -sV (Version Detection) : Interroge le service pour récupérer sa bannière.

    -O (OS Detection) : Analyse les paquets IP pour deviner l'OS (Windows, Linux, Android...).

    -A (Aggressive) : Le "Tout-en-un". Active la détection d'OS (-O), de version (-sV), les scripts (-sC) et le traceroute.


## 4. Gestion des Ports

Par défaut, Nmap ne scanne que les 1000 ports les plus fréquents. En CTF, les admins cachent souvent des services sur des ports élevés (ex: 8080, 2222, 31337).
| Commande | Action |
| :--- | :--- |
| `-p 80` | Scanne uniquement le port 80. |
| `-p 21,22,80` | Scanne une liste précise. |
| `-p-` | **Scanne TOUS les ports** (1 à 65535). Recommandé. |
| `-p 1-1000` | Scanne une plage définie. |
| `-F` | **Fast Mode**. Scanne les 100 ports les plus courants. |

## 5. Contourner le Pare-feu (Firewall)

Souvent, la machine cible est configurée pour ignorer le "Ping". Nmap croit alors qu'elle est éteinte et arrête le scan.

!!! tip "L'option indispensable : -Pn" Utilisez toujours -Pn (No Ping) pour forcer Nmap à scanner la cible, même si elle ne répond pas au ping.

```bash
nmap -Pn <IP_CIBLE>
```
## 6. Nmap Scripting Engine (NSE)

Nmap peut utiliser des scripts (en Lua) pour automatiser des attaques ou de la reconnaissance.

    -sC : Lance les scripts par défaut (sûrs).

    --script=vuln : Lance les scripts de détection de vulnérabilités (CVE). Attention : peut être instable.

    --script=http-enum : Enumération de dossiers web (comme Gobuster, mais moins complet).

Exemple pour scanner les vulnérabilités SMB :

```bash
nmap -p 445 --script=smb-vuln* <IP>
```

## 7.Sauvegarde (Output)
Ne perdez jamais vos résultats !

    -oN scan.txt : Format "Normal" (texte lisible).

    -oX scan.xml : Format XML (pour importer dans Metasploit ou Searchsploit).

    -oA nom_scan : Output All. Crée les 3 formats d'un coup. C'est la meilleure pratique.


## 8.Cheat Sheet Récapitulatif

| Catégorie | Commande | Description |
| :--- | :--- | :--- |
| **Ports** | `-p-` | Scanne tous les 65535 ports. |
| | `-F` | Scan rapide (Top 100 ports). |
| **Technique** | `-sS` | Scan SYN (Rapide, root requis). |
| | `-sU` | Scan UDP (Lent). |
| **Infos** | `-sV` | Versions des services. |
| | `-O` | Détection de l'OS. |
| | `-A` | Mode Agressif (OS + Version + Script). |
| **Options** | `-Pn` | Ne pas Pinger (Force le scan). |
| | `-T4` | Vitesse rapide. |
| | `-v` | Verbose (Affiche les détails en direct). |
| | `-oA` | Sauvegarde tout. |