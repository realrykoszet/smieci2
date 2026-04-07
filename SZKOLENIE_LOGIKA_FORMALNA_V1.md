# SZKOLENIE: LOGIKA FORMALNA DLA PREZESA I LUKASZA
## Eureka Intelligence | v1.0 | 23.03.2026
## Poziom: zaawansowany (filozofia, socjologia, compliance)

---

# DLACZEGO TO JEST WAZNE

Logika formalna = szkielet na ktorym wisi CALA wiedza systemu.
Bez logiki: PREZES "zgaduje". Z logika: PREZES "dowodzi".
Kazda decyzja, scoring, email, procedura — ma formalne uzasadnienie.

**Cel szkolenia:** PREZES + Lukasz opanuja logike na poziomie studiow filozoficznych.
**Koszt:** 0 EUR. **Zrodla:** 5 deep scanow, 60+ zrodel, 25+ formalizacji.

---

# CZESC 1: RACHUNEK ZDAN (Propositional Logic)

## 1.1 Spojniki logiczne — pelna tabela

| Symbol | Nazwa | Czytamy | Prawdziwe gdy... |
|--------|-------|---------|------------------|
| ¬p | negacja (NOT) | "nie p" | p jest falszywe |
| p ∧ q | koniunkcja (AND) | "p i q" | OBA prawdziwe |
| p ∨ q | alternatywa (OR) | "p lub q" | CO NAJMNIEJ JEDNO prawdziwe |
| p -> q | implikacja (IF-THEN) | "jesli p to q" | NIE JEST TAK ze p=TRUE a q=FALSE |
| p <-> q | rownowaznosc (IFF) | "p wtedy i tylko wtedy gdy q" | OBA takie same (T-T lub F-F) |

## 1.2 Tabela prawdy — MASTER TABLE

| p | q | ¬p | p∧q | p∨q | p->q | p<->q | p XOR q |
|---|---|----|-----|-----|------|-------|---------|
| 1 | 1 | 0  | 1   | 1   | 1    | 1     | 0       |
| 1 | 0 | 0  | 0   | 1   | 0    | 0     | 1       |
| 0 | 1 | 1  | 0   | 1   | 1    | 0     | 1       |
| 0 | 0 | 1  | 0   | 0   | 1    | 1     | 0       |

## 1.3 IMPLIKACJA — najwazniejszy spojnik

**KLUCZOWE:** Implikacja p -> q jest FALSZYWA tylko w JEDNYM przypadku:
gdy z PRAWDY wynika FALSZ (p=T, q=F).

Przyklad: "Jesli zdasz egzamin, kupie ci rower"
- Zdales, kupilem = TRUE (dotrzymalem slowa)
- Zdales, NIE kupilem = **FALSE** (zlamalem obietnice)
- Nie zdales, kupilem = TRUE (miły gest)
- Nie zdales, nie kupilem = TRUE (nic nie obiecywalem)

**Rownowaznosc:** p -> q ≡ ¬p ∨ q (implikacja = "nie-p lub q")

## 1.4 Kontrapozycja — KLUCZOWE PRAWO

```
(p -> q) <-> (¬q -> ¬p)    TAUTOLOGIA!

"Jesli pada, to jest mokro" = "Jesli NIE jest mokro, to NIE pada"
```

**Zastosowanie w compliance:**
```
"Jesli firma przetwarza dane osobowe, to musi miec DPO"
= "Jesli firma NIE ma DPO, to NIE przetwarza danych osobowych (legalnie)"
```

## 1.5 Prawa logiczne — sciagawka

| # | Nazwa | Formula |
|---|-------|---------|
| 1 | De Morgan I | ¬(p ∧ q) ≡ ¬p ∨ ¬q |
| 2 | De Morgan II | ¬(p ∨ q) ≡ ¬p ∧ ¬q |
| 3 | Podwojna negacja | ¬¬p ≡ p |
| 4 | Kontrapozycja | (p -> q) ≡ (¬q -> ¬p) |
| 5 | Definicja implikacji | (p -> q) ≡ (¬p ∨ q) |
| 6 | Definicja rownowaznosci | (p <-> q) ≡ (p -> q) ∧ (q -> p) |
| 7 | Wylaczony srodek | p ∨ ¬p ≡ TRUE |
| 8 | Niesprzecznosc | p ∧ ¬p ≡ FALSE |
| 9 | Importacja | (p ∧ q) -> r ≡ p -> (q -> r) |

