# Cours - Les bases de la Cybersécurité



## 1. Définitions 

Voici le vocabulaire essentiel à maîtriser :

* **L'Attaquant** : Une personne qui cherche à exploiter les vulnérabilités potentielles d'un système.
* **Virus** : Un code malveillant attaché à des fichiers exécutables.
* **SSI** : La Sécurité des Systèmes d'Information.
* **Cheval de Troie (Trojan)** : Malware exécutant des opérations malveillantes sous couvert d'une fonction légitime pour tromper l'utilisateur.
* **Rootkit** : Malware complexe permettant de maintenir un accès administrateur (root) sur une machine tout en restant caché.
* **Vulnérabilité** : Faille matérielle ou logicielle qui permet d'obtenir un accès non autorisé.
* **Menace** : Cause potentielle d'incident pouvant résulter en un dommage au système.
* **Attaque** : Tentative volontaire d'exploiter une ou plusieurs vulnérabilités.
* **Intrusion** : Le fait d'accéder sans autorisation aux données d'un système. C'est la conséquence d'une attaque réussie.
* **Cyberspace** : Espace de communication constitué par l'interconnexion mondiale d'équipements (environ 18 milliards d'objets connectés).
* **Phishing (Hameçonnage)** : Technique d'ingénierie sociale (Mail ou SMS trompeur) visant à voler des informations confidentielles.

---

## 2. Le rôle de l'étudiant en Cybersécurité 

!!! info "Mission"
    Notre objectif principal se divise en deux axes :
    
    1.  **Protéger** les Systèmes d'Informations (Défense / Blue Team).
    2.  **Détecter** les failles avant les attaquants pour les sécuriser (Offensif / Red Team).

---

## 3. Comment se protéger ? 

La sécurité repose sur plusieurs couches (défense en profondeur) :

### Sécurité Physique
* Sécuriser l'accès physique aux machines (badges, serrures).
* Protéger les serveurs au sein de l'entreprise.
* Sensibiliser les employés aux risques.

### Sécurité Logique & Réseau
* **Protection des communications** : Utilisation de Pare-feu (Firewall) et d'Antivirus.
* **Mise à jour** : Activer les mises à jour automatiques (OS et logiciels) pour combler les failles.
* **Principe du moindre privilège** : Utiliser des comptes avec des droits limités (ne pas rester en Admin/Root tout le temps).

### Gestion des Mots de passe 
* Utiliser un mot de passe **différent** pour chaque service.
* Utiliser un mot de passe **long et complexe** (Majuscules, minuscules, chiffres, caractères spéciaux).
* Utiliser un **Gestionnaire de Mots de passe** (ex: Keepass, Bitwarden).

---

## 4. Outil : Zphisher 

!!! warning "Avertissement"
    Cet outil doit être utilisé uniquement dans un cadre éducatif ou lors d'un audit autorisé.

**Zphisher** est un outil de script Bash automatisé utilisé pour le Phishing.
Il permet de générer facilement des pages de connexion factices (Facebook, Google, Microsoft, etc.) pour récupérer des identifiants lors de tests d'ingénierie sociale.