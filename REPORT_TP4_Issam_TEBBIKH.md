# Compte-rendu TP3

## Exercice 1 : Gestion des utilisateurs et des groupes

### 1. Commencez par créer deux groupes groupe1 et groupe2

```console
ubuntu@ubuntu-VirtualBox:~$ sudo groupadd groupe1
ubuntu@ubuntu-VirtualBox:~$ sudo groupadd groupe2
ubuntu@ubuntu-VirtualBox:~$ 
```

### 2. Créez ensuite 4 utilisateurs u1, u2, u3, u4 avec la commande useradd, en demandant la création de leur dossier personnel et avec bash pour shell

```console
ubuntu@ubuntu-VirtualBox:~$ sudo useradd --create-home --shell /bin/bash u1
ubuntu@ubuntu-VirtualBox:~$ sudo useradd --create-home --shell /bin/bash u2
ubuntu@ubuntu-VirtualBox:~$ sudo useradd --create-home --shell /bin/bash u3
ubuntu@ubuntu-VirtualBox:~$ sudo useradd --create-home --shell /bin/bash u4
ubuntu@ubuntu-VirtualBox:~$
```

### 3. Placez les utilisateurs dans les groupes :
- u1, u2, u4 dans groupe1
- u2, u3, u4 dans groupe2

```console
ubuntu@ubuntu-VirtualBox:~$ sudo gpasswd -a u1 groupe1
Ajout de l'utilisateur u1 au groupe groupe1
ubuntu@ubuntu-VirtualBox:~$ sudo gpasswd -a u2 groupe1
Ajout de l'utilisateur u2 au groupe groupe1
ubuntu@ubuntu-VirtualBox:~$ sudo gpasswd -a u4 groupe1
Ajout de l'utilisateur u4 au groupe groupe1
ubuntu@ubuntu-VirtualBox:~$ sudo gpasswd -a u2 groupe2
Ajout de l'utilisateur u2 au groupe groupe2
ubuntu@ubuntu-VirtualBox:~$ sudo gpasswd -a u3 groupe2
Ajout de l'utilisateur u3 au groupe groupe2
ubuntu@ubuntu-VirtualBox:~$ sudo gpasswd -a u4 groupe2
Ajout de l'utilisateur u4 au groupe groupe2
ubuntu@ubuntu-VirtualBox:~$
```

### 4. Donnez deux moyens d’afficher les membres de groupe2

```console
ubuntu@ubuntu-VirtualBox:~$ grep groupe2 /etc/group
groupe2:x:1002:u2,u3,u4
ubuntu@ubuntu-VirtualBox:~$ 
```
/\*Je ne connais pas le 2ème moyen\*/

### 5. Faites de groupe1 le groupe propriétaire de /home/u1 et /home/u2 et de groupe2 le groupe propriétaire de /home/u3 et /home/u4

```console
ubuntu@ubuntu-VirtualBox:~$ sudo chgrp -R u1:groupe1 /home/u1
ubuntu@ubuntu-VirtualBox:~$ sudo chgrp -R u2:groupe1 /home/u2
ubuntu@ubuntu-VirtualBox:~$ sudo chgrp -R u3:groupe2 /home/u3
ubuntu@ubuntu-VirtualBox:~$ sudo chgrp -R u4:groupe2 /home/u4
ubuntu@ubuntu-VirtualBox:~$ cd /home
ubuntu@ubuntu-VirtualBox:/home$ ll
total 28
drwxr-xr-x  7 root   root    4096 sept. 30 15:54 ./
drwxr-xr-x 20 root   root    4096 sept. 21 16:23 ../
drwxr-xr-x  2 u1     groupe1 4096 sept. 30 15:54 u1/
drwxr-xr-x  2 u2     groupe1 4096 sept. 30 15:54 u2/
drwxr-xr-x  2 u3     groupe2 4096 sept. 30 15:54 u3/
drwxr-xr-x  2 u4     groupe2 4096 sept. 30 15:54 u4/
drwxr-xr-x 22 ubuntu ubuntu  4096 sept. 30 15:45 ubuntu/
ubuntu@ubuntu-VirtualBox:/home$
```

