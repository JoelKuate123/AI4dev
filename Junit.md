# Configuration Maven — JUnit 5 + Mockito + AssertJ

À fournir si le `pom.xml` ne contient pas déjà ces dépendances. Vérifier les
versions disponibles au moment de l'usage (les numéros ci-dessous sont des
ordres de grandeur stables, pas des versions figées — proposer de confirmer la
dernière version si l'utilisateur veut être à jour).

## Dépendances

```xml
<dependencies>
    <!-- JUnit 5 (agrégateur : API + engine + params) -->
    <dependency>
        <groupId>org.junit.jupiter</groupId>
        <artifactId>junit-jupiter</artifactId>
        <version>5.11.x</version>
        <scope>test</scope>
    </dependency>

    <!-- Mockito + intégration JUnit 5 -->
    <dependency>
        <groupId>org.mockito</groupId>
        <artifactId>mockito-junit-jupiter</artifactId>
        <version>5.x</version>
        <scope>test</scope>
    </dependency>

    <!-- AssertJ -->
    <dependency>
        <groupId>org.assertj</groupId>
        <artifactId>assertj-core</artifactId>
        <version>3.26.x</version>
        <scope>test</scope>
    </dependency>
</dependencies>
```

`mockito-junit-jupiter` tire `mockito-core` en transitif : pas besoin de le
déclarer séparément.

## Plugin Surefire

Surefire exécute les tests pendant `mvn test`. Les versions récentes détectent
JUnit 5 sans configuration supplémentaire ; en cas de tests non découverts,
épingler une version récente :

```xml
<build>
    <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-surefire-plugin</artifactId>
            <version>3.2.x</version>
        </plugin>
    </plugins>
</build>
```

## Imports statiques utiles

```java
import static org.assertj.core.api.Assertions.assertThat;
import static org.assertj.core.api.Assertions.assertThatThrownBy;
import static org.junit.jupiter.api.Assertions.assertAll;
import static org.mockito.Mockito.when;
import static org.mockito.Mockito.verify;
import static org.mockito.ArgumentMatchers.any;
import static org.mockito.ArgumentMatchers.eq;
```

## Couverture (optionnel)

Si l'utilisateur veut mesurer la couverture, ajouter JaCoCo. La couverture est un
indicateur, pas un objectif : 100 % de lignes couvertes par des tests sans
assertion ne vaut rien. Viser des tests qui décrivent le comportement.