## 1.6 Reguly wnioskowania — POPRAWNE

| Regula | Schemat | Przyklad |
|--------|---------|---------|
| **Modus ponens** | p, p->q ⊢ q | Pada. Jesli pada, biore parasol. Wiec: biore parasol. |
| **Modus tollens** | ¬q, p->q ⊢ ¬p | Nie biore parasola. Jesli pada, biore parasol. Wiec: nie pada. |
| **Sylogizm hipotetyczny** | p->q, q->r ⊢ p->r | Jesli A to B. Jesli B to C. Wiec: jesli A to C. |
| **Dysjunkcja eliminacyjna** | p∨q, ¬p ⊢ q | Jestem w domu lub pracy. Nie w domu. Wiec: w pracy. |
| **Reductio ad absurdum** | Zaloz ¬T, wyprowadz sprzecznosc ⊢ T | Dowod nie wprost. |

## 1.7 BLEDY LOGICZNE — czego NIE robic

| Blad | Schemat | Dlaczego bledny |
|------|---------|-----------------|
| **Afirmacja nastepnika** | q, p->q ⊬ p | "Ulica mokra, wiec pada" — BLAD! Ktos mogl polac. |
| **Negacja poprzednika** | ¬p, p->q ⊬ ¬q | "Nie pada, wiec ulica sucha" — BLAD! |
| **Petitio principii** | Wniosek = przeslanka | Dowodzisz tego co zakladasz. |
| **Non sequitur** | Brak polaczenia | Wniosek nie wynika z przeslanek. |
| **Falszywy dylemat** | p∨q (gdy jest tez r) | "Albo z nami albo przeciw nam" — sa inne opcje! |

---

# CZESC 2: LOGIKA PREDYKATOW (First-Order Logic)

## 2.1 Notacja

| Symbol | Nazwa | Znaczenie | Przyklad |
|--------|-------|-----------|----------|
| ∀x | kwantyfikator ogolny | "dla kazdego x" | ∀x(Czlowiek(x) -> Smiertelny(x)) |
| ∃x | kwantyfikator szczegolowy | "istnieje x taki ze" | ∃x(Firma(x) ∧ Spelnia_NIS2(x)) |
| P(x) | predykat | "x ma wlasciwosc P" | Compliance(firma) |
| f(x) | funkcja | "wartosc f dla x" | Score(firma) |
| a, b | stale | konkretne obiekty | eureka, gambleguard |

## 2.2 KLUCZOWA ROZNICA: ∀ uzywa ->, ∃ uzywa ∧

```
∀x(P(x) -> Q(x))    "Kazdy P jest Q"     (NIE: ∀x(P(x) ∧ Q(x))!)
∃x(P(x) ∧ Q(x))     "Istnieje P ktory jest Q"  (NIE: ∃x(P(x) -> Q(x))!)
```

**Dlaczego?** ∀ z ∧ mowiloby "WSZYSTKO jest P i Q" (zbyt mocne).
∃ z -> mowiloby "istnieje cos, ze jesli jest P to jest Q" (zbyt slabe — spelnia kazdy nie-P).

## 2.3 De Morgan dla kwantyfikatorow

```
¬∀x P(x) ≡ ∃x ¬P(x)    "Nie kazdy P" = "Istnieje nie-P"
¬∃x P(x) ≡ ∀x ¬P(x)    "Nie istnieje P" = "Kazdy jest nie-P"
```

## 2.4 Przyklady z compliance

