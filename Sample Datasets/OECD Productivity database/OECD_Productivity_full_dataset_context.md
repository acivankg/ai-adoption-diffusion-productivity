# OECD Productivity Database — 3.366 Satırlık Güncel Extract
## Ana Veri Seti Bağlam ve Kodlama Rehberi

## 1. Kimlik

- **Standart çalışma adı:** OECD Productivity Database — current 3,366-row extract
- **Kullanıcının yüklediği dosya:** `OECD Productivity database.csv`
- **Bu rehberde değerlendirilen tek Productivity dosyası:** **3.366 satır × 34 sütun**
- **Upload/file ID:** `file_00000000931882108803be75538772c9`
- **Resmî OECD dataflow:** `OECD.SDD.TPS:DSD_PDB@DF_PDB(2.0)`
- **Resmî veri seti:** *Productivity database*
- **Frequency:** Annual
- **Ana extract SHA-256:** `98d60ede601214a05e64a7b6c0c16a1bc8189517395010b78a2715ef7bd1c48a`
- **Structure sample:** 153 satır × 34 sütun
- **Sample SHA-256:** `a30939d7323e2d46d8763e5a7bda8a8a34fe99af10f3651364ec79d79fe2a28e`

**Önemli kapsam notu:** Bu belge ve sample yalnızca bu 3.366 satırlık güncel extract'i
tanımlar. Daha önce indirilen başka bir OECD Productivity extract'i bu paketin kapsamına
dahil değildir ve burada hiçbir varsayım ona dayandırılmaz.

OECD'nin güncel Data Explorer açıklamasına göre `DSD_PDB@DF_PDB` veri tabanı önceki
productivity levels, growth rates ve industry productivity veri setlerini konsolide eden
güncel Productivity Database'dir. Veriler rolling basis'te güncellenir. OECD Data Explorer
20 Ağustos 2026 güncelleme tarihini göstermektedir.

## 2. Bu sample'ın amacı

`OECD_Productivity_3366_unchanged_structure_sample.csv` **final analiz sample'ı değildir**.

Amaç:
1. Local bilgisayardaki tam 3.366 × 34 CSV'nin gerçek şemasını modele göstermek,
2. sektör, unit, transformation, conversion ve observation-status kombinasyonlarını doğru
   tanıtmak,
3. full CSV üzerinde çalışacak Python/R filtreleme ve QA kodunu smoke-test etmek,
4. özellikle national-currency level ile growth-rate gözlemlerinin karıştırılmasını
   önlemektir.

### Değişmezlik garantisi

- Ana dosyanın **34 sütununun tamamı aynı isim ve sırayla** sample'dadır.
- Yeni sütun eklenmemiştir.
- Rename, recode, normalization, rounding veya value transformation yapılmamıştır.
- Sample'daki her veri satırı ana CSV'den **byte-for-byte aynı fiziksel CSV satırı**
  olarak kopyalanmıştır.
- Ana CSV değiştirilmemiştir.
- Sample istatistiksel olarak representative değildir.

## 3. Sample seçme yöntemi

Sample structure/code coverage için seçilmiştir.

Her mevcut benzersiz:

`ACTIVITY × UNIT_MEASURE × TRANSFORMATION × CONVERSION_TYPE × TIME_PERIOD × OBS_STATUS`

kombinasyonundan en az bir gerçek satır alınmıştır.

Ek olarak:
- full extract'teki **29 reference area'nın tamamı** en az bir kez sample'dadır;
- her activity için mevcutsa açık bir `2024 + GY` örneği sample'a eklenmiştir.

Sonuç:
- Full: 3.366 × 34
- Sample: **153 × 34**

Sample üzerinden country ranking, ortalama, korelasyon, regression veya coverage sonucu
üretmeyin; final hesaplar local full CSV üzerinde çalıştırılmalıdır.

## 4. Tam sütun şeması

