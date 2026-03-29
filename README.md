# CIB seven Spring Boot OIDC Template

Dieses Projekt zeigt eine einfache Loan-Approval-Anwendung auf Basis von CIB seven BPM mit OAuth2/OIDC-Authentifizierung über Keycloak.

## Voraussetzungen

- Java 17
- Maven 4
- Zugang zum CIB seven Enterprise Maven Repository

## Maven-Konfiguration

Da das CIB seven Enterprise Repository nicht öffentlich zugänglich ist, müssen die Zugangsdaten in `~/.m2/settings.xml` hinterlegt werden.

Falls noch keine `settings.xml` vorhanden ist, muss die Datei neu angelegt werden. Andernfalls die folgenden Abschnitte in die bestehende Datei einfügen:

**In `<servers>` einfügen:**
```xml
<server>
  <id>mvn-cibseven-enterprise</id>
  <username>KUNDENNUMMER</username>
  <password>PASSWORT</password>
</server>
```

**In `<profiles>` einfügen:**
```xml
<profile>
  <id>cibseven-ee</id>
  <repositories>
    <repository>
      <id>mvn-cibseven-enterprise</id>
      <name>CIB seven Enterprise repository</name>
      <url>https://artifacts.cibseven.org/repository/enterprise-group/</url>
    </repository>
  </repositories>
</profile>
```

**In `<activeProfiles>` einfügen:**
```xml
<activeProfile>cibseven-ee</activeProfile>
```

## Anwendungskonfiguration

In `src/main/resources/application.yaml` müssen folgende Platzhalter durch die tatsächlichen Werte ersetzt werden:

- `<url>` — Hostname des Keycloak-Servers (mehrfach vorhanden)
- `<secret>` — Client-Secret der Keycloak-Registrierung `cib-seven-local`

## Bauen und Starten

```bash
# Bauen
mvn clean package -DskipTests

# Starten
mvn spring-boot:run
```

Die Anwendung ist anschließend unter `http://localhost:8080` erreichbar. Die Engine-REST-API ist unter `/engine-rest` verfügbar.
