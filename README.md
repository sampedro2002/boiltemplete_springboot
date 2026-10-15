# boiltemplete_springboot

Boilerplate full‑stack: **Spring Boot** (API REST) + **React/Vite** (frontend).

```
boiltemplete_springboot/
  backend/    Spring Boot 3 · Java 21 · Maven
  frontend/   React 19 · Vite · TypeScript · Tailwind 4
```

## Stack

**Backend:** Spring Web, Spring Data JPA, Validation, Spring Security, Lombok, DevTools, H2 (en memoria).

**Frontend:** React Router, Zustand, React Hook Form + Zod + `@hookform/resolvers`, Axios, Tailwind CSS (`@tailwindcss/vite`), ESLint + Prettier (`eslint-config-prettier`).

## Instalar requisitos

### Node.js + npm (npm viene incluido con Node)

**Windows 10 / 11**

```powershell
# Opción A: winget (Win 11 y Win 10 reciente; si no existe, usa la opción B)
winget install OpenJS.NodeJS.LTS

# Opción B: instalador .msi LTS desde https://nodejs.org (marca "Add to PATH")
```

**Linux (recomendado: nvm, no requiere sudo)**

```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.3/install.sh | bash
# cierra y abre la terminal, luego:
nvm install --lts
```

En Debian/Ubuntu evita `apt install nodejs npm` (trae versiones viejas).

Verifica en cualquier sistema (abre una terminal nueva):

```bash
node -v   # v22 o superior
npm -v
```

### JDK 21 (solo backend Spring Boot)

**Windows 10 / 11**

```powershell
winget install EclipseAdoptium.Temurin.21.JDK
# o descarga el instalador desde https://adoptium.net
```

**Linux**

```bash
# Debian / Ubuntu
sudo apt update && sudo apt install -y openjdk-21-jdk
# Fedora
sudo dnf install -y java-21-openjdk-devel
# o con SDKMAN (cualquier distro): curl -s "https://get.sdkman.io" | bash && sdk install java 21-tem
```

Verifica: `java -version` (debe decir 21). No necesitas instalar Maven: el proyecto trae `mvnw`.

## Plataformas soportadas

Windows 10, Windows 11 y Linux (también macOS). Requisitos: JDK 21 y Node.js 22+.

| Acción         | Linux / macOS / Git Bash   | Windows PowerShell                  | Windows cmd                         |
| -------------- | -------------------------- | ----------------------------------- | ----------------------------------- |
| Copiar .env    | `cp .env.example .env`     | `Copy-Item .env.example .env`       | `copy .env.example .env`            |
| Ejecutar API   | `./mvnw spring-boot:run`   | `.\mvnw.cmd spring-boot:run`       | `mvnw.cmd spring-boot:run`          |

- En Linux, si `mvnw` no es ejecutable: `chmod +x backend/mvnw`.
- Los finales de línea están forzados a LF (`.gitattributes`, `.editorconfig`, Prettier), salvo `.cmd`/`.bat` que usan CRLF.
- Los comandos `npm ...` son idénticos en todas las plataformas.

## Backend

```bash
cd backend
./mvnw spring-boot:run     # Windows: .\mvnw.cmd spring-boot:run  (http://localhost:8080)
```

- Health check: `GET http://localhost:8080/api/health`
- Consola H2: `http://localhost:8080/h2-console` (JDBC URL `jdbc:h2:mem:appdb`, user `sa`)
- Configuración en `backend/src/main/resources/application.properties`
- CORS permite `http://localhost:5173` (`app.cors.allowed-origins`)
- `SecurityConfig` deja `/api/**` abierto como punto de partida; ajusta la autenticación a tu caso.

## Frontend

```bash
cd frontend
npm install
cp .env.example .env       # VITE_API_URL=http://localhost:8080/api
npm run dev                # http://localhost:5173
```

Instalación manual de librerías (referencia):

```bash
npm install axios react-router-dom zustand react-hook-form zod @hookform/resolvers tailwindcss @tailwindcss/vite
npm install -D prettier eslint-config-prettier
```

## Estructura del frontend

```
src/
  api/ components/ hooks/ pages/ routes/ schemas/ store/
```

## Siguientes pasos

- Cambiar H2 por PostgreSQL/MySQL y añadir su driver al `pom.xml`.
- Renombrar `com.example.backend` y el `artifactId` según tu proyecto.
- Implementar autenticación (JWT o sesión) en `SecurityConfig`.
