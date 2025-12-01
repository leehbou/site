# Client Salle d'Escalade

Client Python pour le système de gestion d'une salle d'escalade. Ce programme permet de simuler différents types de bornes interactives utilisées dans une salle d'escalade.

## Description

Ce client se connecte à un serveur de gestion de salle d'escalade et simule différents types de bornes :
- **Borne d'accueil** : Contrôle d'accès à la salle
- **Borne de réservation de cours** : Réservation de cours individuels
- **Borne de location de matériel** : Location d'équipement d'escalade
- **Borne sauna** : Contrôle d'accès au sauna
- **Borne cours collectifs** : Contrôle d'accès aux cours collectifs
- 
## Installation

Aucune installation nécessaire. Téléchargez simplement le fichier Python.

## Utilisation

### Démarrage basique

```bash
python client.py
```

Le client se connectera par défaut à `127.0.0.1:8080`.

### Démarrage avec paramètres personnalisés

```bash
python client.py <adresse_ip> <port>
```

**Exemple :**
```bash
python client.py 192.168.1.100 8080
```

### Configuration initiale

Au démarrage, le programme vous demandera :

1. **ID du client** (1-100) : Identifiant unique de la borne
2. **Type de borne** : Choisir parmi les 5 types disponibles

## Types de bornes

### 1. Borne d'accueil
- Scanne les cartes d'adhérent
- Vérifie l'accès à la salle d'escalade

### 2. Borne de réservation de cours
- Scanne la carte de l'adhérent
- Affiche la liste des cours disponibles
- Permet de réserver un cours

### 3. Borne de location de matériel
- Scanne la carte de l'adhérent
- Affiche le matériel disponible
- Permet de louer du matériel

### 4. Borne sauna
- Scanne les cartes d'adhérent
- Vérifie l'accès au sauna

### 5. Borne cours collectifs
- Scanne les cartes d'adhérent
- Vérifie l'accès aux cours collectifs

## Format des cartes

Les cartes d'adhérent doivent respecter le format suivant :
- **8 caractères exactement**
- **Uniquement des chiffres**

## Protocole de communication

Le client utilise un protocole binaire personnalisé avec la structure suivante :

### Structure du message (7 octets d'en-tête + contenu)

| Champ | Taille | Type | Description |
|-------|--------|------|-------------|
| idClient | 1 octet | uint8 | ID de la borne (1-100) |
| typeClient | 1 octet | uint8 | Type de borne (1-5) |
| typeDemande | 1 octet | uint8 | Type de requête |
| lengthContent | 4 octets | uint32 | Taille du contenu |
| content | Variable | UTF-8 | Données de la requête |

### Types de demandes

| Code | Nom | Description |
|------|-----|-------------|
| 0 | DISCONNECT | Déconnexion |
| 11 | CHECK_ACCES_SALLE | Vérification accès salle |
| 15 | CHECK_ACCES_SAUNA | Vérification accès sauna |
| 20 | LOCATION_SCAN | Scan pour location |
| 21 | LOCATION_LIST | Liste matériel disponible |
| 22 | LOCATION_CHOIX | Choix de matériel |
| 25 | RESERVATION_SCAN | Scan pour réservation |
| 26 | RESERVATION_LIST | Liste cours disponibles |
| 27 | RESERVATION_CHOIX | Choix de cours |
| 30 | CHECK_ACCES_COURS | Vérification accès cours |

## Réponses du serveur

Le serveur peut renvoyer différents types de réponses :

- `ACCES:` - Accès autorisé
- `REFUSE:` - Accès refusé
- `OK:` - Opération réussie
- `ERROR:` - Erreur
- `DISCONNECT:` - Déconnexion forcée

## Limites techniques

- **Taille du buffer** : 1024 octets
- **Taille de l'en-tête** : 7 octets
- **Taille maximale du contenu** : 1016 octets
- **Plage d'ID client** : 1-100
- **Plage de ports** : 1024-65535

## Gestion des erreurs

Le client gère automatiquement :
- Validation de l'adresse IP
- Validation du port
- Validation du format des cartes
- Erreurs de connexion
- Interruptions clavier (Ctrl+C)
- Déconnexions du serveur

## Exemple de session

```
========================================
  CLIENT SALLE D'ESCALADE
========================================

Serveur: 127.0.0.1:8080
ID du client (1-100) > 5

Type de borne :
  1 : Borne d'accueil
  2 : Borne reservation cours
  3 : Borne location materiel
  4 : Borne sauna
  5 : Borne cours collectifs
> 1

[OK] Borne: Accueil (ID=5)

Connexion a 127.0.0.1:8080...
[OK] Connecte !

========================================
     BORNE ACCUEIL
========================================
  1 - Scanner carte
  0 - Quitter

> 1

[SCAN] ID carte (8 chiffres) > 12345678

[OK] Acces autorise : Bienvenue Jean !
```

## Code de sortie

- `0` : Sortie normale
- `1` : Erreur (paramètres invalides, connexion refusée, etc.)

## Auteur

Nathan Ripaud
Adam Leopole dit marie
Iulian Esanu

## Licence

Non spécifiée
