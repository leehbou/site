# 🧗 Club d'Escalade - Application Web

Application web de gestion pour un club d'escalade permettant la réservation de cours et de matériel.

## 📋 Description

Cette application PHP permet aux adhérents d'un club d'escalade de :
- Réserver des cours d'escalade (débutant, intermédiaire, avancé)
- Emprunter du matériel
- Consulter leurs réservations
- Gérer leur profil

## Auteur

- Nathan Ripaud
- Adam Leopole dit marie
- Iulian Esanu

Les employés (professeurs) peuvent également créer des cours.

## 🚀 Fonctionnalités

### Pour les Adhérents
- ✅ **Inscription** avec différentes formules d'abonnement
- 🔐 **Connexion** sécurisée avec mot de passe hashé
- 📚 **Réservation de cours** (3 niveaux disponibles)
- 🎒 **Réservation de matériel** par salle
- 👤 **Profil personnel** avec informations détaillées
- 📋 **Historique des réservations** (cours et matériel)

### Pour les Employés (Professeurs)
- ➕ **Création de cours** avec date et niveau
- 🏢 Affectation automatique à leur salle de travail

### Niveaux de cours
- 🟢 **Débutant** : Techniques de base, sécurité
- 🟡 **Intermédiaire** : Perfectionnement, voies en moulinette
- 🔴 **Avancé** : Escalade en tête, techniques avancées


## 📁 Structure du projet

```
├── acc.php                 # Page d'accueil
├── index.php              # Page de connexion
├── inscription.php        # Formulaire d'inscription
├── profil.php             # Profil utilisateur
├── reservCours.php        # Réservation de cours
├── reservMateriel.php     # Réservation de matériel
├── mesReservation.php     # Historique des réservations
├── creerCours.php         # Création de cours (profs)
├── deconnecter.php        # Déconnexion
├── reussite.php           # Page de confirmation
├── styleClair.css         # Styles CSS
└── include/
    ├── bd.inc.php         # Connexion base de données
    ├── functions.inc.php  # Fonctions métier
    ├── header.inc.php     # En-tête commun
    └── footer.inc.php     # Pied de page
```

## 🔑 Système d'authentification

### Inscription
- Création automatique d'un ID unique
- Âge minimum : 16 ans
- Validation de l'email et du téléphone (uniques)
- Mot de passe hashé avec `password_hash()`

### Clés employés (inscription avec rôle)
- `ePv5` : Professeur voie
- `ePt3` : Professeur tête
- `ePb1` : Professeur bloc
- `eO7` : Ouvreur
- `eA9` : Accueil

## 💳 Types d'abonnements

- **Forfait Normal**
- **Forfait+** 
- Options : Accès sauna, Cours collectifs
- Durée : 1 à 12 mois

## 📱 Pages principales

| Page 			| Description 
|-----------------------|-------------
| `index.php` 		| Connexion 
| `acc.php` 		| Accueil avec actions rapides 
| `reservCours.php` 	| Réserver un cours 
| `reservMateriel.php`  | Emprunter du matériel 
| `mesReservation.php`  | Voir ses réservations 
| `profil.php` 		| Informations personnelles 

## 🔒 Sécurité

- ✅ Sessions PHP pour l'authentification
- ✅ Mots de passe hashés (bcrypt)
- ✅ Requêtes préparées (PDO) contre les injections SQL
- ✅ Validation des entrées utilisateur
- ✅ Échappement HTML avec `htmlspecialchars()`
- ✅ Redirection automatique si non connecté

## 🐛 Gestion des erreurs

L'application affiche des messages clairs :
- Messages de succès (fond vert)
- Messages d'erreur (fond rouge)
- Validation des formulaires
- Vérification de disponibilité (cours, matériel)

## 📊 Fonctions principales

### `functions.inc.php`

```php
// Authentification
existAdherent($id)          // Vérifie l'existence d'un adhérent
bonMDP($id, $mdp)           // Valide le mot de passe

// Gestion des cours
creerCours($idprof, $date, $niveau, $nomCours)
rejoindreCours($idadherent, $idcours)
afficherCours($idDuCours)

// Gestion du matériel
reservMateriel($idadherent, $idmateriel, $datedebut, $dateretour)
descriptionMateriel($idSalle, $idMateriel)

// Inscription
ajoutAdherent($id, $nom, $prenom, ...)
ajoutEmploye($id, $nom, $prenom, ..., $cle, $salle)
```
## 🧪 Tests

Pour tester l'application :

1. **Créer un compte adhérent**
   - Aller sur inscription.php
   - Remplir le formulaire
   - Noter l'ID généré

2. **Créer un compte professeur**
   - Utiliser une clé employé (ex: ePv5)
   - Choisir une salle

3. **Tester les réservations**
   - Cours : sélectionner un cours existant
   - Matériel : choisir salle puis équipement
