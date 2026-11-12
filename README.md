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