1. `STRUCTURE`
2. `STRUCTURE_ID`
3. `STRUCTURE_NAME`
4. `ACTION`
5. `REF_AREA`
6. `Reference area`
7. `FREQ`
8. `Frequency of observation`
9. `MEASURE`
10. `Measure`
11. `ACTIVITY`
12. `Economic activity`
13. `UNIT_MEASURE`
14. `Unit of measure`
15. `PRICE_BASE`
16. `Price base`
17. `TRANSFORMATION`
18. `Transformation`
19. `ASSET_CODE`
20. `Asset type`
21. `CONVERSION_TYPE`
22. `Conversion type`
23. `TIME_PERIOD`
24. `Time period`
25. `OBS_VALUE`
26. `Observation value`
27. `OBS_STATUS`
28. `Observation status`
29. `UNIT_MULT`
30. `Unit multiplier`
31. `BASE_PER`
32. `Base period`
33. `DECIMALS`
34. `Decimals`

## 5. Veri grain'i

Expected unique observation grain:

`REF_AREA × FREQ × MEASURE × ACTIVITY × UNIT_MEASURE × PRICE_BASE × TRANSFORMATION × ASSET_CODE × CONVERSION_TYPE × TIME_PERIOD`

Full extract'te bu grain üzerinde duplicate sayısı: **0**.

Primary code columns:
- `REF_AREA`
- `FREQ`
- `MEASURE`
- `ACTIVITY`
- `UNIT_MEASURE`
- `PRICE_BASE`
- `TRANSFORMATION`
- `ASSET_CODE`
- `CONVERSION_TYPE`
- `TIME_PERIOD`

Value:
- `OBS_VALUE`

Quality:
- `OBS_STATUS`

Production filtering/merge'de descriptive label yerine code columns tercih edilmelidir.

## 6. Full extract'in kesin yapısı

### Measure — tek değer

- `GVAHRS` — Gross value added per hour worked

Bu 3.366 satırlık extract'te `GDPHRS` **yoktur**.

### Price base — tek değer

- `LR` — Chain linked volume (rebased)

### Asset type — tek değer

- `_Z` — Not applicable

### Reference area — 29 değer

- `AUT` — Austria
- `BEL` — Belgium
- `BGR` — Bulgaria
- `CZE` — Czechia
- `DEU` — Germany
- `DNK` — Denmark
- `ESP` — Spain
- `EST` — Estonia
- `EU27_2020` — European Union (27 countries from 01/02/2020)
- `FIN` — Finland
- `FRA` — France
- `GRC` — Greece
- `HRV` — Croatia
- `HUN` — Hungary
- `IRL` — Ireland
- `ITA` — Italy
- `LTU` — Lithuania
- `LUX` — Luxembourg
- `LVA` — Latvia
- `NLD` — Netherlands
- `NOR` — Norway
- `OECD` — OECD
- `POL` — Poland
- `PRT` — Portugal
- `ROU` — Romania
- `SVK` — Slovak Republic
- `SVN` — Slovenia
- `SWE` — Sweden
- `TUR` — Türkiye

Yapı:
- 27 ana ülke
- `EU27_2020`
- `OECD`

`EU27_2020` ve `OECD` yalnızca benchmark olabilir; regression observation değildir.

### Economic activity — 9 değer

- `C` — Manufacturing — 324 satır
- `F` — Construction — 324 satır
- `H` — Transportation and storage — 324 satır
- `I` — Accommodation and food service activities — 324 satır
- `J` — Information and communication — 324 satır
- `L` — Real estate activities — 322 satır
- `M` — Professional, scientific and technical activities — 324 satır
- `N` — Administrative and support service activities — 324 satır
- `_T` — Total - all activities — 776 satır

### Unit of measure

- `USD_PPP_H` — US dollars per hour, PPP converted — 394 satır
- `XDC_H` — National currency per hour — 2,972 satır

### Transformation

- `GY` — Growth rate, over 1 year — 1,683 satır
- `N` — Non transformed data — 1,683 satır

### Conversion type

- `PPP` — PPP converted — 394 satır
- `_Z` — Not applicable — 2,972 satır

### Time period

- `2019` — 546 satır
- `2020` — 546 satır
- `2021` — 546 satır
- `2022` — 542 satır
- `2023` — 540 satır
- `2024` — 526 satır
- `2025` — 120 satır

