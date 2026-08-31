# World Bank Employment in Services — Ana Veri Seti Bağlam ve Kodlama Rehberi

## 1. Kimlik

- **Standart çalışma adı:** World Bank Services Employment
- **Kullanıcının yüklediği dosya:** `Employment in services.csv`
- **Kaynak:** World Development Indicators (WDI)
- **Indicator:** `Employment in services (% of total employment) (modeled ILO estimate)`
- **Indicator code:** `SL.SRV.EMPL.ZS`
- **WDI dosya içi Data Source:** `World Development Indicators`
- **Dosya içi Last Updated Date:** **2026-07-13**
- **Dosya boyutu:** 212,818 byte (~207.8 KB)
- **Data rows:** 265
- **Raw parsed columns:** 71
- **Anlamlı data columns:** 70
- **Ana dosya SHA-256:** `85901bc94aad47b224f932fe78a7baa64e8bf1bb3ed5bd711f34775a0ac8e565`
- **Bu pakette:** `World_Bank_Employment_in_services_full_unchanged.csv`
- **Kopya SHA-256:** `85901bc94aad47b224f932fe78a7baa64e8bf1bb3ed5bd711f34775a0ac8e565`
- **Byte-identical:** Evet

Dosya yaklaşık 213 KB olduğu için sample üretmek yerine **tam, değiştirilmemiş CSV'yi
doğrudan sağlamak** en doğru yaklaşımdır.

World Bank metadata'sına göre bu göstergenin kaynağı **ILO Modelled Estimates database
(ILOEST)**'tir. ILOEST, country-reported labour-market observations ile eksik veriler için
ekonometrik modellerle üretilmiş tahminleri birleştirerek uluslararası karşılaştırılabilir
seri üretir. Bu nedenle bu gösterge country-level structural proxy olarak kullanılabilir,
ancak her ülke-yıl değeri doğrudan gözlenmiş ulusal survey observation'ı gibi yorumlanmamalıdır.

## 2. Çalışmadaki rol

Bu gösterge:

> **Economic structure / service-intensity proxy**

olarak kullanılır.

Ana analytical field:

`services_employment_share_2024`

Tanım:

> total employment içindeki services-sector employment yüzdesi.

Bu değişken:
- AI adoption değildir,
- AI exposure değildir,
- workforce GenAI use değildir,
- ekonominin sektörel bileşimini temsil eden structural control'dür.

## 3. Indicator tanımı

Official World Bank code:

`SL.SRV.EMPL.ZS`

Official name:

> Employment in services (% of total employment) (modeled ILO estimate)

World Bank long definition'e göre services sector şunları kapsar:
- wholesale and retail trade,
- restaurants and hotels,
- transport/storage/communications,
- finance/insurance/real estate/business services,
- community/social/personal services,

ve ISIC revizyonuna göre ilgili services categories'i içerir.

Unit:
> percent of total employment.

Dolayısıyla:
- value `58.0` ≈ total employment'ın %58'i services'da,
- ratio 0.58 değildir,
- kişi sayısı değildir.

## 4. Modeled ILO estimate — kritik yorum kuralı

ILOEST'in amacı:
- internationally comparable labour statistics üretmek,
- missing country data'yı modellemek,
- balanced regional/global series üretmektir.

ILO, limited national information bulunan ülkelerde model estimates'ın daha yüksek
uncertainty taşıyabileceğini ve country-level analysis'te dikkatli kullanılması gerektiğini
belirtir.

Bu projede doğru kullanım:

> structural/economic composition proxy.

Yanlış kullanım:

> “2024 national labour-force survey directly observed exactly X% services employment.”

Bu claim kaynak tarafından garanti edilmez.

## 5. Neden full dosya, sample değil?

- ~207.8 KB
- 265 economy/aggregate row
- tek indicator
- wide 1960–2025 year format

Bu boyutta sample:
- aggregate-country distinction'ı eksik gösterebilir,
- historical/missingness pattern'ı parçalayabilir,
- WDI parser bağlamına ek fayda sağlamaz.

**Karar:** Full unchanged CSV doğrudan kullanılacaktır.

## 6. WDI CSV'nin fiziksel yapısı

İlk satırlar:

```text
1: "Data Source","World Development Indicators",
2: [blank]
3: "Last Updated Date","2026-07-13",
4: [blank]
5: "Country Name","Country Code","Indicator Name","Indicator Code","1960",...,"2025",
```

