# Bibliothèque de Prompts — Développeurs Confirmés
> Version 1.0 — Digital House Company  
> Usage : copier le prompt, remplir les zones `[EN MAJUSCULES]`, exécuter.

---

## TABLE DES MATIÈRES

1. [Architecture & Design](#1-architecture--design)
2. [Refactoring & Clean Code](#2-refactoring--clean-code)
3. [Génération de Code](#3-génération-de-code)
4. [Tests & Qualité](#4-tests--qualité)
5. [Débogage & Diagnostic](#5-débogage--diagnostic)
6. [Sécurité](#6-sécurité)
7. [Performance & Optimisation](#7-performance--optimisation)
8. [Base de Données & SQL](#8-base-de-données--sql)
9. [API & Intégrations](#9-api--intégrations)
10. [DevOps & CI/CD](#10-devops--cicd)
11. [Documentation](#11-documentation)
12. [Code Review](#12-code-review)
13. [Migration & Legacy](#13-migration--legacy)
14. [Prompting Méta](#14-prompting-méta)

---

## 1. Architecture & Design

---

### 1.1 — Choisir une architecture pour un nouveau projet

```
RÔLE
Tu es un architecte logiciel senior avec 15 ans d'expérience.
Tu as conçu des systèmes pour des contextes variés : startups à forte croissance,
entreprises régulées, produits B2B à haute disponibilité.

CONTEXTE DU PROJET
Type de produit : [SaaS / API / monolite / microservices / mobile backend / autre]
Équipe : [taille et niveau moyen : ex. 3 devs mid-level]
Contraintes techniques : [cloud provider, langages imposés, infra existante]
Contraintes non-techniques : [budget, délais, réglementations]
Trafic estimé au lancement : [ex. 1 000 utilisateurs/jour]
Trafic estimé à 12 mois : [ex. 100 000 utilisateurs/jour]
Tolérance aux pannes : [critique / standard / best-effort]

OBJECTIF
Proposer une architecture adaptée à ce contexte.

FORMAT DE RÉPONSE
1. Recommandation principale avec justification (3-4 lignes max)
2. Schéma textuel de l'architecture (ASCII ou liste hiérarchique)
3. Les 3 décisions structurantes et pourquoi
4. Les 2 principaux risques et comment les mitiger
5. Ce que tu NE recommandes pas dans ce contexte et pourquoi

CONTRAINTES
- Pas de sur-ingénierie : l'architecture doit être tenable par l'équipe décrite
- Mentionner explicitement les trade-offs
- Ne pas lister toutes les options possibles : choisir et justifier
```

---

### 1.2 — Évaluer une architecture existante

```
RÔLE
Tu es un architecte expérimenté mandaté pour auditer une architecture existante.
Tu es direct, factuel, sans complaisance.

ARCHITECTURE À ÉVALUER
[Description textuelle ou schéma de l'architecture actuelle]

CONTEXTE
Âge du système : [ex. 4 ans]
Équipe actuelle : [ex. 5 devs]
Principaux problèmes signalés : [ex. lenteurs, couplage fort, déploiements difficiles]
Trafic actuel : [ex. 50 000 requêtes/jour]

OBJECTIF
Auditer cette architecture et identifier les points critiques.

FORMAT DE RÉPONSE
1. Score global [1-10] avec justification en 2 phrases
2. Points forts (max 3, sincères)
3. Points critiques classés par priorité : [BLOQUANT / MAJEUR / MINEUR]
   - Pour chaque point : problème → impact concret → piste de solution
4. Recommandation de roadmap : quick wins (< 1 semaine) / moyen terme / long terme

Ne pas reformuler ce que j'ai dit. Aller directement à l'analyse.
```

---

### 1.3 — Concevoir un système de gestion d'événements (Event-Driven)

```
RÔLE
Tu es expert en architecture event-driven et messaging (Kafka, RabbitMQ, SQS, NATS).

CONTEXTE
Système source : [ex. API de commandes e-commerce]
Événements à propager : [ex. order.created, order.paid, order.shipped, order.cancelled]
Consommateurs : [ex. service stock, service email, service analytics, service facturation]
Volume estimé : [ex. 500 événements/seconde en pic]
Garanties requises : [at-least-once / exactly-once / best-effort]
Technologie cible : [ex. Kafka sur AWS MSK, ou pas de préférence]

OBJECTIF
Concevoir le schéma event-driven pour ce système.

FORMAT DE RÉPONSE
1. Choix technologique recommandé + justification
2. Schéma des topics/queues avec leur rôle
3. Schéma d'un événement (structure JSON avec tous les champs)
4. Stratégie de gestion des erreurs (dead letter queue, retry policy)
5. Ce qu'il faut absolument éviter dans ce design
6. Comment tester ce système en local
```

---

### 1.4 — Découpage en microservices

```
RÔLE
Tu es architecte spécialisé en décomposition de domaines (Domain-Driven Design).

MONOLITHE EXISTANT
[Description des modules/fonctionnalités actuels du monolithe]

DOMAINES MÉTIER IDENTIFIÉS
[Ex. : gestion utilisateurs, catalogue produits, commandes, paiements, notifications]

OBJECTIF
Proposer un découpage en microservices basé sur les bounded contexts.

FORMAT DE RÉPONSE
1. Bounded contexts identifiés avec leur responsabilité précise
2. Pour chaque service :
   - Données dont il est propriétaire
   - API qu'il expose
   - Événements qu'il publie
   - Événements auxquels il souscrit
3. Les couplages résiduels inévitables et comment les gérer
4. Ordre de migration recommandé (quel service extraire en premier et pourquoi)
5. Pattern de migration proposé (strangler fig / parallel run / big bang)

Éviter le piège du "nanoservice" : justifier la granularité choisie.
```

---

## 2. Refactoring & Clean Code

---

### 2.1 — Refactoring ciblé

```
RÔLE
Tu es expert en refactoring [LANGAGE : TypeScript / Python / Java / Go / autre].
Tu maîtrises SOLID, DRY, KISS, YAGNI et les patterns du Gang of Four.

CODE À REFACTORISER
[COLLE LE CODE ICI]

PROBLÈMES CONSTATÉS (facultatif, si tu les connais déjà)
[Ex. : fonction trop longue, couplage fort, tests impossibles, logique dupliquée]

CONTRAINTES
- Comportement observable identique après refactoring
- Pas de nouvelles dépendances externes
- Compatibilité [VERSION / ENVIRONNEMENT]
- [Autre contrainte spécifique]

FORMAT DE RÉPONSE
1. Analyse : les 3-5 problèmes identifiés avec leur impact
2. Code refactorisé complet
3. Journal des changements : ce qui a changé et pourquoi (une ligne par changement)
4. Ce que le refactoring ne règle PAS (honnêteté sur les limites)
```

---

### 2.2 — Réduire la complexité cyclomatique

```
RÔLE
Tu es expert en simplification de code et réduction de la complexité.

CODE
[COLLE LE CODE ICI]

OBJECTIF
Réduire la complexité cyclomatique de ce code sans en changer le comportement.

APPROCHES AUTORISÉES
- Early return / guard clauses
- Extraction de fonctions
- Table de dispatch (lookup table)
- Polymorphisme si pertinent
- Pattern Strategy si pertinent

FORMAT DE RÉPONSE
1. Complexité cyclomatique actuelle estimée
2. Code simplifié
3. Complexité cyclomatique après
4. Explication de l'approche choisie
5. Alternative écartée et pourquoi
```

---

### 2.3 — Éliminer la duplication de code

```
RÔLE
Tu es expert en abstraction et DRY (Don't Repeat Yourself).

CONTEXTE
Voici plusieurs extraits de code qui contiennent de la duplication :

EXTRAIT 1
[CODE]

EXTRAIT 2
[CODE]

EXTRAIT 3 (si applicable)
[CODE]

OBJECTIF
Identifier la duplication et proposer une abstraction réutilisable.

CONTRAINTES
- L'abstraction ne doit pas être sur-généralisée
- Elle doit rester lisible pour un dev qui ne connaît pas le contexte
- Indiquer si la duplication est "accidentelle" ou "essentielle"
  (parfois dupliquer est la bonne décision)

FORMAT DE RÉPONSE
1. Nature de la duplication identifiée
2. Abstraction proposée (fonction, classe, hook, mixin, etc.)
3. Comment les 3 extraits utilisent cette abstraction
4. Verdict : vaut-il vraiment la peine de l'extraire ? Justifier.
```

---

### 2.4 — Rendre du code testable

```
RÔLE
Tu es expert TDD et en conception orientée testabilité.

CODE
[COLLE LE CODE ICI]

PROBLÈME
Ce code est difficile à tester car [ex. : dépendances globales, effets de bord,
singleton, couplage fort avec la base de données, etc.]

OBJECTIF
Restructurer ce code pour le rendre unitairement testable.

FORMAT DE RÉPONSE
1. Diagnostic : pourquoi ce code est actuellement difficile à tester
2. Code restructuré avec injection de dépendances ou autre technique
3. Exemple de test unitaire pour le cas nominal
4. Exemple de test pour le cas d'erreur
5. Interface/contrat créé (si applicable)
```

---

## 3. Génération de Code

---

### 3.1 — Générer une feature complète

```
RÔLE
Tu es un développeur senior [LANGAGE/FRAMEWORK : ex. NestJS + TypeScript].

CONTEXTE TECHNIQUE
Framework : [ex. NestJS 10]
Base de données : [ex. PostgreSQL via TypeORM]
Auth : [ex. JWT, l'utilisateur courant est dans req.user]
Style de code : [ex. fonctionnel / orienté objet / mixte]
Structure du projet : [ex. architecture en modules NestJS]

SCHÉMA DE DONNÉES EXISTANT
[Colle les entités/tables concernées ou leur description]

FEATURE À IMPLÉMENTER
[Description précise de la feature]

COMPORTEMENT ATTENDU
- [Cas nominal 1]
- [Cas nominal 2]
- [Cas d'erreur 1 et réponse attendue]
- [Cas d'erreur 2 et réponse attendue]

FORMAT DE RÉPONSE
1. Liste des fichiers à créer/modifier
2. Chaque fichier complet avec son chemin
3. Migration de base de données si nécessaire
4. Exemples de requêtes HTTP (curl ou format REST)

DOD
- Validation des inputs
- Gestion d'erreurs avec codes HTTP appropriés
- Typage complet (pas de `any`)
- Aucune logique métier dans les controllers
```

---

### 3.2 — Implémenter un algorithme

```
RÔLE
Tu es expert en algorithmique et structures de données.

PROBLÈME
[Description précise du problème à résoudre]

EXEMPLES
Input : [exemple d'entrée]
Output attendu : [exemple de sortie]

Input : [autre exemple]
Output attendu : [autre sortie]

Cas limite : [ex. liste vide, valeur nulle, doublon, très grande entrée]

CONTRAINTES
Langage : [LANGAGE]
Complexité temporelle cible : [ex. O(n log n) ou mieux]
Complexité spatiale cible : [ex. O(n)]
Pas de librairies externes : [OUI / NON]

FORMAT DE RÉPONSE
1. Approche choisie et justification (2-3 lignes)
2. Complexité temporelle et spatiale de la solution
3. Code complet et commenté
4. Tests des cas nominaux et cas limites
5. Alternative écartée et pourquoi
```

---

### 3.3 — Générer un CLI tool

```
RÔLE
Tu es développeur Node.js expert en outils en ligne de commande.

OUTIL À CRÉER
Nom : [ex. db-migrator]
Description : [ex. outil qui compare deux schémas PostgreSQL et génère les migrations]

COMMANDES
[NOM_OUTIL] [COMMANDE_1] [OPTIONS]
  Description : [ce que ça fait]
  Options : [liste des flags avec leur rôle]

[NOM_OUTIL] [COMMANDE_2] [OPTIONS]
  Description : [ce que ça fait]

COMPORTEMENT GLOBAL
- Gestion des erreurs : messages clairs, exit codes corrects (0 = succès, 1 = erreur)
- Output : [coloré / plain text / JSON selon --format]
- Config : [fichier .rc / variables d'env / flags uniquement]

STACK TECHNIQUE
[ex. Commander.js + chalk + ora, ou yargs, ou oclif]

FORMAT DE RÉPONSE
1. Structure des fichiers
2. Code complet de chaque fichier
3. package.json avec les dépendances et le bin
4. Exemples d'utilisation dans README
```

---

### 3.4 — Créer un middleware / intercepteur

```
RÔLE
Tu es expert [FRAMEWORK : Express / NestJS / Fastify / Koa].

CONTEXTE
Framework : [FRAMEWORK + VERSION]
Middleware à créer : [description du comportement]

COMPORTEMENT
- Quand il s'applique : [toutes les routes / certaines routes / selon condition]
- Ce qu'il fait : [ex. log, auth, rate limit, transform request/response]
- Ce qu'il ne doit PAS modifier : [ex. le body des réponses 4xx]
- Ordre d'exécution : [avant / après les autres middlewares]

DONNÉES DISPONIBLES
[Ex. : token JWT dans Authorization header, user_id dans req.user]

FORMAT DE RÉPONSE
1. Code du middleware complet
2. Comment l'enregistrer dans l'app
3. Test unitaire du middleware (happy path + edge case)
4. Un cas où ce middleware ne devrait PAS s'appliquer et comment l'exclure
```

---

### 3.5 — Générer un script de traitement batch

```
RÔLE
Tu es expert en traitement de données et scripts de production.

CONTEXTE
Langage : [Python / Node.js / autre]
Source de données : [ex. CSV de 500 000 lignes / table PostgreSQL / API paginée]
Destination : [ex. autre table / fichier / API externe]

TRANSFORMATION À APPLIQUER
[Description précise de ce qui doit être transformé]

CONTRAINTES
- Volume : [ex. 500 000 lignes]
- Mémoire disponible : [ex. 512 Mo max → traitement en streaming]
- Idempotence : [le script peut-il être relancé sans créer de doublons ?]
- Logging : [ex. progress bar, log toutes les 1000 lignes, rapport final]
- Gestion des erreurs : [ex. skip les lignes invalides et les logger, ou stop à la première erreur]

FORMAT DE RÉPONSE
1. Code complet du script
2. Stratégie de découpage en chunks/batches
3. Comment reprendre après une interruption (checkpoint)
4. Commande d'exécution avec les variables d'environnement
5. Estimation du temps d'exécution sur le volume indiqué
```

---

## 4. Tests & Qualité

---

### 4.1 — Générer une suite de tests unitaires

```
RÔLE
Tu es expert TDD avec [FRAMEWORK : Jest / Vitest / Pytest / JUnit / autre].

CODE À TESTER
[COLLE LE CODE ICI]

OBJECTIF
Générer une suite de tests complète pour ce code.

COUVERTURE REQUISE
- Cas nominaux : tous les chemins "happy path"
- Cas limites : valeurs aux bornes, vides, null/undefined
- Cas d'erreur : exceptions attendues, inputs invalides
- Cas de concurrence si applicable

CONTRAINTES
- Tests isolés : chaque test doit pouvoir tourner seul
- Mocks pour toutes les dépendances externes (I/O, base de données, API)
- Noms de tests descriptifs : "should [FAIRE QUOI] when [CONDITION]"
- Pas de logique dans les tests (pas de if, pas de boucle)
- Arrange / Act / Assert clairement séparés

FORMAT DE RÉPONSE
1. Fichier de test complet, prêt à exécuter
2. Liste des cas couverts (tableau)
3. Ce qui N'est PAS testé et pourquoi (honnêteté sur la couverture)
4. Comment lancer les tests
```

---

### 4.2 — Générer des tests d'intégration

```
RÔLE
Tu es expert en tests d'intégration pour APIs REST / GraphQL.

ENDPOINT À TESTER
Méthode : [GET / POST / PUT / DELETE / PATCH]
Route : [ex. POST /api/orders]
Auth requise : [oui / non, type : Bearer JWT / API Key / Basic]

COMPORTEMENT ATTENDU
Cas 1 : [input valide → status 201 + body attendu]
Cas 2 : [input invalide → status 400 + structure d'erreur]
Cas 3 : [non authentifié → status 401]
Cas 4 : [conflit → status 409]
[Ajouter autant de cas que nécessaire]

STACK TECHNIQUE
[ex. Supertest + Jest, ou Pytest + httpx, ou Postman/Newman]

CONTEXTE DE TEST
[ex. base de données de test réinitialisée avant chaque test,
fixtures définies dans setup.ts]

FORMAT DE RÉPONSE
1. Fichier de test complet
2. Setup et teardown (DB seed, cleanup)
3. Comment isoler les tests les uns des autres
4. Comment lancer uniquement ces tests
```

---

### 4.3 — Générer des tests de performance (load testing)

```
RÔLE
Tu es expert en tests de charge avec [k6 / Artillery / Locust / JMeter].

ENDPOINT CIBLE
[URL ou description de l'API]

OBJECTIFS DE PERFORMANCE
- Throughput cible : [ex. 1 000 req/s]
- Latence p95 cible : [ex. < 200ms]
- Latence p99 cible : [ex. < 500ms]
- Taux d'erreur acceptable : [ex. < 0.1%]

SCÉNARIO DE CHARGE
Phase 1 (warm-up) : [ex. 10 users, 30 secondes]
Phase 2 (montée) : [ex. 0 → 500 users en 2 minutes]
Phase 3 (pic) : [ex. 500 users constant pendant 5 minutes]
Phase 4 (descente) : [ex. 500 → 0 en 1 minute]

DONNÉES DE TEST
[Description des données à envoyer : structure des payloads, variabilité]

FORMAT DE RÉPONSE
1. Script de test complet
2. Comment l'exécuter
3. Comment interpréter les résultats
4. Seuils d'alerte à configurer (thresholds)
```

---

### 4.4 — Audit de couverture de tests

```
RÔLE
Tu es expert QA et tu analyses la couverture de tests existante.

CODE SOURCE
[COLLE LE CODE ICI]

TESTS EXISTANTS (si disponibles)
[COLLE LES TESTS EXISTANTS ICI]

RAPPORT DE COUVERTURE (si disponible)
[Colle le rapport Istanbul / Coverage.py / autre]

OBJECTIF
Identifier les lacunes de couverture et prioriser les tests manquants.

FORMAT DE RÉPONSE
1. Estimation du niveau de couverture actuel
2. Chemins non couverts classés par risque : [CRITIQUE / MAJEUR / MINEUR]
3. Les 5 tests les plus importants à écrire en priorité
4. Tests qui pourraient être supprimés (redondants ou trop fragiles)
```

---

## 5. Débogage & Diagnostic

---

### 5.1 — Analyser une erreur

```
RÔLE
Tu es expert en débogage [LANGAGE / FRAMEWORK].
Tu ne donnes pas de solutions au hasard. Tu raisonnes cause → effet.

CODE CONCERNÉ
[COLLE LE CODE ICI]

ERREUR EXACTE
[COLLE LE MESSAGE D'ERREUR COMPLET AVEC LA STACK TRACE]

CONTEXTE D'EXÉCUTION
OS : [ex. Ubuntu 22.04 / macOS 14]
Version runtime : [ex. Node.js 20.11 / Python 3.11]
Version des dépendances clés : [ex. express 4.18, prisma 5.7]
Quand l'erreur apparaît : [toujours / parfois / dans certaines conditions]
Ce qui a changé récemment : [ex. upgrade de dépendance, nouveau code, changement config]

CE QUE J'AI DÉJÀ ESSAYÉ
[Liste tes tentatives de correction]

OBJECTIF
1. Explication de la cause racine (pas juste les symptômes)
2. Correction
3. Comment éviter ce type d'erreur à l'avenir
4. Y a-t-il d'autres endroits dans le code où le même problème pourrait exister ?
```

---

### 5.2 — Diagnostiquer une fuite mémoire

```
RÔLE
Tu es expert en profilage mémoire et détection de fuites [LANGAGE].

CONTEXTE
Langage / Runtime : [ex. Node.js 20]
Framework : [ex. Express]
Symptôme observé : [ex. mémoire augmente de 50Mo/heure, crash après 12h]
Profil d'utilisation : [ex. 200 req/s, connexions WebSocket longues durée]

CODE SUSPECT
[COLLE LE CODE OU LA SECTION SUSPECTE]

MÉTRIQUES DISPONIBLES
[ex. heap snapshot, graph mémoire, output de --inspect]

OBJECTIF
1. Identifier les patterns de code suspects (event listeners non supprimés,
   closures, caches sans TTL, références circulaires, etc.)
2. Correction pour chaque problème identifié
3. Comment confirmer que la fuite est corrigée
4. Comment surveiller la mémoire en production
```

---

### 5.3 — Analyser une race condition

```
RÔLE
Tu es expert en programmation concurrente et en débogage de conditions de course.

CONTEXTE
Langage : [ex. Node.js / Go / Java]
Type de concurrence : [threads / coroutines / event loop / workers]
Symptôme : [ex. données corrompues, deadlock intermittent, résultat non déterministe]

CODE CONCERNÉ
[COLLE LE CODE ICI]

FRÉQUENCE DU BUG
[ex. 1 fois sur 1000 requêtes, seulement sous forte charge]

OBJECTIF
1. Identifier la section critique et expliquer pourquoi la race condition est possible
2. Proposer une correction (mutex, atomic, queue, redesign)
3. Expliquer le trade-off de la solution proposée (perf, complexité)
4. Comment écrire un test qui reproduit la race condition de façon fiable
```

---

### 5.4 — Analyser des logs de production

```
RÔLE
Tu es expert en analyse de logs et en SRE (Site Reliability Engineering).

LOGS
[COLLE LES LOGS ICI]

CONTEXTE
Système : [ex. API Node.js sur Kubernetes]
Période : [ex. incident du 2025-01-15 entre 14h00 et 14h45 UTC]
Impact observé : [ex. latence × 10, taux d'erreur 5xx passé à 12%]

OBJECTIF
1. Identifier la cause probable de l'incident
2. Timeline de l'incident reconstituée depuis les logs
3. Root cause hypothesis (avec niveau de confiance)
4. Actions immédiates recommandées
5. Logs manquants qui auraient facilité le diagnostic
```

---

## 6. Sécurité

---

### 6.1 — Audit de sécurité d'un endpoint

```
RÔLE
Tu es un pentesteur et expert sécurité applicative (OWASP Top 10).
Tu analyses du code avec un regard offensif.

CODE DE L'ENDPOINT
[COLLE LE CODE ICI]

CONTEXTE
Type d'application : [API REST / GraphQL / application web]
Données manipulées : [ex. données personnelles, paiements, fichiers utilisateurs]
Auth : [ex. JWT, sessions, API Key]

OBJECTIF
Identifier toutes les vulnérabilités de sécurité.

FORMAT DE RÉPONSE
Pour chaque vulnérabilité :
- Catégorie OWASP
- Niveau de risque : [CRITIQUE / ÉLEVÉ / MOYEN / FAIBLE]
- Description de l'attaque possible
- Payload d'exemple (pour démontrer l'exploitabilité)
- Correction recommandée
- Code corrigé si applicable

Ne pas lister les bonnes pratiques génériques.
Se concentrer sur ce qui est réellement vulnérable dans CE code.
```

---

### 6.2 — Sécuriser l'authentification et l'autorisation

```
RÔLE
Tu es expert en IAM (Identity & Access Management) et sécurité web.

SYSTÈME ACTUEL
[Description du système d'auth existant ou à concevoir]

CONTEXTE
Type d'application : [ex. SaaS multi-tenant B2B]
Utilisateurs : [ex. admin, manager, user standard, viewer]
Ressources à protéger : [liste des ressources et des niveaux d'accès requis]
Contraintes : [ex. SSO SAML requis, 2FA obligatoire pour les admins]

OBJECTIF
Concevoir ou auditer le système d'auth et d'authz.

FORMAT DE RÉPONSE
1. Matrice des permissions (tableau rôle × action × ressource)
2. Implémentation du middleware d'autorisation
3. Les 5 erreurs les plus courantes dans ce type de système
4. Comment gérer la révocation de tokens
5. Stratégie de refresh token sécurisée
```

---

### 6.3 — Prévenir les injections

```
RÔLE
Tu es expert en sécurité applicative, spécialiste des injections (SQL, NoSQL, commande, LDAP).

CODE À AUDITER
[COLLE LE CODE ICI]

TYPE D'INJECTION À VÉRIFIER
[SQL / NoSQL / Command injection / XSS / SSTI / path traversal / tout]

OBJECTIF
1. Identifier chaque point d'injection potentiel
2. Pour chaque point : payload d'attaque exemple
3. Correction avec le bon pattern (requêtes paramétrées, échappement, validation)
4. Code corrigé complet

DOD
Aucune concaténation de chaîne pour construire des requêtes ou des commandes.
```

---

### 6.4 — Sécuriser le stockage et le transit des données sensibles

```
RÔLE
Tu es expert en cryptographie appliquée et protection des données (RGPD, PCI-DSS).

DONNÉES À PROTÉGER
[Ex. : mots de passe, tokens, données bancaires, données de santé, PII]

CONTEXTE TECHNIQUE
Langage : [LANGAGE]
Base de données : [ex. PostgreSQL]
Cache : [ex. Redis]
Transport : [ex. HTTPS, WebSocket, message queue]

OBJECTIF
Définir la stratégie de protection pour ces données.

FORMAT DE RÉPONSE
1. Classification des données (sensibilité et réglementation applicable)
2. Pour chaque type de donnée :
   - Méthode de chiffrement/hachage recommandée
   - Implémentation en [LANGAGE]
   - Où stocker les clés
3. Ce qu'il NE faut pas faire (avec explication)
4. Comment auditer que les données sont bien protégées
```

---

## 7. Performance & Optimisation

---

### 7.1 — Optimiser une requête lente

```
RÔLE
Tu es expert en optimisation de bases de données et query planning.

REQUÊTE
[COLLE LA REQUÊTE SQL OU ORM ICI]

EXPLAIN ANALYZE (si disponible)
[COLLE LE PLAN D'EXÉCUTION ICI]

CONTEXTE
Base de données : [PostgreSQL / MySQL / autre + version]
Volume de données : [ex. table orders : 50M lignes, table users : 500K lignes]
Temps d'exécution actuel : [ex. 4.2 secondes]
Objectif : [ex. < 100ms]
Index existants : [liste des index actuels sur les tables concernées]

OBJECTIF
Optimiser cette requête pour atteindre l'objectif de performance.

FORMAT DE RÉPONSE
1. Diagnostic : pourquoi cette requête est lente
2. Requête optimisée
3. Index à créer (avec commande CREATE INDEX)
4. Impact estimé sur les performances
5. Trade-offs : coût en écriture des nouveaux index, espace disque
```

---

### 7.2 — Implémenter une stratégie de cache

```
RÔLE
Tu es expert en stratégies de cache (Redis, Memcached, cache in-process).

CONTEXTE
Données à cacher : [description des données]
Source de données : [base de données / API externe / calcul coûteux]
Taux de lecture : [ex. 10 000 req/s]
Taux d'écriture : [ex. 100 req/s]
Fraîcheur requise : [ex. données pouvant avoir 30s de retard / temps réel impératif]
Infrastructure disponible : [ex. Redis Cluster, ou Redis standalone, ou cache mémoire]

OBJECTIF
Concevoir la stratégie de cache optimale pour ce contexte.

FORMAT DE RÉPONSE
1. Pattern recommandé : [Cache-Aside / Write-Through / Write-Behind / Read-Through]
   + justification
2. Stratégie d'invalidation : TTL / event-based / manual
3. Gestion du cache miss (thundering herd problem si applicable)
4. Implémentation en [LANGAGE]
5. Comment monitorer l'efficacité du cache (hit rate, éviction rate)
6. Ce qui NE doit PAS être mis en cache dans ce contexte
```

---

### 7.3 — Optimiser le code Node.js / Python

```
RÔLE
Tu es expert en optimisation [Node.js / Python] et profilage d'applications.

CODE À OPTIMISER
[COLLE LE CODE ICI]

MÉTRIQUES ACTUELLES
[Ex. : 850ms pour traiter 1000 items, 300Mo de mémoire utilisée]

OBJECTIF DE PERFORMANCE
[Ex. : < 100ms, < 50Mo]

CONTEXTE D'EXÉCUTION
[Ex. : Lambda AWS 512Mo, ou serveur dédié 32 cores]

FORMAT DE RÉPONSE
1. Goulots d'étranglement identifiés (dans l'ordre d'impact)
2. Code optimisé avec les changements annotés
3. Gain de performance estimé par optimisation
4. Comment profiler pour valider les gains (outil + commande)
5. Optimisations NOT recommandées ici et pourquoi (éviter la micro-optimisation inutile)
```

---

### 7.4 — Implémenter le pagination et l'infinite scroll

```
RÔLE
Tu es expert en pagination d'API et performance frontend/backend.

CONTEXTE
Endpoint : [description de l'endpoint]
Volume de données : [ex. 5 millions d'enregistrements]
Cas d'usage : [pagination classique avec pages / infinite scroll / cursor-based]
Tri : [ex. par date décroissante + tri secondaire par ID]
Filtres : [ex. par catégorie, par statut]

OBJECTIF
Implémenter une pagination performante et correcte.

FORMAT DE RÉPONSE
1. Choix entre OFFSET et cursor-based pagination + justification pour ce contexte
2. Implémentation backend (requête + structure de réponse)
3. Gestion des cas : données modifiées entre deux pages, tri instable
4. Implémentation frontend si applicable
5. Comment tester que la pagination est correcte (pas de trous, pas de doublons)
```

---

## 8. Base de Données & SQL

---

### 8.1 — Concevoir un schéma de base de données

```
RÔLE
Tu es expert en modélisation de données relationnelles.

DOMAINE MÉTIER
[Description du domaine : ex. plateforme e-commerce B2B]

ENTITÉS IDENTIFIÉES
[Liste des entités : ex. Company, User, Product, Order, Invoice, Payment]

RÈGLES MÉTIER
[Ex. : un user appartient à une seule company,
une commande peut avoir plusieurs produits avec quantité et prix unitaire,
une facture est générée par commande validée]

CONTRAINTES
[Ex. : multi-devise, soft delete requis, audit trail, RGPD (droit à l'oubli)]

BASE DE DONNÉES
[PostgreSQL / MySQL / autre]

FORMAT DE RÉPONSE
1. Schéma ERD textuel (tables, colonnes, types, clés)
2. Script SQL de création (CREATE TABLE avec contraintes)
3. Index recommandés avec justification
4. Décisions de design expliquées (normalisation, dénormalisation choisie)
5. Ce qui peut évoluer et comment l'anticiper
```

---

### 8.2 — Écrire une requête analytique complexe

```
RÔLE
Tu es expert SQL, spécialisé en requêtes analytiques et window functions.

SCHÉMA
[Description des tables concernées avec leurs colonnes clés]

QUESTION MÉTIER
[Ex. : pour chaque client, donner : le nombre de commandes, le CA total,
le CA du mois courant, le rang par CA sur les 12 derniers mois,
et l'évolution du CA vs le mois précédent en pourcentage]

BASE DE DONNÉES
[PostgreSQL / MySQL 8+ / BigQuery / Snowflake / autre]

VOLUME
[Ex. : 50M lignes dans la table orders]

FORMAT DE RÉPONSE
1. Requête SQL complète avec CTEs pour la lisibilité
2. Explication de chaque CTE
3. Window functions utilisées et pourquoi
4. Index nécessaires pour que la requête soit performante
5. EXPLAIN ANALYZE attendu (estimer si < 1s ou non)
```

---

### 8.3 — Écrire des migrations de base de données

```
RÔLE
Tu es expert en migrations de bases de données et en zero-downtime deployments.

CHANGEMENT À EFFECTUER
[Ex. : ajouter une colonne NOT NULL à une table de 50M lignes,
ou renommer une colonne, ou splitter une table, ou ajouter une FK]

BASE DE DONNÉES
[PostgreSQL + version]
[Outil de migration : Flyway / Liquibase / Prisma / Knex / Alembic]

CONTRAINTES
- Zero downtime : [OUI / NON]
- Rollback requis : [OUI / NON]
- Volume : [nombre de lignes impactées]

FORMAT DE RÉPONSE
1. Stratégie de migration (expand-contract / blue-green / autre)
2. Script de migration (UP)
3. Script de rollback (DOWN)
4. Risques de cette migration et comment les mitiger
5. Comment tester la migration sur un dump de production avant de l'exécuter
6. Temps estimé d'exécution sur le volume indiqué
```

---

### 8.4 — Optimiser la configuration PostgreSQL

```
RÔLE
Tu es expert PostgreSQL DBA.

SERVEUR
RAM totale : [ex. 32 Go]
CPUs : [ex. 8 vCPUs]
Type de stockage : [SSD NVMe / SSD SATA / HDD]
Utilisation principale : [OLTP / OLAP / mixte]

WORKLOAD
Connexions simultanées max : [ex. 200]
Requêtes dominantes : [ex. beaucoup de lectures courtes, peu d'écritures]
Taille de la base : [ex. 500 Go]

PROBLÈME ACTUEL
[Ex. : OOM killer tue postgres, connexions saturées, checkpoint trop fréquents]

FORMAT DE RÉPONSE
1. Paramètres postgresql.conf recommandés avec valeurs et justifications :
   - shared_buffers
   - work_mem
   - max_connections
   - checkpoint_completion_target
   - effective_cache_size
   - (autres pertinents)
2. Configuration du connection pooling (PgBouncer recommandé si applicable)
3. Comment valider que les changements améliorent les choses
```

---

## 9. API & Intégrations

---

### 9.1 — Concevoir une API REST

```
RÔLE
Tu es expert en design d'API REST et en API-first development.

DOMAINE
[Description du domaine métier de l'API]

RESSOURCES
[Liste des ressources à exposer]

CONSOMMATEURS
[Ex. : application mobile iOS/Android, SPA React, intégrations B2B partenaires]

CONTRAINTES
[Ex. : versioning requis, rate limiting, pagination, auth OAuth2]

FORMAT DE RÉPONSE
1. Convention de nommage des routes (avec exemples)
2. Tableau complet des endpoints :
   | Méthode | Route | Description | Auth | Body | Réponse |
3. Structure standard des réponses (succès et erreur)
4. Stratégie de versioning (/v1/ vs header Accept)
5. Ce qui NE doit PAS être dans cette API (erreurs de design fréquentes)
```

---

### 9.2 — Intégrer une API tierce avec résilience

```
RÔLE
Tu es expert en intégrations d'APIs et en patterns de résilience.

API TIERCE
Nom : [ex. Stripe, Twilio, SendGrid, Salesforce]
Documentation : [URL ou description]
SLA de l'API : [ex. 99.9% uptime, rate limit 100 req/s]

APPELS À EFFECTUER
[Description de ce que ton code doit faire avec cette API]

CONTEXTE
Langage : [LANGAGE]
Criticité : [ex. paiement critique / notification best-effort]

FORMAT DE RÉPONSE
1. Client HTTP avec les patterns de résilience adaptés à la criticité :
   - Retry avec exponential backoff et jitter
   - Circuit breaker si applicable
   - Timeout
   - Fallback
2. Gestion des erreurs spécifiques à cette API (codes d'erreur importants)
3. Idempotence : comment éviter les actions dupliquées en cas de retry
4. Logging et monitoring des appels externes
5. Comment mocker cette API en développement et en tests
```

---

### 9.3 — Concevoir un webhook

```
RÔLE
Tu es expert en systèmes webhook et intégrations asynchrones.

CONTEXTE
Tu crées un système qui [envoie / reçoit] des webhooks.

ÉVÉNEMENTS
[Liste des événements : ex. payment.completed, subscription.cancelled]

PAYLOAD EXEMPLE
[Structure JSON d'un événement]

EXIGENCES
- Sécurité : [ex. signature HMAC SHA-256]
- Garanties de livraison : [at-least-once]
- Retry policy : [ex. 3 tentatives, backoff exponentiel]

FORMAT DE RÉPONSE

SI TU ENVOIES DES WEBHOOKS :
1. Système d'envoi avec retry et dead letter queue
2. Mécanisme de signature et comment le vérifier côté récepteur
3. Dashboard de monitoring des webhooks

SI TU REÇOIS DES WEBHOOKS :
1. Endpoint de réception sécurisé (validation de signature)
2. Pattern respond-then-process (répondre 200 immédiatement, traiter en async)
3. Idempotence (éviter de traiter deux fois le même événement)
4. Gestion des événements en désordre (out-of-order events)
```

---

### 9.4 — Concevoir une API GraphQL

```
RÔLE
Tu es expert GraphQL (schéma design, resolvers, performance).

DOMAINE
[Description du domaine]

ENTITÉS
[Liste des types à exposer]

QUERIES PRINCIPALES
[Ex. : liste des produits filtrés, détail d'un utilisateur avec ses commandes]

MUTATIONS PRINCIPALES
[Ex. : créer une commande, modifier le profil]

CONTRAINTES
[Ex. : N+1 problem à résoudre, auth par champ, subscriptions temps réel]

FORMAT DE RÉPONSE
1. Schéma GraphQL complet (types, queries, mutations, subscriptions)
2. Strategy pour le N+1 problem (DataLoader)
3. Stratégie d'authentification et d'autorisation au niveau des resolvers
4. Pagination (Connection pattern avec cursor)
5. Ce qui ne devrait PAS être exposé en GraphQL dans ce cas
```

---

## 10. DevOps & CI/CD

---

### 10.1 — Créer un pipeline CI/CD

```
RÔLE
Tu es expert DevOps et CI/CD ([GitHub Actions / GitLab CI / Jenkins / autre]).

PROJET
Type : [ex. API Node.js + frontend React]
Repository : [GitHub / GitLab / Bitbucket]
Environnements : [dev / staging / production]

ÉTAPES REQUISES
[Ex. : lint, tests unitaires, tests d'intégration, build Docker, push registry,
deploy sur staging, smoke tests, deploy sur prod si manuel]

CONTRAINTES
- Tests en parallèle si possible
- Cache des dépendances
- Variables d'environnement et secrets : [comment ils sont gérés]
- Rollback : [stratégie en cas d'échec]

FORMAT DE RÉPONSE
1. Fichier de config complet (.github/workflows/ci.yml ou .gitlab-ci.yml)
2. Explication de chaque job/stage
3. Comment ajouter une approbation manuelle avant la production
4. Estimation du temps total du pipeline
```

---

### 10.2 — Écrire un Dockerfile optimisé

```
RÔLE
Tu es expert Docker et optimisation d'images de conteneurs.

APPLICATION
Type : [ex. API Node.js 20 / Python 3.11 / Go 1.22]
Dépendances : [ex. npm install avec package-lock.json]
Build process : [ex. tsc build / webpack / rien]
Port exposé : [ex. 3000]

CONTRAINTES
- Taille d'image minimale
- Cache des layers optimisé (rebuild rapide quand seul le code change)
- Utilisateur non-root
- Multi-stage build
- Image de base : [alpine / debian-slim / distroless]
- Secrets de build : [NON / OUI → utiliser BuildKit secrets]

FORMAT DE RÉPONSE
1. Dockerfile multi-stage complet
2. .dockerignore
3. Taille estimée de l'image finale
4. Explication des choix d'optimisation
5. Commandes de build et de run
```

---

### 10.3 — Configurer un monitoring applicatif

```
RÔLE
Tu es expert SRE et observabilité (métriques, logs, traces).

APPLICATION
Type : [ex. API REST Node.js]
Infrastructure : [ex. Kubernetes sur GKE]
Stack d'observabilité : [ex. Prometheus + Grafana + Loki, ou Datadog, ou OpenTelemetry]

OBJECTIF
Mettre en place une observabilité complète (les 3 pilliers).

FORMAT DE RÉPONSE

MÉTRIQUES
1. Les 5 métriques applicatives les plus importantes pour ce type de service
   (latence p50/p95/p99, error rate, throughput, saturation, business metrics)
2. Comment les exposer (instrumentation du code)

LOGS
3. Structure des logs (format JSON recommandé avec les champs standards)
4. Niveaux de log et quand utiliser chaque niveau

TRACES
5. Comment instrumenter avec OpenTelemetry
6. Points de trace importants (entrée API, appels DB, appels externes)

ALERTES
7. Les 3 alertes critiques à configurer en premier
```

---

## 11. Documentation

---

### 11.1 — Documenter une API (OpenAPI / Swagger)

```
RÔLE
Tu es expert en documentation d'API et OpenAPI 3.0.

ENDPOINTS À DOCUMENTER
[COLLE LE CODE DES ROUTES ICI]

CONTEXTE
Framework : [ex. Express / FastAPI / NestJS]
Génération : [manuellement / depuis le code avec annotations]

FORMAT DE RÉPONSE
1. Spec OpenAPI 3.0 complète en YAML
   Couvrir pour chaque endpoint :
   - Description claire
   - Paramètres (path, query, header, body) avec types et exemples
   - Réponses (succès et erreurs) avec schémas
   - Auth (securitySchemes)
2. Comment servir cette spec avec Swagger UI
3. Les 3 erreurs les plus fréquentes dans la documentation d'API
```

---

### 11.2 — Documenter du code complexe

```
RÔLE
Tu es technical writer pour développeurs. Tu documentes pour des devs
qui rejoindront le projet dans 6 mois.

CODE À DOCUMENTER
[COLLE LE CODE ICI]

TYPE DE DOCUMENTATION REQUIS
[JSDoc / docstrings Python / commentaires inline / README de module / tout]

CONTRAINTES
- Expliquer le POURQUOI, pas juste le QUOI (le code dit déjà le quoi)
- Documenter les décisions non-évidentes et leurs raisons
- Documenter les pièges et effets de bord
- Pas de commentaires qui répètent le code

FORMAT DE RÉPONSE
1. Code avec documentation inline complète
2. README du module (si pertinent)
3. Exemples d'utilisation (2-3 cas d'usage représentatifs)
```

---

### 11.3 — Écrire un ADR (Architecture Decision Record)

```
RÔLE
Tu es architecte et tu documentes les décisions d'architecture.

DÉCISION À DOCUMENTER
Titre : [ex. Utilisation de Kafka plutôt que RabbitMQ pour le messaging]

CONTEXTE
[Description de la situation qui a nécessité une décision]

OPTIONS CONSIDÉRÉES
[Liste des options évaluées]

FORMAT DE RÉPONSE
Produire un ADR complet au format MADR (Markdown Architectural Decision Records) :

# ADR-[NUMERO] : [TITRE]

## Statut
[Proposé / Accepté / Déprécié / Remplacé par ADR-X]

## Contexte
[Situation, forces en présence, contraintes]

## Décision
[La décision prise, formulée à l'impératif]

## Conséquences
[Positives et négatives de cette décision]

## Options considérées
[Tableau comparatif des options avec pros/cons]

## Liens
[Liens vers d'autres ADRs liés]
```

---

## 12. Code Review

---

### 12.1 — Effectuer une code review complète

```
RÔLE
Tu es reviewer senior. Tu es direct, précis, bienveillant mais sans complaisance.
Tu donnes des commentaires actionnables, pas des opinions vagues.

CODE À REVIEWER
[COLLE LE CODE ICI]

CONTEXTE
Type de changement : [ex. nouvelle feature / bugfix / refactoring / optimisation]
Criticité : [ex. code de paiement / feature non-critique]
Niveau du développeur : [junior / mid / senior]

FORMAT DE RÉPONSE
Pour chaque commentaire :
- Fichier et ligne(s) concernés
- Catégorie : [BUG / SÉCURITÉ / PERFORMANCE / MAINTENABILITÉ / STYLE / SUGGESTION]
- Niveau : [BLOQUANT / RECOMMANDÉ / NITPICK]
- Description du problème
- Code suggéré (si applicable)

Résumé final :
- Verdict : [APPROVE / REQUEST_CHANGES / NEEDS_DISCUSSION]
- Les 2-3 points les plus importants
```

---

### 12.2 — Review axée sécurité

```
RÔLE
Tu es un security engineer effectuant une security review de ce code.
Tu penses comme un attaquant.

CODE
[COLLE LE CODE ICI]

SURFACE D'ATTAQUE
[Ex. : endpoint public, traite des uploads fichiers, accède à la DB en tant qu'admin]

FORMAT DE RÉPONSE
Pour chaque finding :
- Vulnérabilité : [nom OWASP + CWE si applicable]
- Sévérité : [CRITIQUE / ÉLEVÉE / MOYENNE / FAIBLE]
- Scénario d'attaque (comment un attaquant l'exploiterait)
- Preuve de concept (payload ou code d'attaque)
- Remédiation avec code

Rien sur ce qui est correct. Uniquement les problèmes.
```

---

### 12.3 — Review de Pull Request (commentaires prêts à poster)

```
RÔLE
Tu es un reviewer qui écrit des commentaires de PR clairs, directs, et respectueux.
Les commentaires seront lus par le développeur qui a soumis la PR.

CODE MODIFIÉ
[COLLE LE DIFF OU LE CODE ICI]

PROBLÈMES IDENTIFIÉS
[Liste tes observations]

OBJECTIF
Pour chaque problème, écrire un commentaire de PR :
- Formulé à la deuxième personne
- Qui explique le problème ET son impact
- Qui propose une solution concrète
- Avec le code suggéré si applicable

Ton : constructif, précis, pas condescendant.
Ne pas utiliser de formules comme "Comme vous le savez..." ou "Évidemment...".
```

---

## 13. Migration & Legacy

---

### 13.1 — Migrer de JavaScript vers TypeScript

```
RÔLE
Tu es expert en migration JavaScript → TypeScript et en typage progressif.

CODE JS À MIGRER
[COLLE LE CODE ICI]

CONTEXTE
Version TypeScript cible : [ex. 5.3]
Strictness : [strict: true / graduel : commencer par noImplicitAny seulement]
Framework : [ex. Express / React / Node.js pur]

OBJECTIF
Migrer ce code vers TypeScript.

FORMAT DE RÉPONSE
1. Code TypeScript complet
2. Types créés et pourquoi (interfaces vs type aliases)
3. Là où tu as dû utiliser `unknown` ou `as` et pourquoi (endroits à améliorer)
4. Là où TypeScript a détecté des bugs réels dans le code JS original
5. tsconfig.json recommandé pour ce projet
```

---

### 13.2 — Moderniser du code legacy

```
RÔLE
Tu es expert en modernisation de code et en gestion de dette technique.

CODE LEGACY
[COLLE LE CODE ICI]

ÂGE APPROXIMATIF
[Ex. : code écrit vers 2016, Node.js 8, callbacks, pas de tests]

OBJECTIF DE MODERNISATION
[Ex. : async/await, types TypeScript, tests, suppression des dépendances obsolètes]

CONTRAINTES
- Pas de réécriture complète : migration progressive
- Le comportement doit rester identique
- Les tests actuels (s'ils existent) doivent passer

FORMAT DE RÉPONSE
1. Analyse des patterns obsolètes identifiés
2. Plan de migration en étapes (quelle étape en premier et pourquoi)
3. Code modernisé pour l'étape 1
4. Comment tester que le comportement est identique avant/après
5. Dépendances à upgrader ou remplacer
```

---

### 13.3 — Migrer de REST vers GraphQL (ou inversement)

```
RÔLE
Tu es expert en migration d'APIs.

API EXISTANTE
[Description ou liste des endpoints REST existants]

OBJECTIF
Migrer vers [GraphQL / REST] en assurant une période de transition.

CONSOMMATEURS ACTUELS
[Ex. : application mobile v1 qui ne peut pas être mise à jour immédiatement,
frontend web qui peut être mis à jour]

CONTRAINTES
[Ex. : pas de breaking change pour les clients mobiles pendant 6 mois]

FORMAT DE RÉPONSE
1. Stratégie de migration (parallel running / BFF pattern / autre)
2. Schéma de la nouvelle API
3. Layer de compatibilité pour les anciens clients
4. Plan de dépréciation des anciens endpoints
5. Comment tracker l'usage des endpoints dépréciés
```

---

## 14. Prompting Méta

---

### 14.1 — Générer un prompt pour un cas spécifique

```
RÔLE
Tu es expert en prompt engineering pour des cas d'usage développement.

TÂCHE POUR LAQUELLE JE VEUX UN PROMPT
[Description précise de la tâche]

CONTEXTE D'UTILISATION
[Ex. : utilisé quotidiennement dans Cursor, ou dans un script automatisé,
ou dans Claude Desktop]

CE QUE LE PROMPT DOIT PRODUIRE
[Description du résultat attendu]

CONTRAINTES SUR LE PROMPT
[Ex. : doit fonctionner sans contexte supplémentaire, doit être < 500 tokens,
doit être réutilisable pour différents langages]

OBJECTIF
Génère le prompt optimisé pour cette tâche.
Explique les choix de formulation (pourquoi certains mots, pourquoi cette structure).
```

---

### 14.2 — Créer un skill file pour un agent IA

```
RÔLE
Tu es expert en configuration d'agents IA et en rédaction de system prompts.

AGENT À CONFIGURER
Nom : [ex. code-reviewer-security]
Rôle : [ex. reviewer spécialisé sécurité pour une équipe fintech]
Utilisateurs : [ex. développeurs mid à senior]

COMPORTEMENT ATTENDU
- Ce que l'agent DOIT faire : [liste]
- Ce que l'agent NE DOIT PAS faire : [liste]
- Ton souhaité : [ex. direct, technique, sans ménagement mais constructif]
- Format de sortie systématique : [description]

CONTEXTE MÉTIER
[Ex. : application de paiement, réglementations PCI-DSS applicables,
stack technique de l'équipe]

OBJECTIF
Générer le fichier SKILL.md complet pour cet agent.
Le skill doit être suffisamment précis pour produire des résultats cohérents
à chaque invocation, quel que soit le développeur qui l'utilise.
```

---

### 14.3 — Valider et améliorer un prompt existant

```
RÔLE
Tu es expert en prompt engineering et en évaluation de prompts.

PROMPT EXISTANT
[COLLE TON PROMPT ICI]

RÉSULTAT OBTENU (qui ne te satisfait pas)
[Description ou exemple du résultat actuel]

RÉSULTAT ATTENDU
[Description précise de ce que tu veux]

OBJECTIF
1. Analyser pourquoi le prompt actuel produit ce résultat
2. Identifier les ambiguïtés, les instructions manquantes, les formulations faibles
3. Proposer le prompt amélioré
4. Expliquer chaque modification apportée
```

---

### 14.4 — Créer une chaîne de prompts (prompt chaining)

```
RÔLE
Tu es expert en orchestration de prompts et workflows LLM.

TÂCHE COMPLEXE
[Description de la tâche finale à accomplir]

POURQUOI UN SEUL PROMPT NE SUFFIT PAS
[Ex. : trop d'étapes, résultats intermédiaires nécessaires, validation requise]

FORMAT DE RÉPONSE
1. Décomposition en étapes avec l'objectif de chaque étape
2. Pour chaque étape :
   - Prompt complet
   - Input attendu (venant de l'étape précédente ou de l'utilisateur)
   - Output produit (ce qui est passé à l'étape suivante)
   - Validation possible (comment vérifier que l'output est correct avant de continuer)
3. Diagramme textuel du flux
4. Gestion des erreurs : que faire si une étape échoue
```

---

## ANNEXE — Règles d'or

### Toujours inclure dans tes prompts

1. **Le rôle** : qui est l'IA, son niveau d'expertise, son angle
2. **Le contexte technique précis** : versions, stack, contraintes
3. **Le format de sortie** : structure exacte de ce que tu attends
4. **Les contraintes** : ce qu'elle ne doit PAS faire
5. **Le DoD** : comment savoir que c'est terminé

### Les erreurs qui dégradent la qualité

- Prompt vague → résultat générique
- Pas de contexte → hypothèses incorrectes
- Pas de format → structure imprévisible
- Trop de tâches en un seul prompt → qualité diluée
- Ne pas fournir les messages d'erreur exacts → diagnostic impossible

### Comment itérer

```
Étape 1 : Prompt initial + demande des hypothèses
Étape 2 : Corriger les hypothèses fausses
Étape 3 : Affiner le résultat
Étape 4 : Ajouter les cas limites
Étape 5 : Générer les tests
```

### Prompts à sauvegarder absolument

Les 5 prompts que tout dev devrait avoir dans sa bibliothèque :
1. Refactoring ciblé (2.1)
2. Génération de tests (4.1)
3. Analyse d'erreur (5.1)
4. Code review sécurité (12.2)
5. Optimisation de requête SQL (7.1)

---

*hello@dhcompany.pro*
