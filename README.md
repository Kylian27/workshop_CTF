# Workshop CTF - Tacos Tacos

L'objectif de ce workshop est de vous familiariser avec l'environnement Tryhackme et réaliser un votre premier CTF !

## Comment ça marche les CTF ? (Sur Tryhackme)

### Se connecter à l'environnement Tryhackme :

Tryhackme utilise leur propre réseau privée interne permettant à n'importe qui de s'entrainer sur un environnement sécurisé !
Donc pas de soucis à se faire concernant les autres utilisateurs de la plateforme...

----

Pour connecter votre pc à cette environnement (Tous les OS doivent suivre ces étapes):

#### Étape 1:

Avoir un compte 👍​🗿

#### Étape 2:

Allez dans Access depuis la page d'acceuil

![goto](/assets/gotoacces.png)

#### Étape 3:

Une fois que vous avez cliqué sur ***Access***, vous arriverez normalement sur cette page:

![access](/assets/access.png)

Cliquez sur ***Download configuration file*** et vous téléchargez votre fichier .ovpn (*OpenVPN*) qui contient toutes les infos nécessaires pour que votre ordi puisse se connecter au réseau privé.

----

#### ***A partir de maintenant les étapes sont différentes selon les OS***

### **Pour linux :**

Installer *OpenVPN*:

```sh
sudo apt install openvpn
```

Lancer *OpenVPN* avec le fichier .ovpn téléchargé au préalable pour se connecte au réseau:

```sh
sudo openvpn lefichier.ovpn
```

**Et voilà ! Vous êtes connecté sur le réseau de *Tryhackme*.**

----

### **Pour MacOS:**

**Assurez-vous de bien avoir le packet manager *homebrew* sur votre pc. Si il n'y est pas installé le.**

Installer *OpenVPN*:

```sh
brew install openvpn
```

Lancer *OpenVPN*:

```sh
sudo openvpn le_fichier.ovpn
```

**Et voilà ! Vous êtes connecté sur le réseau de *Tryhackme*.**

----

### **Pour Windows:**

1. **Télécharger l'application OpenVPN GUI**
   - Rendez-vous sur le site officiel d'OpenVPN.
   - Ouvrez le lien de téléchargement, sélectionnez la version la plus récente compatible avec votre machine (x64, x32, ARM) et téléchargez-la.

2. **Installer l'application**
   - Lancez l'assistant d'installation d'OpenVPN.
   - Suivez les étapes jusqu'à la fin de l'installation.
   - Si OpenVPN ne démarre pas automatiquement après l'installation, exécutez le fichier exécutable OpenVPN. **Assurez-vous de l'exécuter en tant qu'administrateur**.

3. **Télécharger votre fichier de configuration**
   - Retournez sur la page web et téléchargez votre configuration dans l'onglet "Machines".
   - Si votre région n'apparaît pas dans la liste, sélectionnez celle qui est la plus proche de vous.

4. **Gérer les connexions OpenVPN**
   - Dans la barre des tâches, en bas à droite de votre écran, cliquez sur l'icône en forme de flèche vers le haut (^).
   - Recherchez l'icône ressemblant à un moniteur avec une prise, puis faites un clic droit dessus. C'est ici que vous pourrez gérer vos connexions OpenVPN.

5. **Importer le fichier de configuration**
   - Passez la souris sur l'option **Importer** et sélectionnez **Importer un fichier**.
   - Naviguez jusqu'à votre profil OpenVPN téléchargé et importez-le.

6. **Se connecter à OpenVPN**
   - Faites un clic droit à nouveau sur l'icône OpenVPN.
   - Sélectionnez **Connecter** et attendez la notification confirmant que vous êtes connecté avec succès.

----

### Bien ! Maintenant qu'on est connecté sur Tryhackme, on va pouvoir faire ce pour quoi on est là ! Hacké.

#### Pour ce workshop, j'ai créé spécialement une room assez simple pour que vous puissiez vous même réfléchir à comment la pirater.

### Voici les étapes pour accéder à cette room:

1. Accéder à la page de la room: [Tacos Tacos](https://tryhackme.com/jr/tacostacosmsc)

2. Lancer la machine virtuelle que vous devez piraté:
    - Ouvrir l'onglet ***Task 1*** si il n'est pas déjà ouvert.
    - Cliquez sur ***Start Machine***
    - Et voilà ! Dans une minute vous aurez l'adresse IP de la machine à pirater.

<br>

## Maintenant que faire ?

### Votre objectif : Capturer les différents flags !

#### C'est quoi un flag ?

Les flags sont, dans la plupart des cas, des << tokens >> dans des fichiers *.txt* disséminer dans la machine. Chacun de ses fichiers est
accessible que avec certains droits,   notamment:

    - web.txt: Fichier accessible juste avec les droits de l'utilisateur www-data. (user qui n'a pratiquement aucun droit sur la machine.)

    - user.txt: Fichier accessible lorsqu'on a les droits d'un user lambda sur la machine, c'est-à-dire qu'il a une session, un home mais qui n'est pas un
    administrateur de la machine.

    - root.txt: Fichier accessible lorsqu'on est administrateur de la machine ou 'root'.


#### Comment les obtenir ?

Vous devez dans un premier temps accéder à la machine, ou en tout cas, pouvoir executer des commandes bash dessus.

Ça c'est un gros objectif, mais pour y arriver il faut trouver une faille permettant d'exécuter ses fameuses commandes.

#### Par où commencer ?

Pour le moment, on a rien, on a juste une adresse IP... voilà.. c'est tout.

1. Il faut trouver un moyen de scanner les ports de la machine facilement:

    - J'en connais un je crois c'est ***Nmap*** ! Regardez comment l'utiliser c'est assez simple en soi !

2. Que trouve-t-on ?

    - Bien vu, des ports ouverts ! Ceux qui ne savent pas à quoi correspondent les différents ports ouvert qui sont
    actuellement ouvert, je vous laisse chercher ! (C'est pas long)

3. Maintenant qu'on sait ce que les ports signifient, on peut y accéder:
    
    - Waw, on peut dire que celui qui l'a créé est un sacré fan des tacos..
    - Visitons un peu les différents endroits où on a accès.
    - Tiens ? On peut chercher des fichiers ? hmmm...

<br>

----

### Petits indices :

En cherchant de mon côté, j'ai découvert ce qui était exécuté pour la recherche de fichier:

```sh
find $escapedFolder -type f -name '$query*' 2>/dev/null
```

Intéressant non ?

----

Pour la suite, on m'a dis que farfouiller un peu partout était parfois la bonne solution.

----

Des fois... l'administrateur fait vraiment des choses bizarres ?