Pandas load:

```python
df = pd.read_csv(
    "Employment in services.csv",
    skiprows=4
)
```

`skiprows=4` uygulanmazsa data header yanlış yorumlanabilir.

## 7. Trailing blank column

Raw WDI header'da `2025` sonrasında trailing comma vardır.

Bu nedenle:
- raw parser = 71 field,
- meaningful fields = 70,
- final field adı `""`,
- tüm 265 satırda final field boş.

Raw file değiştirilmemelidir.

Pandas'ta:

```python
df = pd.read_csv("Employment in services.csv", skiprows=4)

unnamed = [c for c in df.columns if str(c).startswith("Unnamed:")]
assert len(unnamed) <= 1

if unnamed:
    assert df[unnamed[0]].isna().all()
    df = df.drop(columns=unnamed)
```

Bu yalnızca in-memory analytical cleanup'tır.

## 8. Tam raw field şeması

1. `Country Name`
2. `Country Code`
3. `Indicator Name`
4. `Indicator Code`
5. `1960`
6. `1961`
7. `1962`
8. `1963`
9. `1964`
10. `1965`
11. `1966`
12. `1967`
13. `1968`
14. `1969`
15. `1970`
16. `1971`
17. `1972`
18. `1973`
19. `1974`
20. `1975`
21. `1976`
22. `1977`
23. `1978`
24. `1979`
25. `1980`
26. `1981`
27. `1982`
28. `1983`
29. `1984`
30. `1985`
31. `1986`
32. `1987`
33. `1988`
34. `1989`
35. `1990`
36. `1991`
37. `1992`
38. `1993`
39. `1994`
40. `1995`
41. `1996`
42. `1997`
43. `1998`
44. `1999`
45. `2000`
46. `2001`
47. `2002`
48. `2003`
49. `2004`
50. `2005`
51. `2006`
52. `2007`
53. `2008`
54. `2009`
55. `2010`
56. `2011`
57. `2012`
58. `2013`
59. `2014`
60. `2015`
61. `2016`
62. `2017`
63. `2018`
64. `2019`
65. `2020`
66. `2021`
67. `2022`
68. `2023`
69. `2024`
70. `2025`
71. `(blank trailing field)`

Anlamlı yapı:
- 4 identifier
- 66 year column
- 1960–2025
- 1 blank trailing field

## 9. Grain / uniqueness

Data grain:

> `Country Code × Indicator Code`

Full extract:
- Country Code duplicate sayısı: **0**
- Distinct indicator code: `SL.SRV.EMPL.ZS`
- Indicator name: `Employment in services (% of total employment) (modeled ILO estimate)`

265 row'un tamamı sovereign country değildir.

WDI download:
- countries,
- regions,
- income groups,
- lending groups,
- other aggregates

içerebilir.

Bu nedenle explicit core-country whitelist zorunludur.

## 10. Ana 27-country örneklem

ISO3:

`AUT, BEL, BGR, HRV, CZE, DNK, EST, FIN, FRA, DEU, GRC, HUN, IRL, ITA, LVA, LTU, LUX, NLD, NOR, POL, PRT, ROU, SVK, SVN, ESP, SWE, TUR`

Core 27'nin tamamı full file'da vardır.

World Bank naming:
- `TUR` raw Country Name = `Turkiye`

Kural:
- merge key = **Country Code / ISO3**
- raw Country Name merge key değildir.

## 11. Ana yıl = 2024

Ana variable:

`services_employment_share_2024`

Temporal framing:

```text
Economic Structure 2024 → Enterprise AI Adoption 2025
```

Gerekçe:
- AI outcome'dan önce ölçülmüş structural composition,
- 27/27 coverage,
- same-year simultaneity'yi azaltır.

Bu temporal ordering causality kanıtı değildir.

## 12. Core coverage — 2019–2025

| Yıl | Coverage | Missing core ISO3 |
|---|---:|---|
| 2019 | 27/27 | Yok |
| 2020 | 27/27 | Yok |
| 2021 | 27/27 | Yok |
| 2022 | 27/27 | Yok |
| 2023 | 27/27 | Yok |
| 2024 | 27/27 | Yok |
| 2025 | 27/27 | Yok |

Core 27 için 2019–2025 eksiksizdir.

## 13. 2025 kullanımı

