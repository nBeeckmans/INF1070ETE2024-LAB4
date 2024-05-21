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
```

Si on utilise une redirection : 
```sh
```