### Observation status

- `A` — Normal value — 3,362 satır
- `E` — Estimated value — 4 satır

### Missingness / numeric

- Blank `OBS_VALUE`: **0**
- Nonblank `OBS_VALUE` numeric parse failure: **0**
- Bu extract içinde observation-value missingness yoktur.

## 7. Unit × activity yapısı — EN KRİTİK KURAL

### Sektör satırları (`ACTIVITY != "_T"`)

Full extract'te tüm sektör satırları:

- `UNIT_MEASURE = XDC_H` — National currency per hour
- `CONVERSION_TYPE = _Z` — Not applicable
- `PRICE_BASE = LR`

Bu yapı için hem:
- `N` — Non transformed data
- `GY` — Growth rate, over 1 year

bulunur.

### Total (`ACTIVITY = "_T"`) satırları

Total satırlarında hem:
- `XDC_H` + `_Z`
- `USD_PPP_H` + `PPP`

kombinasyonları vardır.

Bu nedenle `Unit of measure` ve `Conversion type` filtrelerinin boş bırakılması yanlışlık
değildir; OECD uygun seri kombinasyonlarını birlikte döndürmüştür.

## 8. `N` ile `GY` birbirine karıştırılmamalıdır

### `TRANSFORMATION = N`

Observation:
> real GVA per hour worked level

Sector rows'da birim:
> national currency per hour

### `TRANSFORMATION = GY`

Observation:
> **annual percentage growth in real GVA per hour worked**

CSV'de unit label hâlâ `National currency per hour` görünebilir. Ancak `GY` satırının
yorumunu transformation dimension belirler.

**Kural:** `GY` value'larını national-currency level olarak yorumlamayın.

## 9. Cross-country sector comparison

National-currency sector levels ülkeler arasında doğrudan karşılaştırılamaz.

### YAPMA

```text
Austria Manufacturing GVA/hour level
vs
Romania Manufacturing GVA/hour level
```

çünkü para birimleri farklıdır.

### YAP

```text
Annual percentage change in GVA per hour worked
TRANSFORMATION = GY
```

OECD Compendium of Productivity Indicators 2026 da sektör karşılaştırmasını **annual
percentage change in GVA per hour worked** olarak sunar.

## 10. Çalışmanın ana sector productivity outcome'u

Ana portfolio sample:

`AUT, BEL, BGR, HRV, CZE, DNK, EST, FIN, FRA, DEU, GRC, HUN, IRL, ITA, LVA, LTU, LUX, NLD, NOR, POL, PRT, ROU, SVK, SVN, ESP, SWE, TUR`

Ana sector codes:

- `C` — Manufacturing
- `F` — Construction
- `H` — Transportation and storage
- `I` — Accommodation and food service activities
- `J` — Information and communication
- `M` — Professional, scientific and technical activities
- `N` — Administrative and support service activities

Local full CSV filtreleri:

```python
sector_prod_2024 = df[
    (df["REF_AREA"].isin(core_27)) &
    (df["MEASURE"] == "GVAHRS") &
    (df["ACTIVITY"].isin(["C","F","H","I","J","M","N"])) &
    (df["UNIT_MEASURE"] == "XDC_H") &
    (df["PRICE_BASE"] == "LR") &
    (df["TRANSFORMATION"] == "GY") &
    (df["ASSET_CODE"] == "_Z") &
    (df["CONVERSION_TYPE"] == "_Z") &
    (df["TIME_PERIOD"].astype(str) == "2024")
]
```

## 11. Ana sector coverage

