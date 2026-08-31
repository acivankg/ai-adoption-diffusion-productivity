# OECD Educational Attainment — Ana Veri Seti Bağlam ve Kodlama Rehberi

## 1. Kimlik

- **Standart çalışma adı:** OECD Educational Attainment
- **Kullanıcının yüklediği dosya:** `OECD educational attainment.csv`
- **Resmî OECD veri seti:** *Adults' educational attainment distribution, by age group and gender*
- **OECD dataflow:** `OECD.EDU.IMEP:DSD_EAG_LSO_EA@DF_LSO_NEAC_DISTR_EA(1.0)`
- **Ana extract:** 193 veri satırı × 50 sütun
- **Dosya boyutu:** 107,727 byte
- **SHA-256:** `89c9f86741a9145158285c64de898fa8ed571ef6833f02475c637ddb6d54153e`
- **Bu paketteki dosya:** `OECD_Educational_Attainment_full_unchanged.csv`
- **Kopya SHA-256:** `89c9f86741a9145158285c64de898fa8ed571ef6833f02475c637ddb6d54153e`
- **Byte-identical:** Evet

Bu dosya yaklaşık 105.2 KB olduğu için sample üretmek yerine tam,
değiştirilmemiş extract'i doğrudan sağlamak en güvenli yaklaşımdır.

OECD Data Explorer'ın güncel açıklamasına göre bu veri seti yetişkinlerin yaş ve cinsiyet
grubuna göre educational attainment dağılımını içerir. Latest available year değerleri
**preliminary** olup final data **29 Eylül 2026** tarihinde yayımlanacaktır. Data Explorer
son güncelleme tarihi **23 Temmuz 2026**'dır.

## 2. Çalışmadaki rol

Ana kavram:

> **General / Educational Human Capital**

Ana analytical variable:

`tertiary_attainment_2024`

Tanım:

> 25–64 yaş toplam nüfusta tertiary education (ISCED 5–8) tamamlamış yetişkinlerin yüzdesi.

Bu değişken:
- AI-specific skill değildir,
- digital skill değildir,
- genel human-capital stock proxy'sidir.

OECD Education at a Glance 2025, Table A1.1 adult attainment sonuçlarını 2024 referansıyla,
25–64 yaş grubunda highest level attained yüzdesi olarak sunar.

## 3. Neden tam dosya, sample değil?

Full extract yalnızca:
- 193 satır
- 50 sütun
- ~105.2 KB

Bu boyut model bağlamına doğrudan verilebilir.

**Karar:** Bu veri seti için sample oluşturulmayacak.

Full CSV:
- schema inspection,
- filtering,
- QA,
- final 2024 extraction,
- benchmark,
- limited trend checks,
- master merge

için doğrudan kullanılabilir.

## 4. Tam sütun şeması

1. `STRUCTURE`
2. `STRUCTURE_ID`
3. `STRUCTURE_NAME`
4. `ACTION`
5. `REF_AREA`
6. `Reference area`
7. `SEX`
8. `Sex`
9. `AGE`
10. `Age`
11. `ATTAINMENT_LEV`
12. `Educational attainment level`
13. `EDUCATION_FIELD`
14. `Field of education`
15. `MEASURE`
16. `Measure`
17. `INCOME`
18. `Income`
19. `BIRTH_PLACE`
20. `Place of birth`
21. `MIGRATION_AGE`
22. `Age at migration`
23. `EDU_STATUS`
24. `Education status`
25. `LABOUR_FORCE_STATUS`
26. `Labour force status`
27. `DURATION_UNEMP`
28. `Unemployment duration`
29. `UNIT_MEASURE`
30. `Unit of measure`
31. `STATISTICAL_OPERATION`
32. `Statistical operation`
33. `WORK_TIME_ARNGMNT`
34. `Work time arrangement`
35. `QUESTIONNAIRE`
36. `Questionnaire name`
37. `FREQ`
38. `Frequency of observation`
39. `TIME_PERIOD`
40. `Time period`
41. `OBS_VALUE`
42. `Observation value`
43. `OBS_STATUS`
44. `Observation status`
45. `CONF_STATUS`
46. `Confidentiality status`
47. `UNIT_MULT`
48. `Unit multiplier`
49. `DECIMALS`
50. `Decimals`

## 5. Veri grain'i

Expected unique grain:

