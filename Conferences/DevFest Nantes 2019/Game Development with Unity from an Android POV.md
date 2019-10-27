---
speakers:
- Julien Salvi
topics:
- Mobile
- Game Development
---

# Game Development with Unity from an Android Point of View

## Overview Game Development on Android

Grosse compétition avec Unreal Engine, Cocos & Godot.

Reste très reconnu :

- 50% des nouveaux jeux mobiles sont fait avec Unity.
- Utilisé par des gros studios :
  - Blizzard avec Heartstone
  - Niantic avec Pokemon Go
  - Square-Enix avec LaraCroft Go
- Aussi utilisé par de plus petit studios :
  - White Elk avec Eclipse en VR
  - Plein d'autres

Points forts :

- Dispo sur Win et Mac (bientôt Linux)
- Possibilité de faire des applications 2D, 3D, AR/VR
- Prototyping et scripting rapide
- Supporte la pluspart des formats 2D et 3D
- Super magasin d'assets
- Support d'OpenGL et Vulkan
- Bridge vers les plateformes natives
- Export vers Android Studio
  - Support Java et Kotlin

## Building Unity Plugins

Développement Unity classique :

- Scripts C#
- Contrôle du pipeline de rendering
- Compilation cross-plateforme des shaders

Plugins externes :

- Comme la création d'un plugin Android
  - Développement Java/Kotlin or C/C++
  - Package en `.jar`, `.arr` ou `.so`
  - Classes Java et Kotlin disponibles directement dans Unity

Exemple plugin de player vidéo intégré à Unity :

- Contrôles côté Unity (Play, Pause, Change Audio Track, etc)
- Travail côté plugin

Implémentations possibles :

- Interface avec un plugin pur Java, mais cela cause beaucoup de boilerplate côté Unity.
- Utilisation d'une librairie C++ pour une interface presque "native" côté Unity.
  - La classe C++ s'interface elle avec le code Java via la Java Native Interface (JNI). Il faut l'initialisé comme on le faisait dans Unity, mais le boilerplate est bien moindre.
- Unity 2018.2 ajoute le support pour les plugins Java ou Kotlin directement dans Unity
  - Pas besoin de compiler une librairie à la main, Unity s'en charge avec Gradle
  - Peut inclure des dépendences Maven directement

## Unity from Android Studio

Unity exporte un projet Android Studio au lieu d'une build directement. Cela permet :

- Un contrôle complet du workflow de build (par exemple, cibler Vulkan ou OpenGL en fonction des appareils)
- D'ajouter du code Android facilement
- Gérer les librairies (et faire du nettoyage)
- Modifier le code généré

## What's next?

- Support Linux
- Meilleure intégration Gradle
- Meilleures performances
- Unity as a Library
  - L'application Unity peut être exportée comme un module a être intégré à une application Android au lieu d'avoir à ajouter l'application Android au jeu Unity.
  - Quelques limitations pour le moment :
    - Rendu plein écran uniquement
    - Une seule instance du runtime à la fois
    - Baesoin d'adapter son produit

## Android from a Unity Developer Point of View

- Point positifs :
  - Facile à build pour Android
  - Bon support des librairies graphiques (OpenGL et Vulkan)
    - Bonne compatibilité abec ShaderLab
  - Pas besoin de se plonger dans la doc Android
- Points négatifs :
  - Code propriétaire, difficile de savoir ce qui se passe vraiment
  - Difficile de faire des UIs
  - L'intégration dans des applications Android (mais comme on l'a vu, Unity as a Library arrive)

## Ressources

- [Android Game Development](https://developer.android.com/game)
- [ExoPlayer for building powerful VR players on Cardboard and GearVr](https://medium.com/@cinemur/73ec7e83dd5c)
- [Building Unity Plugins for Unity](https://docs.unity3d.com/Manual/PluginsForAndroid.html)
- [Android as a Library](https://blogs.unity3d.com/2019/06/17/add-features-powered-by-unity-to-native-mobile-apps)
- [Using Unity as a library in native iOS/Android App](https://forum.unity.com/threads/using-unity-as-a-library-in-native-ios-android-app.685195/)
- [Integration Unity as a library in a native Android app](https://forum.unity.com/threads/integration-unity-as-a-library-in-native-android-app.685240/)
