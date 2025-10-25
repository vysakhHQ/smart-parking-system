# Smart Parking System (Java Swing + MySQL)

Full-stack desktop application with Swing UI, JDBC (HikariCP) MySQL backend, real-time spot statuses, reservations, and basic admin panel.

## Prerequisites (Windows)
- Java Development Kit (JDK) 23 installed
  - Verify: `java -version`
- Apache Maven installed and on PATH
  - Verify: `mvn -version`
- MySQL Server running locally (8.x recommended)
  - Note your MySQL username and password (default often `root`/`<your password>`)

## 1) Database Setup
1. Open MySQL client (MySQL Workbench or `mysql` CLI).
2. Execute schema then seed:
   - In Workbench: open and run:
     - `src/main/resources/db/schema.sql`
     - `src/main/resources/db/sample_data.sql`
   - Or CLI (adjust path and password):
     ```bash
     mysql -u root -p < "src/main/resources/db/schema.sql"
     mysql -u root -p < "src/main/resources/db/sample_data.sql"
     ```

## 2) Configure Application Properties
Edit `src/main/resources/application.properties`:
```
# JDBC URL to your MySQL
db.url=jdbc:mysql://localhost:3306/smart_parking_db?useSSL=false&serverTimezone=UTC
# Credentials
db.username=root
db.password=YOUR_PASSWORD

# Pool tuning (optional)
db.pool.maximumPoolSize=10
```

## 3) Build & Run
From the project root (`smart-parking-system`):
```bash
mvn -DskipTests package
mvn -DskipTests exec:java -Dexec.mainClass=com.smartparking.App
```
This launches the Swing UI. Log in using sample accounts:
- Student: `diksha_23` / `pass123`
- Faculty: `arjun_m` / `pass789`
- Admin: `admin` / `admin123`

## 4) VS Code Tips
- Open folder `smart-parking-system` in VS Code.
- Ensure Java and Maven extensions installed.
- In `App.java`, click "Run" (Java extension) to start the app.

## Features Implemented
- Login with roles (Student/Faculty/Staff/Admin; admin has panel entry)
- Interactive map with color-coded spots: Available (Green), Occupied (Red), Reserved (Yellow), Maintenance (Gray)
- Click to select spot; reserve with start/end time
- Periodic refresh for spot statuses

## Troubleshooting
- `mvn not recognized`: Install Maven and restart terminal. Add Maven `bin` to PATH.
- `Cannot connect to MySQL`: Check `db.url`, `db.username`, `db.password`; ensure MySQL service is running.
- `Access denied for user`: Confirm credentials and privileges for `smart_parking_db`.
- `Timezone or SSL warnings`: Keep `serverTimezone=UTC` and `useSSL=false` (or configure SSL properly).

## Notes
- Passwords are stored in plain text per sample; for production, hash them (e.g., BCrypt).
- Real-time updates simulated via periodic refresh; extend with DB triggers or messaging if needed.
- Admin panel is a stub placeholder.

