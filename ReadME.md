# FootballTeam API

REST API per la gestione di una squadra di calcio, con autenticazione JWT e deploy containerizzato.

## Stack tecnologico

- **Java 21**
- **Spring Boot 3.5.3** — Web, Data JPA, Security, Validation
- **MySQL 8.0**
- **JWT** (jjwt 0.11.5)
- **Docker + Docker Compose**
- **Maven**

## Prerequisiti

- Docker e Docker Compose installati
- (Opzionale) IntelliJ IDEA o Maven per avviare in locale senza Docker

---

## Avvio con Docker

```bash
docker compose up -d
```

Questo comando avvia due container:
- **`app`** — applicazione Spring Boot sulla porta `8080`
- **`db`** — MySQL 8.0 sulla porta `3306`, con database `football_team_db` inizializzato automaticamente tramite `init_db.sql`

Per fermare i container:

```bash
docker compose down
```

---

## Avvio senza Docker (locale)

1. Compilare e creare il JAR:

```bash
mvn clean install -Dmaven.test.skip=true
```

2. Assicurarsi di avere un'istanza MySQL attiva con le credenziali configurate in `src/main/resources/application.properties`.

3. Eseguire il JAR:

```bash
java -jar target/footballTeam-0.0.1-SNAPSHOT.jar
```

---

## Database

Le credenziali del database sono disponibili in `docker-compose.yml`.

In alternativa al populate automatico via Docker, usare il file **`init_db.sql`** presente nella root del progetto per inizializzare manualmente lo schema.

---

## Autenticazione

L'API usa **JWT Bearer Token**.

1. Registrarsi o effettuare il login tramite gli endpoint `/auth`
2. Copiare il token JWT restituito nella risposta
3. Inserirlo in ogni richiesta successiva su Postman: `Authorization > Bearer Token`

---

## Endpoint principali

| Risorsa   | Base path    |
|-----------|--------------|
| Auth      | `/auth`      |
| Utenti    | `/users`     |
| Giocatori | `/players`   |
| Squadre   | `/teams`     |
| Contratti | `/contracts` |
| Leghe     | `/leagues`   |

---

## Postman

La collection esportata si trova nella root del progetto: `Football_Team.postman_collection.json`.

Importarla direttamente in Postman trascinando il file nell'app desktop.

> Ricordare di aggiornare gli ID nell'URL per le richieste su risorse specifiche (es. associazione player/squadra) e di inserire correttamente `posizione` e `nazionalita` nei payload dei giocatori.

---

## Struttura del progetto

```
src/main/java/com/FootballTeam/footballTeam/
├── controller/     # Controller REST
├── dto/            # Request e Response DTO
├── model/          # Entità JPA
├── repository/     # Repository Spring Data
├── security/       # JWT filter, provider, configurazione Spring Security
└── service/        # Business logic e interfacce
```
