# Dossier d'homologation : Le Taxi

## Décision d'homologation

Le Directeur Interministériel du Numérique, des Systèmes d'Information et de Communication

  - vu le Référentiel Général de Sécurité version 2.0 approuvé par arrêté du 13 juin 2014
  - vu le [Guide de l'Homologation de Sécurité de l'ANSSI](https://www.ssi.gouv.fr/uploads/2014/06/guide_homologation_de_securite_en_9_etapes.pdf), version 1.0 d'Août 2014
  - vue la Politique de Sécurité S.I. de l'Incubateur de la DINSIC, https://github.com/sgmap/beta.ssi/ dans sa version du XX janvier 2017
  - vus les articles L. 3121-11-1 et R3121-24 à R3121-33 du Code des transports
  - vu le Décret n° 2016-335 du 21 mars 2016 relatif au registre national de disponibilité des taxis
  - vu les Conditions Générales d'Utilisation, disponibles à l'adresse http://le.taxi/files/CGU.pdf
  - vu les éléments du "Dossier d'homologation : Le Taxi", ci-après ou inclus par référence

décide l'homologation du système constituant le registre national de disponibilité des taxis, aux conditions prévues ci-après.

## Commission d'Homologation

Elle réunit l'autorité d'homologation, son RSSI et au moins un des membres de l'équipe Le Taxi.

## Démarche

La démarche retenue est une démarche autonome _a minima_ ("Pianissimo"), conforme également au Guide d'Analyse des Risques et au Guide d'Homologation visant les équipes dites "Agiles" (ouvrages en cours de réalisation par l'ANSSI conjointement avec la DINSIC).

## Périmètre

L'homologation couvre le système constituant le registre national de disponibilité des taxis, c'est à dire le serveur hébergeant l'API Taxi Exchange Point (TXP), les bases de données, les procédures et administrateurs affectés à son exploitation; ce périmètre exclut tout système ou application, mobile ou non, susceptible d'être connecté à l'API.

![Diagramme de composants logiques](https://cdn.rawgit.com/openmaraude/APITaxi_front/588acd56562385ca02e1de3aba0fb8635480e4e9/APITaxi_front/static/images/overview.svg)

Comme indiqué ci-dessus, les partenaires susceptibles de s'interconnecter au registre sont de deux types:
- *moteurs de recherche* - consommateurs des données de position: 8 actuellement référencés
- *opérateurs de taxis* - fournisseurs des données de position: 20 actuellement référencés

L'adhésion des partenaires des deux types se fait en ligne par formulaire accessible à l'adresse http://le.taxi/join.html et délivre un "jeton" exigé pour toute utilisation de l'API, et *sous réserve d'acceptation des CGU* disponibles à l'adresse http://le.taxi/files/CGU.pdf .

## Durée et conditions de l'homologation

La décision d'homologation est temporaire, pour une durée maximale de 24 mois, et soumise à des conditions de volumétrie d'usage du service : elle n'est valable, et les risques résiduels considérés comme acceptables, que pour un volume de courses journalier inférieur à 500. En cas de dépassement de ce seuil, une nouvelle homologation doit être prononcée sous un délai de 3 mois.

## Suivi

Pendant la durée de l'homologation, une Commission d'Homologation est réunie

- si une modification substantielle de l'architecture du service, de nature a altérer l'analyse des risques, est envisagée ou implémentée
- si la surveillance active de l'exploitation du système (cf. ci-dessous, "Surveillance en continu") fait apparaître des incidents laissant supposer des menaces nouvelles
- si par tout autre moyen une menace nouvelle est portée à la connaissance de l'un des membres de la Commission 
- dans tous les cas, dans un délai de 12 mois à compter de la décision d'homologation initiale, pour un réexamen formel à mi-parcours

## Recensement des composants du système

Composants physiques:

  - un serveur hébergé par OVH, identifiant technique ns376081

Composants logiques:

  - recensés sur https://github.com/openmaraude
  - exposés sur le Web aux adresses
    - http://le.taxi/ (documentation générale)
    - https://api.taxi/documentation (documentation technique)

## Analyse des risques

Cette analyse couvre

  - les composants du SI
  - les événements redoutés et leurs impacts
  - les sources et scénarios de menaces
  - les biens essentiels ("valeurs métier") et besoins de sécurité
  - les risques maîtrisés et mesures de sécurité existantes
  - les risques résiduels

Incorporée par référence: https://github.com/openmaraude/le.taxi/wiki/Anayse-des-risques dans sa version du XX janvier 2017 (page accessible publiquement)

## Procédures d'exploitations sécurisées

### Organisation de l'exploitation

L'exploitation et la maintenance du système sont organisées selon les principes "Devops", c'est-à-dire dans un mode d'organisation bannissant les silos et considérant le "build" comme consubstantiel au "run": une équipe resserrée constituée des deux développeurs et concepteurs qui sont également administrateurs. Ainsi la responsabilité entière des domaines de sécurité (protection, défense, résilience) est entre les mains d'une seule et même équipe.

### Contrôles d’accès physique

Le serveur est hébergé par OVH, unique exploitant du centre de données.  Seuls les salariés accrédités peuvent accéder physiquement aux serveurs informatiques. L'accès est contrôlés par badge, surveillance vidéo et gardiennage 24/7.

L'entreprise OVH revendique pour son offre Cloud les certifications listées à l'adresse suivante: https://www.ovh.com/fr/apropos/certifications.xml - à la date de ce document, les certifications PCI-DSS, ISO/IEC 27001, SOC 1 type II et SOC 2 type II.

### Standards pour les mots de passe

Les mots de passe des utilisateurs (opérateurs de taxi et moteurs de recherche) leur sont attribués par les administrateurs affectés à l'exploitation du Taxi Exchange Point (TXP).
Ils sont générés à l'aide d'un générateur de mots de passe utilisant les réglages suivants :

  - 10 caractères
  - Majuscules, minuscules, chiffres et symboles

### Gestion et réponse aux incidents

Les administrateurs affectés à l'exploitation du Taxi Exchange Point (TXP) sont seuls accrédités à intervenir sur le Taxi Exchange Point (TXP).
L'authentification des administrateurs affectés à l'exploitation du Taxi Exchange Point (TXP) est individuelle, multifacteurs (HOTP) et loguée.

### Sauvegardes 

Les différents éléments sauvegardés sont :

 - les sources : publiquement sur https://github.com/openmaraude
 - la configuration : sur un gitlab privé
 - les données : sauvegardes périodiques chiffrées (GPG) exportées vers un stockage distant

### Chiffrement des données et des communications

Toutes les communications entre le Taxi Exchange Point (TXP) et le monde extérieur sont chiffrées par SSL.
Seule exception, les datagrammes UDP remontant des opérateurs de taxis vers le Taxi Exchange Point (TXP) sont en clair (signés mais pas chiffrés), mais ce canal est unidirectionnel.

### Tests de la sécurité

Des tests réguliers de sécurité sont effectués avec des scanners de vulnérabilité (Qualys SSL Labs, AsafaWeb).
Les résultats de certains de ces tests sont publiquement consultables sur https://verif.site/#api.taxi

### Surveillance en continu

La disponibilité est surveillée en continu et publiquement consultable sur http://opendatataxi.fr/status/
Les opérateurs affectés à l'exploitation du Taxi Exchange Point (TXP) sont automatiquement alertés par e-mail en cas d'incident.

Les paramètres d'exploitation sont surveillés en continu sur https://api.taxi/munin/ et des alertes mail sont adressées aux opérateurs du système en cas de dépassement des valeurs critiques.

## Signature

Paris, le XX janvier 2017
