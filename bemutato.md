# Bemutató-útvonal (operátori forgatókönyv)

Kb. **6–8 perc**, külső oldal. Az első Elemzésnél a modell tölthet — mondd ki: „helyi súly, nincs API”.

Képek: `docs/showcase/kepek/` (JPG). A belső oldal most **nincs** a bemutatóban.

```powershell
.\.venv\Scripts\Activate.ps1
streamlit run app.py
```

---

## 1. Indulás — `01-indulas.jpg`

Oldalválasztó, modellista, üres üzenet, hibrid be. Stakeholder-demó, nem chat-LLM; a teendő a **végső művelet** és a **levél**.

---

## 2. Jelszó — `02-jelszo-muvelet.jpg` + `02-jelszo-talalat.jpg`

Modell: **OHB3-FT**. Üzenet:

```
Hol tudom megváltoztatni a portál jelszavamat?
```

Várt: Semleges + Normál, M **100%**, piszkozat (a jóváhagyás a tanulási fázisban nem kerülhető meg). Forrás **Jelszó módosítása**, *Profil → Biztonság → Jelszó módosítása*; a top 3-ban a belépéses bekezdések lejjebb.

Két kép: először a végső művelet, utána a tudásbázis-találat (görgetve).

Kezeld a javasolt gombbal. Az eredmény bezárul, a mező ürül.

---

## 3. Lista — `03-kezeles-lista.jpg`

Ügygyűjtő: a jelszó-ügy **Jóváhagyva**, kezelésre vár **0**. A tanulás a levél + státusz.

---

## 4. Három modell — `04-harom-modell.jpg`

Modell: **3 modell valószínűsége**. Nincs ügy. Üzenet (ez volt a felvétel):

```
Se nem jó, se nem rossz, de a hiba végre eltűnt.
```

Evalon ez **1** (semleges), FT5 eltalálta. Élőben: OHB3 és HTS2 **pozitív** (a „hiba eltűnt” dicséretnek tűnik), az FT **semleges ~100%**. Mondat: a feltanítás a saját jegyekhez igazít; a Hub-os OHB3 ezért marad a sáv mellett.

---

## 5. Nincs eljárás — `05-nincs-eljaras.jpg`

OHB3 vagy OHB3-FT. Ne a „holdjáró + VPN”-t használd (a KB-ben van VPN).

```
Ki nyerte a 19. századi sakkvilágbajnokságot?
```

M **0%**, `[HELYETTESÍTENDŐ]`, emberi ellenőrzés. Kezeld **Ellenőrizve**.

---

## 6. Frissítés vagy új jegy — `06-frissites-vagy-uj.jpg`

Ugyanaz a téma, ami már a listában van (a felvételen):

```
Milyen jelszókomplexitásra kell figyelni?
```

Kép **kattintás előtt**: *Meglévő ügy frissítése (#…)* / *Új jegy*. Utána Frissítés → kezelés → mező ürül.

---

## Amit ne csinálj

- Ne taníts, ne nyiss `tickets.csv`-t.
- A 3 modell nézet nem hoz létre ügyet.
- Ne ígérj LLM-levelet.