| Code | Sector | 2024 | 2024 missing | 2025 | 2025 missing |
|---|---|---:|---|---:|---|
| `C` | Manufacturing | 26/27 | TUR | 1/27 | AUT, BEL, BGR, CZE, DEU, DNK, ESP, EST, FIN, FRA, GRC, HRV, HUN, IRL, ITA, LTU, LUX, LVA, NLD, POL, PRT, ROU, SVK, SVN, SWE, TUR |
| `F` | Construction | 26/27 | TUR | 1/27 | AUT, BEL, BGR, CZE, DEU, DNK, ESP, EST, FIN, FRA, GRC, HRV, HUN, IRL, ITA, LTU, LUX, LVA, NLD, POL, PRT, ROU, SVK, SVN, SWE, TUR |
| `H` | Transportation and storage | 26/27 | TUR | 1/27 | AUT, BEL, BGR, CZE, DEU, DNK, ESP, EST, FIN, FRA, GRC, HRV, HUN, IRL, ITA, LTU, LUX, LVA, NLD, POL, PRT, ROU, SVK, SVN, SWE, TUR |
| `I` | Accommodation and food service activities | 26/27 | TUR | 1/27 | AUT, BEL, BGR, CZE, DEU, DNK, ESP, EST, FIN, FRA, GRC, HRV, HUN, IRL, ITA, LTU, LUX, LVA, NLD, POL, PRT, ROU, SVK, SVN, SWE, TUR |
| `J` | Information and communication | 26/27 | TUR | 1/27 | AUT, BEL, BGR, CZE, DEU, DNK, ESP, EST, FIN, FRA, GRC, HRV, HUN, IRL, ITA, LTU, LUX, LVA, NLD, POL, PRT, ROU, SVK, SVN, SWE, TUR |
| `M` | Professional, scientific and technical activities | 26/27 | TUR | 1/27 | AUT, BEL, BGR, CZE, DEU, DNK, ESP, EST, FIN, FRA, GRC, HRV, HUN, IRL, ITA, LTU, LUX, LVA, NLD, POL, PRT, ROU, SVK, SVN, SWE, TUR |
| `N` | Administrative and support service activities | 26/27 | TUR | 1/27 | AUT, BEL, BGR, CZE, DEU, DNK, ESP, EST, FIN, FRA, GRC, HRV, HUN, IRL, ITA, LTU, LUX, LVA, NLD, POL, PRT, ROU, SVK, SVN, SWE, TUR |
| `L` | Real estate activities | 26/27 | TUR | 1/27 | AUT, BEL, BGR, CZE, DEU, DNK, ESP, EST, FIN, FRA, GRC, HRV, HUN, IRL, ITA, LTU, LUX, LVA, NLD, POL, PRT, ROU, SVK, SVN, SWE, TUR |

Ana sonuç:
- 2024 ana sektörlerin her birinde **26/27** core-country observation.
- Eksik ülke: **Türkiye**.
- Türkiye için sector productivity değeri impute/carry-forward edilmemelidir.
- 2025 ana sektör verisi core sample'da yalnızca **NOR** için
  bulunur; bu nedenle 2025 sector outcome olarak kullanılmamalıdır.

OECD 2026 Compendium'ın 2024 industry chart coverage notu da Türkiye'yi data
unavailability nedeniyle dışarıda kalan OECD ülkeleri arasında saymaktadır.

## 12. 2019–2024 balanced growth coverage

Her sektör için `GY` + `XDC_H` gözlemlerinde 2019–2024 döneminin tamamında sürekli
bulunan core-country sample:

- `C` Manufacturing: 26/27 — eksik: TUR
- `F` Construction: 26/27 — eksik: TUR
- `H` Transportation and storage: 26/27 — eksik: TUR
- `I` Accommodation and food service activities: 26/27 — eksik: TUR
- `J` Information and communication: 26/27 — eksik: TUR
- `M` Professional, scientific and technical activities: 26/27 — eksik: TUR
- `N` Administrative and support service activities: 26/27 — eksik: TUR
- `L` Real estate activities: 26/27 — eksik: TUR

Bu yapı trend/panel robustness için kullanılabilir. Ana tasarım yine 2024 outcome üzerine
kuruludur.

## 13. Real estate — supplementary

`L` — Real estate activities productivity tarafında 2024 için 26/27 coverage verir.

Ancak OECD Business ICT adoption tarafında Real Estate coverage çok daha zayıftır.
Bu nedenle full productivity dosyasında iyi coverage olsa bile ana AI↔productivity matched
sector analysis'e otomatik dahil edilmez.

