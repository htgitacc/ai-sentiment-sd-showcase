# Hol tart a projekt — rövid út

A részletes mérések, elakadások és eval-tábla a fejlesztői naplóban van: [`docs/projektnaplo.md`](../projektnaplo.md). Ez a fájl csak a **ívet** adja: mit építettem, miért így, hol áll most.

## Most

Portfólió-prototípus: **Alföld Informatika** (fiktív IT-szolgáltató). Egy jegyre helyi magyar modellek adják a hangvételt, szabályok a priorítást és a válaszlogikát, markdown RAG a tudásbázis-bekezdést, sablon a mintaválaszt. **Nincs LLM API.** A tanulási kör: elemzés → sablonlevél → kötelező kezelés → ügygyűjtő.

- Külső / belső oldal, két KB
- OHB3, HTS2, külsőn OHB3-FT (FT5); a Hub-os OHB3 **megmaradt** összevetésre
- Eval 12 érintetlen mondaton: **FT5 10/12** (341 saját jegy; a holdout nem az eval)
- RAG: bekezdés + top-1 hasonlóság; 0%-nál nincs kitalált eljárás

## Lépések (összesűrítve)

1. **Helyi hangvétel** — két NYTK huBERT, hibrid ki/be. Tanulság: a véleménykorpusz és az ügyfélszolgálati panasz nem ugyanaz.
2. **Prioritás szabályokkal** — sürgős / normál / nem sürgős, LLM nélkül megmagyarázható.
3. **Markdown RAG** — a százalék hasonlóság, nem „milyen jó a válasz”. Először gyenge skála és átlag; később bekezdés + top-1 + jelszó-rangsor.
4. **Válaszlogika egy lépésben** — nincs kaszkád; magas M% nem oldja fel az eszkalációt.
5. **Két oldal** — ugyanaz a képernyő, más tudás.
6. **Finomhangolás** — saját jegyek, harmadik modell. A 100%-os holdout nem látta a „közepes” lyukat; az eval 0/12 → 10/12. A cinikus 0 csak *összetett* tanítóval jött (közepes + gúny).
7. **Sablon + ügygyűjtő** — nincs eljárás → soha nem küldésre kész. Kezelés kötelező; ugyanaz a szöveg: frissítés vagy új jegy; kijelölés, csoportos státusz, törlés.

## Szándékosan nincs (még)

Kaszkád AUTO→piszkozat→eszkaláció, ügyféllevél Gemini/Groq/Cerebras, IP-alapú oldal, LoRA. A sablonlevél már megvan; LLM csak akkor, ha a demó tézise (helyi, kitalálás nélkül) megmarad.
