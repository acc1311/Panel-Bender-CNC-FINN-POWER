```markdown
# 🏭 Calculator CNC Panel Bender

**Fișă de lucru pentru atelier de tablă · Editor secvență îndoire · Calcul cote CNC LSX / LDX**

Aplicație web într-un singur fișier HTML, complet offline, pentru calculul și documentarea
cotelor CNC la îndoirea casetelor pe un panel bender (stil Salvagnini).

![HTML5](https://img.shields.io/badge/HTML5-single--file-E34F26?logo=html5&logoColor=white)
![CSS3](https://img.shields.io/badge/CSS3-inline-1572B6?logo=css3&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-vanilla-F7DF1E?logo=javascript&logoColor=black)
![Dependencies](https://img.shields.io/badge/dependințe-0-2ee6a8)
![Offline](https://img.shields.io/badge/offline-100%25-00d2ff)
![License](https://img.shields.io/badge/licență-MIT-ff6b00)

---

## ⚠️ Avertisment de siguranță

> **Acest calculator NU înlocuiește validarea pe mașină.**
> Cotele generate trebuie verificate obligatoriu prin **dry-run** și prin **măsurarea primei piese**
> înainte de execuția automată. Corecțiile de atelier (`+5`, `+33`, `−16`, `+177`) sunt valori
> empirice, specifice unei mașini și unui tip de piesă — ele se calibrează și se salvează în profil.
> Utilizatorul este responsabil pentru verificarea coliziunilor, a curselor și a configurației de lame.

---

## 📖 Cuprins

- [Despre](#-despre)
- [Instalare rapidă](#-instalare-rapidă)
- [Funcționalități](#-funcționalități)
- [Interfață](#-interfață)
- [Parametri](#-parametri)
- [Inventar master lame](#-inventar-master-lame)
- [Referință formule](#-referință-formule)
- [Editor secvență](#-editor-secvență)
- [Profile de producție](#-profile-de-producție)
- [Afișare și încadrare ecran](#-afișare-și-încadrare-ecran)
- [Export și tipărire](#-export-și-tipărire)
- [Persistența datelor](#-persistența-datelor)
- [Scurtături](#-scurtături)
- [Validări](#-validări)
- [Detalii tehnice](#-detalii-tehnice)
- [Publicare pe GitHub Pages](#-publicare-pe-github-pages)
- [Limitări cunoscute](#-limitări-cunoscute)
- [Contribuții](#-contribuții)
- [Licență](#-licență)

---

## 🎯 Despre

În atelier, poziționarea brațelor unui panel bender se face manual, pe baza unor formule care
depinind de lungimea casetei, decalaj, offsetul de montaj și lungimile pachetelor de lame.
Calculul manual este lent și predispus la erori, iar configurațiile se pierd între serii.

Această aplicație rezolvă trei probleme:

1. **Calcul instant** — cotele LSX și LDX pentru fiecare pas, cu formulele afișate cu valori reale substituite.
2. **Configurare corectă a lamelor** — alocare automată din inventarul real, cu respectarea
   constraint-ului de **unicitate** (o singură bucată din fiecare segment).
3. **Documentare și reutilizare** — profilare pe tip de piesă, jurnal `.TXT` și fișă tipărită A4.

---

## 🚀 Instalare rapidă

Nu necesită build, server, npm sau conexiune la internet.

```bash
git clone https://github.com/<utilizator>/<repo>.git
cd <repo>
```

Apoi **dublu-click pe `index.html`** — se deschide în browser și funcționează complet.

Sau folosește direct versiunea găzduită prin GitHub Pages (vezi [mai jos](#-publicare-pe-github-pages)).

**Cerințe:** un browser modern (Chrome, Edge, Firefox, Safari). Nu necesită instalare.

---

## ✨ Funcționalități

### Calcul și editare
- **Editor de secvență** cu formule editabile inline, recalculare live la fiecare tastă
- **Parser matematic propriu** (fără `eval`) — operatorii `+ − × ÷ ^`, paranteze, unar minus, zecimale cu `.` sau `,`
- **Referințe între pași** — `U1_LSX`, `U2_DX`, `L1_LDX` etc., evaluate în ordinea din tabel
- **Formule substituite** — se afișează valorile numerice reale, colorate pe tip de termen
- **4 șabloane** — Standard Box, K-Tech (negativ sus / pozitiv jos), 1 Lamă SX, 1 Lamă DX
- **Acțiuni pe rând** — mută sus/jos, duplică, marchează rotire 180°, șterge — toate cu **Undo**

### Lame
- **Inventar unic** — o singură bucată din fiecare segment, alocare disjunctă între LSX și LDX
- **Alocare automată echilibrată** — acoperire completă, diferență minimă între pachete, număr minim de segmente
- **Mod manual** cu validare față de inventar (detectează și conflictul de segmente partajate)
- **Vizualizare live** — segmentele alocate sunt evidențiate portocaliu (stânga) / albastru (dreapta)

### Profile
- **Salvare completă** — parametri, opțiuni, lame manuale și întreaga secvență
- **Comutare cu aplicare automată** — la selectarea unui profil se aplică totul și se recalculează
- **Auto-salvare** opțională în profilul activ
- **Bibliotecă** — căutare live, sortare, filtre pe tip, selecție multiplă, drag & drop pentru reordonare
- **Import / Export JSON** — transfer între stații de lucru
- **Undo** după ștergere, duplicare și import

### Documentare
- **Jurnal `.TXT`** structurat, cu BOM UTF-8 (compatibil Notepad), CRLF
- **Tipărire A4 landscape** — fișă alb/negru cu antet, tabel complet, validări și convenții
- **Copiere cotă în clipboard** — click pe orice cotă din tabel

### Vizualizare
- **Schematică SVG animată** — axă 0–2150 mm, centru 1245, pachete pe segmente, zona de cursă blocată
- **Redare secvență** — auto-avans prin pași, sincronizat cu tabelul
- **Sumar live** — pachete, acoperire, cursă utilizată, cu bare de progres

---

## 🖥️ Interfață

Layout pe două zone, optimizat pentru panouri CNC cu ecran mic:

```
┌──────────────────────────────────────────────────────────────┐
│ TOPBAR · profil activ · rezoluție · stare · Jurnal · Tipărește │
├────────┬─────────────────────────────────────────────────────┤
│  DOCK  │  MAIN                                               │
│  48px  │  Banner stare                                       │
│  rail  │  📋 Editor Secvență (toate cele 8 coloane)           │
│   +    │  Sumar (4 carduri)                                  │
│  panou │  Schematică axă                                     │
├────────┴─────────────────────────────────────────────────────┤
```

**Dock compact** — rail vertical de 48px + panou expandabil (~200px). Se restrânge automat
sub 1180px lățime, lăsând tabelului toată lățimea disponibilă. Buton dedicat de extindere/restrângere.

**Taburi** (fără derulare pentru a ajunge la setări):

| Tab | Conținut |
|---|---|
| ⚙ **Parametri** | Parametri piesă & mașină **+ Opțiuni de lucru** |
| 🗄 **Lame** | Inventar master, alocare, statistici |
| 🗂 **Profil** | Comutare, salvare, auto-salvare, bibliotecă |
| 🖥 **Ecran** | Mod afișare, densitate, indicator de încadrare |

**Tabel editor** — `table-layout: fixed`, coloane pe procente, toate vizibile simultan:

`Pas · Etapă/Operație · Configurație lame · Formulă LSX · Cotă LSX · Formulă LDX · Cotă LDX · Acțiuni`

---

## 🔧 Parametri

| Parametru | Implicit | Descriere |
|---|---|---|
| Lungime Casetă `L` | **451.6 mm** | Latura principală a casetei |
| Lungime Urechiușă `Lu` | **110 mm** | Tab-ul scurt (disponibil ca variabilă) |
| Decalaj / Offset | **4 mm** | Depășirea lamelor peste linia de îndoire |
| Offset Montaj Lame | **0 mm** | Corecție de calibrare (acceptă ±50) |
| Lungime Braț Melc | **320 mm** | Disponibil ca variabilă, **nu** se scade automat |
| Centru mașină | **1245 mm** | Fix, necalculabil |
| Cursă liberă axă | **0 – 2150 mm** | Fix |

### Opțiuni de lucru (în tabul Parametri)

| Opțiune | Implicit | Efect |
|---|---|---|
| Activează Offset Interior | **PORNIT** | `OFF = offset` când e pornit, altfel `OFF = 0` |
| Cursă extinsă (2150 mm) | **PORNIT** | Elimină plafonul de 1245 mm pentru cote |
| Setare Manuală Lame | OPRIT | Înlocuiește alocarea automată; apar input-uri LSX / LDX |

---

## 🗄️ Inventar master lame

Segmente disponibile (**o singură bucată din fiecare**):

```
400 · 345 · 200 · 160 · 85 · 80 · 69 · 55 · 42 · 35   [mm]
TOTAL = 1471 mm
```

### Regula de unicitate

Fiecare segment poate fi alocat **o singură dată** — nici în interiorul aceluiași pachet,
nici între pachetul LSX și pachetul LDX. Alocarea este **disjunctă**.

### Algoritm automat

```
Necesar:  T = L + 2 × OFF
Condiție: PL + PR ≥ T
Scor:     12 × depășire + 6 × |PL − PR| + 8 × număr_segmente
```

Se enumeră toate submulțimile (2¹⁰ = 1024) și perechile disjuncte (3¹⁰ ≈ 59 049), cu
constrângeri de cursă pe fiecare braț. Dacă nimic nu e fezabil, se returnează cea mai
apropiată soluție sub necesar, însoțită de eroare explicită.

**Exemplu implicit** (`L = 451.6`, `OFF = 4` → `T = 459.6`):

```
PL = 229 = 160 + 69
PR = 235 = 200 + 35
Total = 464 mm  (+4.4 mm)   Δ echilibru = 6 mm
```

### Mod manual

Valorile introduse sunt validate față de inventar: trebuie să existe două submulțimi
**disjuncte** cu sumele exacte. Erorile sunt distincte:

- „LSX nu poate fi compus din inventar"
- „LDX nu poate fi compus din inventar"
- „ar necesita aceleași segmente în ambele pachete"

---

## 📐 Referință formule

### Variabile disponibile

| Variabilă | Semnificație |
|---|---|
| `C` | 1245 — centrul mașinii (fix) |
| `L` | Lungimea casetei |
| `Lu` | Lungimea urechiușei |
| `OFF` | Decalaj activ (0 dacă Offset Interior e oprit) |
| `MOUNT` | Offset montaj lame |
| `ARM` | Lungime braț melc (nu se scade automat) |
| `PL` | Lungime pachet LSX |
| `PR` | Lungime pachet LDX |

### Referințe între pași

`<CHEIE>_LSX` · `<CHEIE>_LDX` · aliasuri `<CHEIE>_SX` · `<CHEIE>_DX`

Exemple: `U1_LSX`, `U2_DX`, `L1_LDX`. Se evaluează în ordinea din tabel.
Referința la un pas ulterior, la un braț liber sau la un pas cu eroare produce mesaj specific.

### Șablon Standard Box

| Pas | Operație | Formulă LSX | Formulă LDX |
|---|---|---|---|
| **1** | Urechiușă 1 (U1) | `C - L/2 - OFF - MOUNT` | *liber* |
| **2** | Latură 1 (L1) | `U1_LSX + PL + 5` | `U1_LSX + 33` |
| **3** | Rotire 180° ➔ Urechiușă 2 (U2) | *liber* | `U1_LSX - 16` |
| **4** | Latură 2 (L2) | `U2_DX + 177` | `U2_DX + PR` |

> **Ancora:** `U1_LSX = 1245 − L/2 − OFF − MOUNT`
> Brațul melc **nu** se scade din cotă. Câmp gol = braț liber / poziție de așteptare.

#### Verificare — referința de atelier

```
L = 620 · OFF = 2.4 · MOUNT = 2.2 · PL = 309 (160+80+69) · PR = 255 (200+55)

