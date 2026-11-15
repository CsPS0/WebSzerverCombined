# NJSZKI — WebSzerverCombined

[![Vite](https://img.shields.io/badge/Vite-5-646CFF?style=for-the-badge&logo=vite&logoColor=white)](https://vitejs.dev/)
[![JSON-Server](https://img.shields.io/badge/JSON--Server-Mock_API-blue?style=for-the-badge)](https://github.com/typicode/json-server)
[![Node.js](https://img.shields.io/badge/Node.js-18+-green?style=for-the-badge&logo=node.js&logoColor=white)](https://nodejs.org/)
[![Docker](https://img.shields.io/badge/Docker-Compose-2496ED?style=for-the-badge&logo=docker&logoColor=white)](https://www.docker.com/)
[![License: MIT](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)](LICENSE)

Integrált, full-stack helyi fejlesztői környezet és proxy sablon, amely egyesíti a modern **Vite (Frontend)** és a moduláris **JSON-Server (Backend)** képességeit iskolai és gyakorlati feladatok egyszerű megoldásához.

> **Eredeti kód & inspiráció:** Az alap struktúra és kódok **[@ignaczdominik](https://github.com/ignaczdominik)** munkájára épülnek.

---

## Főbb Jellemzők

- **Egyesített Indítás:** A `pnpm dev` futtatásával egyszerre indul el a Vite Hot Module Replacement (HMR) szervere és a JSON-Server REST API, így nem szükséges külön terminálokat menedzselni.
- **Automatikus Reverse Proxy:** A frontend felől érkező `/api/...` hálózati kéréseket a Vite belső proxyja transzparensen továbbítja a backendre (`localhost:3000`), elkerülve a CORS (Cross-Origin Resource Sharing) problémákat.
- **Relációs Adatkezelés:** A szerver logikájából leválasztott `relationships.js` modul lehetővé teszi összetett mock adatkapcsolatok (foreign key, relációk) kezelését.
- **Többféle Futtatási Mód:**
  * Szabványos helyi Node.js fejlesztés
  * Konténerizált futtatás `docker-compose`-zal
  * Beépített PHP webszerver mód (`php -S`), amennyiben a feladat PHP környezetet követel meg.

---

## Hálózati Port-kiosztás

| Szolgáltatás | Belső Cím / Port | Megjegyzés |
|:---|:---|:---|
| **Frontend (Vite Dev)** | `http://localhost:8080` | Fejlesztői felület gyors újrafordítással (HMR) |
| **Backend (JSON-Server)** | `http://localhost:3000` | REST API végpontok és adatbázis |
| **Belső API Proxy** | `http://localhost:8080/api` | CORS-mentes belső útvonal a frontendből |
| **PHP Webszerver Mód** | `http://localhost:8000` | Statikus/PHP teszteléshez (`pnpm php`) |

---

## Telepítés és Indítás

### 1. Függőségek telepítése
```bash
pnpm install
# vagy npm esetén:
npm install
```

### 2. Fejlesztői mód (Ajánlott)
Egyszerre elindítja a frontendet és a backend REST szervert egyetlen terminálban:
```bash
pnpm dev
```
Nyisd meg a böngészőben: **`http://localhost:8080`**

### 3. Docker konténerben történő futtatás
Teljes elszigetelt környezet indítása Docker Compose segítségével:
```bash
docker-compose up --build
```
A szolgáltatás elérhető: `http://localhost:3000`

### 4. PHP kompatibilitási mód
Ha az adott feladat statikus kiszolgálást vagy natív PHP webszervert kér:
```bash
pnpm php
```
Ez a parancs lefordítja a frontendet a `dist` mappába, elindítja a PHP beépített szerverét (`localhost:8000`), miközben a háttérben futtatja a Node.js REST API-t is.

---

## Mappastruktúra

```
├── data/
│   └── db.json            # A JSON-Server adatbázisa
├── public/                # Statikus webes eszközök (képek, ikonok)
├── src/                   # A frontend alkalmazás forráskódja
├── Dockerfile             # Docker konténer definíció
├── docker-compose.yml     # Többkonténeres futtatási konfiguráció
├── relationships.js       # Relációs mock adatkapcsolatok logikája
├── server.js              # A backend API szerver belépési pontja
└── vite.config.js         # Vite konfiguráció és beépített /api reverse proxy
```

---

## Licenc és Köszönetnyilvánítás

- **Eredeti kód:** [@ignaczdominik](https://github.com/ignaczdominik)
- **Karbantartó:** [Solti Csongor Péter](https://github.com/CsPS0)
- **Licenc:** [MIT Licenc](./LICENSE)