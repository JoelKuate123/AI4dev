# Patterns Mockito & pièges

Le minimum (`@Mock`, `@InjectMocks`, stubbing parcimonieux) est dans le SKILL.md.
Ce fichier couvre les cas avancés.

## Setup

```java
@ExtendWith(MockitoExtension.class)   // active la validation stricte des stubs
class FooServiceTest {
    @Mock private BarRepository barRepository;
    @InjectMocks private FooService fooService;
}
```

`MockitoExtension` est en mode `STRICT_STUBS` par défaut : un stub déclaré mais
jamais appelé fait échouer le test. C'est un garde-fou contre les tests qui ne
testent pas ce qu'ils prétendent. Ne pas le désactiver globalement.

## ArgumentCaptor — inspecter ce qui a été passé à un mock

À privilégier sur des `Matchers` complexes quand on veut asserter finement
l'argument réellement transmis.

```java
@Captor private ArgumentCaptor<User> userCaptor;

@Test
void should_persistUserWithNormalizedEmail_when_created() {
    fooService.register("ADA@EXAMPLE.COM");

    verify(barRepository).save(userCaptor.capture());
    assertThat(userCaptor.getValue().getEmail()).isEqualTo("ada@example.com");
}
```

## Matchers — règle du tout ou rien

Si un argument utilise un matcher (`any()`, `eq()`...), **tous** les arguments
de cet appel doivent être des matchers. Mélanger valeur brute et matcher lève
`InvalidUseOfMatchersException`.

```java
// FAUX : "x" est une valeur brute à côté d'un matcher
when(repo.find("x", any())).thenReturn(...);
// CORRECT
when(repo.find(eq("x"), any())).thenReturn(...);
```

## Stubber une exception / une séquence

```java
when(repo.findById(1L)).thenThrow(new DataAccessException("down"));

// réponses successives sur appels répétés
when(counter.next()).thenReturn(1, 2, 3);
```

Pour les méthodes `void` : `doThrow(...).when(mock).method();`.

## @Spy — n'utiliser qu'à bon escient

Un spy exécute le vrai code sauf pour les méthodes stubbées. Utile pour des
objets legacy difficiles à refactorer, mais c'est souvent le signe qu'une classe
fait trop de choses. Préférer l'injection de dépendances. Sur un spy, stubber
avec `doReturn(...).when(spy).method()` (la forme `when(spy.method())` exécute le
vrai code pendant le stubbing).

## BDDMockito — style given/when/then

Alias lisibles alignés sur la structure Arrange-Act-Assert :

```java
import static org.mockito.BDDMockito.given;
import static org.mockito.BDDMockito.then;

given(repo.findById(1L)).willReturn(Optional.of(user));
// ...
then(repo).should().save(user);
```

Cohérent à l'échelle d'un projet : choisir BDDMockito **ou** when/verify, pas les
deux dans la même base.

## verifyNoMoreInteractions — avec parcimonie

Garantit qu'aucune interaction non vérifiée n'a eu lieu. Puissant mais fragile :
le moindre appel ajouté casse le test. Réserver aux cas où l'absence
d'interaction fait explicitement partie du contrat (`verifyNoInteractions(repo)`
pour « ne doit pas toucher la base si le cache répond »).

## Ce qu'on ne mocke pas

- La classe sous test.
- Les types de valeur : `String`, `List`, `Optional`, DTO, records → les
  construire réellement.
- Les types qu'on ne possède pas et dont le comportement réel importe — préférer
  un vrai objet ou un fake léger.