### 6. Remplacez le groupe primaire des utilisateurs :
- groupe1 pour u1 et u2
- groupe2 pour u3 et u4

```console
ubuntu@ubuntu-VirtualBox:/home$ sudo usermod u1 -g groupe1
ubuntu@ubuntu-VirtualBox:/home$ sudo usermod u2 -g groupe1
ubuntu@ubuntu-VirtualBox:/home$ sudo usermod u3 -g groupe2
ubuntu@ubuntu-VirtualBox:/home$ sudo usermod u4 -g groupe2
ubuntu@ubuntu-VirtualBox:/home$
```

### 7. Créez deux répertoires /home/groupe1 et /home/groupe2 pour le contenu commun aux groupes, et mettez en place les permissions permettant aux membres de chaque groupe d’écrire dans le dossier associé.

```console
ubuntu@ubuntu-VirtualBox:/home$ sudo chgrp -R groupe1 /home/groupe1
ubuntu@ubuntu-VirtualBox:/home$ sudo chgrp -R groupe2 /home/groupe2
ubuntu@ubuntu-VirtualBox:/home$
```
```console
drwxr-xr-x  9 root   root    4096 sept. 30 16:49 ./
drwxr-xr-x 20 root   root    4096 sept. 21 16:23 ../
drwxr-xr-x  2 root     groupe1 4096 sept. 30 16:49 groupe1/
drwxr-xr-x  2 root     groupe2 4096 sept. 30 16:49 groupe2/
drwxr-xr-x  2 u1     groupe1 4096 sept. 30 15:54 u1/
drwxr-xr-x  2 u2     groupe1 4096 sept. 30 15:54 u2/
drwxr-xr-x  2 u3     groupe2 4096 sept. 30 15:54 u3/
drwxr-xr-x  2 u4     groupe2 4096 sept. 30 15:54 u4/
drwxr-xr-x 22 ubuntu ubuntu  4096 sept. 30 15:45 ubuntu/
ubuntu@ubuntu-VirtualBox:/home$
```
```console
ubuntu@ubuntu-VirtualBox:/home$ sudo chmod 775 /home/groupe1
ubuntu@ubuntu-VirtualBox:/home$ sudo chmod 775 /home/groupe2
ubuntu@ubuntu-VirtualBox:/home$
```
```console
ubuntu@ubuntu-VirtualBox:/home$ ll
total 36
drwxr-xr-x  9 root   root    4096 sept. 30 16:49 ./
drwxr-xr-x 20 root   root    4096 sept. 21 16:23 ../
drwxrwxr-x  2 root     groupe1 4096 sept. 30 16:49 groupe1/
drwxrwxr-x  2 root     groupe2 4096 sept. 30 16:49 groupe2/
drwxr-xr-x  2 u1     groupe1 4096 sept. 30 15:54 u1/
drwxr-xr-x  2 u2     groupe1 4096 sept. 30 15:54 u2/
drwxr-xr-x  2 u3     groupe2 4096 sept. 30 15:54 u3/
drwxr-xr-x  2 u4     groupe2 4096 sept. 30 15:54 u4/
drwxr-xr-x 22 ubuntu ubuntu  4096 sept. 30 15:45 ubuntu/
ubuntu@ubuntu-VirtualBox:/home$
```

### 8. Comment faire pour que, dans ces dossiers, seul le propriétaire d’un fichier ait le droit de renommer ou supprimer ce fichier ?


Activer de manière cummuler le sticky bit et le Set-User-ID pour les deux groupes

