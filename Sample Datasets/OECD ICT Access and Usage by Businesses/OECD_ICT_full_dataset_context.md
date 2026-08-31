# OECD Business ICT — Ana Veri Seti Bağlam ve Kodlama Rehberi

## 1. Kimlik

- **Standart çalışma adı:** OECD Business ICT
- **Kullanıcının yüklediği dosya:** `OECD ICT Access and Usage by Businesses.csv`
- **Resmî veri seti:** *ICT Access and Usage by Businesses*
- **OECD dataflow:** `OECD.STI.DEP:DSD_ICT_B@DF_BUSINESSES(1.0)`
- **Resmî konu:** Science, technology and innovation → Information and communication technology (ICT)
- **Ana yüklenen extract:** 5,933 veri satırı × 34 sütun
- **Ana extract SHA-256:** `d05e1a81a5bed18fed128def321068ae5f8ba579d99c3da928e2a4469502647b`
- **Bu schema sample:** 321 veri satırı × 34 sütun
- **Sample SHA-256:** `193b86a7de0c87ffdde28f5276194513c8f6c3ff248f2d2490beadf1eac8a9fb`

OECD'nin resmî Data Explorer açıklamasına göre veri tabanı OECD Model Survey on ICT
Access and Usage by Businesses'ın 2. revizyonuna dayanan 60 gösterge içerir. OECD/katılım
ülkelerinin bir bölümü doğrudan OECD collection'dan, European Statistical System içindeki
ülkeler ise Eurostat business ICT statistics kaynaklarından gelir. Dolayısıyla ülke metadata
ve methodological break'leri önemlidir.

## 2. Bu sample'ın amacı

Bu CSV **analiz için küçültülmüş veri seti değildir** ve sample değerlerinden sonuç
hesaplanmamalıdır.

Amaç:
1. Bir insanın veya yapay zekânın ana CSV'nin gerçek şemasını tanıması,
2. local bilgisayarda ana 5,933-satırlık dosyaya uygulanacak kodu doğru yazması,
3. column names, codes, labels, status flags ve structural combinations'ı görmesi,
4. sample üzerinde kodu smoke-test edip aynı kodu ana dosyaya uygulamasıdır.

### Değişmezlik garantisi

- Sample'da **ana dosyadaki 34 sütunun tamamı vardır**.
- Sütun isimleri ve sırası ana dosyayla birebir aynıdır.
- Yeni sütun eklenmemiştir.
- Hiçbir değer temizlenmemiş, dönüştürülmemiş, yeniden kodlanmamış veya yuvarlanmamıştır.
- Sample'daki her veri satırı ana CSV'den **byte düzeyinde aynı fiziksel satır olarak**
  kopyalanmıştır.
- Orijinal CSV değiştirilmemiştir.

## 3. Sample seçme yöntemi

Sample istatistiksel temsil için değil **schema/coverage temsili** için seçilmiştir.

- Ana dosyada mevcut her benzersiz
  `MEASURE × ACTIVITY × SIZE_CLASS × TIME_PERIOD`
  kombinasyonundan en az bir gerçek satır alınmıştır.
- Ana dosyada bu tür **320 yapısal kombinasyon** vardır.
- Flag mantığının görülmesi için mümkün olduğunda `A` dışı observation-status satırı
  tercih edilmiştir.
- Ülke seçimi dengelenmiş ve ana extract'teki tüm **35 reference area**
  en az bir kez sample'a dahil edilmiştir.
- Sonuç: 321 satır.

**Önemli:** Bu seçim yöntemi nedeniyle sample'daki ülke ve flag dağılımı ana dosyanın
istatistiksel dağılımını temsil etmez. Sample üzerinden ortalama, korelasyon, regression,
ranking veya coverage sonucu üretmeyin.

## 4. Veri grain'i / primary dimensions

Ana extract'te bir gözlem şu kombinasyonda benzersizdir:

`REF_AREA × FREQ × MEASURE × UNIT_MEASURE × ACTIVITY × SIZE_CLASS × TIME_PERIOD`

Ana dosyada bu grain üzerinde duplicate yoktur.

Kod yazarken descriptive label yerine filtreleme/merge için öncelikle **code columns**
kullanılmalıdır:

- `REF_AREA`
- `MEASURE`
- `UNIT_MEASURE`
- `ACTIVITY`
- `SIZE_CLASS`
- `TIME_PERIOD`

Değer:
- `OBS_VALUE`

Kalite/status:
- `OBS_STATUS`
- `OBS_STATUS_2`
- `OBS_STATUS_3`

## 5. Tam sütun şeması — ana dosyada ve sample'da aynı

