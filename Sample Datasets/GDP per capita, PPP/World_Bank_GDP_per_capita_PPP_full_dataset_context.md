# World Bank GDP per capita, PPP — Ana Veri Seti Bağlam ve Kodlama Rehberi

## 1. Kimlik

- **Standart çalışma adı:** World Bank GDP per capita PPP
- **Kullanıcının yüklediği dosya:** `GDP per capita, PPP.csv`
- **Kaynak:** World Development Indicators (WDI)
- **Indicator:** `GDP per capita, PPP (constant 2021 international $)`
- **Indicator code:** `NY.GDP.PCAP.PP.KD`
- **Dosya içi Data Source:** `World Development Indicators`
- **Dosya içi Last Updated Date:** **2026-07-13**
- **Dosya boyutu:** 216,352 byte (~211.3 KB)
- **Data rows:** 265
- **Raw parsed columns:** 71
- **Anlamlı data columns:** 70
- **Ana dosya SHA-256:** `c24950a2cc57e381656c5446c01f8f9ca76cbfe7c15c68111f9356d4b7566605`
- **Bu pakette:** `World_Bank_GDP_per_capita_PPP_full_unchanged.csv`
- **Kopya SHA-256:** `c24950a2cc57e381656c5446c01f8f9ca76cbfe7c15c68111f9356d4b7566605`
- **Byte-identical:** Evet

Dosya yalnızca yaklaşık 216 KB olduğu için sample üretmek yerine **tam, değiştirilmemiş
CSV'yi doğrudan sağlamak** en doğru yaklaşımdır.

World Bank WDI metadata'sına göre bu gösterge kişi başına GDP'yi purchasing power parity
(PPP) ile dönüştürülmüş **constant 2021 international dollars** cinsinden ölçer. PPP
ülkeler arasındaki fiyat düzeyi farklarını hesaba katar; constant-price ifade ise zaman
içindeki fiyat değişimlerini 2021 referans fiyatlarıyla düzeltir.

## 2. Çalışmadaki rol

Bu gösterge:

> **Economic development / general prosperity control**

olarak kullanılır.

Ana raw analytical field:

`gdp_per_capita_ppp_2024`

Ana regression field:

`log_gdp_per_capita_ppp_2024`

Formül:

```python
log_gdp_per_capita_ppp_2024 = np.log(gdp_per_capita_ppp_2024)
```

Bu değişken:
- productivity outcome değildir,
- AI readiness'in kendisi değildir,
- general development control'dür.

## 3. Neden full dosya, sample değil?

- ~211.3 KB
- 265 economy/aggregate satırı
- tek indicator
- wide 1960–2025 year yapısı

Bu boyutta sample oluşturmak, country/aggregate ayrımını ve WDI wide formatını eksik
gösterebilir.

**Karar:** Full unchanged CSV doğrudan kullanılacaktır.

## 4. WDI CSV'nin fiziksel yapısı — kritik

Dosyanın ilk satırları:

```text
1: "Data Source","World Development Indicators",
2: [blank]
3: "Last Updated Date","2026-07-13",
4: [blank]
5: "Country Name","Country Code","Indicator Name","Indicator Code","1960",...,"2025",
```

Yani actual data header 5. satırdadır.

Pandas:

```python
df = pd.read_csv(
    "GDP per capita, PPP.csv",
    skiprows=4
)
```

## 5. Trailing blank column — raw format özelliği

Header satırında `2025` sonrasında **trailing comma** vardır.

Bu nedenle:
- raw CSV parser 71 field görür,
- 70 field anlamlıdır,
- son field adı boş string `""`,
- bu boş trailing field'in 265 satırın tamamındaki değeri de boştur.

Raw dosya **değiştirilmemelidir**.

Pandas çoğu durumda bu alanı `Unnamed: 70` benzeri adla okuyabilir.

Local code'da ancak explicit QA sonrasında düşürün:

```python
df = pd.read_csv("GDP per capita, PPP.csv", skiprows=4)

unnamed = [c for c in df.columns if str(c).startswith("Unnamed:")]
assert len(unnamed) <= 1

if unnamed:
    assert df[unnamed[0]].isna().all()
    df = df.drop(columns=unnamed)
```