```console
ubuntu@ubuntu-VirtualBox:/home$ sudo chmod 5775 /home/groupe2
ubuntu@ubuntu-VirtualBox:/home$ sudo chmod 5775 /home/groupe2
ubuntu@ubuntu-VirtualBox:/home$ ll
total 36
drwxr-xr-x  9 root   root    4096 sept. 30 21:06 ./
drwxr-xr-x 20 root   root    4096 sept. 21 16:23 ../
drwsrwxr-t  2 root   groupe1 4096 oct.   1 21:27 groupe1/
drwsrwxr-t  2 root   groupe2 4096 sept. 30 21:06 groupe2/
drwxr-xr-x  2 u1     groupe1 4096 sept. 30 21:14 u1/
drwxr-xr-x  2 u2     groupe1 4096 sept. 30 21:17 u2/
drwxr-xr-x  2 u3     groupe2 4096 sept. 30 21:01 u3/
drwxr-xr-x  2 u4     groupe2 4096 sept. 30 21:01 u4/
drwxr-xr-x 22 ubuntu ubuntu  4096 oct.   1 20:36 ubuntu/
ubuntu@ubuntu-VirtualBox:/home$
```
```console
ubuntu@ubuntu-VirtualBox:/home$ su u1
Mot de passe : 
u1@ubuntu-VirtualBox:/home$ cd groupe1
u1@ubuntu-VirtualBox:/home/groupe1$ touch file
u1@ubuntu-VirtualBox:/home/groupe1$ su u2
Mot de passe : 
u2@ubuntu-VirtualBox:/home/groupe1$ rm file 
rm : supprimer 'file' qui est protégé en écriture et est du type « fichier vide » ? o
rm: impossible de supprimer 'file': Opération non permise
u2@ubuntu-VirtualBox:/home/groupe1$ mv file fichier
mv: impossible de déplacer 'file' vers 'fichier': Opération non permise
u2@ubuntu-VirtualBox:/home/groupe1$ exit
exit
u1@ubuntu-VirtualBox:/home/groupe1$ mv file fichier
u1@ubuntu-VirtualBox:/home/groupe1$ ls
fichier
u1@ubuntu-VirtualBox:/home/groupe1$ rm fichier
u1@ubuntu-VirtualBox:/home/groupe1$ ls
u1@ubuntu-VirtualBox:/home/groupe1$
```

### 9. Pouvez-vous vous connecter en tant que u1 ? Pourquoi ?

Normalement ce n'est pas possible car il faut définir un mot de passe. Je l'ai fait précédement.

### 10. Activez le compte de l’utilisateur u1 et vérifiez que vous pouvez désormais vous connecter avec son compte.

Je l'ai fait précédement. Je n'ai pas eu besoin d'activer le compte, seulement de créer un mot de passe.

### 11. Quels sont l’uid et le gid de u1 ?

```console
ubuntu@ubuntu-VirtualBox:~$ id u1
uid=1001(u1) gid=1001(groupe1) groupes=1001(groupe1)
ubuntu@ubuntu-VirtualBox:~$
```

### 12. Quel utilisateur a pour uid 1003 ?

```console
ubuntu@ubuntu-VirtualBox:~$ cat /etc/passwd | grep "1003"
u3:x:1003:1002::/home/u3:/bin/bash
ubuntu@ubuntu-VirtualBox:~$
```

### 13. Quel est l’id du groupe groupe1 ?

```console
ubuntu@ubuntu-VirtualBox:~$ grep groupe1 /etc/group
groupe1:x:1001:u1,u2,u4
ubuntu@ubuntu-VirtualBox:~$
```

### 14. Quel groupe a pour guid 1002 ? ( Rien n’empêche d’avoir un groupe dont le nom serait 1002...)

```console
ubuntu@ubuntu-VirtualBox:~$ grep 1002 /etc/group
groupe2:x:1002:u2,u3,u4
ubuntu@ubuntu-VirtualBox:~$
```

### 15. Retirez l’utilisateur u3 du groupe groupe2. Que se passe-t-il ? Expliquez.

