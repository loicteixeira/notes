---
speakers:
- Thomas Blaisot
topics:
- Authentication
videos:
- https://www.youtube.com/watch?v=taZ2rS-CjAs
---

# WebAuthn : Le renouveau de l'authentification

Petit rappel, l'authentification c'est qui vous être, l'autorisation c'est quelles permissions vous avez.

Pour une authentification multi-facteurs, on va vouloir utiliser des facteurs de plusieurs catégories :

- Quelque chose que vous connaissez (e.g. mot de passe)
- Quelque chose que vous avez (e.g. une clef USB)
- Ce que vous être (e.g. empreinte digitale)
- Où vous êtes

## La Norme

### Historique

1. Credential API (rappel des mots de passes par le navigateur)
2. 2FA
   1. One Time Password (norme RFC 6238)
   2. Authenticateur Customs
   3. FIDO (U2F v1.0)
3. FIDO v2 repris par W3C et nommé Web Authentication API

### Components

- Password Storage
- Federated Token Storage
- PublicKey Authentication

### Workflow

Sign-up :

1. Envoie username à app
2. App renvoie un challenge
3. Challenge est passé à WebAuthn
4. Transmis à l'authenticateur
5. Action utilisateur (Press ou PIN)
6. Génération d'un credentialID (rawId) et d'une Public Key par authenticateur
7. Envoie au server
8. Validation backend
9. Success

Sign-in :

1. Envoie username à app
2. App renvoie un challenge et la liste des authenticateurs connus
3. Challenge est passé à WebAuthn
4. Transmis à l'authenticateur
5. Action utilisateur (Press ou PIN)
6. Signature du challenge
7. Envoie au server
8. Validation backend
9. Success

### Interfaçage différents authenticateurs

- Plateforme (e.g. empreinte digitale, etc)
- Roaming (e.g. USB, Bluetooth, etc)
- Software

## Est-ce qu'on peut l'utiliser ?

Du côté des navigateurs, tous sauf Safari & Opera supportent la norme.

Du côté utilisateurs, tout le monde n'a pas d'authenticateur donc un fallback avec mot de passe est toujours nécessaire.

Surtout, pensez à :

- Séparé l'authentification de votre application
- Ne pas coder cette partie vous même, utiliser des libraries