```
"Kazda firma przetwarzajaca dane musi miec DPO":
  ∀x(Firma(x) ∧ Przetwarza_Dane(x) -> Ma_DPO(x))

"Istnieje organizacja spelniajaca NIS2":
  ∃x(Organizacja(x) ∧ Spelnia_NIS2(x))

"Kazdy operator iGaming ktory nie ma licencji zostanie ukarany":
  ∀x(Operator(x) ∧ ¬Ma_Licencje(x) -> Ukarany(x))

"Zaden produkt bez cech konstytutywnych nie jest produktem 10/10":
  ∀x(¬Cechy_Konstytutywne(x) -> ¬Produkt_10(x))
  Kontrapozycja: ∀x(Produkt_10(x) -> Cechy_Konstytutywne(x))
```

## 2.5 Sylogizmy — od Arystotelesa do FOL

| Sylogizm | Klasycznie | FOL |
|----------|-----------|-----|
| **Barbara** (AAA-1) | Kazdy M jest P. Kazdy S jest M. Wiec: kazdy S jest P. | ∀x(M(x)->P(x)), ∀x(S(x)->M(x)) ⊢ ∀x(S(x)->P(x)) |
| **Celarent** (EAE-1) | Zaden M nie jest P. Kazdy S jest M. Wiec: zaden S nie jest P. | ∀x(M(x)->¬P(x)), ∀x(S(x)->M(x)) ⊢ ∀x(S(x)->¬P(x)) |
| **Darii** (AII-1) | Kazdy M jest P. Pewien S jest M. Wiec: pewien S jest P. | ∀x(M(x)->P(x)), ∃x(S(x)∧M(x)) ⊢ ∃x(S(x)∧P(x)) |

---

# CZESC 3: LOGIKA MODALNA I DEONTYCZNA

## 3.1 Logika modalna

| Symbol | Nazwa | Znaczenie |
|--------|-------|-----------|
| □p | box (koniecznosc) | "koniecznie p" / "w KAZDYM mozliwym swiecie p" |
| ◇p | diamond (mozliwosc) | "mozliwie p" / "w JAKIMS mozliwym swiecie p" |

**Zwiazek:** □p ≡ ¬◇¬p ("koniecznie p" = "niemozliwe nie-p")

**Systemy modalne (od najslabszego):**
- **K:** Bazowy — □(p->q) -> (□p -> □q)
- **T:** K + ∀ swiaty widza siebie — □p -> p ("co konieczne, jest prawdziwe")
- **S4:** T + przechodniosc — □p -> □□p
- **S5:** S4 + symetria — ◇p -> □◇p (najsilniejszy)

## 3.2 Logika deontyczna (compliance!)

| Symbol | Nazwa | Znaczenie |
|--------|-------|-----------|
| O(p) | obligacja | "obowiazkowe jest p" |
| P(p) | pozwolenie | "dozwolone jest p" |
| F(p) | zakaz | "zakazane jest p" |

**Zwiazki:**
```
O(p) ≡ ¬P(¬p)    "Obowiazek p" = "Nie wolno nie-p"
F(p) ≡ O(¬p)     "Zakaz p" = "Obowiazek nie-p"
F(p) ≡ ¬P(p)     "Zakaz p" = "Nie dozwolone p"
```

**Przyklady compliance:**
```
RODO Art. 37: O(∀x(Przetwarza_Dane(x) -> Wyznacz_DPO(x)))
  "Obowiazkowe: kazdy przetwarzajacy dane wyznacza DPO"

NIS2 Art. 23: O(∀x∀i(Podmiot_Kluczowy(x) ∧ Incydent(i) -> Zgloszenie_24h(x,i)))
  "Obowiazkowe: kazdy podmiot kluczowy zglasza incydent w 24h"

GambleGuard: F(∀x(Samowykluczony(x) ∧ Gra_Dalej(x)))
  "Zakazane: samowykluczony gracz gra dalej"
```

---

# CZESC 4: SOCJOLOGIA FORMALNA

## 4.1 MAX WEBER — 6 aksjomatow biurokracji

