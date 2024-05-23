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

## 1.2 Renommage, type et extention 

```sh
mv bonjour ave 
```

Nous donne donc : 

```sh
ls -l
total 4
-rw-rw-r-- 1 nb nb 15 May 21 10:48 ave
```

Avec : 
```sh
file ave 
ave: ASCII text
```

`ave` est un fichier ASCII !

On renomme avec : 
```sh
mv ave ave.png
```

On voit que le type reste le même ! 
```sh
file ave.png 
ave.png: ASCII text
```

Le contenu n'a pas changé ! 

```sh
cat ave.txt 
salut le monde
```
On met la bonne extention : 
```sh
mv ave.png ave.txt
```

Ceci n'impacte pas la capacité à lire ou éditer le fichier ! 

```sh 
stat ave.txt
  File: ave.txt
  Size: 15              Blocks: 8          IO Block: 4096   regular file
Device: 10303h/66307d   Inode: 38806470    Links: 1
Access: (0664/-rw-rw-r--)  Uid: ( 1000/      nb)   Gid: ( 1000/      nb)
Access: 2024-05-21 10:48:35.518182399 -0400
Modify: 2024-05-21 10:48:35.518182399 -0400
Change: 2024-05-21 11:02:42.674064823 -0400
 Birth: 2024-05-21 10:48:35.518182399 -0400
```

Création de fichiers :

```sh 
echo Bonjour > jour.txt 
echo Bonsoir > soir.txt 
echo "Bonne nuit" > nuit.txt
```

donne : 

```sh 
ls -l
total 16
-rw-rw-r-- 1 nb nb 15 May 21 10:48 ave.txt
-rw-rw-r-- 1 nb nb  8 May 22 13:39 jour.txt
-rw-rw-r-- 1 nb nb 11 May 22 13:59 nuit.txt
-rw-rw-r-- 1 nb nb  8 May 22 13:39 soir.txt
```

et : 

```sh 
cat jour.txt 
Bonjour
cat nuit.txt 
Bonne nuit
cat soir.txt 
Bonsoir
```


Écrasement de fichiers : 

```sh 
mv jour.txt soir.txt

ls -l
total 12
-rw-rw-r-- 1 nb nb 15 May 21 10:48 ave.txt
-rw-rw-r-- 1 nb nb 11 May 22 13:59 nuit.txt
-rw-rw-r-- 1 nb nb  8 May 22 13:39 soir.txt

cat soir.txt
Bonjour
```

"Backup" de fichiers : 

```sh
mv -b ave.txt nuit.txt

ls -l 
total 12
-rw-rw-r-- 1 nb nb 15 May 21 10:48 nuit.txt
-rw-rw-r-- 1 nb nb 11 May 22 13:59 nuit.txt~
-rw-rw-r-- 1 nb nb  8 May 22 13:39 soir.txt

cat nuit.txt 
salut le monde
cat nuit.txt~
Bonne nuit
```

```sh 
cp nuit.txt ave.txt 
```
donne : 
```sh
stat nuit.txt
  File: nuit.txt
  Size: 15              Blocks: 8          IO Block: 4096   regular file
Device: 10303h/66307d   Inode: 38806470    Links: 1
Access: (0664/-rw-rw-r--)  Uid: ( 1000/      nb)   Gid: ( 1000/      nb)
Access: 2024-05-21 10:48:35.518182399 -0400
Modify: 2024-05-21 10:48:35.518182399 -0400
Change: 2024-05-22 14:06:57.636638458 -0400
 Birth: 2024-05-21 10:48:35.518182399 -0400
stat ave.txt 
  File: ave.txt
  Size: 15              Blocks: 8          IO Block: 4096   regular file
Device: 10303h/66307d   Inode: 38807526    Links: 1
Access: (0664/-rw-rw-r--)  Uid: ( 1000/      nb)   Gid: ( 1000/      nb)
Access: 2024-05-22 14:19:09.236367016 -0400
Modify: 2024-05-22 14:19:09.236367016 -0400
Change: 2024-05-22 14:19:09.236367016 -0400
 Birth: 2024-05-22 14:19:09.236367016 -0400
```

```sh 
cp -p soir.txt matin.txt
```

