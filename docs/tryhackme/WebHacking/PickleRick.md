# Pickle Rick CTF



## Procédure : 

### FLAG 1 :
On commence avec un scan : 
![](img/2025-11-24-21-15-21.png)

On voit qu'on peut aller sur le port 80 donc http : 
http://10.82.134.213/

On arrive sur cette page :
![](img/2025-11-24-21-15-53.png)
En inspectant le code source on à : 
![](img/2025-11-24-21-16-09.png)
On récupère donc l'username : 
    - *R1ckRul3s*
On a donc un username.


On utilise ensuite gobuster pour découvrir les directory qu'on peut utiliser : 

![](img/2025-11-24-21-18-55.png)

On a donc pleins de choses intéressantes :
    -robots.txt
    -/assets

On va commencer par robots.txt : 
http://10.82.134.213/robots.txt

on va curl ca : 
![](img/2025-11-24-21-20-34.png)

On a : *Wubbalubbadubdub*

On essaye maintenant de se connecter à http://<ip>/login.php
![](img/2025-11-24-21-26-42.png)
Ca marche, 

On essaye l'user et le mdp :
user : *R1ckRul3s*
psswd : *Wubbalubbadubdub*

On arrive sur http://10.82.134.213/portal.php
![](img/2025-11-24-21-27-37.png)

On voit donc maintenant un command pannel, c'est une console utilisable, on va tester des commandes :

*ls -l*
![](img/2025-11-24-21-28-36.png)

On a pleins de nouveau fichier à découvrir : 

On curl : http://10.82.134.213/Sup3rS3cretPickl3Ingred.txt
![](img/2025-11-24-21-29-36.png)
On à le premier ingrédient ! 

FLAG 1 : *mr. meeseek hair*


### FLAG 2:

On va se balader sur le système :

*ls /home/*
![](img/2025-11-24-21-32-10.png)


*ls /home/rick*
![](img/2025-11-24-21-32-53.png)


On va lire le fichier pour voir le nouveau flag : 
*less /home/rick/"second ingredients"*
![](img/2025-11-24-21-33-49.png)

On a maintenant : *1 jerry tear*

FLAG 2 : *1 jerry tear*


### FLAG 3 : 

![](img/2025-11-24-21-35-09.png)


On recupère les privilèges assez facilement :
*sudo -l*
![](img/2025-11-24-21-36-23.png)


On peut donc utiliser sudo ici ! 

on va donc voir le dossier root : 
*sudo ls -l /root/*
![](img/2025-11-24-21-37-13.png)


On peut pas utiliser cat donc on utilise less :

*sudo less /root/3rd.txt*

On obtient donc le troisième et dernier flag : 

![](img/2025-11-24-21-38-49.png)

FLAG 3 : fleeb juice 

## On obtient donc les 3 flags et le CTF est terminé !