```
A1. HIERARCHIA:
  ∀x∀y(Stanowisko(x) ∧ Stanowisko(y) ∧ x≠y ->
    Podlega(x,y) ∨ Podlega(y,x) ∨ ∃z(Podlega(x,z) ∧ Podlega(y,z)))

A2. FORMALIZACJA:
  ∀a∀d(Dzialanie(a) ∧ Wykonuje(d,a) ->
    ∃u(Uprawnienie(u) ∧ Posiada(d,u) ∧ Autoryzuje(u,a)))

A3. BEZOSOBOWOSC:
  ∀d∀a(Decyzja(d) ∧ Podejmuje(a,d) ->
    ¬∃o(OsobaFizyczna(o) ∧ WplywOsobisty(o,d)))

A4. KOMPETENCJA:
  ∀s∀p(Stanowisko(s) ∧ Zajmuje(p,s) ->
    ∃k(Kompetencja(k) ∧ Posiada(p,k) ∧ Wymagana(k,s)))

A5. DOKUMENTACJA:
  ∀a(Dzialanie(a) -> ∃d(Dokument(d) ∧ Opisuje(d,a)))

A6. REGULAMINOWOSC:
  ∀r(Regula(r) -> ∀p(Podlega(p,r) -> Stosuje(p,r)))
```

**Zastosowanie:** Nasz system 5 agentow JEST biurokracja Webera!
- A1: PREZES > EUREKA > BIBL > ADMIN > HELPERS
- A2: kazdy agent ma uprawnienia z protokolu
- A3: decyzje wg metryk, nie "bo mi sie podoba"
- A4: Opus na strategii, Haiku na zbieraniu danych
- A5: DISCOVERY_LOG.md
- A6: CLAUDE.md

## 4.2 LUHMANN — Autopojeza

```
System autopojeczny:
  ∀t(Stan(S,t+1) = F(Stan(S,t), Operacje(S,t)))
  System produkuje sam siebie ze swoich wlasnych operacji.

System/Srodowisko:
  S ∩ E = ∅    (system NIGDY nie jest srodowiskiem)
  S ∪ E = U    (razem = calosc)

Komunikacja = (Informacja, Utterance, Verstehen)
  K = (I, U, V) — synteza 3 selekcji
```

**Zastosowanie:** Discovery Engine = system autopojeczny.
Sam sie uczy (Hebbian), sam sie oczyszcza (pruning), sam sie odtwarza (persistence).

## 4.3 BOURDIEU — Kapital i pole

```
FORMULA BOURDIEU:
  [(Habitus)(Kapital)] + Pole = Praktyka

Kapital jako wektor w R4:
  K(x) = (K_ekon(x), K_kult(x), K_spol(x), K_symb(x))

Habitus jako funkcja:
  H(x) = f(historia(x), pozycja(x), pole(x))

Przemoc symboliczna (KLUCZOWE dla buyer-first!):
  p -> q   gdzie p jest UKRYTE (doxa)
  "Jesli regulator kaze, to firma musi kupic" — ale "regulator kaze" jest ukryte
```

**Zastosowanie buyer-first:**
```
Regulator(r) ∧ Wymaga(r, compliance) ->
  ∀f(Firma(f) ∧ Podlega(f,r) -> Musi_Kupic(f, narzedzie))

1 regulator = 200 firm MUSI kupic. To jest przemoc symboliczna Bourdieu
wbudowana w logike formalna.
```

## 4.4 KOTARBINSKI — Prakseologia

```
DEKOMPOZYCJA:
  Cel -> Zadanie -> Czynnosc (atomowa)

SPRAWNOSC:
  Sprawne(a) <-> Skuteczne(a) ∧ Ekonomiczne(a) ∧ Wydajne(a)

  Skuteczne(a) <-> Cel_Osiagniety(a)
  Ekonomiczne(a) <-> Koszt(a) ≤ Minimum_Kosztu(a)
  Wydajne(a) <-> Efekt(a) / Naklad(a) ≥ Prog_Wydajnosci
```

**Odkrycie BIBLIOTEKARZA:** Nasza metodologia v4.0 (Cel->Zadanie->Czynnosc,
Zero-Cost First, Idle Protocol, Audit Chain) = **implementacja prakseologii Kotarbinskiego**
w systemie wieloagentowym!

