---
speakers:
- Steven Le Roux
- Quentin Adam
topics:
- Big Data
- AI
videos:
- https://www.youtube.com/watch?v=5fqhT82wghY
---

# Apache Pulsar 101: Architecture, Concepts et Comparaison

## What is it?

- Open-source distributed pub-sub messaging system.
- Built on top of Bookkeeper (WAL), using Zookeeper (concensus distribué).
- Les brokers et le stockage étant séparés, ils peuvent scaler séparemment.
- Used by big players. Sit behind Twitter Manathan.
- Bien packagé : install et start en 4 lignes. C'est facile de commencer.
- C'est le début du renouveau Apache avec le premier projet full GitHub.

## Layered

Plusieurs niveaux :

- Messaging (via Pulsar) Stateless, scale-out, not tight to storage constraints
- Storage (via Bookkeeper a.k.a. Bookie)

## Multi-Model Messaging Platform

On peut utiliser plusieurs models car c'est un Pub-Sub distribué.

Il repose sur un Log Steam, une séquence ordonnée d'entrée immuables.

Pulsar n'utilise pas des partitions mais des de segments (par heure). Ces segments sont ensuite regroupé dans un topic.

Les segments peuvent être déplacé d'un storage à l'autre.

## Distributed Log

- WAL
- Non Blocking Ingress

La synchronisation du cluster séparé de la gestion du cluster avec un Zookeeper interne et un autre externe.

## Protocols

Protobuff est utilisé pour la discussion binaire des brokers. Le reste (administration, création de topics) se fait par HTTP.

S'interfersera avec d'autre brokers (voir PIP-46).

## PubSub

API unifié pour Cumulative ou Selective Acking

Prise par segment ou par élement (par acknoledgement).

## Messaging Semantic

- Choose your Delivery Guarantee
- Server side Deduplication
- Server side Dead Lettering
  - Accepté une entrée, mais impossible de finir donc renvoyé vers un sous topic d'erreur au lieu d'être renvoyé dans le même topic.

Producers et Consummers sont tous nommés pour un meilleur suivi de qui à envoyé/traité un event.

- Si taggé avec le commit ID du changement et qu'un bug apparaît, il est alors facile de les exclure dans un autre topic les mauvais messages générés suite à un mauvais déploiement afin de les traiter plus tard.

## Virtual Topic

Topics créés en virtuel et n'utilisent pas ou peu de ressources.

Comme les topics sont virtuels, il est possible d'en écouter plusieurs à la fois. En revanche, il n'y a plus de garantie d'ordre (entre les topics)

## Schema registry

On envoie des bytes à Kafka et Pulsar, mais les messages devraient être "typé".

Le schema registry peut définir le format des messages avec Apache AVRO.

Cela permet d'empêcher un mauvais message d'être intégré dans un topic. Il sera bougé vers un autre topic d'erreur.

## IO Isolation & Access Pattern

- Write
- Tailing Read
- Catchup Read (e.g. relire les données du mois)

La lecture en catchup d'une vielle donnée ne pénalisera pas le write car ils utilisent des caches séparés.

## Durability Stratégies

- Non-persistent, pas de latence mais possibilité de perte de donnée si un noeud tombe.
- Persistent, plus de latence mais pas de perte de donnée.
- Compacted, ne garde que les derniers élements en mémoire, le boot d'un nouveau noeud est rapide.
- Decuplicated

## Messages Retention & Expiry

- Deleted
- Retention Policy
- Within TTL
- TTL Expired
- Tiered Storage via JClouds pour exporter les anciens messages sur d'autres storage. Ce sera plus lent mais toujours accéssible.

## Sécurité

- Proxy frontal
  - Brokers protégés
- Proxy interne
  - Donnée toujours lisible même si les frontaux tombent
- Multi-Tenancy.
  - Découpe Tennant > Namespace > Topics
- Pluggable Auth
  - Biscuit, comme JWT mais plus réduit
    - ACL, au lieu de transmettre les droits, les droits sont demandés
    - Attenuation, à partir d'un token, on peut recrée un sous token (donc plus petit)
    - Decentralized

## Multi Cluster Management

2 clusters Zookeepers, 1 global qui fait la liaison entre tous les clusters :

- Discovery à travers 1 seule URL
- Geo Replication simple

## What else?

Presto :
- Récuperer les message des topics via SQL.
- Les tables SQL sont crées à partir des schémas du Schema Registry

Clients :

- Il y a des clients pour plusieurs languages (Rust, C++, Python, etc)