**Statü: supplementary only.**

## 14. Total - all activities satırları

`_T` satırları bu 3.366 satırlık full extract'in doğal parçasıdır ve sample'da da temsil
edilir.

Uygun kullanım:
- aggregate GVA/hour level/growth benchmark,
- sector vs aggregate descriptive comparison,
- QA / robustness.

Ancak bu dosyada `GDP per hour worked` yoktur; yalnızca `GVAHRS` vardır.

Bu nedenle bu dosyayı kullanarak `GDPHRS` değişkeni varmış gibi kod yazılmamalıdır.

## 15. Observation status

Full extract:
- `A` — Normal value: **3,362**
- `E` — Estimated value: **4**

Non-normal (`E`) satırlar:

- `SWE` / `_T` / 2025 / `N` / `E`
- `SWE` / `_T` / 2025 / `GY` / `E`
- `SWE` / `_T` / 2025 / `N` / `E`
- `SWE` / `_T` / 2025 / `GY` / `E`

Kural:
- `E` automatic deletion değildir.
- Analysis filter sonrası status distribution mutlaka yeniden raporlanmalıdır.
- Gerekiyorsa main vs exclude-estimated sensitivity yapılmalıdır.

## 16. 2025 neden ana sector outcome değil?

Full extract 2019–2025 indirildiği halde 2025 industry data henüz çok sınırlıdır.

Ana seven-sector/core-country `GY` coverage 2025'te yalnızca Norway'a ulaşmaktadır.
OECD Productivity Database rolling basis'te güncellendiği için farklı variable/country
serilerinin latest year coverage'ı eşit olmak zorunda değildir.

**Kural:** Raw 2025 satırlarını silme; fakat current portfolio ana sector outcome = 2024.

## 17. OECD Business ICT ile temporal eşleştirme

Ana exploratory ilişki:

```text
Sector enterprise AI adoption 2023
        ↓
Sector real GVA/hour growth 2024
```

Gerekçe:
- temporal ordering sağlar,
- `AI 2025 → productivity 2024` gibi ters zaman sıralamasını önler.

Bu ilişki:
- associative/exploratory,
- causal değildir.

Ana matched sectors:
`C, F, H, I, J, M, N`.

Final merge local full OECD ICT + local full 3.366-row Productivity CSV üzerinde
yapılmalıdır.

## 18. Full dataset local-load QA — KESİN

```python
assert df.shape == (3366, 34)
assert list(df.columns) == ['STRUCTURE', 'STRUCTURE_ID', 'STRUCTURE_NAME', 'ACTION', 'REF_AREA', 'Reference area', 'FREQ', 'Frequency of observation', 'MEASURE', 'Measure', 'ACTIVITY', 'Economic activity', 'UNIT_MEASURE', 'Unit of measure', 'PRICE_BASE', 'Price base', 'TRANSFORMATION', 'Transformation', 'ASSET_CODE', 'Asset type', 'CONVERSION_TYPE', 'Conversion type', 'TIME_PERIOD', 'Time period', 'OBS_VALUE', 'Observation value', 'OBS_STATUS', 'Observation status', 'UNIT_MULT', 'Unit multiplier', 'BASE_PER', 'Base period', 'DECIMALS', 'Decimals']

grain = ['REF_AREA', 'FREQ', 'MEASURE', 'ACTIVITY', 'UNIT_MEASURE', 'PRICE_BASE', 'TRANSFORMATION', 'ASSET_CODE', 'CONVERSION_TYPE', 'TIME_PERIOD']
assert not df.duplicated(grain).any()

assert set(df["MEASURE"].unique()) == {"GVAHRS"}
assert set(df["PRICE_BASE"].unique()) == {"LR"}
assert set(df["ASSET_CODE"].unique()) == {"_Z"}
assert set(df["TRANSFORMATION"].unique()) == {"N","GY"}
assert set(df["UNIT_MEASURE"].unique()) == {"XDC_H","USD_PPP_H"}
assert set(df["CONVERSION_TYPE"].unique()) == {"_Z","PPP"}
assert set(df["TIME_PERIOD"].astype(str).unique()) == {
    "2019","2020","2021","2022","2023","2024","2025"
}
assert df["OBS_VALUE"].notna().all()
```