```console
ubuntu@ubuntu-VirtualBox:~$ sudo deluser u3 groupe2
/usr/sbin/deluser: Impossible de retirer un utilisateur de son groupe primaire.
ubuntu@ubuntu-VirtualBox:~$
```

### 16. Modifiez le compte de u4 de sorte que :
- il expire au 1er juin 2019
```console
ubuntu@ubuntu-VirtualBox:~$ sudo chage -E 2019/06/01 u4
```
- il faut changer de mot de passe avant 90 jours
```console
ubuntu@ubuntu-VirtualBox:~$ sudo chage -M 90 u4
```
- il faut attendre 5 jours pour modifier un mot de passe
```console
ubuntu@ubuntu-VirtualBox:~$ sudo chage -m 5 u4
```
- l’utilisateur est averti 14 jours avant l’expiration de son mot de passe
```console
ubuntu@ubuntu-VirtualBox:~$ sudo chage -W 14 u4
```
- le compte sera bloqué 30 jours après expiration du mot de passe
```console
ubuntu@ubuntu-VirtualBox:~$ sudo chage -I 30 u4
```

### 17. Quel est l’interpréteur de commandes (Shell) de l’utilisateur root ?

```console
ubuntu@ubuntu-VirtualBox:~$ grep root /etc/passwd
root:x:0:0:root:/root:/bin/bash
ubuntu@ubuntu-VirtualBox:~$
```
L'interpretteur de commande est le bash.

### 18. à quoi correspond l’utilisateur nobody ?

Nobody est le nom conventionnel d'un compte d'utilisateur à qui aucun fichier n'appartient, qui n'est dans aucun groupe qui a des privilèges et dont les seules possibilités sont celles que tous les "autres utilisateurs" ont.

### 19. Par défaut, combien de temps la commande sudo conserve-t-elle votre mot de passe en mémoire ? Quelle commande permet de forcer sudo à oublier votre mot de passe ?

La commande sudo conserve le mot de passe 15 minutes. La commande pour forcer l'oublie du mot de passe est ___sudo -k___

## Exercice 2 : Gestion des permissions

### 1. Dans votre $HOME, créez un dossier test, et dans ce dossier un fichier ___fichier___ contenant quelques lignes de texte. Quels sont les droits sur test et fichier ?

```console
ubuntu@ubuntu-VirtualBox:/home$ cd $HOME
ubuntu@ubuntu-VirtualBox:~$ mkdir test
ubuntu@ubuntu-VirtualBox:~$ touch test/fichier
ubuntu@ubuntu-VirtualBox:~$ echo "hello" > test/fichier 
ubuntu@ubuntu-VirtualBox:~$ ll test
total 8
drwxr-xr-x  2 ubuntu ubuntu 4096 oct.   2 12:53 ./
drwxr-xr-x 23 ubuntu ubuntu 4096 oct.   2 12:53 ../
-rw-r--r--  1 ubuntu ubuntu    0 oct.   2 12:53 fichier
ubuntu@ubuntu-VirtualBox:~$ ll
total 188
.
.
drwxr-xr-x  2 ubuntu ubuntu  4096 oct.   2 12:53 test/
.
.
ubuntu@ubuntu-VirtualBox:~$  
```

Comme on peut le voir, voici les droits sur ___test___ et ___fichier___ :
- test
    - user : lecture, écriture, exécution
    - group :  lecture, exécution
    - other :  lecture, exécution
- fichier
    - user : lecture, écriture
    - group :  lecture
    - other :  lecture

### 2. Retirez tous les droits sur ce fichier (même pour vous), puis essayez de le modifier et de l’afficher en tant que root. Conclusion ?

Il est toujours possible d'afficher le contenu fichier mais pas de le modifier en tant que root. Donc l'utilisateur root garde toujours les droit de lecture, peu importe les droits affectés au fichier.

### 3. Redonnez vous les droits en écriture et exécution sur fichier puis exécutez la commande echo "echo Hello" > fichier. On a vu lors des TP précédents que cette commande remplace le contenu d’un fichier s’il existe déjà. Que peut-on dire au sujet des droits ?