Ana dosya sütunları sırasıyla:

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
11. `UNIT_MEASURE`
12. `Unit of measure`
13. `ACTIVITY`
14. `Economic activity`
15. `SIZE_CLASS`
16. `Employment size class`
17. `TIME_PERIOD`
18. `Time period`
19. `OBS_VALUE`
20. `Observation value`
21. `OBS_STATUS`
22. `Observation status`
23. `OBS_STATUS_2`
24. `Observation status 2`
25. `OBS_STATUS_3`
26. `Observation status 3`
27. `UNIT_MULT`
28. `Unit multiplier`
29. `TIME_HORIZON_USE`
30. `Time horizon`
31. `DECIMALS`
32. `Decimals`
33. `BREAKDOWN_V7`
34. `V7 Breakdowns`

### Tip önerisi — local kod için

CSV'nin kendisi tip saklamaz. Load sonrasında:

- code/label/metadata sütunları: string
- `TIME_PERIOD`: tercihen integer veya string; filtrelerde tutarlı olun
- `OBS_VALUE`: numeric/float
- `UNIT_MULT`: integer-like metadata
- `DECIMALS`: integer-like metadata

`_T`, `S_GE10`, `G14_B` gibi kodlar string olarak korunmalıdır.

## 6. Ana extract'teki dimension değerleri

### Reference area — 35

- `AUS` — Australia
- `AUT` — Austria
- `BEL` — Belgium
- `BGR` — Bulgaria
- `BRA` — Brazil
- `CAN` — Canada
- `CZE` — Czechia
- `DEU` — Germany
- `DNK` — Denmark
- `ESP` — Spain
- `EST` — Estonia
- `EU27` — European Union (27 countries)
- `FIN` — Finland
- `FRA` — France
- `GRC` — Greece
- `HRV` — Croatia
- `HUN` — Hungary
- `IRL` — Ireland
- `ITA` — Italy
- `JPN` — Japan
- `KOR` — Korea
- `LTU` — Lithuania
- `LUX` — Luxembourg
- `LVA` — Latvia
- `NLD` — Netherlands
- `NOR` — Norway
- `NZL` — New Zealand
- `OECD` — OECD
- `POL` — Poland
- `PRT` — Portugal
- `ROU` — Romania
- `SVK` — Slovak Republic
- `SVN` — Slovenia
- `SWE` — Sweden
- `TUR` — Türkiye

### Measure — 5

- `G14_B` — Businesses using artificial intelligence (AI) — ana extract'te 1,779 satır
- `G3_B` — Businesses purchasing cloud computing services — ana extract'te 1,414 satır
- `G7_B` — Businesses having performed big data analysis — ana extract'te 970 satır
- `H1_B` — Businesses which employ ICT specialists — ana extract'te 886 satır
- `H3_B` — Businesses which provided any type of training to develop ICT related skills of the persons employed — ana extract'te 884 satır

### Unit — tek değer

- `PT_ENT` — Percentage of enterprises

### Economic activity — 11

- `C` — Manufacturing — 435 satır
- `F` — Construction — 437 satır
- `G46` — Wholesale trade, except of motor vehicles and motorcycles — 401 satır
- `G47` — Retail trade, except of motor vehicles and motorcycles — 404 satır
- `H` — Transportation and storage — 426 satır
- `I` — Accommodation and food service activities — 432 satır
- `J` — Information and communication — 432 satır
- `L` — Real estate activities — 375 satır
- `M` — Professional, scientific and technical activities — 428 satır
- `N` — Administrative and support service activities — 420 satır
- `_T` — Total - all activities — 1,743 satır

### Employment size class — 4

- `S10T49` — From 10 to 49 — 438 satır
- `S50T249` — From 50 to 249 — 429 satır
- `S_GE10` — 10 or more — 4,628 satır
- `S_GE250` — 250 or more — 438 satır

### Time period

- `2021` — 1,413 satır
- `2022` — 590 satır
- `2023` — 1,761 satır
- `2024` — 992 satır
- `2025` — 1,177 satır

## 7. Observation-status metadata

### `OBS_STATUS`

- `A` — Normal value — 4,627 satır
- `B` — Time series break — 1,164 satır
- `D` — Definition differs — 131 satır
- `U` — Low reliability — 11 satır

### `OBS_STATUS_2`

- boş: 5,910 satır
- `D` — Definition differs: 3 satır
- `U` — Low reliability: 20 satır

### Kural

Status alanlarını load sırasında kaybetmeyin.

- `A` = normal.
- `B` = time-series break.
- `D` = definition differs.
- `U` = low reliability.
- `B/D/U` gözlemleri otomatik olarak silinmemelidir.
- Main analysis ve sensitivity/robustness sample'ları ayrı üretilmelidir.
- İmputation yapılmamalıdır; önce neden ve coverage kontrol edilmelidir.