donne (la date d'accès et de modification sont restées les mêmes): 

```sh 
stat soir.txt 
  File: soir.txt
  Size: 8               Blocks: 8          IO Block: 4096   regular file
Device: 10303h/66307d   Inode: 38807647    Links: 1
Access: (0664/-rw-rw-r--)  Uid: ( 1000/      nb)   Gid: ( 1000/      nb)
Access: 2024-05-22 13:39:35.637821124 -0400
Modify: 2024-05-22 13:39:35.641821204 -0400
Change: 2024-05-22 14:02:07.105514644 -0400
 Birth: 2024-05-22 13:39:35.637821124 -0400

stat matin.txt
  File: matin.txt
  Size: 8               Blocks: 8          IO Block: 4096   regular file
Device: 10303h/66307d   Inode: 38807529    Links: 1
Access: (0664/-rw-rw-r--)  Uid: ( 1000/      nb)   Gid: ( 1000/      nb)
Access: 2024-05-22 13:39:35.637821124 -0400
Modify: 2024-05-22 13:39:35.641821204 -0400
Change: 2024-05-22 14:19:40.336796521 -0400
 Birth: 2024-05-22 14:19:40.332796465 -0400
```

```sh
cp -b nuit.txt matin.txt
``` 
donne : 

```sh 
ls -l 
total 40
-rw-rw-r-- 1 nb nb    8 May 23 08:24 ave.txt
drwxrwxr-x 4 nb nb 4096 May 23 08:14 cours
drwxrwxr-x 2 nb nb 4096 May 23 08:14 doc
-rw-rw-r-- 1 nb nb   15 May 23 10:45 matin.txt
-rw-rw-r-- 1 nb nb   15 May 23 08:23 matin.txt~
-rw-rw-r-- 1 nb nb   15 May 21 10:48 nuit.txt
-rw-rw-r-- 1 nb nb   11 May 22 13:59 nuit.txt~
-rw-rw-r-- 1 nb nb    8 May 22 13:39 soir.txt
drwxrwxr-x 4 nb nb 4096 May 23 08:19 Web
```

```sh 
cp -b --suffix=.old  matin.txt~ ave.txt
```
donne : 

```sh
ls -l
total 44
-rw-rw-r-- 1 nb nb   15 May 23 10:53 ave.txt
-rw-rw-r-- 1 nb nb    8 May 23 08:24 ave.txt.old
drwxrwxr-x 4 nb nb 4096 May 23 08:14 cours
drwxrwxr-x 2 nb nb 4096 May 23 08:14 doc
-rw-rw-r-- 1 nb nb   15 May 23 10:45 matin.txt
-rw-rw-r-- 1 nb nb   15 May 23 08:23 matin.txt~
-rw-rw-r-- 1 nb nb   15 May 21 10:48 nuit.txt
-rw-rw-r-- 1 nb nb   11 May 22 13:59 nuit.txt~
-rw-rw-r-- 1 nb nb    8 May 22 13:39 soir.txt
drwxrwxr-x 4 nb nb 4096 May 23 08:19 Web
```

# Repertoires 

```sh
mkdir dir 
mv ave.txt dir/
```

donne : 

```sh 
stat dir/ave.txt 
  File: dir/ave.txt
  Size: 15              Blocks: 8          IO Block: 4096   regular file
Device: 10303h/66307d   Inode: 38807373    Links: 1
Access: (0664/-rw-rw-r--)  Uid: ( 1000/      nb)   Gid: ( 1000/      nb)
Access: 2024-05-23 10:53:51.414990081 -0400
Modify: 2024-05-23 10:53:51.414990081 -0400
Change: 2024-05-23 10:55:34.781709675 -0400
 Birth: 2024-05-23 10:53:51.414990081 -0400
```

Création de `cours/inf1070/avenue.txt` : 
```sh 
mkdir -p cours/inf1070
cp dir/ave.txt cours/inf1070/avenue.txt 
```

Création de `cours/inf1120/avenue.txt` : 

```sh 
cd dir/
mkdir ../cours/inf1120
```

Utilisation de `tree` :
```sh
cd ..
tree cours/
cours/
├── inf1070
│   └── avenue.txt
└── inf1120
```

2 méthodes de créations : 

```sh 
mkdir -p Web/inf3190/examen Web/inf3190/quiz Web/inf3190/tp Web/INF5190/evaluation
```

```sh 
mkdir -p Web/{inf3190/{examen,quiz,tp},INF5190/evaluation}
```

déplacement relatif : 

```sh 
cd Web/INF5190/evaluation/
cd ../../inf3190/quiz/
cd -
```
`/home/nb/tmp/Web/INF5190/evaluation` est donné comme résultat par `cd -` !