`REF_AREA × SEX × AGE × ATTAINMENT_LEV × EDUCATION_FIELD × MEASURE × INCOME × BIRTH_PLACE × MIGRATION_AGE × EDU_STATUS × LABOUR_FORCE_STATUS × DURATION_UNEMP × UNIT_MEASURE × STATISTICAL_OPERATION × WORK_TIME_ARNGMNT × QUESTIONNAIRE × FREQ × TIME_PERIOD`

Duplicate sayısı: **0**.

Primary filter columns:
- `REF_AREA`
- `SEX`
- `AGE`
- `ATTAINMENT_LEV`
- `UNIT_MEASURE`
- `STATISTICAL_OPERATION`
- `TIME_PERIOD`

Value:
- `OBS_VALUE`

Quality:
- `OBS_STATUS`

Production filtering'de code columns label sütunlarına tercih edilmelidir.

## 6. Full extract'teki dimension değerleri

### `REF_AREA` — Reference area

- `AUT` — Austria
- `BEL` — Belgium
- `BGR` — Bulgaria
- `CZE` — Czechia
- `DEU` — Germany
- `DNK` — Denmark
- `ESP` — Spain
- `EST` — Estonia
- `EU25` — European Union (25 countries)
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

### `SEX` — Sex

- `_T` — Total

### `AGE` — Age

- `Y25T64` — From 25 to 64 years

### `ATTAINMENT_LEV` — Educational attainment level

- `ISCED11A_5T8` — Tertiary education

### `EDUCATION_FIELD` — Field of education

- `_T` — Total

### `MEASURE` — Measure

- `POP` — Population

### `INCOME` — Income

- `_Z` — Not applicable

### `BIRTH_PLACE` — Place of birth

- `_T` — Total

### `MIGRATION_AGE` — Age at migration

- `_Z` — Not applicable

### `EDU_STATUS` — Education status

- `ED_NED` — In education or not in education

### `LABOUR_FORCE_STATUS` — Labour force status

- `POP` — Population

### `DURATION_UNEMP` — Unemployment duration

- `_Z` — Not applicable

### `UNIT_MEASURE` — Unit of measure

- `PT_POP_SEX_AGE` — Percentage of population in the same sex and age

### `STATISTICAL_OPERATION` — Statistical operation

- `OBS` — Observed

### `WORK_TIME_ARNGMNT` — Work time arrangement

- `_Z` — Not applicable

### `QUESTIONNAIRE` — Questionnaire name

- `NEAC` — LSO-NEAC regular data collection

### `FREQ` — Frequency of observation

- `A` — Annual

### `OBS_STATUS` — Observation status

- `A` — Normal value
- `B` — Time series break
- `O` — Missing value

### `CONF_STATUS` — Confidentiality status

- `(blank)` — (blank)

Bu mappings, extract'in zaten çok dar filtrelenmiş olduğunu gösterir.

## 7. Bu dosyada sabitlenmiş exact seçimler

### Reference area
- 27 ana ülke
- OECD
- EU25

Toplam 29 reference area.

### Sex
- `_T` — Total

### Age
- `Y25T64` — From 25 to 64 years

### Educational attainment
- `ISCED11A_5T8` — Tertiary education

### Statistical operation
- `OBS` — Observed

### Unit
- `PT_POP_SEX_AGE` — Percentage of population in the same sex and age

### Time
- 2019–2025

Bu nedenle local kodda bu file içinde Female/Male, başka age group veya başka education
level varmış gibi davranılmamalıdır.

## 8. Ana 27-country sample

Core codes:

`AUT, BEL, BGR, HRV, CZE, DNK, EST, FIN, FRA, DEU, GRC, HUN, IRL, ITA, LVA, LTU, LUX, NLD, NOR, POL, PRT, ROU, SVK, SVN, ESP, SWE, TUR`

Benchmark:
- `OECD`
- `EU25`

Benchmark'lar regression observation değildir ve z-score/standardization sample'ına
girmemelidir.

## 9. Ana analytical filter

```python
core_27 = ['AUT', 'BEL', 'BGR', 'HRV', 'CZE', 'DNK', 'EST', 'FIN', 'FRA', 'DEU', 'GRC', 'HUN', 'IRL', 'ITA', 'LVA', 'LTU', 'LUX', 'NLD', 'NOR', 'POL', 'PRT', 'ROU', 'SVK', 'SVN', 'ESP', 'SWE', 'TUR']

edu_2024 = df[
    df["REF_AREA"].isin(core_27)
    & (df["SEX"] == "_T")
    & (df["AGE"] == "Y25T64")
    & (df["ATTAINMENT_LEV"] == "ISCED11A_5T8")
    & (df["STATISTICAL_OPERATION"] == "OBS")
    & (df["UNIT_MEASURE"] == "PT_POP_SEX_AGE")
    & (df["TIME_PERIOD"].astype(str) == "2024")
]
```

