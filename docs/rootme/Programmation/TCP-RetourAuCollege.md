#  	TCP - Retour au collège

**Lien vers le challenge :** [Challenge Root-Me](https://www.root-me.org/fr/Challenges/Programmation/TCP-Retour-au-college)
## Énoncé : 
![](img/2025-11-24-16-21-24.png)
## Procédure : 

Le challenge impose un délai de réponse très court (2 secondes), ce qui rend la résolution manuelle impossible. J'ai donc écrit un script Python pour automatiser la tâche :

1. Connexion au serveur : Utilisation de la bibliothèque socket pour établir une connexion TCP sur le port 52002.

2. Extraction des données : Réception de l'énoncé brut. J'ai identifié les positions fixes des deux nombres dans la chaîne de caractères reçue pour les extraire (via du slicing sur les index 171 et 191).

3. Calcul mathématique : Application de la formule : sqrt(nombre1)​​×nombre2​, puis arrondissement du résultat à 2 chiffres après la virgule.

4. Envoi de la réponse : Conversion du résultat en chaîne de caractères (encodée en bytes), ajout d'un saut de ligne (\n) et envoi au serveur pour récupérer le flag.


## Code : 

```py
import math
import socket

HOST = "challenge01.root-me.org"  
PORT = 52002  

with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as s:
    s.connect((HOST, PORT))
    data = s.recv(1024)
    print(data)
    print("a="+str(data[171:174]))     
    print("b="+str(data[191:195]))
    a=math.sqrt(int(data[171:174]))
    b=int(data[191:195])*a
    r=round(b, 2)
    print(r)
    c=bytes(str(r)+"\n",'utf-8')
    print("c="+c.decode())

    s.send(c)
    data2=s.recv(1024)

print(f"Received {data2!r}")
```

## Résultat
On obtient donc le flag en executant le code : 
![](img/2025-11-24-16-23-54.png)

## Flag : 

Le Flag est donc *RM{TCP_C0nnecT_4nD_m4Th}*