Les droits définissent les actions qu'un utilisateur peut effectuer sur un fichier.

### 4. Essayez d’exécuter le fichier. Est-ce que cela fonctionne ? Et avec sudo ? Expliquez.

Exécuter un fichier revient à le lire, or l'utilisateur n'a pas de droit de lecture. Il ne peut donc pas l'exécuter. L'utilisateur root peut l'exécuter car il a le droit de lecture en permanence.

### 5. Placez-vous dans le répertoire test, et retirez-vous le droit en lecture pour ce répertoire. Listez le contenu du répertoire, puis exécutez ou affichez le contenu du fichier fichier. Qu’en déduisez-vous ? Rétablissez le droit en lecture sur test

Il n'est ni possible d'afficher le contenu du dossier, ni d'afficher le contenu de fichier, sauf en tant que root. On en déduit que les droits appliqués à un dossier affectent toutes les actions effectuées sur les fichiers qu'il contient.

### 6. Créez dans test un fichier nouveau ainsi qu’un répertoire sstest. Retirez au fichier nouveau et au répertoire test le droit en écriture. Tentez de modifier le fichier nouveau. Rétablissez ensuite le droit en écriture au répertoire test. Tentez de modifier le fichier nouveau, puis de le supprimer. Que pouvez-vous déduire de toutes ces manipulations ?

On en déduit que la modification d'un fichier dépend des droits qui lui sont affectés et sa suppression dépend des droits du dossier où il est.

### 7. Positionnez vous dans votre répertoire personnel, puis retirez le droit en exécution du répertoire test. Tentez de créer, supprimer, ou modifier un fichier dans le répertoire test, de vous y déplacer, d’en lister le contenu, etc…Qu’en déduisez vous quant au sens du droit en exécution pour les répertoires ?

Aucune de ces actions n'est possible. Donc le droit d'exécution influence toutes les actions sur le dossier.

### 8. Rétablissez le droit en exécution du répertoire test. Positionnez vous dans ce répertoire et retirez lui à nouveau le droit d’exécution. Essayez de créer, supprimer et modifier un fichier dans le répertoire test, de vous déplacer dans ssrep, de lister son contenu. Qu’en concluez-vous quant à l’influence des droits que l’on possède sur le répertoire courant ? Peut-on retourner dans le répertoire parent avec ”cd ..” ? Pouvez-vous donner une explication ?

Aucune de ces actions n'est possible. Donc le droit d'exécution influence toutes les actions sur le dossier. Il n'est même pas possible de le traverser pour aller dans un sous dossier. Il est tout de même possible de revenir au répertoire parent car il n'est pas affecté par les droits du dossier ___test___.

### 9. Rétablissez le droit en exécution du répertoire test. Attribuez au fichier fichier les droits suffisants pour qu’une autre personne de votre groupe puisse y accéder en lecture, mais pas en écriture.

```console
ubuntu@ubuntu-VirtualBox:~/test$ rm fichier 
ubuntu@ubuntu-VirtualBox:~/test$ su u1
Mot de passe : 
u1@ubuntu-VirtualBox:/home/ubuntu/test$ touch fichier
u1@ubuntu-VirtualBox:/home/ubuntu/test$ ll
total 12
drwxrwxrwx  3 ubuntu ubuntu  4096 oct.   2 13:24 ./
drwxr-xr-x 23 ubuntu ubuntu  4096 oct.   2 13:06 ../
-rw-r--r--  1 u1     groupe1    0 oct.   2 13:24 fichier
-r-xr-xr-x  1 ubuntu ubuntu     0 oct.   2 13:14 nouveau*
drwxr-xr-x  2 ubuntu ubuntu  4096 oct.   2 13:12 sstest/
u1@ubuntu-VirtualBox:/home/ubuntu/test$ echo "toto" > fichier 
u1@ubuntu-VirtualBox:/home/ubuntu/test$ cat fichier 
toto
u1@ubuntu-VirtualBox:/home/ubuntu/test$ su u2
Mot de passe : 
u2@ubuntu-VirtualBox:/home/ubuntu/test$ cat fichier 
toto
u2@ubuntu-VirtualBox:/home/ubuntu/test$ echo "titi" > fichier 
bash: fichier: Permission non accordée
u2@ubuntu-VirtualBox:/home/ubuntu/test$
```
Lorsqu'on exécute la commande ___ll___, on voit que les membres du groupe de ___u1___ ont seulement le droit de lecture. C'est pour cela que u2 ne peut pas écrire.