Sector-specific structure QA:

```python
sector = df[df["ACTIVITY"] != "_T"]

assert set(sector["UNIT_MEASURE"].unique()) == {"XDC_H"}
assert set(sector["CONVERSION_TYPE"].unique()) == {"_Z"}
assert set(sector["MEASURE"].unique()) == {"GVAHRS"}
```

Main 2024 outcome QA:

```python
core_27 = ['AUT', 'BEL', 'BGR', 'HRV', 'CZE', 'DNK', 'EST', 'FIN', 'FRA', 'DEU', 'GRC', 'HUN', 'IRL', 'ITA', 'LVA', 'LTU', 'LUX', 'NLD', 'NOR', 'POL', 'PRT', 'ROU', 'SVK', 'SVN', 'ESP', 'SWE', 'TUR']
main_sectors = ["C","F","H","I","J","M","N"]

x = df[
    df["REF_AREA"].isin(core_27)
    & df["ACTIVITY"].isin(main_sectors)
    & (df["UNIT_MEASURE"] == "XDC_H")
    & (df["TRANSFORMATION"] == "GY")
    & (df["TIME_PERIOD"].astype(str) == "2024")
]

assert x.shape[0] == 26 * 7
assert "TUR" not in set(x["REF_AREA"])
```

## 19. Sample'ın smoke-test sınırı

`OECD_Productivity_3366_unchanged_structure_sample.csv` şu işler için uygundur:

- CSV parser/schema,
- code/label mapping,
- activity filtering,
- unit/conversion filtering,
- transformation `N/GY` handling,
- status handling,
- pivot/reshape logic,
- local filter code smoke test.

Uygun değildir:
- final country values,
- final coverage inference,
- correlations,
- panel estimation,
- sector regressions,
- final report findings.

Bunlar local tam 3.366-row CSV üzerinde yapılmalıdır.

## 20. AI/model'e yüklerken önerilen açıklama

> `OECD_Productivity_3366_unchanged_structure_sample.csv`, local bilgisayarda bulunan tam
> 3.366 × 34 `OECD Productivity database.csv` dosyasından değiştirilmeden seçilmiş gerçek
> satırlardan oluşan schema/structure sample'dır. Bu sample final istatistik üretmek için
> değil, full CSV üzerinde çalışacak Python/R kodunu geliştirmek ve smoke-test etmek için
> kullanılacaktır. Full extract yalnızca `GVAHRS` measure'ını içerir; `GDPHRS` yoktur.
> Sektör satırlarında `XDC_H` national-currency levels vardır ve bunlar ülkeler arasında
> level olarak karşılaştırılmamalıdır. Cross-country sector productivity outcome için
> `TRANSFORMATION = GY`, `YEAR = 2024`, ana sektörler `C/F/H/I/J/M/N` kullanılmalıdır.
> Türkiye 2024 sector productivity'de eksiktir ve impute/carry-forward yapılmamalıdır.
> 2025 industry coverage yetersizdir. `OBS_STATUS = E` estimated satırları koru ve
> sensitivity gerektiğinde ayrıca test et. Final hesaplar local tam CSV üzerinde yapılacaktır.

## 21. Resmî metodolojik doğrulama

OECD Data Explorer:
- `DSD_PDB@DF_PDB`
- güncel konsolide Productivity Database,
- annual labour productivity ve industry detail,
- rolling updates.

OECD Compendium of Productivity Indicators 2026:
- industry labour productivity karşılaştırmasını
  **annual percentage change in GVA per hour worked** olarak tanımlar;
- 2024 coverage'da 25 OECD country + Bulgaria, Croatia, Romania;
- Türkiye data unavailability nedeniyle dahil değildir.

Bu kaynaklar, current extract için `GVAHRS + GY + 2024` sector comparison yaklaşımını
desteklemektedir.