Derived analytical name:

```text
tertiary_attainment_2024 = OBS_VALUE
```

## 10. Yıllık core coverage

| Year | Core obs | Blank value | Missing core refs | Non-normal status |
|---|---:|---:|---|---|
| 2019 | 27/27 | 0 | Yok | Yok |
| 2020 | 23/27 | 0 | BGR, HRV, ROU, TUR | Yok |
| 2021 | 25/27 | 0 | BGR, HRV | Yok |
| 2022 | 26/27 | 0 | HRV | Yok |
| 2023 | 27/27 | 0 | Yok | Yok |
| 2024 | 27/27 | 0 | Yok | Yok |
| 2025 | 26/27 | 0 | FRA | DNK=B |

## 11. Ana yıl = 2024

Kesin seçim:

> **2024**

Gerekçe:
- 27/27 core coverage,
- 27/27 normal value,
- Education at a Glance 2025 adult-attainment table 2024 referanslı,
- 2025 OECD latest-year values preliminary,
- AI outcome 2025'ten önce ölçülen structural stock sağlar.

Temporal framing:

```text
Human Capital 2024 → Enterprise AI Adoption 2025
```

Bu zaman sıralaması causality kanıtı değildir.

## 12. 2025 neden ana değişken değil?

OECD Data Explorer:
- latest-year data preliminary,
- final release 29 September 2026.

Bu extract'teki 2025 issue'ları:

- `DNK` — value `45.9920195071463` — status `B` / Time series break

Bilinen ana durum:
- France 2025 observation yok.
- Denmark 2025 `B` / Time series break.

Bu nedenle 2025 ana explanatory variable yapılmamalıdır.

## 13. 2024 benchmark değerleri

- `EU25` — 38.5637% — status `A`
- `OECD` — 41.8299% — status `A`

Benchmark'lar yalnızca chart/reference amaçlıdır.

## 14. Trend kullanımı

Human capital yavaş hareket eden structural stock olduğu için trend ana analiz için zorunlu
değildir.

Trend yapılacaksa:
- year-by-year coverage kontrol et,
- `OBS_STATUS` kontrol et,
- break satırlarını annotation/sensitivity ile yönet,
- missing year impute/interpolate etme.

2019, 2023 ve 2024 core coverage 27/27'dir.
2020–2022 bazı core country eksikleri vardır.

## 15. Observation status

Full extract:

- `A` — Normal value — 190 satır
- `B` — Time series break — 1 satır
- `O` — Missing value — 2 satır

Kural:
- `A` = Normal value.
- `B` = Time series break.
- Main 2024 slice tamamen `A`.
- `B` otomatik deletion değildir; trend bağlamında ayrıca yönetilir.

## 16. Missingness / numeric

- Blank `OBS_VALUE`: **2**
- Nonblank numeric parse failure: **0**

Missing:
- 0 değildir,
- impute edilmemelidir,
- year coverage ile yönetilmelidir.

## 17. Doğru kavramsal isim

Kullan:
- `tertiary_attainment_2024`
- `educational_human_capital`
- `general_human_capital`

Kullanma:
- `AI skills`
- `digital skills`

Çünkü tertiary attainment AI-specific competency ölçmez.

## 18. Merge kuralı

Primary country code:
- `REF_AREA`

Country master'a canonical ISO3 üzerinden merge edilmelidir.

2024 ana slice 27/27 tam olduğu için bu değişken örneklem kaybı yaratmaz.

`OECD` ve `EU25` benchmark table'da ayrı tutulmalıdır.

## 19. Regression kullanım kuralı

H2 skills/human-capital pillar için aday model:

```text
AI_2025 =
β0
+ β1 ICTTraining_2023
+ β2 ICTSpecialists_2024
+ β3 TertiaryAttainment_2024
+ ε
```

Small n≈27 nedeniyle tertiary attainment, services share, GDPpc ve çok sayıda diğer predictor
ile tek kitchen-sink model'e zorla doldurulmamalıdır.