Full file:
- 2025 column vardır,
- core 27 coverage 27/27.

Ancak ana portfolio design:
- structural control = **2024**
- 2025 raw/supplementary.

2025 kullanmak veri availability açısından mümkün olsa da ana temporal design'ı değiştirmek
için gerekçe değildir.

## 14. 2024 sanity-check range

Parser/year alignment QA için:

- Core minimum:
  - `ROU` — Romania — 56.082720%
- Core maximum:
  - `LUX` — Luxembourg — 91.280798%

Core 2024 QA values:

- `AUT` — Austria — 72.341669
- `BEL` — Belgium — 79.467683
- `BGR` — Bulgaria — 67.025115
- `HRV` — Croatia — 68.852096
- `CZE` — Czechia — 61.851669
- `DNK` — Denmark — 79.330803
- `EST` — Estonia — 70.478745
- `FIN` — Finland — 75.457254
- `FRA` — France — 78.065015
- `DEU` — Germany — 72.616424
- `GRC` — Greece — 72.656677
- `HUN` — Hungary — 64.944193
- `IRL` — Ireland — 77.594764
- `ITA` — Italy — 69.890478
- `LVA` — Latvia — 71.097735
- `LTU` — Lithuania — 69.165590
- `LUX` — Luxembourg — 91.280798
- `NLD` — Netherlands — 84.232713
- `NOR` — Norway — 79.376217
- `POL` — Poland — 63.297809
- `PRT` — Portugal — 72.380988
- `ROU` — Romania — 56.082720
- `SVK` — Slovak Republic — 62.808395
- `SVN` — Slovenia — 64.171392
- `ESP` — Spain — 76.435075
- `SWE` — Sweden — 81.166619
- `TUR` — Turkiye — 58.079946

Bu liste final consulting finding değildir; local parser/year alignment kontrolüdür.

## 15. Analytical extraction

```python
import pandas as pd

df = pd.read_csv(
    "Employment in services.csv",
    skiprows=4
)

# Optional all-null trailing field cleanup
unnamed = [c for c in df.columns if str(c).startswith("Unnamed:")]
if unnamed:
    assert len(unnamed) == 1
    assert df[unnamed[0]].isna().all()
    df = df.drop(columns=unnamed)

core_27 = ['AUT', 'BEL', 'BGR', 'HRV', 'CZE', 'DNK', 'EST', 'FIN', 'FRA', 'DEU', 'GRC', 'HUN', 'IRL', 'ITA', 'LVA', 'LTU', 'LUX', 'NLD', 'NOR', 'POL', 'PRT', 'ROU', 'SVK', 'SVN', 'ESP', 'SWE', 'TUR']

services = df[
    (df["Indicator Code"] == "SL.SRV.EMPL.ZS")
    & (df["Country Code"].isin(core_27))
][["Country Name","Country Code","2024","2025"]].copy()

services["2024"] = pd.to_numeric(
    services["2024"],
    errors="raise"
)

services["2025"] = pd.to_numeric(
    services["2025"],
    errors="raise"
)

services = services.rename(columns={
    "2024": "services_employment_share_2024",
    "2025": "services_employment_share_2025"
})
```

Bu variable yüzde olduğu için log transform varsayılan olarak uygulanmaz.

## 16. Aggregate rows — explicit filtering

Yanlış:

```python
df[df["2024"].notna()]
```

Bu aggregate rows'u bırakır.

Doğru:

```python
df[
    df["Country Code"].isin(core_27)
]
```

Core whitelist source-of-truth'tur.

## 17. Missing-data kuralı

Full global historical file'da blank year-cells bulunabilir.

Core 2019–2025:
- missing yok.

Kural:
- blank = 0 değil,
- forward-fill yok,
- interpolation yok,
- automatic nearest-year substitution yok.

Core 2024 missing çıkarsa source/version/parsing problem'i araştırılmalıdır.

## 18. Numeric parsing

Nonblank year-cell numeric parse failure:
- **0**

Production code'da:

```python
pd.to_numeric(..., errors="raise")
```

kullanılması önerilir.

## 19. Merge kuralı

Primary key:
- `Country Code`

Canonical master:
- `Country Code` → `iso3`

Örnek:
- raw: `TUR`, `Turkiye`
- display: `TUR`, `Türkiye`

Names standardization raw file'a uygulanmamalıdır; derived/master layer'da yapılır.