### 10. Définissez un umask très restrictif qui interdit à quiconque à part vous l’accès en lecture ou en écriture, ainsi que la traversée de vos répertoires. Testez sur un nouveau fichier et un nouveau répertoire.

```console
u2@ubuntu-VirtualBox:/home/ubuntu/test$ mkdir new
u2@ubuntu-VirtualBox:/home/ubuntu/test$ ll
total 20
drwxrwxrwx  4 ubuntu ubuntu  4096 oct.   2 13:36 ./
drwxr-xr-x 23 ubuntu ubuntu  4096 oct.   2 13:06 ../
-rw-r--r--  1 u1     groupe1    3 oct.   2 13:26 fichier
drwxr-xr-x  2 u2     groupe1 4096 oct.   2 13:36 new/
-r-xr-xr-x  1 ubuntu ubuntu     0 oct.   2 13:14 nouveau*
drwxr-xr-x  2 ubuntu ubuntu  4096 oct.   2 13:12 sstest/
u2@ubuntu-VirtualBox:/home/ubuntu/test$ rmdir new/
u2@ubuntu-VirtualBox:/home/ubuntu/test$ umask 0077
u2@ubuntu-VirtualBox:/home/ubuntu/test$ mkdir new
u2@ubuntu-VirtualBox:/home/ubuntu/test$ ll
total 20
drwxrwxrwx  4 ubuntu ubuntu  4096 oct.   2 13:37 ./
drwxr-xr-x 23 ubuntu ubuntu  4096 oct.   2 13:06 ../
-rw-r--r--  1 u1     groupe1    3 oct.   2 13:26 fichier
drwx------  2 u2     groupe1 4096 oct.   2 13:37 new/
-r-xr-xr-x  1 ubuntu ubuntu     0 oct.   2 13:14 nouveau*
drwxr-xr-x  2 ubuntu ubuntu  4096 oct.   2 13:12 sstest/
u2@ubuntu-VirtualBox:/home/ubuntu/test$ touch file
u2@ubuntu-VirtualBox:/home/ubuntu/test$ ll
total 20
drwxrwxrwx  4 ubuntu ubuntu  4096 oct.   2 13:39 ./
drwxr-xr-x 23 ubuntu ubuntu  4096 oct.   2 13:06 ../
-rw-r--r--  1 u1     groupe1    3 oct.   2 13:26 fichier
-rw-------  1 u2     groupe1    0 oct.   2 13:39 file
drwx------  2 u2     groupe1 4096 oct.   2 13:37 new/
-r-xr-xr-x  1 ubuntu ubuntu     0 oct.   2 13:14 nouveau*
drwxr-xr-x  2 ubuntu ubuntu  4096 oct.   2 13:12 sstest/
u2@ubuntu-VirtualBox:/home/ubuntu/test$
```

### 11. Définissez un umask très permissif qui autorise tout le monde à lire vos fichiers et traverser vos répertoires, mais n’autorise que vous à écrire. Testez sur un nouveau fichier et un nouveau répertoire.

