# 🏭 Calculator CNC Panel Bender
https://acc1311.github.io/Panel-Bender-CNC-FINN-POWER/
**Fișă de lucru pentru atelier de tablă · Editor secvență îndoire · Calcul cote CNC LSX / LDX**

Aplicație web completă, într-un singur fișier `index.html`, care rulează 100% offline, fără server, fără build și fără dependințe externe.

![HTML5](https://img.shields.io/badge/HTML5-single--file-E34F26?logo=html5&logoColor=white)
![CSS3](https://img.shields.io/badge/CSS3-inline-1572B6?logo=css3&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-vanilla-F7DF1E?logo=javascript&logoColor=black)
![Dependencies](https://img.shields.io/badge/dependințe-0-2ee6a8)
![Offline](https://img.shields.io/badge/offline-100%25-00d2ff)
![License](https://img.shields.io/badge/licență-MIT-ff6b00)

---

## ⚠️ Avertisment de siguranță

> **Acest calculator NU înlocuiește validarea pe mașină.**
>
> Cotele generate trebuie verificate obligatoriu prin:
> - **dry-run** pe mașina CNC
> - **măsurarea primei piese**
> - verificarea coliziunilor și a configurației reale de lame
>
> Valorile de corecție `+5`, `+33`, `−16`, `+177` sunt **empirice**, provin dintr-un atelier specific și trebuie recalibrate pentru fiecare mașină / tip de piesă.
>
> Utilizatorul este responsabil pentru verificarea finală a cotelor înainte de execuție.

---

## 📖 Cuprins

1. [Ce este aplicația](#1-ce-este-aplicația)
2. [Ce NU face aplicația](#2-ce-nu-face-aplicația)
3. [Instalare și rulare](#3-instalare-și-rulare)
4. [Structura repository-ului](#4-structura-repository-ului)
5. [Funcționalități complete](#5-funcționalități-complete)
6. [Interfață — vedere de ansamblu](#6-interfață--vedere-de-ansamblu)
7. [Topbar — bara de sus](#7-topbar--bara-de-sus)
8. [Dock stânga — control compact](#8-dock-stânga--control-compact)
9. [Tab-ul Parametri](#9-tab-ul-parametri)
10. [Tab-ul Lame](#10-tab-ul-lame)
11. [Tab-ul Profil](#11-tab-ul-profil)
12. [Tab-ul Ecran](#12-tab-ul-ecran)
13. [Inventar master lame](#13-inventar-master-lame)
14. [Algoritmul de alocare automată](#14-algoritmul-de-alocare-automată)
15. [Modul manual de lame](#15-modul-manual-de-lame)
16. [Motorul de formule](#16-motorul-de-formule)
17. [Șabloane de secvență](#17-șabloane-de-secvență)
18. [Editorul de secvență](#18-editorul-de-secvență)
19. [Tabelul de cote CNC](#19-tabelul-de-cote-cnc)
20. [Schematica axei](#20-schematica-axei)
21. [Cardurile sumar](#21-cardurile-sumar)
22. [Validări și alerte](#22-validări-și-alerte)
23. [Profile de producție](#23-profile-de-producție)
24. [Biblioteca de profile](#24-biblioteca-de-profile)
25. [Import / Export JSON](#25-import--export-json)
26. [Jurnal TXT](#26-jurnal-txt)
27. [Tipărire fișă](#27-tipărire-fișă)
28. [Persistența datelor](#28-persistența-datelor)
29. [Scurtături și gesturi](#29-scurtături-și-gesturi)
30. [Afișare și încadrare ecran](#30-afișare-și-încadrare-ecran)
31. [Design system](#31-design-system)
32. [Arhitectură tehnică](#32-arhitectură-tehnică)
33. [Publicare pe GitHub Pages](#33-publicare-pe-github-pages)
34. [Fluxuri de lucru](#34-fluxuri-de-lucru)
35. [Depanare](#35-depanare)
36. [Întrebări frecvente](#36-întrebări-frecvente)
37. [Limitări cunoscute](#37-limitări-cunoscute)
38. [Contribuții](#38-contribuții)
39. [Licență](#39-licență)
40. [Istoric versiuni](#40-istoric-versiuni)

---

## 1. Ce este aplicația

**Calculator CNC Panel Bender** este o aplicație pentru operatori și tehnologi în atelier de tablă. Calculează și documentează cotele pentru brațul stânga (**LSX**) și brațul drept (**LDX**) la îndoirea casetelor pe un panel bender stil Salvagnini.

Aplicația pornește de la:
- lungimea casetei `L`
- lungimea urechiușei `Lu`
- decalajul / offset-ul de lucru
- offset-ul de montaj lame
- lungimea brațului melc
- lungimile pachetelor de lame (`PL`, `PR`)
- centrul fix al mașinii: **1245 mm**
- cursa liberă pe axă: **0 – 2150 mm**

și produce:
- cote CNC pentru fiecare pas
- formule cu valori numerice reale substituite
- configurația de lame pe fiecare pas
- jurnal de lucru `.TXT`
- fișă tipărită A4 landscape
- profile reutilizabile pentru serii de producție

---

## 2. Ce NU face aplicația

Aplicația **nu**:
- comunică direct cu mașina CNC
- generează G-code
- trimite cote către controller-ul mașinii
- validează coliziuni 3D reale
- înlocuiește software-ul CAM al mașinii
- înlocuiește măsurarea primei piese
- sincronizează date în cloud
- cere cont sau autentificare

Este un **instrument de calcul, configurare și documentare** pentru operator.

---

## 3. Instalare și rulare

### Varianta A — local, direct din fișier

1. Descarcă `index.html`.
2. Dublu-click pe fișier.
3. Aplicația se deschide în browser și funcționează complet offline.

Nu este necesar:
- npm
- build
- server web
- conexiune la internet
- instalare

### Varianta B — de pe stick USB, pe panoul mașinii

1. Copiază `index.html` pe un stick USB.
2. Deschide fișierul în browserul panoului CNC.
3. Aplicația funcționează identic, fără internet.

### Varianta C — GitHub Pages

Vezi secțiunea [33. Publicare pe GitHub Pages](#33-publicare-pe-github-pages).

---

## 4. Structura repository-ului

Structură minimă recomandată:

```text
.
├── index.html      # aplicația completă (HTML + CSS + JS inline)
├── README.md       # documentația completă
└── LICENSE         # opțional, dacă alegi o licență
```

Nu există:
- `package.json`
- `node_modules`
- folder de assets
- fișiere CSS sau JS separate
- workflow-uri de build

---

## 5. Funcționalități complete

### Calcul
- editor de secvență cu pași editabili
- formule editabile inline pentru LSX și LDX
- recalculare live
- parser matematic propriu, fără `eval()`
- referințe între pași (`U1_LSX`, `U2_DX` etc.)
- afișare formule cu valori reale substituite
- evidențiere colorată a termenilor
- șabloane: Standard Box, K-Tech, 1 Lamă SX, 1 Lamă DX

### Lame
- inventar master unic
- alocare automată echilibrată
- mod manual cu validare pe inventar
- statistici live: total, alocat, rămas
- evidențiere segmente folosite pe stânga / dreapta

### Profile
- salvare profil cu toate setările
- încărcare cu aplicare automată
- auto-salvare opțională
- bibliotecă cu căutare, sortare, filtre
- selecție multiplă
- drag & drop pentru reordonare
- import / export JSON
- undo după acțiuni distructive

### Documentare
- jurnal `.TXT` structurat
- tipărire A4 landscape
- copiere cotă în clipboard
- schematică SVG animată
- redare secvență pas cu pas

### Interfață
- temă industrială dark
- dock compact pe taburi
- mod Fit HMI rapid
- mod Fluid responsive
- densitate Auto / Compact / Normal
- scrollbar-uri custom
- feedback vizual pentru toate acțiunile

---

## 6. Interfață — vedere de ansamblu

```text
┌────────────────────────────────────────────────────────────────────┐
│ TOPBAR: logo · profil activ · rezoluție · stare · jurnal · tipărire│
├──────────┬─────────────────────────────────────────────────────────┤
│          │ BANNER STARE                                            │
│  DOCK    │ ┌─────────────────────────────────────────────────────┐ │
│  STÂNGA  │ │ EDITOR SECVENȚĂ ÎNDOIRE & CALCUL COTE CNC            │ │
│          │ │ toolbar + variabile + tabel 8 coloane               │ │
│  rail    │ └─────────────────────────────────────────────────────┘ │
│  48px    │ SUMAR: 4 carduri                                       │
│  +       │ SCHEMATICĂ AXĂ                                         │
│  panou   │ FOOTER                                                 │
└──────────┴─────────────────────────────────────────────────────────┘
```

---

## 7. Topbar — bara de sus

Conține:
- logo SVG inline (profil de tablă îndoită)
- titlu aplicație
- chip **profil activ** — click deschide biblioteca
- badge **rezoluție live** (ex: `1280×1024 · FIT`)
- LED stare:
  - verde `LIVE · VALID`
  - amber `ATENȚIE`
  - roșu `EROARE`
- butoane:
  - 🗂 Profile
  - 💾 Jurnal
  - 🖨️ Tipărește

---

## 8. Dock stânga — control compact

### Structură

- **rail vertical**: 48px lățime, conține butoanele de tab
- **panou conținut**: ~200px, apare când dock-ul este extins
- **lățime totală extinsă**: ~248px
- **lățime restrânsă**: 48px

### Comportament

- click pe un tab → deschide tab-ul și extinde dock-ul dacă era restrâns
- buton dedicat `◀ / ▶` → restrânge / extinde
- sub 1180px lățime, dock-ul se restrânge automat (dacă nu a fost setat manual)
- starea se salvează în `localStorage`

### Taburi (4)

| Tab | Conținut |
|---|---|
| ⚙ Parametri | parametri piesă & mașină **+ Opțiuni de lucru** |
| 🗄 Lame | inventar master, alocare, statistici |
| 🗂 Profil | salvare, comutare, auto-salvare, bibliotecă |
| 🖥 Ecran | afișare, densitate, indicator încadrare, reset |

**Important:** „Opțiuni de lucru" NU este tab separat — este inclus în tabul Parametri.

---

## 9. Tab-ul Parametri

### Parametri piesă & mașină

| Câmp | Implicit | Interval | Pas | Observații |
|---|---:|---:|---:|---|
| Lungime Casetă `L` | 451.6 mm | 1 – 2000 | 0.1 | latura principală |
| Lungime Urechiușă `Lu` | 110 mm | 1 – 1200 | 1 | disponibil ca variabilă |
| Decalaj / Offset | 4 mm | 0 – 50 | 0.5 | **implicit 4** |
| Offset Montaj Lame | 0 mm | −50 – +50 | 0.1 | acceptă negativ |
| Lungime Braț Melc | 320 mm | 10 – 900 | 5 | nu se scade automat din cote |

### Constante mașină (fixe)

```text
Centru mașină = 1245 mm
Cursă axă     = 0 – 2150 mm
```

### Opțiuni de lucru (în același tab)

| Opțiune | Implicit | Efect |
|---|---|---|
| Activează Offset Interior | PORNIT | `OFF = offset`, altfel `OFF = 0` |
| Cursă extinsă (2150 mm) | PORNIT | permite cote peste 1245 mm |
| Setare Manuală Lame | OPRIT | înlocuiește calculul automat |

Când „Setare Manuală Lame" este pornit apar:
- Lamă Stânga LSX (mm)
- Lamă Dreapta LDX (mm)

---

## 10. Tab-ul Lame

Afișează:
- lista segmentelor din inventar
- evidențiere portocalie pentru segmentele LSX
- evidențiere albastră pentru segmentele LDX
- total inventar: **1471 mm**
- total alocat
- total rămas
- pachetul LSX (`PL`)
- pachetul LDX (`PR`)
- diferența de echilibru `|PL − PR|`
- modul de alocare: AUTO / MANUAL

---

## 11. Tab-ul Profil

Conține:
- numele profilului activ
- tipul profilului (Box / K-Tech / 1 Lamă / Custom)
- indicator:
  - `● modificat` — setările curente diferă de profil
  - `✓ salvat` — setările curente sunt identice cu profilul
- dropdown de comutare rapidă
- buton 🗂 Bibliotecă
- buton ⟳ Actualizează profilul activ
- câmp nume profil nou
- selector tip profil
- buton 💾 Salvează profil nou
- switch auto-salvare în profilul activ

---

## 12. Tab-ul Ecran

Conține:
- rezoluția live și DPR
- selector mod afișare:
  - Fit HMI
  - Fluid
- selector densitate:
  - Auto
  - Compact
  - Normal
- indicator de încadrare măsurat real
- buton ↺ Reset valori implicite

---

## 13. Inventar master lame

Segmente disponibile:

```text
400 · 345 · 200 · 160 · 85 · 80 · 69 · 55 · 42 · 35   [mm]
```

**Total inventar = 1471 mm**

### Regula de unicitate

Fiecare segment există în **o singură bucată**.

Nu poate fi folosit:
- de două ori în același pachet
- simultan în LSX și LDX

Alocarea este **disjunctă**.

---

## 14. Algoritmul de alocare automată

### Necesar

```text
T = L + 2 × OFF
```

### Condiție

```text
PL + PR ≥ T
```

### Scor

```text
scor = 12 × depășire + 6 × |PL − PR| + 8 × număr_segmente
```

Se minimizează scorul.

### Căutare

- se enumeră toate submulțimile: `2¹⁰ = 1024`
- se enumeră perechile disjuncte: `3¹⁰ ≈ 59 049`
- se aplică constrângeri de cursă
- se alege perechea cu scor minim

### Exemplu implicit

```text
L = 451.6
OFF = 4
T = 451.6 + 8 = 459.6

PL = 229 = 160 + 69
PR = 235 = 200 + 35

Total = 464 mm
Depășire = +4.4 mm
Δ echilibru = 6 mm
```

---

## 15. Modul manual de lame

Când „Setare Manuală Lame" este activ:
- `PL` și `PR` sunt valorile introduse manual
- aplicația verifică dacă pot fi compuse din inventarul unic
- dacă nu, afișează eroare

### Erori posibile

```text
LSX manual nu poate fi compus din inventar
LDX manual nu poate fi compus din inventar
LSX și LDX manuale cer aceleași segmente
Valorile manuale nu există în inventar
```

---

## 16. Motorul de formule

### Variabile

| Variabilă | Valoare |
|---|---|
| `C` | 1245 |
| `L` | lungime casetă |
| `Lu` | lungime urechiușă |
| `OFF` | decalaj activ |
| `MOUNT` | offset montaj |
| `ARM` | braț melc |
| `PL` | pachet LSX |
| `PR` | pachet LDX |

### Operatori

```text
+   adunare
-   scădere
*   înmulțire
/   împărțire
^   putere
( ) paranteze
```

Acceptă și:
- `−` (minus tipografic)
- `×`
- `÷`
- zecimale cu `.` sau `,`

### Referințe între pași

```text
U1_LSX
U1_LDX
U2_DX
L1_LSX
...
```

Aliasuri:
- `_SX` = `_LSX`
- `_DX` = `_LDX`

### Reguli

- referințele se evaluează în ordinea pașilor
- referința la un pas ulterior → eroare
- referința la un braț liber → eroare
- referința la un pas cu eroare → eroare
- câmp gol = braț liber / așteptare
- împărțirea la zero → eroare
- variabilă necunoscută → eroare

---

## 17. Șabloane de secvență

### 17.1 Standard Box

| Pas | Operație | LSX | LDX |
|---|---|---|---|
| 1 | Urechiușă 1 (U1) | `C - L/2 - OFF - MOUNT` | liber |
| 2 | Latură 1 (L1) | `U1_LSX + PL + 5` | `U1_LSX + 33` |
| 3 | Rotire 180° ➔ U2 | liber | `U1_LSX - 16` |
| 4 | Latură 2 (L2) | `U2_DX + 177` | `U2_DX + PR` |

### Verificare referință atelier

```text
L = 620
OFF = 2.4
MOUNT = 2.2
PL = 309  (160 + 80 + 69)
PR = 255  (200 + 55)

U1_LSX = 1245 - 310 - 2.4 - 2.2 = 930.4
L1_LSX = 930.4 + 309 + 5        = 1244.4
L1_LDX = 930.4 + 33             = 963.4
U2_LDX = 930.4 - 16             = 914.4
L2_LSX = 914.4 + 177            = 1091.4
L2_LDX = 914.4 + 255            = 1169.4
```

### Verificare valori implicite

```text
L = 451.6
OFF = 4
MOUNT = 0
PL = 229
PR = 235

U1_LSX = 1015.2
L1_LSX = 1249.2   (>1245 → necesită cursă extinsă)
L1_LDX = 1048.2
U2_LDX = 999.2
L2_LSX = 1176.2
L2_LDX = 1234.2
```

### 17.2 K-Tech

| Pas | Operație | LSX | LDX |
|---|---|---|---|
| 1 | Negativ SUS | `C - L/2 + OFF - MOUNT` | `C + L/2 - OFF + MOUNT` |
| 2 | Rotire 180° | liber | liber |
| 3 | Pozitiv JOS | `C - L/2 - OFF - MOUNT` | `C + L/2 + OFF + MOUNT` |

### 17.3 O lamă SX

Toate îndoirile pe LSX:

```text
C - L/2 - OFF - MOUNT
```

LDX liber pe tot ciclul.

### 17.4 O lamă DX

Toate îndoirile pe LDX:

```text
C + L/2 + OFF + MOUNT
```

LSX liber pe tot ciclul.

---

## 18. Editorul de secvență

### Toolbar

```text
➕ Pas
🔄 Standard
Șabloane…
🗑 Golește
💾 Jurnal
🖨️ Tipărește
```

### Funcții

- adaugă pas cu cheie unică (`P5`, `P6`…)
- aplică șablon Standard Box
- aplică șabloane alternative
- golește secvența
- exportă jurnal
- tipărește fișa

### Acțiuni pe rând

| Buton | Acțiune |
|---|---|
| ⬆ | mută pasul mai sus |
| ⬇ | mută pasul mai jos |
| ⧉ | duplică pasul |
| ⟳ | marchează rotire 180° |
| ✕ | șterge pasul |

Toate acțiunile distructive au **Undo**.

---

## 19. Tabelul de cote CNC

### Coloane

```text
Pas | Etapă / Operație | Configurație lame | Formulă LSX |
Cotă LSX | Formulă LDX | Cotă LDX | Acțiuni
```

### Layout fix pe procente

```text
4%   Pas
13%  Etapă / Operație
12%  Configurație lame
20%  Formulă LSX
10%  Cotă LSX
20%  Formulă LDX
10%  Cotă LDX
11%  Acțiuni
```

La lățimi utile peste ~760px, tabelul nu are scroll orizontal.

### Pe fiecare rând

- nume operație editabil
- cheie pas (`U1`, `L1`, `U2`, `L2`, `P5`…)
- formulă LSX editabilă
- afișaj formulă substituită
- cotă CNC LSX
- formulă LDX editabilă
- afișaj formulă substituită
- cotă CNC LDX
- configurație lame
- acțiuni

### Interacțiuni

- click pe cotă → copiere în clipboard
- click pe rând → selectare pas + sincronizare schematică
- click pe chip de referință → salt la pasul sursă

---

## 20. Schematica axei

Elemente:
- axă unică 0 – 2150 mm
- gradații
- linie centru 1245 mm
- piesa centrată (lungimea `L`)
- pachet LSX (portocaliu) cu segmentele componente
- pachet LDX (albastru) cu segmentele componente
- sanii LSX / LDX
- cote afișate sub axă

### Interacțiuni

- chips-uri de pas (`P1`, `P2`…)
- buton ▶ Rulează / ⏸ Pauză
- auto-avans la ~2 secunde
- sincronizare cu rândul selectat din tabel
- brațele libere sunt afișate estompat

---

## 21. Cardurile sumar

Patru carduri:

| Card | Afișează |
|---|---|
| Pachet LSX | `PL` + segmentele componente |
| Pachet LDX | `PR` + segmentele componente |
| Acoperire | total pachete / necesar + delta |
| Cursă | cotă maximă / limită + procent utilizare |

---

## 22. Validări și alerte

### Erori

- cotă negativă
- cotă peste cursa activă
- sintaxă invalidă
- variabilă necunoscută
- referință ulterioară
- referință la braț liber
- referință la pas cu eroare
- împărțire la zero
- lame manuale imposibile
- conflict segmente în modul manual

### Avertizări

- `Lu > L`
- acoperire pachete sub necesar
- offset negativ (eroare)

### Afișare

- banner global colorat
- LED în topbar
- mesaje inline pe rând
- stare în antetul de tipărire

---

## 23. Profile de producție

Un profil salvează:
- `L`, `Lu`, `offset`, `mount`, `arm`
- `interior`, `extended`, `manual`
- `mLSX`, `mLDX`
- întreaga secvență de pași
- tipul profilului
- tag-uri
- notițe

### Încărcare profil

La selectare:
1. se aplică parametrii
2. se aplică opțiunile
3. se aplică lamele
4. se aplică secvența
5. se recalculează tot
6. se închide biblioteca
7. se afișează toast de confirmare

### Auto-salvare

- opțională
- debounce ~700 ms
- scrie doar în profilul activ
- afișează ora ultimei salvări
- indicator `● modificat` / `✓ salvat`

---

## 24. Biblioteca de profile

Drawer lateral cu:
- listă profile
- panou de detaliu

### Listă

- căutare live după nume, tag-uri, notițe
- sortare:
  - ordine manuală
  - recente
  - nume
  - dimensiune L
- filtre:
  - Toate
  - Box
  - K-Tech
  - 1 Lamă
  - Custom
- selecție multiplă
- drag & drop pentru reordonare
- acțiuni rapide:
  - ▶ Încarcă
  - ⧉ Duplică
  - 🗑 Șterge

### Panou detaliu

- redenumire
- tip
- tag-uri
- notițe
- grilă parametri
- previzualizare pași
- butoane:
  - Încarcă
  - Salvează fișa
  - Exportă
  - Șterge

### Profile demo

| Profil | Configurație |
|---|---|
| Casetă 451.6×110 · OFF 4 | Standard, alocare automată |
| Casetă 620×120 · Referință atelier | Manual, LSX 309 / LDX 255 |
| K-Tech 451.6 | Negativ sus + pozitiv jos |
| Urechiușe 380×90 · SX | O lamă, braț opus retras |
| Casetă 800×150 · Extins | Piesă lungă, cursă extinsă |

---

## 25. Import / Export JSON

### Export

- exportă toate profilele
- exportă selecția
- exportă profilul individual

Format:

```json
{
  "app": "panel-bender-cnc",
  "version": 6,
  "profiles": [
    {
      "id": "...",
      "name": "Casetă 451.6×110 · OFF 4",
      "kind": "box",
      "tags": ["standard", "off4"],
      "notes": "Profil de bază, decalaj 4 mm.",
      "createdAt": 1700000000000,
      "updatedAt": 1700000000000,
      "settings": {
        "L": 451.6,
        "Lu": 110,
        "offset": 4,
        "mount": 0,
        "arm": 320,
        "interior": true,
        "extended": true,
        "manual": false,
        "mLSX": 229,
        "mLDX": 235
      },
      "steps": [
        {
          "key": "U1",
          "name": "Urechiușă 1 (U1)",
          "lsx": "C - L/2 - OFF - MOUNT",
          "ldx": "",
          "rot": false
        }
      ]
    }
  ]
}
```

### Import

- acceptă formatul propriu
- acceptă array simplu de profile
- acceptă un profil singular
- validează și sanitizează datele
- adaugă profilele în bibliotecă
- oferă Undo

---

## 26. Jurnal TXT

Buton: **💾 Jurnal**

Generează fișier `.TXT` cu:
- BOM UTF-8 (diacritice corecte în Notepad)
- CRLF (compatibil Windows)

### Conținut

```text
========================================================================
FIȘĂ DE LUCRU — PANEL BENDER CNC
Generat: <data, ora>
Profil: <nume profil>
========================================================================

PARAMETRI
  L, Lu, OFF, MOUNT, cursă

LAME
  Inventar unic
  Pachet LSX
  Pachet LDX
  Acoperire

SECVENȚĂ
  [PAS n] cheie · nume
    LSX: formulă substituită = cotă mm
    LDX: formulă substituită = cotă mm

VALIDĂRI
  [ERR/WARN] mesaje

========================================================================
Verificați cotele înainte de execuție.
========================================================================
```

Nume fișier:

```text
Fisa_CNC_YYYYMMDD_HHMM.txt
```

---

## 27. Tipărire fișă

Buton: **🖨️ Tipărește**

Setări implicite:
- A4 landscape
- margini ~7 mm
- alb / negru
- fără dock
- fără topbar
- fără schematică
- fără toolbar
- fără coloana Acțiuni

Include:
- antet cu dată, profil, parametri, pachete, stare
- banner de stare
- carduri sumar
- tabel complet cu formule substituite
- convenții de calcul
- subsol cu avertisment de siguranță

---

## 28. Persistența datelor

Totul se salvează în `localStorage`.

### Chei

| Cheie | Conținut |
|---|---|
| `cnc_v6_state` | parametri, opțiuni, lame, secvență, profil activ |
| `cnc_v6_profiles` | toate profilurile |
| `cnc_v6_view` | căutare, sortare, filtru bibliotecă |
| `cnc_v6_display` | mod afișare + densitate |
| `cnc_v6_dock` | dock restrâns / extins |
| `cnc_v6_tab` | tab activ |

### Backup

Folosește **Export JSON** pentru backup.

### Atenție

Ștergerea datelor browserului șterge și profilurile.

---

## 29. Scurtături și gesturi

| Acțiune | Efect |
|---|---|
| `Ctrl` / `Cmd` + `S` | actualizează profilul activ sau salvează profil nou |
| `Ctrl` / `Cmd` + `O` | deschide biblioteca |
| `Esc` | închide biblioteca |
| click pe cotă | copiere în clipboard |
| click pe rând | selectare pas |
| click pe chip referință | salt la pasul sursă |
| click pe chip variabilă | inserare în formula curentă |
| apăsare lungă `−` / `+` | repetare stepper |
| focus pe input | selectare automată a valorii |

---

## 30. Afișare și încadrare ecran

### Mod Fit HMI

- redare nativă 1:1
- fără `transform: scale`
- fără letterbox
- aplicația umple viewport-ul
- dock și main derulează independent
- optimizat pentru panouri CNC

### Mod Fluid

- layout responsive clasic
- derulare pe pagină

### Densitate

| Densitate | Când se aplică |
|---|---|
| Auto | Compact sub 860px înălțime sau 1180px lățime |
| Compact | permanent compact |
| Normal | permanent normal |

### Rezoluții țintă

```text
840×795
1024×768
1280×1024
1366×768
1920×1080
```

### Dock

- 48px restrâns
- ~248px extins
- auto-restrâns sub 1180px
- comutare manuală prin buton

---

## 31. Design system

### Culori

| Rol | Culoare |
|---|---|
| fundal | `#0b0f19`, `#070b13` |
| carduri | `#151d2a` |
| inset | `#0e1522` |
| borduri | `#243349`, `#2e405e` |
| LSX / accent principal | `#ff6b00` |
| LDX / info | `#00d2ff` |
| succes | `#2ee6a8` |
| avertizare | `#ffb020` |
| eroare | `#ff4d5e` |
| accent acid | `#b6ff3d` |
| accent magenta | `#ff3d9a` |
| accent violet | `#b48cff` |

### Tipografie

- UI: `Segoe UI`, `system-ui`, `Roboto`, `Arial`
- numeric / formule: `JetBrains Mono`, `Cascadia Mono`, `Consolas`
- titluri: `Bahnschrift`, `Arial Narrow`

### Scrollbar

- track închis
- thumb `#2e405e`
- hover portocaliu
- prezent în dock, main, drawer, tabele

---

## 32. Arhitectură tehnică

### Fișier unic

- HTML
- CSS inline în `<style>`
- JavaScript inline în `<script>`
- zero dependințe
- zero CDN
- funcționează de pe `file://`

### Motor formule

- tokenizer
- parser recursiv:
  - `expr`
  - `term`
  - `unary`
  - `power`
  - `primary`
- evaluator AST
- fără `eval()` și fără `new Function()`

### Inventar

- enumerare submulțimi prin măști de biți
- perechi disjuncte
- constrângeri de cursă
- scor de optimizare

### Randare

- recalculare cu debounce (~70 ms)
- fără pierderea focusului la tastare
- o singură buclă de animație, anulată corect
- tranziții scurte
- feedback la acțiuni

---

## 33. Publicare pe GitHub Pages

1. Creează repository-ul.
2. Încarcă `index.html` și `README.md` în rădăcină.
3. Mergi la **Settings → Pages**.
4. La **Source** alege **Deploy from a branch**.
5. Selectează:
   - branch: `main`
   - folder: `/ (root)`
6. Apasă **Save**.
7. După câteva minute aplicația este la:

```text
https://<utilizator>.github.io/<repo>/
```

---

## 34. Fluxuri de lucru

### Flux A — piesă nouă

1. Deschide tabul Parametri.
2. Setează `L`, `Lu`, `OFF`, `MOUNT`.
3. Verifică opțiunile.
4. Verifică tabul Lame.
5. Verifică cotele în editor.
6. Salvează profil.
7. Exportă jurnal sau tipărește.

### Flux B — piesă cunoscută

1. Deschide tabul Profil.
2. Selectează profilul din dropdown.
3. Toate setările se aplică automat.
4. Verifică bannerul de stare.
5. Tipărește fișa.

### Flux C — lame manuale

1. Pornește „Setare Manuală Lame".
2. Introdu `PL` și `PR`.
3. Verifică validarea în tabul Lame.
4. Verifică cotele.
5. Salvează profilul.

### Flux D — transfer între stații

1. Pe stația 1: Bibliotecă → Export JSON.
2. Copiază fișierul JSON pe stația 2.
3. Pe stația 2: Bibliotecă → Import JSON.
4. Verifică profilurile importate.

---

## 35. Depanare

| Problemă | Cauză probabilă | Soluție |
|---|---|---|
| Cotele sunt cu roșu | depășesc cursa | activează „Cursă extinsă" |
| Lame manuale imposibile | segmentele nu există sau se repetă | alege alte valori |
| Nu se văd toate coloanele | dock extins pe ecran mic | restrânge dock-ul la 48px |
| Nu se salvează | localStorage blocat | verifică setările browserului |
| Diacritice stricate în TXT | editor vechi | deschide cu Notepad / editor UTF-8 |
| Clipboard nu merge | browser restricționat | fallback-ul intern este folosit automat |
| Profilurile au dispărut | date browser șterse | importă backup JSON |
| Tabelul are scroll | ecran foarte îngust | folosește Fit HMI + dock restrâns |

---

## 36. Întrebări frecvente

**Î: Pot folosi aplicația fără internet?**  
R: Da, 100% offline, inclusiv de pe stick USB.

**Î: Se trimit cotele automat în mașina CNC?**  
R: Nu. Aplicația doar calculează și documentează.

**Î: Pot modifica formulele?**  
R: Da, orice formulă din tabel este editabilă.

**Î: Pot salva mai multe tipuri de casetă?**  
R: Da, în profile de producție.

**Î: Pot folosi lamele de două ori?**  
R: Nu. Inventarul este unic: o bucată din fiecare segment.

**Î: Ce reprezintă `+5`, `+33`, `−16`, `+177`?**  
R: Corecții empirice de atelier, care se calibrează per mașină.

**Î: De ce U1 este `1245 - L/2 - OFF - MOUNT`?**  
R: Aceasta este ancora confirmată pentru urechiușa 1 — 1245 minus jumătate din piesă minus decalajul.

**Î: Pot tipări fișa?**  
R: Da, A4 landscape, optimizată alb/negru.

**Î: Pot muta pașii?**  
R: Da, cu ⬆ / ⬇ și cu Undo.

**Î: Ce fac dacă schimb ordinea pașilor?**  
R: Referințele se recalculează în noua ordine. Referințele la pași ulteriori devin erori.

---

## 37. Limitări cunoscute

- nu generează G-code
- nu comunică cu controller-ul CNC
- nu validează coliziuni 3D reale
- modelul de cursă verifică doar valoarea cotei pe axă
- corecțiile empirice trebuie validate pe mașină
- backup-ul este manual (Export JSON)
- nu există sincronizare cloud
- nu există autentificare / conturi

---

## 38. Contribuții

Contribuțiile sunt binevenite pentru:
- adaptarea formulelor la alte modele de panel bender
- șabloane suplimentare
- validări geometrice mai stricte
- traduceri ale interfeței
- optimizare pentru alte rezoluții

Reguli:
- păstrează aplicația într-un singur fișier
- păstrează funcționarea offline
- păstrează lipsa dependințelor
- documentează formulele noi în README

---

## 39. Licență

Distribuit sub licența **MIT**.

Adaugă un fișier `LICENSE` în rădăcina repository-ului cu textul licenței MIT dacă vrei ca aceasta să fie aplicată oficial.

---

## 40. Istoric versiuni

| Versiune | Modificări |
|---|---|
| v1 | calculator de bază, 4 pași, jurnal TXT, tipărire |
| v2 | inventar unic — o bucată din fiecare segment |
| v3 | corectare ancoră U1, editor de secvență cu formule editabile |
| v4 | profile de producție, import/export JSON, auto-fit ecran |
| v4.2 | offset implicit 4, fit nativ rapid, reordonare carduri |
| v5 | control pe taburi, fără derulare în stânga |
| v6 | dock compact 48px, opțiuni integrate în Parametri, tabel fără scroll orizontal |

---

## 📌 Note finale

- Aplicația este gândită pentru **utilizare în atelier**, pe panouri CNC cu ecran mic.
- Toate setările sunt **locale** — nu se trimite nimic către servere externe.
- Pentru producție serioasă, folosește **profile** pentru fiecare tip de piesă și **exportă JSON** periodic ca backup.
- Păstrează o copie a `index.html` pe un stick USB la mașină, ca fallback dacă rețeaua cade.

---

<div align="center">

**Verificați întotdeauna cotele înainte de execuția programului.**

Centru mașină 1245 mm · Cursă axă 0–2150 mm · Inventar unic 1471 mm

</div>