## 8. Diğer metadata alanları

- `FREQ = A` ve label `Annual`
- `UNIT_MULT = 0`, label `Units`
- `DECIMALS = 2`, label `Two`
- `TIME_HORIZON_USE`:
  - boş: 4,163 satır
  - `L_3` / `within last 3 months`: 1,770 satır
- Bu extract'te `L_3` değeri ICT specialists ve ICT training measure'larında bulunur.
- `BREAKDOWN_V7` ve `V7 Breakdowns` source breakdown metadata'sıdır; load sırasında
  korunabilir, ana filtre/merge key'i değildir.
- `Time period`, `Observation value`, `Observation status 3` gibi bazı label/secondary
  sütunlar bu extract'te boş olabilir. Boş metadata sütunları sample hazırlanırken
  kaldırılmamıştır.

## 9. Çalışmanın ana 27-country örneklemi

Ana analiz country listesi:

`AUT`, `BEL`, `BGR`, `HRV`, `CZE`, `DNK`, `EST`, `FIN`, `FRA`, `DEU`, `GRC`, `HUN`, `IRL`, `ITA`, `LVA`, `LTU`, `LUX`, `NLD`, `NOR`, `POL`, `PRT`, `ROU`, `SVK`, `SVN`, `ESP`, `SWE`, `TUR`

Ana extract ayrıca:
`AUS`, `BRA`, `CAN`, `JPN`, `KOR`, `NZL`, `EU27`, `OECD`
satırlarını da içerir.

- `EU27` ve `OECD`: benchmark olabilir, regression observation değildir.
- Diğer non-core ülkeler ana portfolio regression sample'ına otomatik eklenmemelidir.
- Ana sample filtresi explicit ISO/reference-code listesiyle uygulanmalıdır.

## 10. Çalışma için kesinleşmiş country-level analytical filters

Bu filtreler **sample CSV'ye uygulanmamıştır**. Bunlar local bilgisayarda ANA CSV üzerinde
kodla uygulanmalıdır.

Ortak filtre:
- `REF_AREA in core_27`
- `ACTIVITY == "_T"`
- `SIZE_CLASS == "S_GE10"`
- `UNIT_MEASURE == "PT_ENT"`

| Analitik değişken | Measure | Yıl | Core coverage | Ana status istisnası |
|---|---|---:|---:|---|
| Enterprise AI adoption | `G14_B` | 2025 | 27/27 | `NLD`=B |
| Lagged enterprise AI adoption | `G14_B` | 2023 | 27/27 | `FRA`=B, `SWE`=B |
| Cloud computing | `G3_B` | 2025 | 27/27 | Yok |
| Big data / data analytics | `G7_B` | 2025 | 27/27 | `CZE`=B |
| ICT specialists | `H1_B` | 2024 | 27/27 | `SWE`=B |
| ICT training | `H3_B` | 2023 | 27/27 | `SWE`=B |

### Zamanlama gerekçesi

- Ana enterprise AI outcome: 2025.
- Cloud ve data capability: 2025.
- ICT specialists: en uygun ortak yıl 2024.
- ICT training: en uygun ortak yıl 2023.
- Productivity temporal analysis için lagged enterprise AI: 2023.
- Bu mixed-year eşleştirme bilinçlidir; yanlışlıkla bütün değişkenleri 2025'e zorlamayın.

## 11. 2021 AI trend uyarısı

Core 27 ülkenin `Total + 10 or more + AI + 2021` gözlemlerinin tamamı `B`
(time-series break) statüsündedir.

Bu nedenle:
- **2021→2025 AI adoption headline trend kullanılmamalıdır.**
- Trend gerekiyorsa 2023→2025 daha uygun başlangıçtır.
- 2023 AI'da France ve Sweden için `B` vardır; robustness gerekir.

## 12. Firm-size analizi için local filtreler

Ana dataset üzerinde:

- `REF_AREA in core_27`
- `ACTIVITY == "_T"`
- `TIME_PERIOD == 2025`
- `UNIT_MEASURE == "PT_ENT"`
- `SIZE_CLASS in ["S10T49","S50T249","S_GE250"]`
- Ana firm-size outcome measure: `G14_B`

Ana türetilmiş metrik:

`SME AI gap = AI(250 or more) - AI(10–49)`

Coverage:
- AI 2025 dört size class: core 27 ülkenin tamamı.
- Cloud/data medium (`S50T249`) için Portugal eksik olabilir.
- Missing değer impute edilmemelidir.

## 13. Sector analysis için local filtreler

