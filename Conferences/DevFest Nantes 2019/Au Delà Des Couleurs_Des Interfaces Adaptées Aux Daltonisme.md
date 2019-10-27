---
slides:
- https://bit.ly/devfestnantes-daltonisme
speaker:
- Laura Wacrenier
topics:
- Accessibility
- UX
---

# Au Delà Des Couleurs : Des Interfaces Adaptées Aux Daltonisme

## C'est quoi le daltonisme ?

4% de la population caucassienne (8% des hommes et 0.5% des femmes) sont touchés par une forme de daltonisme. Pourtant, les codes couleurs existant comme le rouge pour le danger ou l'erreur et vert pour la sécurité ou le succès ne sont pas remis en question.

Il existe [plusieurs formes de daltonisme](https://fr.wikipedia.org/wiki/Daltonisme#Types_de_dyschromatopsie) qui affecte les cônes de couleurs (photorécepteurs) situés dans la rétine. Ces cones peuvent avoir mutés, être abîmés ou voir même manquants pour une ou plusieurs couleur (rouge, vert et bleu).

La *Deutéranopie*, la *Deutéranomalie* et la *Protanopie* représente 75% des cas, "confondant" le vert et le rouge en jaune. En ce focalisant sur ces deux couleurs, il est alors possible de régler une grande partie des cas.

## Quelles solutions ?

### Fort contraste des textes

Respecter les normes WCAG (Web Content Accessibility Guidelines) quand au contraste de la couleur du texte et de la couleur du background :

- `AA` pour contraste minimum
- `AAA` pour contraste optima

Plusieurs outils permettent de vérifier ce contraste :

- Web AIM Color Contrast Checker
- Tanaguru Contrast Finder
- Les outils d'inspections des navigateurs :
  - FireFox : Onglet Accessibility
  - Chrome : Intégré au Color Picker
- Plugins pour Adobe et Sketch

### Fort contraste non-textuels

Passer son écran en noir & blanc peut être un bon premier indicateur, mais l'utilisation d'outils de simulation permettra une inspection plus poussée :

- Plugins pour Adobe et Sketch
- Plugins navigatuers :
  - FireFox : Let's Get Colorblind
  - Chrome : Colorblinding
- Plugins Operating System : Color Oracle

### Ne pas utiliser uniquement les couleurs

La couleur ne devrait pas être le seul indicateur pour une information donnée.

L'information peut aussi être transmise par :

- Des formes, par example :
  - un bouton principal avec icone et contour à côté d'un bouton secondaire sans icone ni contour)
  - une séparation entre 2 zones de couleurs (au lieu d'avoir les 2 couleurs qui se touchent)
- Des textures
- Des icônes
- L'utilisation de messages d'erreur
- L'inclusion des labels directement dans le graphique (au lieu d'une légende de couleur)

### Liens hypertext

C'est simple, <u>soulignez les liens</u>.

### Modes Spéciaux

Des modes spéciaux peuvent être créés, mais ce n'est pas optimal parce qu'il faut savoir que ça existe et comment l'activer.

Vous ne construiriez pas la rampe d'accès à votre magasin à l'arrière de la boutique mais bien devant, alors ne faites pas un mode spécial caché.

## Comment convaincre qu'il est important de traiter ce sujet ?

Ce n'est pas difficile techniquement mais ça demande du temps alors comment convaincre une équipe ou un client septique ?

### Utile pour tous

Une des partie de l'Inclusive Design Program de Microsoft dit "Solve for one, extend to many". Au lieu de penser qu'on a des handicaps, on peut penser qu'on a tous des facultés avec des limites, limites qui peuvent être permanentes, temporaires ou situationnelles (environnement bruyant qui empêche de bien entrendre, faible luminosité qui empêche de bien lire, etc).

En d'autres termes, à un moment donné, on est tous dans le besoin. En multipliant les canaux de communication, il y a moins de chance de confusion.

### Décisions facilitées

Chaque élément ayant été soigneusement choisi et codifié, il n'y aura plus de confusion plus tard et il y aura un guide, un référenciel.

Cela provoquera aussi une simplification du code car moins de cas spéciaux, donc moins de code à maintenir et moins de bugs.

## Comment mettre en place ?

Faire un audit complet d'un système puis remettre un compte-rendu à la direction est vouée à l'échec, alors comment faire ?

### Considérer comme des bugs

Après tout, certains utilisateurs ne peuvent pas utiliser l'application correctement donc c'est un bug.

### Sensibiliser

Lors de la création de tickets de bug, ajouter des screenshots qui simulent le daltonisme. De cette manière, les développeurs comprendront mieux pourquoi le changement est nécessaire et que ce n'est pas simplement du zèle de designer.

### Faciliter le travail

Dans les tickets de bugs, si le designer a la connaissance technique, inclure les changements de CSS nécessaire. De cette manière, ce sera un ticket facile à gérer et aura une plus grande chance d'être embarqué.

### Instaurer des Design Reviews

A l'image des code reviews, chaque design doit être revu par au moins un autre designer.

L'utilisation d'une checklist lors de cette review est essentielle afin de n'oublier aucun point.