Correlation/VIF diagnostics uygulanmalıdır.

## 20. 29 Eylül 2026 sonrası versioning

Çalışma final release sonrasında devam ediyorsa:
1. latest OECD file yeniden indirilebilir,
2. yeni dosya ayrı version olarak saklanır,
3. mevcut dosyanın hash'i korunur; overwrite edilmez,
4. France 2025 ve Denmark break durumu yeniden kontrol edilir.

Ancak 2025 final data gelmesi 2024'ü ana human-capital year olarak değiştirmeyi zorunlu
kılmaz; 2024 temporal design açısından hâlâ uygundur.

## 21. Local production QA

```python
assert df.shape == (193, 50)
assert list(df.columns) == ['STRUCTURE', 'STRUCTURE_ID', 'STRUCTURE_NAME', 'ACTION', 'REF_AREA', 'Reference area', 'SEX', 'Sex', 'AGE', 'Age', 'ATTAINMENT_LEV', 'Educational attainment level', 'EDUCATION_FIELD', 'Field of education', 'MEASURE', 'Measure', 'INCOME', 'Income', 'BIRTH_PLACE', 'Place of birth', 'MIGRATION_AGE', 'Age at migration', 'EDU_STATUS', 'Education status', 'LABOUR_FORCE_STATUS', 'Labour force status', 'DURATION_UNEMP', 'Unemployment duration', 'UNIT_MEASURE', 'Unit of measure', 'STATISTICAL_OPERATION', 'Statistical operation', 'WORK_TIME_ARNGMNT', 'Work time arrangement', 'QUESTIONNAIRE', 'Questionnaire name', 'FREQ', 'Frequency of observation', 'TIME_PERIOD', 'Time period', 'OBS_VALUE', 'Observation value', 'OBS_STATUS', 'Observation status', 'CONF_STATUS', 'Confidentiality status', 'UNIT_MULT', 'Unit multiplier', 'DECIMALS', 'Decimals']

assert set(df["SEX"].unique()) == {"_T"}
assert set(df["AGE"].unique()) == {"Y25T64"}
assert set(df["ATTAINMENT_LEV"].unique()) == {"ISCED11A_5T8"}
assert set(df["STATISTICAL_OPERATION"].unique()) == {"OBS"}
assert set(df["UNIT_MEASURE"].unique()) == {"PT_POP_SEX_AGE"}
assert set(df["TIME_PERIOD"].astype(str).unique()) == {
    "2019","2020","2021","2022","2023","2024","2025"
}
```

Main 2024 assertion:

```python
x = df[
    df["REF_AREA"].isin(core_27)
    & (df["TIME_PERIOD"].astype(str) == "2024")
]

assert len(x) == 27
assert x["REF_AREA"].nunique() == 27
assert x["OBS_VALUE"].notna().all()
assert set(x["OBS_STATUS"].unique()) == {"A"}
```

Benchmark:

```python
bench = df[
    df["REF_AREA"].isin(["OECD","EU25"])
    & (df["TIME_PERIOD"].astype(str) == "2024")
]
assert len(bench) == 2
```

## 22. AI/model'e yüklerken önerilen açıklama

> `OECD_Educational_Attainment_full_unchanged.csv`, OECD
> `Adults' educational attainment distribution, by age group and gender` veri setinden
> indirilmiş 193 × 50 tam extract'in byte-identical kopyasıdır; sample değildir ve doğrudan
> kullanılabilir. Extract zaten `Sex=Total`, `Age=25–64`, `Tertiary education`,
> `Observed`, `Percentage of population in same sex and age`, `2019–2025` olarak
> filtrelenmiştir. Ana portfolio değişkeni 27 core country için 2024 `OBS_VALUE`
> (`tertiary_attainment_2024`) değeridir; 2024 coverage 27/27 ve tamamı normaldir. 2025
> latest-year data preliminary'dir; France 2025 eksik, Denmark 2025 time-series-break'dir.
> `OECD` ve `EU25` benchmark'tır, regression observation değildir. Bu değişken general
> human capital proxy'sidir, AI-specific skill değildir. Missing değerleri impute etme ve
> `OBS_STATUS` flag'lerini koru.

## 23. Kullanım sınırı

Bu full CSV doğrudan yeterlidir:
- schema/QA,
- 2024 human-capital extraction,
- benchmark,
- limited trend checks,
- country-master merge,
- final model input preparation.

Ek sample gerekli değildir.