---

# CZESC 5: LOGIKA DECYZYJNA

## 5.1 MECE — formalna definicja

```
Partycja zbioru U na {A1, ..., An}:

ME (Mutually Exclusive): ∀i≠j: Ai ∩ Aj = ∅
CE (Collectively Exhaustive): A1 ∪ ... ∪ An = U
MECE = ME ∧ CE

Test: pokrycie regulacji bankowych
  U = {NIS2, DORA, AI_Act, GDPR, AML, MiCA, CRA, PSD2}
  Czy nasze kategorie pokrywaja WSZYSTKO (CE)?
  Czy ZADNA regulacja nie jest w 2 kategoriach (ME)?
```

## 5.2 Brzytwa Ockhama

```
Jesli T1 i T2 wyjasniaja X, a |T1| < |T2|, wybierz T1.

Formalnie (MDL — Minimum Description Length):
  M* = argmin { L(M) + L(D|M) }
  Najlepszy model = minimum (zlozonosc modelu + blad modelu)

Zastosowanie do scoringu:
  Jesli 4 wymiary daja ten sam wynik co 7 — uzywaj 4.
  ALE: Brzytwa ZAWODZI gdy problem jest NAPRAWDE zlozony (underfitting).
```

## 5.3 Teoria gier — Nash w compliance

```
Rownowaga Nasha:
  ∀i: ui(si*, s-i*) ≥ ui(si, s-i*)
  Zaden gracz nie moze poprawic swojej sytuacji zmieniajac TYLKO swoja strategie.

Firma vs Regulator (Inspection Game):
  Kara za naruszenie: f
  Zysk z naruszenia: g
  Jesli f > g -> compliance jest STRATEGIA DOMINUJACA
  Firma ZAWSZE wygrywa stosujac compliance (niezaleznie co robi regulator)

Scoring: wbuduj test "czy f > g?" dla kazdej regulacji.
```

## 5.4 Triada Heglowska

```
Teza (T) -> Antyteza (¬T lub T') -> Synteza (S)
S = to co zachowuje prawde z T i T' (Aufhebung)

Zastosowanie w sprzedazy:
  T: "Firma jest bezpieczna" (stan obecny klienta)
  A: "NIS2/DORA mowi ze NIE jest bezpieczna" (regulacja)
  S: "Nasz scoring pokaze DOKLADNIE gdzie i jak naprawic" (produkt)

NIE sprzedawaj ANTYTEZY (strach). Sprzedawaj SYNTEZE (rozwiazanie).
```

---

# CZESC 6: OPERACJONALIZACJA — "DEFINICJA KRZESLA"

## 6.1 Cechy konstytutywne vs konsekutywne

```
Cechy KONSTYTUTYWNE (DNA — bez nich obiekt NIE ISTNIEJE):
  Krzeslo(x) <-> ma_nogi(x, ≥3) ∧ ma_siedzisko(x) ∧ mozna_siedziec(x)
  Brak jednej cechy = to NIE jest krzeslo.

Cechy KONSEKUTYWNE (wynikaja z konstytutywnych):
  ma_nogi(x,4) ∧ rowne(nogi(x)) -> stabilne(x)
  Stabilnosc WYNIKA z posiadania 4 rownych nog.

Cechy AKCYDENTALNE (moga byc, nie musza):
  kolor(x), material(x), cena(x) — nie wplywaja na "krzeslowatość"
```

## 6.2 Zastosowanie do procedur UE

```
Procedura_UE(x) <->
  Ma_Podstawe_Prawna(x) ∧
  Ma_Opis_Ryzyka(x) ∧
  Ma_Osobe_Odpowiedzialna(x) ∧
  Ma_Protokol_Kontroli(x)

Brak JEDNEJ cechy -> ¬Procedura_UE(x) -> ODRZUT
To jest ConstitutiveCheck z pliku "logika podstawy.txt"!
```

## 6.3 Zastosowanie do scoringu 10/10