## 20. Model kullanım kuralı

Bu değişken H3 / economic structure testinde kullanılır.

Aday model:

```text
AI_2025 =
β0
+ β1 ServicesShare_2024
+ β2 logGDPpc_2024
+ ε
```

Ancak suitability diagnostics daha önce:
- services ↔ tertiary attainment ≈ yüksek,
- services ↔ GDPpc ≈ yüksek

ilişki göstermiştir.

Dolayısıyla:
- VIF/correlation kontrolü,
- parsimonious model,
- kitchen-sink regression'dan kaçınma

zorunludur.

## 21. Indicator transformation kuralı

Bu variable zaten yüzde:

`services_employment_share_2024`

Default:
- log transform YOK.
- z-standardization regression coefficient comparison amacıyla uygulanabilir.

Z-score yapılacaksa:
- yalnızca core 27 sample üzerinde,
- OECD/region aggregates hariç,
- sample SD açıkça tanımlı.

## 22. Modeled-estimate sensitivity / wording

Bu indicator için standard report wording:

> “ILO modelled estimate of the share of total employment in services.”

Kaçınılacak:

> “Observed national share of workers in services.”

ILOEST uncertainty country-by-country aynı değildir.

Bu çalışmada variable:
- structural control,
- directional interpretation

içindir; hassas causal estimate değildir.

## 23. Versioning

Current raw:
- update date = `2026-07-13`
- SHA-256 = `85901bc94aad47b224f932fe78a7baa64e8bf1bb3ed5bd711f34775a0ac8e565`

Yeni WDI file gelirse:
- current raw overwrite edilmez,
- separate version saklanır,
- update date/hash kaydedilir.

Önerilen archive alias:

`wb_services_employment_2026-07-13_raw.csv`

## 24. Local production QA

```python
df_raw = pd.read_csv(
    "Employment in services.csv",
    skiprows=4
)

assert df_raw.shape[0] == 265
assert "Country Name" in df_raw.columns
assert "Country Code" in df_raw.columns
assert "Indicator Code" in df_raw.columns
assert "2024" in df_raw.columns
assert "2025" in df_raw.columns

assert df_raw["Indicator Code"].nunique() == 1
assert df_raw["Indicator Code"].iloc[0] == "SL.SRV.EMPL.ZS"
assert df_raw["Country Code"].nunique() == 265
```

Core:

```python
core = df_raw[
    df_raw["Country Code"].isin(core_27)
].copy()

assert len(core) == 27
assert core["Country Code"].nunique() == 27
assert core["2024"].notna().all()
assert core["2025"].notna().all()

core["2024"] = pd.to_numeric(
    core["2024"],
    errors="raise"
)

assert core["2024"].between(0,100).all()
```

Türkiye:

```python
assert core.loc[
    core["Country Code"].eq("TUR"),
    "Country Name"
].iloc[0] == "Turkiye"
```

## 25. AI/model'e yüklerken önerilen açıklama

> `World_Bank_Employment_in_services_full_unchanged.csv`, localde kullanılan
> `Employment in services.csv` WDI download'unun byte-identical tam kopyasıdır; sample
> değildir. Dosya World Bank indicator `SL.SRV.EMPL.ZS = Employment in services
> (% of total employment) (modeled ILO estimate)` serisini içerir. İlk 4 satır WDI
> metadata/preamble olduğu için pandas'ta `skiprows=4` kullan. Raw header'da trailing comma
> nedeniyle all-null bir `Unnamed` field oluşabilir; yalnızca explicit QA sonrasında
> in-memory dataframe'den düşür. Ana portfolio variable 27 core ISO3 için 2024 value'dur:
> `services_employment_share_2024`. Core 2019–2025 coverage 27/27'dir. Full file
> region/income-group aggregates içerir; explicit core ISO3 whitelist kullan ve merge'i
> Country Code üzerinden yap. Bu gösterge ILO Modelled Estimates database'den gelir:
> country-level direct observation gibi yorumlama; structural/economic-composition proxy
> olarak kullan. Missing historical cells'i 0/forward-fill/interpolate etme.

## 26. Kullanım sınırı

Bu full CSV doğrudan yeterlidir:
- WDI schema/parser,
- 2024/2025 extraction,
- country master merge,
- final structural-control preparation,
- version/hash QA.

Ek sample gerekli değildir.