U1_LSX = 1245 - 310 - 2.4 - 2.2  =  930.4 mm
L1_LSX = 930.4 + 309 + 5         = 1244.4 mm
L1_LDX = 930.4 + 33              =  963.4 mm
U2_LDX = 930.4 - 16              =  914.4 mm
L2_LSX = 914.4 + 177             = 1091.4 mm
L2_LDX = 914.4 + 255             = 1169.4 mm
```

#### Verificare — valorile implicite

```
L = 451.6 · OFF = 4 · MOUNT = 0 · PL = 229 · PR = 235

U1_LSX = 1015.2 mm
L1_LSX = 1249.2 mm   ← necesită Cursă extinsă PORNITĂ (> 1245)
L1_LDX = 1048.2 mm
U2_LDX =  999.2 mm
L2_LSX = 1176.2 mm
L2_LDX = 1234.2 mm
```

### Șablon K-Tech

| Pas | Operație | LSX | LDX |
|---|---|---|---|
| 1 | Latură negativă — SUS | `C - L/2 + OFF - MOUNT` | `C + L/2 - OFF + MOUNT` |
| 2 | Rotire 180° — retragere | *liber* | *liber* |
| 3 | Latură pozitivă — JOS | `C - L/2 - OFF - MOUNT` | `C + L/2 + OFF + MOUNT` |

La îndoirea negativă offsetul se aplică **inversat**, spre interiorul piesei.

### Șabloane 1 Lamă

- **SX** — toate îndoirile pe `LSX = C - L/2 - OFF - MOUNT`, LDX liber pe tot ciclul
- **DX** — oglindit, `LDX = C + L/2 + OFF + MOUNT`, LSX liber

---

## 📋 Editor secvență

### Bară de instrumente

`➕ Pas` · `🔄 Standard` · `Șabloane…` · `🗑 Golește` · `💾 Jurnal` · `🖨️ Tipărește`

### Pe fiecare rând

- **Nume operație** editabil inline
- **Formulă LSX** și **Formulă LDX** editabile, cu afișaj substituit dedesubt
- **Cotă CNC** — click pentru copiere în clipboard
- **Configurație lame** — pachetele active pe pas
- **Acțiuni** — `⬆` `⬇` `⧉` `⟳` `✕`

### Panou variabile

Chips-uri cu valorile curente ale tuturor variabilelor și referințelor. Click = inserare
la poziția cursorului în ultima formulă focalizată. Click pe un chip de referință = salt la pasul sursă.

### Undo

Orice acțiune distructivă (ștergere pas, golire secvență, aplicare șablon, mutare, duplicare)
afișează un toast cu buton **Anulează**.

---

## 🗂️ Profile de producție

Un profil salvează **tot**: parametri, opțiuni, lame manuale și întreaga secvență de pași.

### Comutare

Selectarea unui profil din dropdown aplică automat toate setările și recalculează instant,
cu flash vizual de confirmare.

### Auto-salvare

Switch opțional — modificările se scriu în profilul activ după ~700 ms de inactivitate,
cu afișarea orei ultimei salvări. Indicator `● modificat` / `✓ salvat` în tabul Profil.

### Bibliotecă (drawer)

- **Căutare live** după nume, tag-uri și notițe
- **Sortare** — ordine manuală, recente, nume, dimensiune L
- **Filtre** — Toate / Box / K-Tech / 1 Lamă / Custom
- **Selecție multiplă** + bară bulk (exportă / șterge / deselectează)
- **Drag & drop** pentru reordonare (ordinea se persistă)
- **Panou de detaliu** — redenumire, tip, tag-uri, notițe, grilă parametri, previzualizare pași
- **Import / Export JSON** — complet, pe selecție sau individual
- **Undo** după ștergere, duplicare și import

### Profile incluse la prima rulare

| Profil | Configurație |
|---|---|
| Casetă 451.6×110 · OFF 4 | Standard, alocare automată |
| Casetă 620×120 · Referință atelier | Manual, LSX 309 / LDX 255 |
| K-Tech 451.6 | Negativ sus + pozitiv jos |
| Urechiușe 380×90 · SX | O lamă, braț opus retras |
| Casetă 800×150 · Extins | Piesă lungă, cursă extinsă |

---

## 🖥️ Afișare și încadrare ecran

### Mod „Fit HMI rapid" (implicit)

- Redare **nativă 1:1** — aplicația umple viewport-ul, fără `transform: scale` pe DOM
- Fără letterbox, fără `backdrop-filter`, animații reduse — randare rapidă pe panouri industriale
- Dock și zona principală derulează **independent**, cu scrollbar-uri în paleta proprie
- Dock auto-restrâns la 48px sub 1180px, pentru ca tabelul să aibă toată lățimea

### Mod „Fluid responsive"

Layout clasic, cu derulare pe pagină și breakpoint-uri.

### Densitate

`Auto` / `Compact` / `Normal` — `Auto` alege `Compact` când înălțimea < 860 px sau lățimea < 1180 px.

### Rezoluții țintă

`840×795` · `1024×768` · `1280×1024` · `1366×768` · `1920×1080`

Indicator live de încadrare, măsurat real: lățimea tabelului vs. spațiul disponibil și starea dock-ului.

---

## 💾 Export și tipărire

### Jurnal `.TXT`

Fișier text structurat, cu **BOM UTF-8** (diacritice corecte în Notepad) și **CRLF**:

```
======================================================================
FIȘĂ DE LUCRU — PANEL BENDER CNC
Generat: <dată, oră>
Profil: <nume profil activ>
======================================================================