Ana source sector activity codes:
`C`, `F`, `G46`, `G47`, `H`, `I`, `J`, `L`, `M`, `N`

Sector AI/productivity ana matched set:
- `C` Manufacturing
- `F` Construction
- `H` Transportation and storage
- `I` Accommodation and food service
- `J` Information and communication
- `M` Professional/scientific/technical
- `N` Administrative/support

`L` Real estate supplementary'dir.
`G46/G47` ICT descriptives için tutulabilir; mevcut sector-productivity extract ile ana
matched analysis'e girmez.

Productivity temporal association için:
- sector AI predictor = `G14_B`, **2023**
- sector productivity outcome = **2024**

Current descriptive sector adoption için:
- AI/cloud/data = 2025 kullanılabilir.

## 14. Yapısal kaynak kısıtı

Bu OECD ICT extract'inde:

- Country × firm size mümkündür.
- Country × sector mümkündür.
- **Country × sector × firm size aynı observation grain'inde mevcut değildir.**

Kod yazarken sector ve size'ı birlikte filtreleyip bir cross-tab varmış gibi davranmayın.

## 15. Local kodun uyması gereken minimum QA

Ana CSV load edildikten sonra en az şu kontroller yapılmalıdır:

```python
assert df.shape[0] == 5933
assert df.shape[1] == 34
assert list(df.columns) == ['STRUCTURE', 'STRUCTURE_ID', 'STRUCTURE_NAME', 'ACTION', 'REF_AREA', 'Reference area', 'FREQ', 'Frequency of observation', 'MEASURE', 'Measure', 'UNIT_MEASURE', 'Unit of measure', 'ACTIVITY', 'Economic activity', 'SIZE_CLASS', 'Employment size class', 'TIME_PERIOD', 'Time period', 'OBS_VALUE', 'Observation value', 'OBS_STATUS', 'Observation status', 'OBS_STATUS_2', 'Observation status 2', 'OBS_STATUS_3', 'Observation status 3', 'UNIT_MULT', 'Unit multiplier', 'TIME_HORIZON_USE', 'Time horizon', 'DECIMALS', 'Decimals', 'BREAKDOWN_V7', 'V7 Breakdowns']
assert df["UNIT_MEASURE"].dropna().unique().tolist() == ["PT_ENT"]
assert set(df["MEASURE"].unique()) == {'G7_B', 'H1_B', 'H3_B', 'G3_B', 'G14_B'}
assert set(df["ACTIVITY"].unique()) == {'_T', 'F', 'H', 'J', 'M', 'L', 'G47', 'G46', 'I', 'N', 'C'}
assert set(df["SIZE_CLASS"].unique()) == {'S_GE250', 'S_GE10', 'S10T49', 'S50T249'}
assert set(df["TIME_PERIOD"].astype(str).unique()) == {'2025', '2022', '2021', '2024', '2023'}
assert not df.duplicated(
    ["REF_AREA","FREQ","MEASURE","UNIT_MEASURE","ACTIVITY","SIZE_CLASS","TIME_PERIOD"]
).any()
```

`OBS_VALUE` numeric'e çevrilirken coercion sonrası unexpected NaN sayısı ayrıca kontrol edilmelidir.

## 16. AI/model'e sample ve ana dosya bağlamını verirken önerilen mesaj

> `OECD_ICT_unchanged_structure_sample.csv`, localde bulunan tam
> `OECD ICT Access and Usage by Businesses.csv` dosyasından seçilmiş, sütunları ve satır
> değerleri değiştirilmemiş bir schema/structure sample'dır. Sample'da analiz sonucu üretme;
> amacı tam dosyada çalışacak Python/R kodunu geliştirmek ve test etmektir. Tam dosya
> 5,933 satır × 34 sütundur ve bu bağlam belgesindeki full-dataset
> dimension/coverage metadata'sı source of truth'tur. Filtrelerde label yerine code
> columns (`REF_AREA`, `MEASURE`, `UNIT_MEASURE`, `ACTIVITY`, `SIZE_CLASS`,
> `TIME_PERIOD`) kullan. `OBS_STATUS*` flag'lerini koru. Sample istatistiksel olarak
> representative değildir. Üretilen production kodu localde tam CSV'ye uygulanacaktır.

## 17. Kullanım sınırı

Bu sample yeterlidir:
- schema inspection,
- parser/load code,
- filtering code,
- reshaping/pivot logic,
- merge-key preparation,
- status handling code,
- unit tests/smoke tests.

Bu sample yeterli değildir:
- final descriptive statistics,
- country rankings,
- correlations,
- regressions,
- coverage inference,
- statistical conclusions.

Bunların tamamı localde ana CSV üzerinde çalıştırılmalıdır.