Bu işlem raw dosyayı değil yalnızca in-memory analytical dataframe'i etkiler.

## 6. Tam raw field şeması

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
- 4 identifier field
- 66 annual year field
- 1960–2025
- 1 boş trailing field

## 7. Grain / uniqueness

Data grain:

> `Country Code × Indicator Code`

Bu extract'te:
- Country Code duplicate sayısı: **0**
- Distinct Indicator Code: `NY.GDP.PCAP.PP.KD`
- Tek indicator name: `GDP per capita, PPP (constant 2021 international $)`

265 satırın tamamı sovereign country değildir. WDI bulk downloads:
- regions,
- income groups,
- lending groups,
- other aggregates

da içerebilir.

Bu nedenle 265 satır = 265 ülke diye yorumlanmamalıdır.

## 8. Indicator tanımı

Official code:

`NY.GDP.PCAP.PP.KD`

Official name:

> GDP per capita, PPP (constant 2021 international $)

Interpretation:
- GDP per person,
- PPP conversion,
- constant 2021 international dollars.

Karıştırılmaması gereken benzer seri:

`NY.GDP.PCAP.PP.CD`
= GDP per capita, PPP **current** international dollars.

Bu projede **KD / constant 2021** seri kullanılacaktır.

## 9. Ana 27-country örneklem

ISO3:

`AUT, BEL, BGR, HRV, CZE, DNK, EST, FIN, FRA, DEU, GRC, HUN, IRL, ITA, LVA, LTU, LUX, NLD, NOR, POL, PRT, ROU, SVK, SVN, ESP, SWE, TUR`

27 ülkenin tamamı bu file'da vardır.

World Bank naming farkı:
- `TUR` row label = `Turkiye`

Kural:
- merge `Country Name` ile değil,
- **Country Code / ISO3** ile yapılır.

Display layer'da sonradan `Türkiye` kullanılabilir; raw label değiştirilmemelidir.

## 10. Ana yıl = 2024

Temporal framing:

```text
Economic Development 2024 → Enterprise AI Adoption 2025
```

Raw:
`gdp_per_capita_ppp_2024`

Model:
`log_gdp_per_capita_ppp_2024`

2024 seçiminin nedeni:
- 27/27 coverage,
- AI 2025'ten önce ölçülmüş development level,
- same-year simultaneity'yi azaltır.

Bu causality kanıtı değildir.

## 11. Core coverage — 2019–2025

| Yıl | Coverage | Missing core ISO3 |
|---|---:|---|
| 2019 | 27/27 | Yok |
| 2020 | 27/27 | Yok |
| 2021 | 27/27 | Yok |
| 2022 | 27/27 | Yok |
| 2023 | 27/27 | Yok |
| 2024 | 27/27 | Yok |
| 2025 | 27/27 | Yok |

2019–2025 boyunca core 27'nin tamamı eksiksizdir.

## 12. 2025 coverage ile World Bank web sayfası arasındaki olası fark

World Bank public indicator page'in bazı web snapshot/crawl'ları `1990–2024` şeklinde
görünebilir. Bununla birlikte kullanıcının yüklediği WDI CSV:

- `Last Updated Date = 2026-07-13`
- 2025 sütununa sahip
- core 27'nin tamamında 2025 value içeriyor.

Bu nedenle:
- **indicator definition** için official World Bank metadata,
- **actual file coverage/version** için yüklenen CSV

source of truth olarak kullanılmalıdır.

Ana model yine 2024 kullanır.

## 13. Natural-log transform

Regression'da:

```python
x["log_gdp_per_capita_ppp_2024"] = np.log(
    x["gdp_per_capita_ppp_2024"]
)
```

kullanılır.

Gerekçe:
- GDPpc dağılımı sağa çarpık,
- yüksek-income observations leverage yaratabilir,
- log scale relative development differences'ı daha stabil temsil eder.

Önce:

```python
assert (x["gdp_per_capita_ppp_2024"] > 0).all()
```

kontrol edilmelidir.

## 14. 2024 parser/year-alignment sanity check

