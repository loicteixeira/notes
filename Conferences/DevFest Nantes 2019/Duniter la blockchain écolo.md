---
speakers:
- Adrien Lasselle
- Bertrand Presles
topics:
- blockchain
---

# Duniter la blockchain écolo

Sur une année, l'envoie d'emails d'une PME de 100 personnes produit 18 tonnes de CO₂.

## Blockchain

Un réseau peut être centralisé, décentralisé ou distribué.

Les blockchains sont distribuées car le registre (ledger) est présent sur chaque noeud du réseau et que les mises à jours se font par consensus.

Les blockchains sont sécurisés, infalsibiables, inviolables et fiables (c.a.d. résilientes et confiance sans tier de confiance).

Les blockchains peuvent être publiques, privée (par exemple tracabilité d'un produit) ou semi-privé (lecture publique mais écriture sous conditions).

## Block

Un bloc est un élément du registre contant une transation (au sens d'opération, pas forcemment une transaction financière) et est identifié par son hash.

Le hash est généré via un arbre de Merkle et se base sur son identité et l'identité du bloc précédent. Cela permet de vérifier l'intégrité d'un block sans avoir à comparer tous les précédents.

## Registre

Il est mis à jour par consensus, c.a.d. qu'au moins 50% des noeux du réseau doivent le valider.

La validation d'un block se fait par une preuve de travail (Proof Of Work ou PoW)

## Proof of Work

Chaque noeud essaye de résourdre un puzzle cryptographique qui consiste à trouver le hash du block avec un préfix de n zéros. L'horloge réseau permet de régler la difficulté du challenge afin de conserver un certain équilibre.

Pour la blockchain Bitcoin, le mineur qui trouve le hash d'un block gagne une récompense en crypto-monnaie. Il y a donc un intérêt financier à trouver le plus de blocs possible, ce qui a entrainé la création d'énormes fermes de calculs. Cela créé un système très inégalitaire où ceux qui ont plus de moyens, gagnent plus d'argent (qu'ils peuvent ensuite réinvestir pour toujours être devant).

Une des alternatives au PoW est le Proof of Stake (PoS), qui voir le mineur proposant un hash déposé une caution en crypto-monnaie. Cette caution sera saisie s'il s'avère que c'était une proposition frauduleuse. Cependant, cette méthode reste tout aussi inégalitaire car c'est celui qui met la plus grosse caution qui l'emporte.

## PoW Duniter

Duniter a choisi la Proof of Work comme méthode de validation, mais celle-ci fonctionne différemment de celle de Bitcoin.

Tout d'abord, Duniter étant une blockchain semi-privée et la participation est donc limitée au membres. Ces membres font parti de la toile de confiance et reçoivent tous une partie de la récompense journalière pour le minnage. Il n'y a donc pas de compétition mais une collaboration.

Reste la question de l'énergie consommée, que Duniter résout via une difficultée personnalisée via plusieurs leviers :

- La *fenêtre courante* qui veut qu'un tier du réseau ne participe pas au minnage pour chaque bloc donné
- Le *facteur d'exclusion* qui exclu les membres ayant récemment validé un bloc
- Le *handicap* donné aux machines puissantes

Le tout crée une blockchain moins énergivore (évaluation de la consommation du réseau à quelques ampoules) :

- Les calculateurs modestes peuvent participer (certains noeud sont de simple Raspberry Pi)
- Par de récompense avec la création monnétaire journalière répartie entre tous les membres
- Un bloc minné toutes les 5 minutes (1 bloc peut contenir plusieurs transactions)
- Pas de course au minning

## La Crypto-Monnaie Ǧ1 (June)

Basée sur la théorie relative de la monnaie (conçue scientifiquement) afin d'être une bonne monnaie d'échange.

Utilisation concrète sur un restaurant de Nantes et via le site d'annonces [gchange.fr](https://gchange.fr).
