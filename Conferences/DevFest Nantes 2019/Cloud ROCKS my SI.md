---
speakers:
- Didier Girard
- Cyril Balit
topics:
- Cloud
- DevOps
---

# Cloud ROCKS my SI

Migrer le SI de SFEIR sur le cloud. Avant de l'implémenter pour les clients, implémenter pour eux-même. DOG FOODING?

Les clients demandent souvent une application. Ils essayent de changer cette vision en proposant de coder une plateforme qui expose des APIs consommés par des frontaux.

## Patterns existants ou émergeants

- 12 Factors
- Managed (gestion par le Cloud Provider, dimensionnement par le client
- Serverless (dimensionnement & gestion par le Cloud Provider)
- WebHook
- API
- RPA (Robotic Process Automation, automatisation de la communication entre application)

 ## Step 0 - Utiliser des services Cloud-Native

Bascule sur GSuite en 2008. Plus de gestion des serveurs mail et application bureautique pour la collaboration.

Création du S.I. Coud Native en 2016.

Tout nouveau produit intégré doit être Cloud-Native :

- Test de feature classique
- Consommable via mobile
- Bonne expérience développeur (API disponible & utilisable).
  - Hackaton d'une semaine pour valider que le produit pourra être intégré dans le SI de l'entreprise
  - Donner l'opportunité aux devs de dire non

## Step 1 - La Brique d'Intégration & le premier service

Avec l'approche Cloud-Native, il est possible de choisir des petits outils qui répondent à un besoin spécique au lieu d'un outil général façon usine à gaz.

SFEIR était à la recherche d'une solution ATS (Acquisition Talent Systems) pour suivre les étapes de recrutement d'un candidat. Ils ont choisi *Lever*.

L'interfacage des besoins additionnels se fait via la brique d'intégration de SFEIR (Pub-Sub et fonctions Lambdas, le tout en serverless).

Première étape : Enregistrer les events dans une une BDD

1. Fonction appelée par le WebHook de Lever pour enregistrement dans le Pub-Sub technique
2. Fonction pour lire le topic et enregistrement dans la BDD de logs.

Deuxième étape : Ajout d'un nouvelle fonctionnalitée

1. Une première fonction récupère l'event depuis le même Pub-Sub technique
2. Contacte l'API de Lever pour avoir plus d'infos (par exemple le nom du candidat plutôt que son ID)
3. Envoie dans un Pub-Sub métier
4. Une autre fonction récupère l'event depuis le Pub-Sub métier
5. Envoie de mail via SendGrid
5. Fonction appelée par le WebHook de SendGrid pour enregistrement dans le Pub-Sub technique (uniquement pour logging pour le moment)

## Step 2 - De nouveaux besoins

Les nouvelles briques sont simplement connectées aux mêmes Pub-Sub avec une simple fonction.

Un pattern émerge, le Robotic Process Automation (RPA) :

1. En amont, le code d'intégration (e.g. récupération )
2. Le code technique (e.g. envoie de mail)
3. Notification au SI

Volume faible donc coût infrastructure faible.

## Sécurité

La sécurité est portée par la plateforme.

Les utilisateurs et leurs droits étant déjà gérés par la plateforme, pas besoin de réinventer la roue.

## CI/CD

Terraform pour l'infra afin de normaliser les environnements (dev et prod)

Gitlab CI pour les test-unitaires, etc.

## What's next

Plein de nouveaux besoins :

- CRM Commerce
- HCM (gestion des entretiens, des rencontes, des formations, etc)
- SI RH
- Note de frais

D'un point de vue technique, la mise en place APIGEE, un gestionnaire d'API afin de manager les APIs externes à destination des utilisations internes :

- transformation des messages à la convenance
- authentification centralisée
- mocks par environnement puisque les SASS n'ont pas forcemment d'environnement de test
	- APIGEE peut mapper chaque environnement sur des targets différentes (par exemple mocks pour DEV et API du service pour PRD).