Core minimum:
- `BGR` — Bulgaria — 34,221.387

Core maximum:
- `LUX` — Luxembourg — 128,475.284

Tüm core 2024 QA values:

- `AUT` — Austria — 63,787.989
- `BEL` — Belgium — 63,311.277
- `BGR` — Bulgaria — 34,221.387
- `HRV` — Croatia — 42,828.800
- `CZE` — Czechia — 47,972.532
- `DNK` — Denmark — 71,034.579
- `EST` — Estonia — 41,185.835
- `FIN` — Finland — 55,901.320
- `FRA` — France — 54,799.348
- `DEU` — Germany — 62,654.602
- `GRC` — Greece — 37,474.280
- `HUN` — Hungary — 40,747.199
- `IRL` — Ireland — 118,833.312
- `ITA` — Italy — 53,284.875
- `LVA` — Latvia — 37,615.076
- `LTU` — Lithuania — 47,462.004
- `LUX` — Luxembourg — 128,475.284
- `NLD` — Netherlands — 70,493.905
- `NOR` — Norway — 94,803.670
- `POL` — Poland — 45,153.044
- `PRT` — Portugal — 42,228.158
- `ROU` — Romania — 40,503.832
- `SVK` — Slovak Republic — 40,302.451
- `SVN` — Slovenia — 48,658.027
- `ESP` — Spain — 48,460.291
- `SWE` — Sweden — 62,558.407
- `TUR` — Turkiye — 36,154.490

Bu liste final finding değil, **local parser/year alignment QA** referansıdır.

## 15. Analytical extraction — önerilen kod

```python
import numpy as np
import pandas as pd

df = pd.read_csv("GDP per capita, PPP.csv", skiprows=4)

# WDI trailing blank field cleanup — explicit QA sonrası
unnamed = [c for c in df.columns if str(c).startswith("Unnamed:")]
if unnamed:
    assert len(unnamed) == 1
    assert df[unnamed[0]].isna().all()
    df = df.drop(columns=unnamed)

core_27 = ['AUT', 'BEL', 'BGR', 'HRV', 'CZE', 'DNK', 'EST', 'FIN', 'FRA', 'DEU', 'GRC', 'HUN', 'IRL', 'ITA', 'LVA', 'LTU', 'LUX', 'NLD', 'NOR', 'POL', 'PRT', 'ROU', 'SVK', 'SVN', 'ESP', 'SWE', 'TUR']

gdp = df[
    (df["Indicator Code"] == "NY.GDP.PCAP.PP.KD")
    & (df["Country Code"].isin(core_27))
][["Country Name","Country Code","2024","2025"]].copy()

gdp["2024"] = pd.to_numeric(gdp["2024"], errors="raise")
gdp["2025"] = pd.to_numeric(gdp["2025"], errors="raise")

gdp = gdp.rename(columns={
    "2024": "gdp_per_capita_ppp_2024",
    "2025": "gdp_per_capita_ppp_2025",
})

gdp["log_gdp_per_capita_ppp_2024"] = np.log(
    gdp["gdp_per_capita_ppp_2024"]
)
```

## 16. Aggregate filtering — zorunlu

Full file aggregate rows içerdiği için:

```python
df[df["Country Code"].isin(core_27)]
```

gibi explicit whitelist kullanılmalıdır.

Aşağıdaki gibi bir yaklaşım güvenli değildir:

```python
df.dropna(subset=["2024"])
```

çünkü bu aggregate rows'u da bırakır.

## 17. Missing-data kuralı

Global historical file'da çok sayıda blank year-cell olabilir.

Core 2019–2025:
- missing yok.

Kural:
- blank = 0 değil,
- forward fill yok,
- interpolation yok,
- otomatik nearest-year fallback yok.

Core 2024 missing çıkarsa production code durmalı ve version/file issue araştırılmalıdır.

## 18. Numeric parsing

Nonblank year-cell numeric parse failure:
- **0**

Production code'da gerekli year columns için:

```python
pd.to_numeric(..., errors="raise")
```

tercih edilmesi unexpected format'ı erken yakalar.

## 19. Merge / country map

