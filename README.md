# Security TP 

## Level 00

En utilisant une bonne command de find, on peut lister les fichiers set uid. Ici, le setuid était caché dans le dossier bin/..., qu'on ne pouvait pas voir sans ls -a et qui pouvait passer inaperçu dans la liste


## Level 01

Les 2 indices sont à décoder avec base64 --decode et nous donne un indice sur l'utilisation du path et d'un symlink.

La faille est l'utilsation de : 

1. System, qui permet d'utiliser n'importe quoi 
2. D'un chemin "relatif" à echo défini par l'env

on constate que le code utilise "echo" en se basant sur les variables d'environnement. On va donc créer un symlink de getflag, le nommer echo, le placer dans un dossier ou nous avons les permissions (~ par exemple) et changer le path pour le diriger uniquement vers le dossier ou nous avons placé notre symlink

Par la suite, lors du lancement du programme, le programme lance "echo" en mode system, mais ce "echo" est en fait getflag.


