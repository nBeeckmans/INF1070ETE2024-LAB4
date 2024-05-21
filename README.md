# INF1070ETE2024-LAB4

## 1.1 Création 

Ceci permet de créer et écrire le message en une seule commande ! 

```sh
echo "bonjour le monde" > bonjour
```

Avec : 
```sh
ls -l
total 4
-rw-rw-r-- 1 nb nb 17 May 21 09:38 bonjour 
```

On sait que la taille est de 17 octets ! ( On peut aussi utiliser `wc -c bonjour` pour s'assurer du résultat ! )

Avec : 
```sh
cat bonjour
bonjour le monde
```

Avec : 
```sh
ls -li
total 4
38806470 -rw-rw-r-- 1 nb nb 17 May 21 09:38 bonjour
```
L'inode ne sera probablement pas le même pour vous ! 

## Pour éditer le fichier : 
Si on utilise vim :
```sh
vim bonjour
```
éditer et sauvegarder !

```sh
ls -li
total 4
38806470 -rw-rw-r-- 1 nb nb 15 May 21 10:48 bonjour
```
La taille et la date ont changées mais pas l'inode ! (Attention : Vim peut créer un fichier temporaire et écraser le fichier bonjour lors de la sauvegarde ! L'inode pourrait donc changer) 

Si on utilise une redirection : 
```sh
echo "salut le monde" > bonjour
```

```sh
ls -li
total 4
38806470 -rw-rw-r-- 1 nb nb 15 May 21 10:27 bonjour
```

La taille et la date ont changées mais pas l'inode !  