PARAMETRI
  L, Lu, OFF, MOUNT, ARM, Centru, Cursă

LAME & INVENTAR UNIC
  Inventar, pachete LSX / LDX, acoperire, segmente nefolosite

SECVENȚĂ DE ÎNDOIRE
  [PAS n] cheie · nume operație
    LSX raw / substituit / cotă
    LDX raw / substituit / cotă

VALIDĂRI
CONVENȚII DE CALC
======================================================================
```

Nume fișier: `Fisa_CNC_<YYYYMMDD>_<HHMM>.txt`

### Tipărire

`@media print` — **A4 landscape**, alb/negru, cu:

- antet (dată, profil, parametri, pachete, stare)
- tabel complet cu formule substituite (input-urile ascunse)
- coloana Acțiuni ascunsă
- sumar, validări, convenții de calcul, subsol
- fără întreruperi de pagină în interiorul rândurilor

---

## 🗃️ Persistența datelor

Totul se salvează în `localStorage`, separat pe categorii:

| Categorie | Conținut |
|---|---|
| Stare curentă | Parametri, opțiuni, lame, secvență, profil activ |
| Bibliotecă profile | Toate profilurile salvate |
| Vizualizare listă | Căutare, sortare, filtru |
| Afișare | Mod (fit/fluid), densitate |
| Dock | Stare restrâns/extins, tab activ |

Datele **nu părăsesc stația de lucru**. Pentru transfer între stații se folosește Export / Import JSON.

> Ștergerea datelor browserului (Clear site data) șterge și profilurile.
> Folosește **Export JSON** ca backup.

---

## ⌨️ Scurtături

| Combinație | Acțiune |
|---|---|
| `Ctrl` / `Cmd` + `S` | Actualizează profilul activ, sau salvează profil nou |
| `Ctrl` / `Cmd` + `O` | Deschide biblioteca de profile |
| `Esc` | Închide drawer-ul |
| `←` / `→` | Parcurgere pași (cu focus pe schematică) |
| Click pe cotă | Copiere în clipboard |
| Click pe rând | Selectare pas + sincronizare schematică |
| Apăsare lungă `−` / `+` | Repetare stepper |

---

## ✅ Validări

| Tip | Verificare |
|---|---|
| **Eroare** | Cotă negativă (sania iese din cursă) |
| **Eroare** | Cotă peste cursa activă (1245 / 2150) — cu sugestie de activare a extensiei |
| **Eroare** | Sintaxă de formulă, variabilă necunoscută, împărțire la zero |
| **Eroare** | Referință la pas ulterior, braț liber sau pas cu eroare |
| **Eroare** | Lame manuale ≤ 0 sau necompunibile din inventarul unic |
| **Eroare** | Conflict de segmente între pachete în modul manual |
| **Avertizare** | Acoperire pachete sub necesar, cu deficitul în mm |
| **Avertizare** | `Lu > L`, offset neobișnuit de mare, braț invalid |

Starea este afișată în banner-ul global, în LED-ul din topbar (`VALID` / `ATENȚIE` / `EROARE`)
și inline pe fiecare rând.

---

## 🛠️ Detalii tehnice

- **Un singur fișier** — CSS în `<style>`, JS în `<script>`, zero dependințe
- **Fără `eval()`** — parser matematic propriu: tokenizer + descent recursiv
  (`expr → term → unary → power → primary`)
- **Fără CDN** — fonturi din stack-uri de sistem, logo SVG inline, favicon data-URI
- **Funcționează de pe `file://`** — inclusiv `localStorage`, download Blob, clipboard cu fallback
- **Randare eficientă** — recalculare cu debounce (~70 ms), fără pierderea focusului la tastare;
  o singură buclă `rAF` pentru animația schematicii, anulată corect la schimbare