Primary key:
- `Country Code`

Master:
- `Country Code` → `iso3`

Örnek:
- raw `TUR`, `Turkiye`
- canonical `TUR`, `Türkiye`

Name mismatch merge failure yaratmamalıdır.

## 20. Model kullanım kuralı

Bu variable:
- Digital Foundation modelinde development control,
- Economic Structure modelinde development control,
- Integrated Readiness modelinde development control

olabilir.

Small sample nedeniyle:
- GDPpc,
- services share,
- tertiary attainment

aynı kitchen-sink regression'a otomatik doldurulmamalıdır.

Correlation matrix + VIF kullanılmalıdır.

## 21. Productivity model uyarısı

GDP per capita PPP:
> general economic development

GDP/hour:
> labour productivity

Productivity outcome modeline GDPpc'yi otomatik eklemek conceptual overlap / over-control
yaratabilir.

Bu nedenle productivity regressions ayrı tasarım kuralına tabidir.

## 22. Versioning

Current file:
- `Last Updated Date = 2026-07-13`
- SHA-256 = `c24950a2cc57e381656c5446c01f8f9ca76cbfe7c15c68111f9356d4b7566605`

Yeni WDI download gelirse:
- overwrite etme,
- ayrı version sakla,
- update date + hash kaydet.

Önerilen archive alias:

`wb_gdppc_ppp_2026-07-13_raw.csv`

Alias değiştirmek raw content'i değiştirmek anlamına gelmez.

## 23. Local production QA

```python
df_raw = pd.read_csv("GDP per capita, PPP.csv", skiprows=4)

assert df_raw.shape[0] == 265
assert "Country Name" in df_raw.columns
assert "Country Code" in df_raw.columns
assert "Indicator Code" in df_raw.columns
assert "1960" in df_raw.columns
assert "2024" in df_raw.columns
assert "2025" in df_raw.columns

assert df_raw["Indicator Code"].nunique() == 1
assert df_raw["Indicator Code"].iloc[0] == "NY.GDP.PCAP.PP.KD"
assert df_raw["Country Code"].nunique() == 265
```

Core:

```python
core = df_raw[df_raw["Country Code"].isin(core_27)].copy()

assert len(core) == 27
assert core["Country Code"].nunique() == 27
assert core["2024"].notna().all()
assert core["2025"].notna().all()

core["2024"] = pd.to_numeric(core["2024"], errors="raise")
assert (core["2024"] > 0).all()
```

Türkiye:

```python
assert core.loc[
    core["Country Code"].eq("TUR"),
    "Country Name"
].iloc[0] == "Turkiye"
```

## 24. AI/model'e yüklerken önerilen açıklama

> `World_Bank_GDP_per_capita_PPP_full_unchanged.csv`, localde kullanılan
> `GDP per capita, PPP.csv` WDI download'unun byte-identical tam kopyasıdır; sample
> değildir. Dosyanın ilk dört satırı WDI metadata/preamble'dır; data header 5. satırdadır,
> dolayısıyla pandas'ta `skiprows=4` kullan. Raw header'da trailing comma nedeniyle tamamı
> boş ek bir field/`Unnamed` column oluşabilir; raw dosyayı değiştirme, yalnızca explicit
> all-null QA sonrasında in-memory dataframe'den düşür. Indicator
> `NY.GDP.PCAP.PP.KD = GDP per capita, PPP (constant 2021 international $)`'dır. Ana
> portfolio değişkeni 27 core ISO3 için 2024 value'dur ve regression'da natural log
> kullanılır. Core 2019–2025 coverage 27/27'dir. Full file country dışı aggregate rows da
> içerir; explicit `Country Code in core_27` filtresi kullan. Merge'i country name ile
> yapma; `TUR` raw label'ı `Turkiye`'dir. Missing historical cells'i zero/forward-fill/
> interpolate etme.

## 25. Kullanım sınırı

Bu full CSV doğrudan yeterlidir:
- schema / WDI parser,
- 2024/2025 extraction,
- log transformation,
- master merge,
- final regression input preparation,
- version/hash QA.

Ek sample gerekli değildir.
