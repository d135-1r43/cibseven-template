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

## Starten

### 1. Keycloak starten

Keycloak wird über Docker Compose gestartet und ist vorkonfiguriert (Realm, Client, Benutzer werden automatisch importiert):

```bash
docker compose up -d
```

Keycloak ist anschließend unter `http://localhost:8180` erreichbar.
Admin-Zugang: `admin` / `admin`

### 2. Anwendung bauen und starten

```bash
mvn clean package -DskipTests
mvn spring-boot:run
```

Die Anwendung ist unter `http://localhost:8080` erreichbar.

### Einloggen

Nach dem Öffnen von `http://localhost:8080` wird automatisch zu Keycloak weitergeleitet. Login mit:

- **Benutzername:** `demo`
- **Passwort:** `demo`

Der Benutzer `demo` ist Mitglied der Gruppe `camunda-admin` und hat vollen Zugriff auf die Anwendung.
