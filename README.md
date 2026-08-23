# Ügyfélszolgálati AI prototípus — bemutató

Helyi, **magyar** ügyfélszolgálati demó: hangvétel, priorítás, tudásbázis-találat és sablonlevél — **LLM API nélkül**. A fiktív cég: **Alföld Informatika**.

Ez a mappa a későbbi nyilvános showcase-repo vázlata (nem a teljes fejlesztői projekt). A kód, a modellek és a címkézett jegyek **nincsenek** itt.

Részletes mérés és tanulság: [`docs/projektnaplo.md`](../projektnaplo.md). Rövid ív: [`HALADAS.md`](HALADAS.md). Operátori forgatókönyv + mikor mit fotózz: [`bemutato.md`](bemutato.md).

## Tech

| | |
| --- | --- |
| Felület | Python, Streamlit |
| Hangvétel | NYTK huBERT: OHB3 (3 osztály), HTS2 (2 osztály + küszöb), OHB3-FT (saját jegyek, FT5) |
| Hibrid | Szabályréteg tényszerű panaszmintákra (OHB3-FT-n ki) |
| Prioritás / logika | Szabályok, egy lépés, nincs kaszkád |
| RAG | `paraphrase-multilingual-MiniLM-L12-v2`, bekezdés, numpy cosine, 0% → nincs kitalált eljárás |
| Levél | Sablon a találatból; `[HELYETTESÍTENDŐ]` ha nincs eljárás |
| Adat | Helyi JSONL ügygyűjtő; a tanító CSV és a súlyok gitignore |

CPU elég. Az első futás Hub-letöltés; utána cache.

## Hol tart

A tanulási kör összejött: elemzés → sablon → kötelező kezelés → szűrhető ügygyűjtő (frissítés vs. új jegy, kijelölés, törlés). FT5 a 12 érintetlen evalon **10/12**. A Hub-os OHB3 megmaradt, hogy a feltanítás összevethető legyen.

Hogyan jutott ide (egy mondat / lépés): helyi két modell → priorítás → RAG → egy lépéses logika → két oldal → FT harmadik modellként → sablon + ügygyűjtő → cinikus 0 javítás. A lyukak (langyos 1, jelszó-bekezdés, holdout ≠ eval) a naplóban vannak.

## Működés — bemutató

A képek a [`kepek/`](kepek/) mappában vannak. Élő sorrend: [`bemutato.md`](bemutato.md).

### 1. Ugyanaz a képernyő, két oldal

Külső (ügyfél) vagy belső (dolgozó). Egy üzenetmező, nincs típusválasztó. A modell helyben fut.

![Indulás: oldal, modell, üres üzenet](kepek/01-indulas.jpg)

### 2. A válasz a tudásbázis bekezdése

„Hol tudom megváltoztatni a portál jelszavamat?” → Semleges, M **100%**, piszkozat (a tanulási fázisban a jóváhagyás nem kerülhető meg). A találat *Jelszó módosítása*: *Profil → Biztonság → Jelszó módosítása* — nem az első belépés, nem generált levél.

![Jelszó-kérdés: végső művelet](kepek/02-jelszo-muvelet.jpg)

![Jelszó-kérdés: extractív RAG, top 3](kepek/02-jelszo-talalat.jpg)

Kezelés után a blokk bezárul; az ügy a listában marad.

![Ügygyűjtő kezelés után](kepek/03-kezeles-lista.jpg)

### 3. A feltanítást a bázis mellett kell nézni

„Se nem jó, se nem rossz, de a hiba végre eltűnt.” — evalon **1**, az FT5 eltalálta. A bázis OHB3 és az HTS2 **pozitív** (a hiba eltűnt), az FT **semleges**. A Hub-os OHB3 ezért marad a sáv mellett; a holdout 100% ezt a különbséget nem mutatta volna.

![3 modell valószínűsége](kepek/04-harom-modell.jpg)

### 4. Ha nincs eljárás, nincs kitalált levél

Irreleváns kérdés → M 0%, `[HELYETTESÍTENDŐ]`, emberi ellenőrzés.

![Nincs eljárás, 0%](kepek/05-nincs-eljaras.jpg)

### 5. Ugyanaz a szöveg: frissítés vagy új jegy

Nem klónoz automatikusan. A gombon látszik, melyik `#id` frissül.

![Frissítés vagy új jegy](kepek/06-frissites-vagy-uj.jpg)

## Mit nem állítok

A holdout nem gyártási pontosság. Az eval 12 mondat kicsi. Nincs Gemini/Groq-levél. A cég fiktív.