- **Accesibilitate** — `role="tablist"` / `role="tabpanel"`, `aria-live` pentru validări,
  `aria-selected`, focus vizibil, `prefers-reduced-motion` respectat
- **Teme** — paletă industrială derivată din subject: portocaliu = braț stânga,
  albastru = braț dreapta, semantic verde / amber / roșu

---

## 🌐 Publicare pe GitHub Pages

1. Creează un repository și încarcă `index.html` și `README.md` în rădăcină.
2. Mergi la **Settings → Pages**.
3. La **Source** alege **Deploy from a branch**.
4. Selectează branch-ul `main` și folderul `/ (root)`, apoi **Save**.
5. După câteva minute aplicația este disponibilă la:

```
https://<utilizator>.github.io/<repo>/
```

### Structură recomandată

```
.
├── index.html      # aplicația completă
├── README.md       # acest fișier
└── LICENSE         # opțional
```

Nu este necesar build, `package.json` sau workflow de CI.

---

## 🚧 Limitări cunoscute

- **Nu comunică cu mașina CNC** — nu generează G-code și nu trimite cote către controller.
  Este un instrument de calcul și documentare pentru operator.
- **Nu înlocuiește software-ul CAM** al mașinii și nu validează coliziunile tridimensionale.
- **Corecțiile empirice** (`+5`, `+33`, `−16`, `+177`) provin dintr-un atelier specific.
  Pentru altă mașină sau alt tip de piesă ele trebuie recalibrate și salvate într-un profil separat.
- **Modelul de cursă** verifică valoarea cotei pe axă, nu geometria reală a sculei sau a piesei.
- **Backup-ul profilelor** este manual (Export JSON); nu există sincronizare în cloud.

---

## 🤝 Contribuții

Contribuțiile sunt binevenite, în special pentru:

- adaptarea formulelor la alte modele de panel bender
- șabloane suplimentare de secvență
- validări geometrice mai stricte
- traduceri ale interfeței

Deschide un **Issue** pentru propuneri sau un **Pull Request** cu modificările.
Păstrează constrângerea de **fișier unic, fără dependințe**.

---

## 📄 Licență

Distribuit sub licența **MIT**. Vezi fișierul `LICENSE` pentru detalii.

---

<div align="center">

**Verificați întotdeauna cotele înainte de execuția programului.**

Centru mașină 1245 mm · Cursă axă 0–2150 mm · Inventar unic 1471 mm

</div>
```
