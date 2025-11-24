# TPD-Les fichiers et périphériques


## 1. Les périphériques

### 1a) quoi correspondent ces périphériques ?


    /dev/null = tout ce qui est écrit dedans est éffacé c'est une corbeille

    /dev/zero = source infini d'octet 0 

    /dev/random = générateur de nombre aléatoire

    /dev/urandom = autre générateur de nombre aléatoire

    /dev/loop0 = périphérique de boucle 

### 1b)En utilisant les fonctions open (man 3 open ) et read (man 3 read), écrivez un programme qui affiche un nombre aléatoire sur un int.
Programme qui affiche un nombre aléatoire avec /dev/urandom :
```c
#include <stdio.h>
#include <stdlib.h>
#include <fcntl.h>
#include <unistd.h>
#include <errno.h>

int main() {
    int random_int;
    int fd;
    // open le fichier périphérique
    fd = open("/dev/urandom", O_RDONLY);
    if (fd == -1) {
        perror("Erreur lors de l'ouverture de /dev/urandom");
        return EXIT_FAILURE;
    }
    // read la taille d'un entier (sizeof(int))
    // On passe l'adresse de notre variable pour que read la remplisse
    ssize_t bytes_read = read(fd, &random_int, sizeof(int));
    // Affichage du résultat
    printf("Nombre aléatoire lu : %d\n", random_int);
    close(fd);

    return EXIT_SUCCESS;
}
```
## 3. Le système de fichiers /proc

### 3a)  A quoi correspondent les répertoires nommés par des numéros ?
Correspond au procéssus en cours d'utilisation avec le PID correspondant 
### 3b) A quoi correspond le fichier cmdline à l'intérieur d'un de ces répertoires ?
Contient la ligne de commande utilisé pour lancer le processus 
### 3c) A quoi correspond le fichier cwd à l'intérieur d'un de ces répertoires ?
Current Working Directory  :pointe vers le repertoir courant du processus 
### 3d) A quoi correspond le fichier exe à l'intérieur d'un de ces répertoires ?
Le fichier binaire qui execute le processus 
### 3e) Que contient le fichier /proc/devices ?
Liste des pilotes graphiques actuellement chargés.
### 3f) Que pouvez vous dire du répertoire /proc/self ?
Un lien symbolique pointant vers le repertoire du processus qui est en train d'y acceder.