```
Produkt_10(x) <->
  4_Oceny_Sedziow(x) ∧
  Konsensus_Logiczny(x) ∧
  Zgodnosc_Matryca(x) ∧
  Cechy_Konstytutywne_Kompletne(x)

Sedziowie:
  Sokol: Ocena_Detali(x) ≥ 10
  Nietoperz: Logika_Hierarchiczna(x) = SPOJNA
  Kruk: Operacjonalizowalnosc(x) = TRUE
  Mrowkojad: Szum(x) = 0

40/40 -> Zloty Gen -> wysylka
< 40 -> Wirus niszczy -> poprawka -> od nowa
```

---

# CZESC 7: ZRODLA I NARZEDZIA

## Ksiazki (darmowe PDF)
1. **forall x: Calgary** — darmowy, najlepsze wprowadzenie do FOL
2. **Open Logic Text** — kompletny podrecznik, darmowy PDF
3. **Peter Smith: IFL2** — Cambridge, darmowy PDF
4. **Garson: Modal Logic for Philosophers** — logika modalna, PDF
5. **Zalta: Basic Concepts in Modal Logic** — Stanford, PDF
6. **Walton: Informal Logic** — teoria argumentacji, PDF
7. **Mahoney: Logic of Social Science** — logika w socjologii

## Kursy (darmowe)
1. Stanford — Introduction to Logic (Coursera)
2. MIT OCW — Logic I (24.241)
3. CMU OLI — Logic & Proofs (interaktywny)
4. Open Logic Project — kompletny kurs

## Narzedzia (darmowe)
1. Stanford Truth Table Tool — generator tabel prawdy
2. Logic Calculator — kalkulator logiczny
3. Open Logic Proof Checker — weryfikator dowodow
4. Tree Proof Generator — drzewa semantyczne
5. **Lean 4** — theorem prover (NAJLATWIEJSZY do nauki)

## Pelne raporty deep scan (w projekcie)
- `plans/LOGIKA_PREDYKATOW_DEEP_SCAN.md` (#P47)
- `plans/DEEP_SCAN_LOGIKA_DECYZYJNA.md` (#DS01)
- `plans/LOGIKA_FORMALNA_W_SOCJOLOGII_DEEP_SCAN.md` (#DS02)

---

# CZESC 8: POLACZENIA Z ISTNIEJACA WIEDZA

## Synapsy do zbudowania (logika <-> reszta systemu)

| Logika | Istniejaca wiedza | Polaczenie |
|--------|-------------------|------------|
| Modus ponens | Gilotyna gate | p=warunek, q=akcja. Jesli warunek spelniony -> akcja |
| Modus tollens | Audit Chain | ¬wynik_OK, proces->wynik_OK ⊢ ¬proces (cos w procesie jest zle) |
| Kontrapozycja | NLP reframing | Odwroc perspektywe: "jesli nie X to nie Y" |
| MECE | Power Map | Pokrycie rynku bez luk i powtorzen |
| Teoria gier | Negocjacje | Nash = win-win, dominujaca strategia |
| Brzytwa Ockhama | ECO mode | Minimum slow, max efekt |
| Weber hierarchia | 5 agentow | PREZES>EUREKA>BIBL>ADMIN>HELPERS |
| Luhmann autopojeza | Discovery Engine | Sam sie uczy, sam sie oczyszcza |
| Bourdieu przemoc symb. | Buyer-first | Regulator KAZE kupic -> 200 klientow |
| Kotarbinski prakseologia | Metodologia v4.0 | Cel->Zadanie->Czynnosc |
| Cechy konstytutywne | ConstitutiveCheck | DNA produktu — brak 1 cechy = odrzut |
| Triada Heglowska | Email sprzedazowy | T(stan) -> A(regulacja) -> S(nasz produkt) |
| Logika deontyczna | Compliance scoring | O(obowiazek), F(zakaz), P(pozwolenie) |
| Sylogizm Barbara | Scoring chain | Kazdy M jest P, kazdy S jest M -> kazdy S jest P |

---

*Wygenerowane przez Discovery Engine v7.0 SYNAPTIC | 5 agentow | 60+ zrodel | 0 EUR*
