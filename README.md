# Kontra Slice – Figma to WordPress starter

Kontra Slice je **frontend starter** za pretvaranje Figma dizajna u čisti, modularni **HTML / SCSS / JavaScript** koji se kasnije jednostavno integrira u **WordPress temu**.

Projekt koristi **Webpack 5**, **SCSS**, **Bootstrap 5** i **PurgeCSS** kako bi generirao optimizirani produkcijski build (HTML, minificirani CSS, JS, slike i fontove) spreman za WordPress.

---

## ✨ Značajke

* Strukturirani `src` folder prilagođen za *sliceanje* Figma dizajna u sekcije, layout i komponente
* Modularna SCSS arhitektura (`base`, `layout`, `components`, `bootstrap`)
* Bootstrap 5 integriran kroz SCSS (moguće uključiti samo potrebne module)
* PurgeCSS u produkcijskom buildu za uklanjanje neiskorištenog CSS-a (Bootstrap-safe)
* Webpack Dev Server s **live reload / HMR**
* Čist output za WordPress:

  * `css/style.css`
  * `js/main.js`
  * `assets/images`, `assets/fonts`

---

## 📁 Struktura projekta

```bash
/project-root
│
├─ /src
│   ├─ /js
│   │   └─ main.js              # Glavni JS entry (učitava SCSS + Bootstrap JS)
│   │
│   ├─ /styles
│   │   ├─ main.scss            # Glavni SCSS entry
│   │   ├─ /base                # Varijable, mixini, reseti
│   │   ├─ /layout              # Globalni layout (header, footer, offcanvas…)
│   │   ├─ /components          # UI komponente (gumbi, kartice, modali…)
│   │   └─ /bootstrap           # Bootstrap importi i override varijable
│   │
│   └─ index.html               # Ulazni HTML (Figma slice markup)
│
├─ /dist                        # Build output (NE DIRATI ručno)
│   ├─ css/style.css
│   ├─ js/main.js
│   └─ assets/…
│
├─ package.json
└─ webpack.config.js
```

> Ovakva struktura olakšava kasnije mapiranje na WordPress temu (`header.php`, `footer.php`, `template-parts`, `style.css`).

---

## ⚙️ Preduvjeti

* **Node.js** (preporučeno zadnja LTS verzija)
* **npm** ili **yarn**
* **Git** (ako kloniraš repozitorij)

---

## 🚀 Instalacija

### 1️⃣ Kloniranje repozitorija

```bash
git clone https://github.com/tomi9186/kontra-slice.git
cd kontra-slice
```

### 2️⃣ Instalacija dependencija

```bash
npm install
```

---

## 📜 NPM skripte

U `package.json` definirane su sljedeće skripte:

```json
"scripts": {
  "dev": "cross-env NODE_ENV=development webpack serve",
  "build": "cross-env NODE_ENV=production webpack"
}
```

| Skripta         | Opis                                                        |
| --------------- | ----------------------------------------------------------- |
| `npm run dev`   | Pokreće development server s HMR-om                         |
| `npm run build` | Generira produkcijski build (minificiran CSS/JS + PurgeCSS) |

---

## 🧑‍💻 Development workflow

### Pokretanje projekta

```bash
npm run dev
```

Ako se browser ne otvori automatski, ručno otvori:

```
http://localhost:8080
```

### U development modu radiš sljedeće:

* Uređuješ HTML u `src/index.html`
* Pišeš stilove u odgovarajućim SCSS modulima:

  * `styles/base`
  * `styles/layout`
  * `styles/components`
  * `styles/bootstrap`
* Dodaješ JavaScript u `src/js/main.js` ili dodatne module

➡️ Dev server automatski rebuilda bundle i osvježava stranicu

---

## 📦 Produkcijski build

Za generiranje optimiziranog paketa:

```bash
npm run build
```

Build proces će:

* Očistiti `dist/` folder
* Generirati `dist/css/style.css` (minificiran + PurgeCSS)
* Generirati `dist/js/main.js` (minificiran)
* Kopirati assete u `dist/assets/`

---

## 🧩 Tipična WordPress integracija

1. `dist/index.html` razbiti u WP templateove:

   * `header.php`
   * `index.php`
   * `footer.php`

2. `dist/css/style.css` kopirati ili preimenovati u `style.css` u root teme

3. `dist/js/main.js` uključiti pomoću `wp_enqueue_script`

4. `dist/assets/` kopirati u temu i prilagoditi putanje

---

## 🎨 Korištenje za novi Figma slice

### 1️⃣ Dupliciraj projekt

* Kloniraj repo u novi folder za svaki novi dizajn
* Ili napravi vlastiti starter repo baziran na ovom projektu

### 2️⃣ Ubaci HTML iz Figma dizajna

* Prekopiraj markup u `src/index.html`
* Po potrebi razbij na sekcije (hero, features, footer…)

### 3️⃣ Organiziraj SCSS

* **Globalno**: `styles/base/variables.scss`
* **Layout**: `styles/layout/*.scss`
* **Komponente**: `styles/components/*.scss`
* **Bootstrap override**: `styles/bootstrap/bootstrap-overrides.scss`

### 4️⃣ Bootstrap & PurgeCSS safe usage

* Bootstrap klase koristi normalno (`container`, `row`, `btn`, `modal`, `offcanvas`…)
* Dinamičke klase (JS / WordPress) **moraš dodati u safelist** u `webpack.config.js`

### 5️⃣ JavaScript

* Bootstrap interakcije su dostupne (bundle uključuje JS)
* Vlastitu logiku piši u `main.js` ili modularno kroz importe

---

## ⚠️ Napomene

* **PurgeCSS je aktivan samo u produkciji** (`npm run build`)
* Ako u produkciji nestanu stilovi:

  * Dodaj klase u `safelist` u `webpack.config.js`
* Projekt je zamišljen kao **frontend most između Figma dizajna i WordPress teme**

  * HTML / CSS / JS ovdje
  * PHP i templating kasnije u WordPressu

---

✅ Ovaj README je namijenjen internom timu kako bi svi imali jasan i ujednačen workflow pri sliceanju Figma dizajna i integraciji u WordPress.
