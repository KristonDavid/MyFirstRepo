# Recept Projekt - Telepítési Útmutató

## 1. Előfeltételek

A projekt futtatásához az alábbi szoftverek szükségesek:

- **Node.js + npm** (Angular futtatáshoz)
- **Angular CLI 21.0**
- **PHP 8.4+**
- **Composer**
- **Laravel**
- **MySQL** (javasoljuk: XAMPP)
- **GitHub**

## 2. Projekt letöltése

Klónozd le a repository-t:

```bash
git clone [repository-url]
```

**Mappastruktúra:**
- `backend/` - Laravel backend
- `frontend/` - Angular frontend

## 3. Adatbázis telepítés (MySQL)

1. Indítsd el a MySQL szervert (XAMPP/MySQL)
2. Hozz létre egy új adatbázist (pl. `receptadatbazis`)
3. **Megjegyzés:** A migrációk automatikusan létrehozzák a táblákat, így egyéb teendő nem szükséges

## 4. Backend telepítés (Laravel)

Navigálj a `backend/` mappába, majd kövesd az alábbi lépéseket:

### 4.1 Függőségek telepítése
```bash
composer install
```

### 4.2 Környezeti fájl létrehozása
Másold le a `.env.example` fájlt `.env` néven:
```bash
cp .env.example .env
```

### 4.3 Adatbázis beállítása
Nyisd meg a `.env` fájlt, és töröld a `#` jeleket az alábbi sorok elől:
```env
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=receptadatbazis
DB_USERNAME=root
DB_PASSWORD=
```

### 4.4 Kulcs generálása
```bash
php artisan key:generate
```

### 4.5 Migrációk és seederek futtatása
```bash
php artisan migrate --seed
```

### 4.6 Backend indítása
```bash
php artisan serve
```
A backend alapértelmezetten a `http://127.0.0.1:8000` címen érhető el.

## 5. Frontend telepítés (Angular)

Navigálj a `frontend/` mappába, majd kövesd az alábbi lépéseket:

### 5.1 Függőségek telepítése
```bash
npm install
```

### 5.2 API alap URL ellenőrzése
Ellenőrizd a service-ekben, hogy az API URL helyes-e (pl.):
```typescript
http://127.0.0.1:8000/api/...
```

### 5.3 Frontend indítása
```bash
ng serve -o
```
A frontend alapértelmezetten a `http://localhost:4200` címen érhető el.

## 6. Ellenőrzés / Teszt

### Backend ellenőrzés
Nyisd meg böngészőben: `http://127.0.0.1:8000/api/etel`

### Frontend ellenőrzés
- A recept-tár betölt
- A kártyák kattinthatók
- A detail oldal megnyílik

## 7. Gyakori hibák és megoldásuk

| Probléma | Megoldás |
|----------|----------|
| Adat nem jelenik meg, de a console-ban látszik | Ellenőrizd a JSON struktúrát (tömb vs `{data: ...}`) |
| Adat nem jelenik meg, és console-on sem látszik | Ellenőrizd, hogy megfelelő API végpontok vannak-e a service-ben |
| CORS hiba | Ellenőrizd a Laravel `cors.php` konfigurációt |
| Adatbázis kapcsolódási hiba | Ellenőrizd a `.env` fájlban az adatbázis beállításokat |

## 8. Futtatási sorrend

1. **MySQL indítás** (XAMPP/MySQL szerver)
2. **Laravel backend indítása:** `php artisan serve`
3. **Angular frontend indítása:** `ng serve`

---

## További segítség

Ha bármilyen probléma merül fel, ellenőrizd a log fájlokat:
- Laravel: `backend/storage/logs/laravel.log`
- Angular: Böngésző Developer Console

**Jó munkát!** 🚀
