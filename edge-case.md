# Checklist des cas limites & anti-patterns

À consulter pour les workflows B (suggérer les cas) et C (auditer), et pour
compléter A. Ne retenir que ce qui est **pertinent pour la méthode testée** :
une liste générique recopiée intégralement est inutile.

## Table des matières

1. Entrées & arguments
2. Collections & tableaux
3. Nombres & arithmétique
4. Chaînes de caractères
5. Dates & temps
6. Exceptions & erreurs
7. État & cycle de vie
8. Concurrence (si pertinent)
9. Anti-patterns de test à corriger

---

## 1. Entrées & arguments

- `null` passé à chaque paramètre objet : exception attendue ou tolérance ?
- Valeur par défaut / Optional vide.
- Argument hors domaine (négatif là où positif attendu, enum inconnue).
- Argument à la frontière exacte d'une condition (`<`, `<=`).
- Objet partiellement initialisé (champs obligatoires manquants).

## 2. Collections & tableaux

- Collection vide vs `null` (comportements souvent différents).
- Un seul élément (révèle les bugs d'itération/agrégation).
- Doublons, ordre non garanti, éléments `null` dans la collection.
- Très grande collection si une limite/pagination existe.

## 3. Nombres & arithmétique

- Zéro, valeurs négatives, `Integer.MAX_VALUE` / `MIN_VALUE` (débordement).
- Division par zéro.
- Arrondi et précision (`double` vs `BigDecimal` pour la monnaie).
- Frontières d'intervalle inclusives/exclusives.

## 4. Chaînes de caractères

- Chaîne vide `""` vs `null` vs blancs `"   "`.
- Casse, accents/Unicode, espaces en bordure (`trim`).
- Très longue chaîne si une limite de taille existe.
- Caractères spéciaux pour les entrées parsées (séparateurs, échappement).

## 5. Dates & temps

- Limites de jour/mois/année, années bissextiles.
- Fuseaux horaires et passage heure d'été (utiliser une `Clock` injectable
  plutôt que `LocalDateTime.now()` directement).
- Date passée vs future quand la logique en dépend.

## 6. Exceptions & erreurs

- Chaque exception déclarée est-elle effectivement déclenchée par un test ?
- Vérifier le **type** ET le **message/cause**, pas juste « ça lève quelque chose ».
- L'exception laisse-t-elle l'objet dans un état cohérent (pas de mutation partielle) ?
- Exception d'un collaborateur mocké correctement propagée ou traduite ?

## 7. État & cycle de vie

- Premier appel vs appels suivants (cache, lazy init, compteur).
- Idempotence : appeler deux fois donne-t-il le même résultat ?
- Réinitialisation entre deux scénarios (`@BeforeEach` propre).

## 8. Concurrence (seulement si la classe est concurrente)

- Accès simultané à un état partagé.
- Atomicité d'une opération composée.
- Ne pas tester avec `Thread.sleep` ; utiliser des latches/`Awaitility`.

---

## 9. Anti-patterns de test à corriger (workflow C)

| Anti-pattern | Pourquoi c'est un problème | Correction |
|---|---|---|
| `assertNotNull(result)` comme seule assertion | Le test passe même si le résultat est faux | Asserter la valeur attendue |
| Test sans assertion (juste un appel) | Ne peut jamais échouer | Ajouter l'assertion sur le comportement |
| `if`/boucle dans le test | Plusieurs cas masqués, échec ambigu | Un test par cas, ou `@ParameterizedTest` |
| Sur-mocking (mocker la classe testée ou des DTO) | Teste les mocks, pas le code | Instancier réel, mocker seulement les collaborateurs |
| `verify` sur tout | Test fragile au moindre refactor | Vérifier uniquement le contrat observable |
| Dépendance à l'ordre des tests | Échecs intermittents | État isolé via `@BeforeEach` |
| Noms type `test1`, `testIt` | Échec illisible | `should_x_when_y` + `@DisplayName` |
| `Thread.sleep` | Lent et instable | Abstraction de temps / `Awaitility` |
| Données magiques non expliquées | Test incompréhensible | Constantes nommées, fixtures explicites |
| Un test qui couvre 5 scénarios | Une seule raison d'échec impossible | Découper |