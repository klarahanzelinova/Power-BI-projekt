# Analýza prodejů maloobchodního řetězce

Interaktivní Power BI report zaměřený na vizualizaci obchodních dat nejmenované maloobchodní firmy – tržby, nákupní chování zákazníků a přehled sortimentu napříč kategoriemi a regiony.

**Autor:** Klára Hanzelínová

**Projekt vznikl pro vzdělávací účely** v rámci kurzu zaměřeného na vizualizaci dat v Power BI.

> **Poznámka k datům:** Report vychází z reálných dat nejmenované firmy, která byla pro účely tohoto projektu anonymizována s ohledem na GDPR.

## Náhled reportu
<img width="1032" height="614" alt="Úvod" src="https://github.com/user-attachments/assets/87453fa1-911e-42e6-8a7e-27ccd8ec059d" />
<img width="1032" height="583" alt="Finanční ukazatele" src="https://github.com/user-attachments/assets/e843860b-a10b-4010-b665-fd4ae172a03e" />
<img width="1032" height="582" alt="Identifikované nákupy" src="https://github.com/user-attachments/assets/0c819f63-1dbc-41de-b5ec-3a583855bcfe" />
<img width="1032" height="580" alt="Sortiment" src="https://github.com/user-attachments/assets/39e46a75-3a5c-4615-beac-ec41e5889f26" />


## O projektu

Cílem projektu je vizuálně a interaktivně zpracovat obchodní dataset tak, aby čtenáři nabídl rychlý přehled o výkonnosti firmy z několika úhlů pohledu – finančního, zákaznického i produktového. Report klade důraz na přehlednost, interaktivitu a možnost vlastní analýzy dat pomocí filtrů a průřezů.

## Klíčová zjištění
- **E-shop jednoznačně dominuje** nad kamennými prodejnami – tvoří přibližně 87 % celkového obratu
- **Regionální rozdíly jsou výrazné** – Liberecký kraj dosahuje výrazně nejvyššího obratu ze všech krajů, naopak Hlavní město Praha vykazuje nejnižší tržby i počet nákupů
- **Elektronika a Sport** jsou tahouny tržeb a společně tvoří více než polovinu obratu ze sledovaných kategorií
- **Marže se výrazně liší podle kategorie** – oblečení a obuv patří k nejziskovějším segmentům, zatímco potraviny a drogerie mají marži nejnižší
- **Prodeje vykazují sezónní vzorec** s vrcholem v letních měsících a poklesem směrem ke konci sledovaného období
- **Věková skupina zákazníka má jen omezený vliv** na výši průměrného nákupu – rozdíly mezi skupinami jsou spíše mírné

## O datech
Report zobrazuje obchodní data řetězce, který kombinuje prodej přes **e-shop** a síť **kamenných poboček** rozmístěných napříč kraji České republiky. Sortiment pokrývá širokou škálu spotřebního zboží v osmi kategoriích:

- Elektronika
- Sport
- Oblečení a obuv
- Domácnost
- Drogerie
- Potraviny
- Hračky
- Zahrada

## Datový model
Report pracuje se třemi vzájemně propojenými tabulkami ve hvězdicovém schématu:

| Tabulka | Role | Klíčové sloupce |
|---|---|---|
| **TabProdeje** | Faktová tabulka | Datum, Mnozstvi, JednotkovaCena, CelkovaCastka, Kanal, PobockaID, ProductID, CustomerID |
| **TabProdukty** | Dimenze (produkty) | ProductID, NazevProduktu, Kategorie, Podkategorie, NakupniCena, ProdejniCena, Aktivni |
| **TabZakaznici** | Dimenze (zákazníci) | CustomerID, Jmeno, Prijmeni, Kraj, Mesto, Pohlavi |

Vazby mezi tabulkami jsou typu 1:N (TabProdukty → TabProdeje, TabZakaznici → TabProdeje), vytvořené přímo v datovém modelu Power BI.

## Struktura reportu
Report obsahuje 4 stránky:

1. **Úvod** – titulní stránka s popisem reportu a navigací na jednotlivé sekce
2. **Finanční ukazatele** – přehled tržeb, plnění ročního cíle, rozdělení obratu podle kanálu a typu platby, vývoj v čase
3. **Identifikované nákupy** – nákupní chování podle kraje, pohlaví, věkové skupiny a zákaznického segmentu
4. **Přehled sortimentu** – detailní přehled produktů (marže, zisk, ceny) s rozkladem podle kategorií

## Použité vizuály
- Tabulka
- Prstencový (donut) graf
- Ukazatel (gauge)
- Kombinovaný sloupcový a spojnicový graf
- Skládaný sloupcový graf
- Decomposition tree

## Interaktivita a filtrování
- **Slicery**: rozsah data (posuvník), měsíc, pobočka, kanál, kraj, název produktu (vyhledávání), aktivita produktu
- **Hierarchie**: Kategorie → Podkategorie → Název produktu, využitá v decomposition tree
- **Záložky (bookmarks)**: uložený filtrovaný pohled pro rychlý přístup ke klíčovým datům (např. pobočka Praha)
- **Navigace**: tlačítka pro přepínání mezi stránkami reportu
- **Reset filtrů**: tlačítko pro rychlé vymazání všech aktivních průřezů na stránce
- **Podmíněné formátování**: barevné škálování marže (červená/žlutá/zelená podle výše marže) a stavové ikony u aktivních produktů

## DAX prvky
- **Kalkulovaný sloupec** `Celé jméno` (TabZakaznici) – spojuje jméno a příjmení zákazníka do jednoho pole
- **Measure** `Průměrná hodnota nákupu` (TabProdeje) – vypočtená metrika nad tabulkou prodejů

```dax
Průměrná hodnota nákupu = sum(TabProdeje[CelkovaCastka]) / [Počet nákupů]
```

## Technologie
- **Microsoft Power BI Desktop** – tvorba reportu a interaktivních vizualizací
- **Power Query** – transformace, čištění a propojení datových zdrojů
- **DAX (Data Analysis Expressions)** – tvorba measures a kalkulovaných sloupců
- **Datové modelování** – hvězdicové schéma s relacemi 1:N mezi faktovou a dimenzními tabulkami
- **Interaktivní prvky Power BI** – záložky, akce tlačítek, průřezy a hierarchie

## Jak report otevřít
Pro otevření souboru `.pbix` je potřeba mít nainstalované **Power BI Desktop** (zdarma ke stažení na [powerbi.microsoft.com](https://powerbi.microsoft.com)). Po otevření je možné report interaktivně procházet napříč všemi čtyřmi stránkami, filtrovat data pomocí průřezů a využívat připravené záložky.