```console
u2@ubuntu-VirtualBox:/home/ubuntu/test$ umask 0022
u2@ubuntu-VirtualBox:/home/ubuntu/test$ mkdir test
u2@ubuntu-VirtualBox:/home/ubuntu/test$ touch test
u2@ubuntu-VirtualBox:/home/ubuntu/test$ ll
total 24
drwxrwxrwx  5 ubuntu ubuntu  4096 oct.   2 13:42 ./
drwxr-xr-x 23 ubuntu ubuntu  4096 oct.   2 13:06 ../
-rw-r--r--  1 u1     groupe1    3 oct.   2 13:26 fichier
-rw-------  1 u2     groupe1    0 oct.   2 13:39 file
drwx------  2 u2     groupe1 4096 oct.   2 13:37 new/
-r-xr-xr-x  1 ubuntu ubuntu     0 oct.   2 13:14 nouveau*
drwxr-xr-x  2 ubuntu ubuntu  4096 oct.   2 13:12 sstest/
drwxr-xr-x  2 u2     groupe1 4096 oct.   2 13:42 test/
u2@ubuntu-VirtualBox:/home/ubuntu/test$
```

### 12. Définissez un umask équilibré qui vous autorise un accès complet et autorise un accès en lecture aux membres de votre groupe. Testez sur un nouveau fichier et un nouveau répertoire.

```console
u2@ubuntu-VirtualBox:/home/ubuntu/test$ umask 0027
u2@ubuntu-VirtualBox:/home/ubuntu/test$ mkdir new_test
u2@ubuntu-VirtualBox:/home/ubuntu/test$ touch new_test
u2@ubuntu-VirtualBox:/home/ubuntu/test$ ll
total 28
drwxrwxrwx  6 ubuntu ubuntu  4096 oct.   2 13:44 ./
drwxr-xr-x 23 ubuntu ubuntu  4096 oct.   2 13:06 ../
-rw-r--r--  1 u1     groupe1    3 oct.   2 13:26 fichier
-rw-------  1 u2     groupe1    0 oct.   2 13:39 file
drwx------  2 u2     groupe1 4096 oct.   2 13:37 new/
drwxr-x---  2 u2     groupe1 4096 oct.   2 13:44 new_test/
-r-xr-xr-x  1 ubuntu ubuntu     0 oct.   2 13:14 nouveau*
drwxr-xr-x  2 ubuntu ubuntu  4096 oct.   2 13:12 sstest/
drwxr-xr-x  2 u2     groupe1 4096 oct.   2 13:42 test/
u2@ubuntu-VirtualBox:/home/ubuntu/test$
```

### 13.. Transcrivez les commandes suivantes de la notation classique à la notation octale ou vice-versa (vous pourrez vous aider de la commande stat pour valider vos réponses) :
- chmod u=rx,g=wx,o=r fic  ==> chmod 534 fic
- chmod uo+w,g-rx fic en sachant que les droits initiaux de fic sont r--r-x---  ==> chmod 602 fic
- chmod 653 fic en sachant que les droits initiaux de fic sont 711 ==> chmod u-x,g+r,o+w fic
- chmod u+x,g=w,o-r fic en sachant que les droits initiaux de fic sont r--r-x--- ==> chmod 574 fic

### 14. Affichez les droits sur le programme passwd. Que remarquez-vous ? En affichant les droits du fichier /etc/passwd, pouvez-vous justifier les permissions sur le programme passwd ?

```console
ubuntu@ubuntu-VirtualBox:~/test$ ls -l /bin/passwd 
-rwsr-xr-x 1 root root 63736 mars  22  2019 /bin/passwd
ubuntu@ubuntu-VirtualBox:~/test$
```
Le programme ___passwd___ n'a pas les droit d'écriture pour les groupes et les autres utilisateurs mais les autres droits. 
```console
ubuntu@ubuntu-VirtualBox:~/test$ ls -l /etc/passwd
-rw-r--r-- 1 root root 2775 sept. 30 21:05 /etc/passwd
ubuntu@ubuntu-VirtualBox:~/test$
```
Le programme a plus de droits que le fichier pour permettre une utilisation optimal de celui-ci.
