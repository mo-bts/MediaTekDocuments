# MediatekDocuments 
Cette application permet de gérer les documents (livres, DVD, revues) d'une médiathèque. Elle a été codée en C# sous Visual Studio 2019. C'est une application de bureau, prévue d'être installée sur plusieurs postes accédant à la même base de données.<br>
L'application exploite une API REST pour accéder à la BDD MySQL. Des explications sont données plus loin, ainsi que le lien de récupération.
<br>MediatekDocuments est un fork de [MediaTekDocuments](https://github.com/CNED-SLAM/MediaTekDocuments).
C'est un projet réalisé dans le cadre du BTS SIO SLAM.

## Présentation
[Page de presentation du projet](https://www.nicolasfrere.fr/pages/mediatekDocuments.html)  
L'application dispose de quatre niveaux de droit différents correspondant aux services de la médiathèque :
<br>-les services non habilités ne peuvent accéder au programme.
<br>-le service comptabilité a la possibilité de consulter les livres, les dvd et revues.
<br>-l'accueil peut gérer les documents (livres, DVD, revues) mais ne peut effectuer de commandes ou prise d'abonnements.
<br>-les bibliothécaires peuvent accéder à l'enssemble des fonctionnalités.

<br>L'application ne comporte qu'une seule fenêtre divisée en plusieurs onglets.
## Les différents onglets
### Onglet 1 : Livres
Cet onglet présente la liste des livres, triée par défaut sur le titre.<br>
La liste comporte les informations suivantes : titre, auteur, collection, genre, public, rayon.
![img2](https://www.nicolasfrere.fr/ressources/MediatekDocumentsCapture.jpg)
#### Recherches
<strong>Par le titre :</strong> Il est possible de rechercher un ou plusieurs livres par le titre. La saisie dans la zone de recherche se fait en autocomplétions sans tenir compte de la casse. Seuls les livres concernés apparaissent dans la liste.<br>
<strong>Par le numéro :</strong> il est possible de saisir un numéro et, en cliquant sur "Rechercher", seul le livre concerné apparait dans la liste (ou un message d'erreur si le livre n'est pas trouvé, avec la liste remplie à nouveau).
#### Filtres
Il est possible d'appliquer un filtre (un seul à la fois) sur une de ces 3 catégories : genre, public, rayon.<br>
Un combo par catégorie permet de sélectionner un item. Seuls les livres correspondant à l'item sélectionné, apparaissent dans la liste (par exemple, en choisissant le genre "Policier", seuls les livres de genre "Policier" apparaissent).<br>
Le fait de sélectionner un autre filtre ou de faire une recherche, annule le filtre actuel.<br>
Il est possible aussi d'annuler le filtre en cliquant sur une des croix.
#### Tris
Le fait de cliquer sur le titre d'une des colonnes de la liste des livres, permet de trier la liste par rapport à la colonne choisie.
#### Affichage des informations détaillées
Si la liste des livres contient des éléments, par défaut il y en a toujours un de sélectionné. Il est aussi possible de sélectionner une ligne (donc un livre) en cliquant n'importe où sur la ligne.<br>
La fenêtre affiche les informations détaillées du livre sélectionné (numéro de document, code ISBN, titre, auteur(e), collection, genre, public, rayon, chemin de l'image) ainsi que l'image. Les services habilités peuvent modifier les documents.
#### Affichage des exemplaires
Le fait de cliquer sur le titre d'une des lignes de la liste des livres, permet d'afficher ses exemplaires en circulation.  Les services habilités peuvent modifier leurs états.
### Onglet 2 : DVD
Cet onglet présente la liste des DVD, triée par titre.<br>
La liste comporte les informations suivantes : titre, durée, réalisateur, genre, public, rayon.<br>
Le fonctionnement est identique à l'onglet des livres.<br>
La seule différence réside dans certaines informations détaillées, spécifiques aux DVD : durée (à la place de ISBN), réalisateur (à la place de l'auteur), synopsis (à la place de collection).
### Onglet 3 : Revues
Cet onglet présente la liste des revues, triées par titre.<br>
La liste comporte les informations suivantes : titre, périodicité, délai mise à dispo, genre, public, rayon.<br>
Le fonctionnement est identique à l'onglet des livres.<br>
La seule différence réside dans certaines informations détaillées, spécifiques aux revues : périodicité (à la place de l'auteur), délai mise à dispo (à la place de collection).
### Onglet 4 : Parutions des revues
Cet onglet permet d'enregistrer la réception de nouvelles parutions d'une revue.<br>
Il se décompose en 2 parties (groupbox).
#### Partie "Recherche revue"
Cette partie permet, à partir de la saisie d'un numéro de revue (puis en cliquant sur le bouton "Rechercher"), d'afficher toutes les informations de la revue (comme dans l'onglet précédent), ainsi que son image principale en petit, avec en plus la liste des parutions déjà reçues (numéro, date achat, chemin photo). Sur la sélection d'une ligne dans la liste des parutions, la photo de la parution correspondante s'affiche à droite.<br>
Dès qu'un numéro de revue est reconnu et ses informations affichées, la seconde partie ("Nouvelle parution réceptionnée pour cette revue") devient accessible.<br>
Si une modification est apportée au numéro de la revue, toutes les zones sont réinitialisées et la seconde partie est rendue inaccessible, tant que le bouton "Rechercher" n'est pas utilisé.
#### Partie "Nouvelle parution réceptionnée pour cette revue"
Cette partie n'est accessible que si une revue a bien été trouvée dans la première partie.<br>
Il est possible alors de réceptionner une nouvelle parution en saisissant son numéro, en sélectionnant une date (date du jour proposée par défaut) et en cherchant l'image correspondante (optionnel) qui doit alors s'afficher à droite.<br>
Le clic sur "Valider la réception" va permettre d'ajouter un tuple dans la table Exemplaire de la BDD. La parution correspondante apparaitra alors automatiquement dans la liste des parutions et les zones de la partie "Nouvelle parution réceptionnée pour cette revue" seront réinitialisées.<br>
Si le numéro de la parution existe déjà, il n’est pas ajouté et un message est affiché.
![img3](https://github.com/CNED-SLAM/MediaTekDocuments/assets/100127886/225e10f2-406a-4b5e-bfa9-368d45456056)

### Onglet 5 :Commandes de livres
La partie haute de cet onglet présente la liste des livres, triée par défaut sur le titre.<br>
Le fonctionnement est identique à l'onglet des livres.<br>
La partie basse permet de consulter les commandes des livres et de modifier leurs etats.
Certaines règles s'applique aux commandes:
-les nouvelles commande ont par défaut leurs statuts a "en cours".
-les commandes livrées ne peuvent etre supprimer. Quand le statuts d'une commande passe a livrée, le nombre de livres correpondant est ajouté aux exemplaires en circulation.
-une commande ne peut repasser au statuts précédent. Pour pouvoir être réglée, elle doit au préalable avoir été livrée.
![img4](https://github.com/Gotlub/MediatekDocuments/blob/main/images/ap3Commandes.png?raw=true)
### Onglet 6 : Commandes de DVD

Le fonctionnement est identique à l'onglet des livres.<br>
La seule différence réside dans certaines informations détaillées, spécifiques aux DVD.

### Onglet 7 : Abonnements

Le fonctionnement de la partie haute de l'ongle est identique à celui des commandes de livres.<br>
Un abonnement correspond à une revue. Il a un début (Date de commande) et une fin.
Il n'est pas possible de supprimer un abonnement dont un exemplaire a été acquis pendant sa durée.

![img5](https://github.com/Gotlub/MediatekDocuments/blob/main/images/ap3Abonnements.png?raw=true)
## La base de données
La base de données 'mediatek86 ' est au format MySQL.<br>
Voici sa structure :<br>
![img6](https://github.com/Gotlub/MediatekDocuments/blob/main/images/schemaSGBD.jpg?raw=true)
<br>On distingue les documents "génériques" (ce sont les entités Document, Revue, Livres-DVD, Livre et DVD) des documents "physiques" qui sont les exemplaires de livres ou de DVD, ou bien les numéros d’une revue ou d’un journal.<br>
Chaque exemplaire est numéroté à l’intérieur du document correspondant, et a donc un identifiant relatif. Cet identifiant est réel : ce n'est pas un numéro automatique. <br>
Un exemplaire est caractérisé par :<br>
. un état d’usure, les différents états étant mémorisés dans la table Etat ;<br>
. sa date d’achat ou de parution dans le cas d’une revue ;<br>
. un lien vers le fichier contenant sa photo de couverture de l'exemplaire, renseigné uniquement pour les exemplaires des revues, donc les parutions (chemin complet) ;
<br>
Un document a un titre (titre de livre, titre de DVD ou titre de la revue), concerne une catégorie de public, possède un genre et est entreposé dans un rayon défini. Les genres, les catégories de public et les rayons sont gérés dans la base de données. Un document possède aussi une image dont le chemin complet est mémorisé. Même les revues peuvent avoir une image générique, en plus des photos liées à chaque exemplaire (parution).<br>
Une revue est un document, d’où le lien de spécialisation entre les 2 entités. Une revue est donc identifiée par son numéro de document. Elle a une périodicité (quotidien, hebdomadaire, etc.) et un délai de mise à disposition (temps pendant lequel chaque exemplaire est laissé en consultation). Chaque parution (exemplaire) d'une revue n'est disponible qu'en un seul "exemplaire".<br>
Un livre a aussi pour identifiant son numéro de document, possède un code ISBN, un auteur et peut faire partie d’une collection. Les auteurs et les collections ne sont pas gérés dans des tables séparées (ce sont de simples champs textes dans la table Livre).<br>
De même, un DVD est aussi identifié par son numéro de document, et possède un synopsis, un réalisateur et une durée. Les réalisateurs ne sont pas gérés dans une table séparée (c’est un simple champ texte dans la table DVD).
Enfin, 3 tables permettent de mémoriser les données concernant les commandes de livres ou DVD et les abonnements. Une commande est effectuée à une date pour un certain montant. Un abonnement est une commande qui a pour propriété complémentaire la date de fin de l’abonnement : il concerne une revue.  Une commande de livre ou DVD a comme caractéristique le nombre d’exemplaires commandé et concerne donc un livre ou un DVD.<br>
<br>
La base de données est remplie de quelques exemples pour pouvoir tester son application. Dans les champs image (de Document) et photo (de Exemplaire) doit normalement se trouver le chemin complet vers l'image correspondante. Pour les tests, vous devrez créer un dossier, le remplir de quelques images et mettre directement les chemins dans certains tuples de la base de données qui, pour le moment, ne contient aucune image.<br>
Lorsque l'application sera opérationnelle, c'est le personnel de la médiathèque qui sera en charge de saisir les informations des documents.


## L'API REST
L'accès à la BDD se fait à travers une API REST protégée par une authentification basique.<br>
Le code de l'API se trouve ici :<br>
https://github.com/Gotlub/rest_mediatekdocuments<br>
avec toutes les explications pour l'utiliser (dans le readme).

## Installation de l'application
Ce mode opératoire permet d'installer l'application pour pouvoir travailler dessus.<br>
- Installer Visual Studio 2019 entreprise et les extension Specflow et newtonsoft.json (pour ce dernier, voir l'article "Accéder à une API REST à partir d'une application C#" dans le wiki de ce dépôt : consulter juste le début pour la configuration, car la suite permet de comprendre le code existant).<br>
- Télécharger le code et le dézipper puis renommer le dossier en "mediatekdocuments".<br>
- Récupérer et installer l'API REST nécessaire (https://github.com/Gotlub/rest_mediatekdocuments) ainsi que la base de données (les explications sont données dans le readme correspondant).
- Le projet est en .NET Framework 4.7.2.
![img7](https://github.com/Gotlub/MediatekDocuments/blob/main/images/netFramework.png?raw=true)

## Tests fonctionnels
Installer Specflow dans les extensions de Visual Studio 2019.
<br>Puis pour pouvoir réaliser les tests fonctionnels, il faut commenter ("//")  dans le constructeur d'Access (dal/Access.cs) la ligne ```api + ApiRest.GetInstance()``` et rentrer les données de connexion en dur ```api = ApiRest.GetInstance("http://localhost/rest_mediatekdocuments/", "admin:adminpwd");``` comme dans la capture si dessous.
![img8](https://raw.githubusercontent.com/Gotlub/MediatekDocuments/main/images/Access.png)
