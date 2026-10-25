# Milosz Paid Ads — strona agencji

Jednostronicowa, statyczna strona agencji **Milosz Paid Ads** (Google Ads dla gabinetów
fizjoterapii i rehabilitacji). Czysty HTML + CSS, bez frameworka i bez builda.

- Adres publiczny: **https://miloszagency.github.io/**
- Hosting: GitHub Pages (za darmo, HTTPS automatycznie)
- Repozytorium: https://github.com/MiloszAgency/MiloszAgency.github.io (konto GitHub: `MiloszAgency`)

## Pliki

| Plik | Co to jest |
|---|---|
| `index.html` | cała strona: hero, oferta, współpraca, o mnie, kontakt, polityka prywatności |
| `style.css` | style (mobile-first, bez zewnętrznych fontów i skryptów) |
| `favicon.svg` | ikona w karcie przeglądarki |
| `robots.txt` | zezwala wyszukiwarkom na indeksowanie |
| `.nojekyll` | mówi GitHub Pages, żeby nie przetwarzał plików przez Jekyll |
| `CNAME` | (pojawi się po podpięciu domeny) nazwa własnej domeny |

## Podgląd lokalny

W folderze projektu:

```bash
python3 -m http.server 8765
```

i otwórz http://localhost:8765 w przeglądarce.

## Jak zmienić treść

1. Edytuj `index.html` (treści) albo `style.css` (wygląd).
2. Wgraj zmiany:

```bash
git add -A && git commit -m "Aktualizacja treści" && git push
```

GitHub Pages publikuje nową wersję zwykle w ciągu 1–2 minut.

Miejsca do uzupełnienia w `index.html`:
- sekcja **O mnie** (`id="o-mnie"`) — doświadczenie, od kiedy działasz;
- sekcja **Kontakt** (`id="kontakt"`) — telefon jest zakomentowany; odkomentuj blok `TELEFON` i wpisz numer.

## Jak podpiąć własną domenę `.pl` (np. `miloszpaidads.pl`)

GitHub Pages obsługuje własne domeny bez opłat, z certyfikatem HTTPS (Let's Encrypt)
wystawianym automatycznie. Cała operacja to ok. 15 minut pracy + czas na propagację DNS.

### Krok 1. Kup domenę

U dowolnego polskiego rejestratora (np. OVH, home.pl, nazwa.pl, cyber_Folks) albo zagranicznego
(np. Dynadot, Porkbun — sprawdź, czy obsługują `.pl`). Przy zakupie **nie** kupuj hostingu —
strona jest na GitHub Pages. Potrzebujesz tylko domeny i dostępu do jej panelu DNS.

### Krok 2. Dodaj rekordy DNS u rejestratora

W panelu DNS domeny dodaj (zostaw TTL domyślny):

| Typ | Nazwa (host) | Wartość |
|---|---|---|
| A | `@` | `185.199.108.153` |
| A | `@` | `185.199.109.153` |
| A | `@` | `185.199.110.153` |
| A | `@` | `185.199.111.153` |
| AAAA | `@` | `2606:50c0:8000::153` |
| AAAA | `@` | `2606:50c0:8001::153` |
| AAAA | `@` | `2606:50c0:8002::153` |
| AAAA | `@` | `2606:50c0:8003::153` |
| CNAME | `www` | `miloszagency.github.io.` |

Uwagi:
- `@` oznacza samą domenę (`miloszpaidads.pl`). W niektórych panelach pole „nazwa" zostawia się puste.
- Jeśli rejestrator wstawił już własne rekordy A/AAAA dla `@` (np. „strona w budowie"), usuń je.
- Rekordy AAAA są opcjonalne (IPv6), ale GitHub je zaleca.
- Aktualną listę adresów IP GitHub Pages znajdziesz w dokumentacji:
  https://docs.github.com/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site

### Krok 3. Ustaw domenę w repozytorium

Na GitHubie: **repozytorium → Settings → Pages → Custom domain** → wpisz `miloszpaidads.pl` → **Save**.
GitHub sam doda do repozytorium plik `CNAME` z nazwą domeny.

Alternatywnie z terminala (w folderze projektu):

```bash
echo "miloszpaidads.pl" > CNAME && git add CNAME && git commit -m "Własna domena" && git push
```

### Krok 4. Poczekaj na DNS i włącz HTTPS

- Propagacja DNS trwa zwykle od kilku minut do kilku godzin (maksymalnie 24–48 h).
- W **Settings → Pages** pojawi się „DNS check successful". Jeśli jest błąd, sprawdź rekordy z kroku 2.
- Gdy DNS jest poprawny, zaznacz **Enforce HTTPS**. Certyfikat wystawia się automatycznie;
  jeśli opcja jest jeszcze wyszarzona, odczekaj do godziny i odśwież stronę ustawień.

Sprawdzenie z terminala:

```bash
dig +short miloszpaidads.pl A
```

powinno zwrócić cztery adresy `185.199.*.153`.

### Krok 5. (Zalecane) Zweryfikuj domenę na koncie GitHub

Zapobiega to przejęciu domeny przez obce repozytorium:
**GitHub → Settings (konta) → Pages → Add a domain** → wpisz domenę → dodaj u rejestratora
rekord `TXT` o nazwie `_github-pages-challenge-MiloszAgency` z podaną wartością → **Verify**.

### Krok 6. Po podpięciu domeny

- Stary adres `https://miloszagency.github.io/` będzie automatycznie przekierowywał na nową domenę.
- W Google Ads API Center (i wszędzie, gdzie podałeś adres firmy) zaktualizuj URL na `https://miloszpaidads.pl`.
- W `index.html` dodaj w `<head>`:

```html
<link rel="canonical" href="https://miloszpaidads.pl/">
<meta property="og:url" content="https://miloszpaidads.pl/">
```

- `www.miloszpaidads.pl` będzie przekierowywać na `miloszpaidads.pl` (dzięki rekordowi CNAME z kroku 2).

## Polityka prywatności

Strona nie zbiera danych: brak formularzy, cookies, analityki i skryptów firm trzecich.
Treść polityki jest w `index.html` w sekcji `id="polityka-prywatnosci"`
(adres: `…/#polityka-prywatnosci`). Jeśli kiedyś dodasz Google Analytics, formularz
albo piksel reklamowy, zaktualizuj tę sekcję.
