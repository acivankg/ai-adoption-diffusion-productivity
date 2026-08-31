# AI Readiness → Adoption → Productivity Portfolio Çalışması  
## Devir-Teslim ve Devam Kılavuzu — Tek Kaynak / Source of Truth

**Belge sürümü:** 1.2  
**Durum tarihi:** 31 Ağustos 2026  
**Mevcut aşama:** AŞAMA 3 tamamlandı  
**Sonraki aşama:** AŞAMA 4 — veri temizleme, standardizasyon, merge ve master analytical dataset  
**Dil:** Türkçe  
**Amaç:** Bu belgeyi okuyan ve önceki konuşmalara erişimi olmayan bir kişi veya yapay zekâ, çalışmayı mevcut noktadan doğru şekilde sürdürebilmelidir.

---

# 1. Çalışmanın Tanımı

## 1.1 Amaç

Bu çalışma, uluslararası danışmanlık firmalarına gönderilebilecek profesyonel bir portföy projesi olarak tasarlanmıştır. Temel amaç yalnızca “AI kullanımı yüksek ülkeleri sıralamak” değil; ülkelerin mevcut dijital altyapı, işletme becerileri, genel insan sermayesi ve ekonomik yapılarını **enterprise AI adoption’a ne ölçüde dönüştürebildiğini**, AI kullanımının firmalar ve çalışanlar arasında ne kadar yaygın/dengeli dağıldığını ve daha erken AI adoption ile daha sonraki productivity growth arasında keşifsel bir ilişki olup olmadığını değerlendiren açıklanabilir bir danışmanlık çerçevesi oluşturmaktır.

Çalışma şu profesyonel yetkinlikleri göstermeyi hedefler:

- araştırma problemi ve hipotez yapılandırma,
- çok kaynaklı veri seçimi ve uygunluk değerlendirmesi,
- veri temizleme / standardizasyon / merge,
- tanımlayıcı istatistik ve EDA,
- veri görselleştirme,
- hipotez testleri ve regresyon,
- küçük örneklemde robust istatistiksel uygulama,
- sektör ve firma büyüklüğü kırılımları,
- workforce diffusion / inclusion analizi,
- ilişki ile nedensellik arasındaki sınırların doğru kurulması,
- karar verici odaklı ülke segmentasyonu,
- stratejik ve politika çıkarımları,
- profesyonel rapor/sunum tasarımı.

Teknik karmaşıklık kendi başına hedef değildir. Yöntemler, çalışmanın iş ve politika açısından yorumlanabilirliğine hizmet etmelidir.

---

# 2. Güncel Araştırma Çerçevesi

## 2.1 Güncel önerilen başlık

> **From AI Readiness to Economic Advantage — Which Economies Are Best Positioned to Convert Digital and Human Capital into AI Adoption and Productivity Gains?**

## 2.2 Ana araştırma sorusu

> **Which European economies are most effectively converting digital infrastructure, enterprise skills and human capital into AI adoption; how evenly is adoption diffusing across firms and workers; and is earlier AI adoption associated with subsequent labour-productivity growth?**

## 2.3 Kavramsal zincir

```text
Digital & Skills Readiness
        ↓
Enterprise AI Adoption
        ↔
Workforce GenAI Adoption
        ↓
Productivity Association
```

Dağılım/eşitsizlik boyutları:

```text
Firm-size diffusion gaps
Workforce inclusion gaps
```

Yapısal bağlam:

```text
Economic development
Economic structure
```

## 2.4 Geçersizleşmiş eski çerçeve

İlk aşamada “AI exposure → readiness → adoption → outcomes” çerçevesi düşünülmüş ve çalışma başlığında “AI Exposure” / “Workforce Disruption” ifadeleri kullanılmıştır. Bu çerçeve **ana ampirik çalışma için geçersizdir**:

- ILO GenAI exposure veri setinin ana 27 ülkeyle ortak kapsamı yalnızca **Czechia ve France** olmuştur.
- Mevcut veri setlerinde doğrudan “job displacement/workforce disruption” outcome’u bulunmamaktadır.
- Bu nedenle exposure ve disruption ana ölçülen değişkenler gibi sunulmamalıdır.

ILO exposure verisi yalnızca **literatür/politika bağlamı veya supplementary material** olarak tutulabilir.

---

# 3. Kesinleşmiş Temel Örneklem

## 3.1 Ana 27 ülke

Ana country-level ampirik örneklem:

1. Austria
2. Belgium
3. Bulgaria
4. Croatia
5. Czechia
6. Denmark
7. Estonia
8. Finland
9. France
10. Germany
11. Greece
12. Hungary
13. Ireland
14. Italy
15. Latvia
16. Lithuania
17. Luxembourg
18. Netherlands
19. Norway
20. Poland
21. Portugal
22. Romania
23. Slovak Republic
24. Slovenia
25. Spain
26. Sweden
27. Türkiye

Ana regresyonlarda ve ülke skorlarında **aggregate bölgeler gözlem olarak kullanılmaz**.

## 3.2 Benchmark aggregate’lar

Kaynağa göre raw dosyada tutulabilecek aggregate’lar:

- OECD
- European Union benchmark (kaynak veri setine göre EU25 veya EU27)

Bunlar yalnızca grafik/benchmark için kullanılabilir. **Regresyon gözlemi değildir.**

## 3.3 ISO3 master country key

Merge işlemlerinde ülke adına değil mümkün olduğunca ISO3 koda güvenilmelidir.

| Ülke | ISO3 |
|---|---|
| Austria | AUT |
| Belgium | BEL |
| Bulgaria | BGR |
| Croatia | HRV |
| Czechia | CZE |
| Denmark | DNK |
| Estonia | EST |
| Finland | FIN |
| France | FRA |
| Germany | DEU |
| Greece | GRC |
| Hungary | HUN |
| Ireland | IRL |
| Italy | ITA |
| Latvia | LVA |
| Lithuania | LTU |
| Luxembourg | LUX |
| Netherlands | NLD |
| Norway | NOR |
| Poland | POL |
| Portugal | PRT |
| Romania | ROU |
| Slovak Republic | SVK |
| Slovenia | SVN |
| Spain | ESP |
| Sweden | SWE |
| Türkiye | TUR |

World Bank’te ülke adı `Turkiye` olabilir; ISO3 `TUR` doğrudur. Eurostat geo kodlarında Greece `EL`, Türkiye `TR` olarak gelir. Master map açıkça tutulmalıdır.

---

# 4. Veri Kaynakları — Nihai Envanter

## 4.1 Aktif ana kaynaklar

**Adlandırma kuralı:** Her veri seti bu bölümde yalnızca bir kez `Standart çalışma adı (yüklenen dosya adı)` biçiminde tanımlanır. Belgenin sonraki bölümlerinde yalnızca standart çalışma adı kullanılır. Productivity extract’lerinde yükleme ekranında aynı basename göründüğü için ilk/ikinci yükleme ve file ID ayrıca belirtilmiştir.


| Katman | Veri seti — standart çalışma adı (yüklenen dosya adı) | Statü |
|---|---|---|
| Enterprise AI + digital readiness + firm size + sectors | **OECD Business ICT** (`OECD ICT Access and Usage by Businesses.csv`) | ONAYLI |
| Workforce GenAI | **Eurostat Workforce GenAI** (`Eurostat Individuals – use of generative AI tools.csv`) | ONAYLI |
| Human capital | **OECD Educational Attainment** (`OECD educational attainment.csv`) | ONAYLI |
| Economic development | **World Bank GDP per capita PPP** (`GDP per capita, PPP.csv`) | ONAYLI |
| Economic structure | **World Bank Services Employment** (`Employment in services.csv`) | ONAYLI |
| Macro productivity | **OECD Productivity — Macro/Total extract** (`OECD Productivity database.csv`, ilk Productivity yüklemesi; file ID `file_0000000008fc821086469ea000a9a69e`) | ONAYLI |
| Sector productivity | **OECD Productivity — Sector extract** (`OECD Productivity database.csv`, ikinci Productivity yüklemesi; file ID `file_00000000931882108803be75538772c9`) | ONAYLI |

## 4.2 Supplementary / ana merge dışında

| Veri seti — standart çalışma adı (yüklenen dosya adı) | Karar |
|---|---|
| **ILOSTAT GenAI Exposure** (`Employment by sex and generative AI exposure (thousands).csv`) | Ana modelde KULLANMA; yalnızca contextual/supplementary |

## 4.3 Kritik dosya adı ve kimliklendirme notu

İki OECD Productivity extract’i kullanıcı tarafından **aynı görünen özgün dosya adıyla** (`OECD Productivity database.csv`) iki ayrı zamanda yüklenmiştir. Bunlar OECD’nin iki farklı veri seti değil, aynı `OECD Productivity Database (DSD_PDB@DF_PDB)` içinden farklı filtrelerle alınmış iki ayrı extract’tir.

Kesin kimlik:

- **Macro/Total extract — ilk yükleme**
  - Özgün görünen dosya adı: `OECD Productivity database.csv`
  - Upload/file ID: `file_0000000008fc821086469ea000a9a69e`
  - 573 data row × 34 column
  - Measure: `GDP per hour worked` + `Gross value added per hour worked`
  - Economic activity: yalnızca `Total - all activities`
  - Unit: `US dollars per hour, PPP converted`

- **Sector extract — ikinci yükleme**
  - Özgün görünen dosya adı: `OECD Productivity database.csv`
  - Upload/file ID: `file_00000000931882108803be75538772c9`
  - 3.366 data row × 34 column
  - Measure: yalnızca `Gross value added per hour worked`
  - Economic activity: Total + sekiz seçilmiş sektör
  - Unit: sektörlerde `National currency per hour`; Total satırlarında ayrıca PPP-USD serileri

`OECD Productivity database - macro.csv` ve `OECD Productivity database - sector.csv` ifadeleri **kullanıcının özgün dosya adları değil**, çalışma içinde çakışmayı önlemek amacıyla önerilen/oluşturulan iç alias adlarıdır.

---

# 5. OECD Business ICT — Kaynak Spesifikasyonu

**Boyut:** 5.933 satır × 34 sütun  
**Rol:** Ana enterprise AI adoption, digital readiness, firm-size diffusion, sector adoption.

Resmî kaynak:
- OECD Data Explorer — *ICT Access and Usage by Businesses*
- Veri akışı: `OECD.STI.DEP / DSD_ICT_B@DF_BUSINESSES`
- OECD sayfası bu verinin OECD model survey + European Statistical System/Eurostat kaynaklarıyla üretildiğini belirtir.

## 5.1 Seçilmiş measure’lar — aynen korunacak

1. `Businesses purchasing cloud computing services`
2. `Businesses having performed big data analysis`
3. `Businesses using artificial intelligence (AI)`
4. `Businesses which employ ICT specialists`
5. `Businesses which provided any type of training to develop ICT related skills of the persons employed`

## 5.2 Unit

- `Percentage of enterprises`

Başka unit kullanılmamalıdır.

## 5.3 Economic activity

Raw extract’te tutulmuş 11 activity:

- Total - all activities
- Manufacturing
- Construction
- Wholesale trade, except of motor vehicles and motorcycles
- Retail trade, except of motor vehicles and motorcycles
- Transportation and storage
- Accommodation and food service activities
- Information and communication
- Real estate activities
- Professional, scientific and technical activities
- Administrative and support service activities

Financial and insurance ana extract’e alınmamıştır.

## 5.4 Employment size class

- 10 or more
- From 10 to 49
- From 50 to 249
- 250 or more

## 5.5 Time period

- 2021–2025 raw olarak korunmuş.

## 5.6 Ana country-level yıl eşleştirmesi — KESİN

| Kavram | Değişken | Yıl |
|---|---|---:|
| Enterprise AI adoption | Businesses using AI | **2025** |
| Digital foundation | Cloud computing | **2025** |
| Data capability | Big data analysis | **2025** |
| Enterprise specialist capacity | ICT specialists | **2024** |
| Enterprise skills investment | ICT training | **2023** |

ICT specialists ve ICT training için 2025 yoktur / survey module timing nedeniyle ana en güncel uygun yıllar sırasıyla 2024 ve 2023’tür.

## 5.7 27-country coverage — ana değişkenler

Aşağıdaki kombinasyonda `Total - all activities + 10 or more`:

- AI 2025: 27/27
- Cloud 2025: 27/27
- Data analytics 2025: 27/27
- ICT specialists 2024: 27/27
- ICT training 2023: 27/27

## 5.8 Observation-status flag’leri — ana cross-section

- AI 2025: Netherlands = `Time series break`; diğer 26 normal.
- Data analytics 2025: Czechia = `Time series break`; diğer 26 normal.
- ICT specialists 2024: Sweden = `Time series break`; diğer 26 normal.
- ICT training 2023: Sweden = `Time series break`; diğer 26 normal.
- Cloud 2025: 27/27 normal.

**Kural:** Flagged değerler ana cross-sectional analizden otomatik silinmeyecek; fakat ilgili modeller için **flag-exclusion robustness** yapılacak.

## 5.9 Trend kuralı

- 2021 AI serisinde ana 27 ülkenin tamamı `Time series break` flag’i taşır.
- Bu nedenle **2021→2025 headline trend KULLANILMAMALI**.
- Trend gerekiyorsa 2023→2025 daha güvenlidir; yine 2023 AI’da France ve Sweden time-series-break flag’i vardır ve sensitivity gerekir.

## 5.10 Firm-size coverage

2025:

- AI: dört size class’ın tamamı 27/27.
- Cloud: 10+, small ve large 27/27; medium (50–249) Portugal eksik.
- Data analytics: aynı şekilde medium Portugal eksik.

Ana firm-size değişkeni için AI kullanılacağı için 27 ülke korunur.

## 5.11 Sektör coverage — 2025 AI + cloud + data aynı anda

| Sektör | Ortak ülke sayısı |
|---|---:|
| Construction | 27 |
| Professional, scientific and technical | 27 |
| Accommodation and food service | 26 |
| Information and communication | 26 |
| Manufacturing | 26 |
| Administrative and support | 25 |
| Transportation and storage | 25 |
| Wholesale | 25 |
| Retail | 24 |
| Real estate | 17 |

**Real estate ana sektör analizinde kullanılmamalı; supplementary.**

## 5.12 Yapısal kısıt

OECD ICT extract’inde:

- Country × Size mümkündür.
- Country × Industry mümkündür.
- **Country × Industry × Size mümkün değildir.**

Sektör ve firma büyüklüğü aynı analizde çaprazlanmamalıdır.

---

# 6. Eurostat Workforce GenAI — Kaynak Spesifikasyonu

**Boyut:** 39.006 satır × 21 sütun  
**Yıl:** yalnızca 2025  
**Rol:** Workforce GenAI adoption, gender/education/age inclusion gaps.

Resmî Eurostat gösterge ailesi:
- `I_IUAI` — use of generative AI in last 3 months
- `I_IUAIPR` — private purposes
- `I_IUAIWP` — professional (work) purposes
- `I_IUAIFE` — formal education

## 6.1 Ana workforce değişkeni — KESİN

Filtre:

- `indic_is = I_IUAIWP`
- `ind_type = SAL_SELF_FAM`
- `unit = PC_IND`

Tanım:

> Percentage of employees, self-employed and family workers aged 16–74 who used generative AI tools for professional/work purposes in the last 3 months.

Analytical name:

`workforce_genai_use_pct`

## 6.2 Ana coverage

- 27/27 ana ülke.
- Ana workforce değişkeninde low reliability flag yoktur.

## 6.3 Demografik kırılımlar

### Gender — ana
- `F_Y16_74`
- `M_Y16_74`
- Coverage 27/27, reliability sorunu yok.

### Education — ana
- `I0_2` = low
- `I3_4` = medium
- `I5_8` = high

High ve medium 27/27.
Low category’de Croatia `u` unreliable/missing; education high-low gap ana testte **n=26** olabilir. **İmpute etme.**

### Age — ikincil ama kullanılabilir
- 16–24
- 25–34
- 35–44
- 45–54
- 55–64

Ana gap önerisi 25–34 vs 55–64’tür. Coverage 27/27.

Citizenship, country of birth, urbanisation ve çok sayıda diğer alt kırılım **scope creep** yaratacağı için ana çalışmaya alınmamalıdır.

## 6.4 Enterprise vs workforce ölçüm uyarısı

Enterprise AI yüzdesi ile workforce GenAI yüzdesinin paydaları farklıdır.

Bu nedenle:

```text
Enterprise AI % − Workforce GenAI %
```

hesabı yapılabilir ancak **aynı popülasyondaki gerçek “shortfall”** olarak sunulamaz.

Doğru yorum:

> relative enterprise–workforce diffusion alignment indicator.

---

# 7. OECD Educational Attainment — Human Capital

**Boyut:** 193 satır × 50 sütun  
**Rol:** General/educational human capital.

## 7.1 Exact download filters

### Reference area
27 ana ülke +:
- OECD
- European Union (25 countries)

### Sex
- **Total only**

### Age
- **From 25 to 64 years only**

### Educational attainment level
- **Tertiary education only**

### Statistical operation
- **Observed only**

### Time
- 2019–2025

## 7.2 Ana değişken

`tertiary_attainment_2024`

Tanım:

> 25–64 yaş toplam yetişkin nüfusta tertiary education tamamlamış olanların yüzdesi.

Kavramsal rol:

> General Human Capital / Educational Human Capital.

**AI-specific skill diye adlandırılmamalıdır.**

## 7.3 Yıllık coverage

Ana 27 ülke:

| Yıl | Geçerli ülke |
|---:|---:|
| 2019 | 27 |
| 2020 | 23 |
| 2021 | 25 |
| 2022 | 26 |
| 2023 | 27 |
| **2024** | **27** |
| 2025 | 26 |

2024’te 27/27 `Normal value`.

2025:
- 26/27 geçerli,
- Denmark = time series break,
- France 2025 eksik.

OECD Data Explorer, latest available year verilerinin preliminary olduğunu ve final 2025 verilerinin **29 Eylül 2026** tarihinde yayımlanacağını belirtmektedir.

**Ana modelde 2024 kullanılacak.**

---

# 8. World Bank GDP per capita PPP — Economic Development

**Kaynak:** World Development Indicators  
**Indicator code:** `NY.GDP.PCAP.PP.KD`  
**Indicator:** `GDP per capita, PPP (constant 2021 international $)`  
**Dosya WDI update tarihi:** 13 Temmuz 2026

## 8.1 Coverage

Ana 27 ülkenin tamamında 2019–2025 eksiksiz.

## 8.2 Ana değişken

Raw:
`gdp_per_capita_ppp_2024`

Modelde tercih:
`log_gdp_per_capita_ppp_2024 = ln(gdp_per_capita_ppp_2024)`

## 8.3 Neden log?

GDPpc dağılımında Ireland ve Luxembourg gibi yüksek değerler leverage yaratabilir. Log dönüşümü ekonomik gelişmişlik ilişkisini daha stabilize eder.

**Ireland ve Luxembourg otomatik silinmez.** Sensitivity analizinde ayrıca değerlendirilebilir.

## 8.4 Kullanım kuralı

Bu değişken:

- AI adoption modellerinde general development control olabilir.
- Productivity outcome modelinde otomatik/standart kontrol olarak eklenmemeli; outcome ile kavramsal olarak yakın olabilir ve over-control yaratabilir.

---

# 9. World Bank Services Employment — Economic Structure

**Indicator code:** `SL.SRV.EMPL.ZS`  
**Indicator:** `Employment in services (% of total employment) (modeled ILO estimate)`  
**Kaynak:** WDI / ILO Modelled Estimates (ILOEST)  
**Dosya WDI update tarihi:** 13 Temmuz 2026

## 9.1 Coverage

Ana 27 ülkenin tamamında 2019–2025 eksiksiz.

## 9.2 Ana değişken

`services_employment_share_2024`

## 9.3 Yorum kuralı

Bu değer doğrudan tek bir ulusal anket gözlemi olarak sunulmamalıdır. ILO modelled estimate’tir.

Rolü:

> structural/economic composition proxy.

## 9.4 Multicollinearity riski

Suitability diagnostic:

- services ↔ tertiary attainment ≈ 0.80
- services ↔ log GDPpc ≈ 0.75
- services ↔ cloud ≈ 0.50

Bu nedenle services + tertiary + GDPpc aynı küçük regresyona otomatik olarak doldurulmamalıdır.

---

# 10. OECD Productivity — Macro/Total Extract

**Kimlik:** ilk Productivity yüklemesi; file ID `file_0000000008fc821086469ea000a9a69e`  
**Önerilen raw çalışma alias’ı:** `oecd_productivity_macro_raw.csv`  
**Boyut:** 573 satır × 34 sütun  
**Rol:** Macro productivity positioning + lagged productivity association.

## 10.1 İçerik

Measure:
- `GDP per hour worked`
- `Gross value added per hour worked`

Economic activity:
- `Total - all activities`

Unit:
- `US dollars per hour, PPP converted`

Price base:
- `Chain linked volume (rebased)`

Transformation:
- `Non transformed data`
- `Growth rate, over 1 year`

Not:
- GDP/hour satırlarında ana extract’te yalnızca non-transformed levels vardır.
- GVA/hour için level + growth bulunmaktadır.

## 10.2 Ana productivity level

`GDP per hour worked`, **2024**.

Coverage:
- 26/27.
- Türkiye bu PPP-rebased seri için 2021 sonrası yoktur; 2024’e carry-forward yapılmaz.

## 10.3 2025

2025’te coverage düşer:
- Türkiye eksik,
- Bulgaria eksik,
- Sweden estimated.

Bu nedenle ana level yılı 2024’tür.

## 10.4 Ireland/Luxembourg

OECD 2026 Compendium, Ireland ve Luxembourg headline GDP/hour değerlerinin multinational activities nedeniyle şişebildiğini açıkça belirtir.

Kural:

- Ana örneklemde tutulabilir.
- Productivity robustness’ta **Ireland + Luxembourg exclusion sensitivity** yapılmalıdır.

## 10.5 Macro growth outcome

AŞAMA 3 tasarımında ana lagged productivity outcome olarak GDP/hour growth 2024 kullanılmak istenmektedir.

GDPHRS için direct `GY` satırı extract’te yoktur; bu nedenle:

```text
gdp_hour_growth_2024 =
100 * (GDPHRS_2024 / GDPHRS_2023 - 1)
```

şeklinde aynı real/rebased GDPHRS level serisinden hesaplanmalıdır.

Robustness:
- OECD’nin direct `GVAHRS + GY + 2024` serisiyle kontrol edilebilir.

**Transformation=GY satırlarında unit label USD/hour olarak kalabilse bile observation gerçek anlamda yıllık yüzde büyümedir; transformation dimension önceliklidir.**

---

# 11. OECD Productivity — Sector Extract

**Kimlik:** ikinci Productivity yüklemesi; file ID `file_00000000931882108803be75538772c9`  
**Önerilen raw çalışma alias’ı:** `oecd_productivity_sector_raw.csv`  
**Boyut:** 3.366 satır × 34 sütun  
**Rol:** Sector AI adoption ↔ subsequent sector productivity growth.

## 11.1 Exact download structure

Reference area:
- 27 ana ülke
- EU27
- OECD

Measure:
- **Gross value added per hour worked only**

Economic activity:
- Total - all activities
- Manufacturing
- Construction
- Transportation and storage
- Accommodation and food service activities
- Information and communication
- Real estate activities
- Professional, scientific and technical activities
- Administrative and support service activities

Unit:
- filtre boş bırakılmıştır.
- sektörlerde fiilen `National currency per hour`,
- Total’da ayrıca PPP-USD satırları gelir.

Price base:
- `Chain linked volume (rebased)`

Transformation:
- `Growth rate, over 1 year`
- `Non transformed data`

Asset:
- `Not applicable`

Conversion:
- filtre boş; data appropriate combination’ı döndürür:
  - sectors: Not applicable
  - PPP total: PPP converted

Time:
- 2019–2025

## 11.2 Ana sektör outcome

```text
Sector GVA/hour annual growth, 2024
```

Cross-country sector productivity **levels** national currency cinsinden karşılaştırılmamalıdır.

Cross-country karşılaştırma yalnızca:

> growth rate over 1 year

üzerinden yapılır.

## 11.3 Coverage

2019–2024 döneminde seçilen sekiz sektörün her birinde:

- 26/27 ülke,
- tek eksik ülke Türkiye.

2025 sector productivity fiilen yalnızca Norway için mevcuttur; ana analize uygun değildir.

Bu OECD 2026 sektör coverage notuyla uyumludur; Türkiye data availability nedeniyle sektör grafiğinde dışarıda bırakılan ülkeler arasındadır.

## 11.4 Ana yedi sektör

Sector productivity ana modelinde:

1. Manufacturing
2. Construction
3. Transportation and storage
4. Accommodation and food service activities
5. Information and communication
6. Professional, scientific and technical activities
7. Administrative and support service activities

**Real estate supplementary**.

Retail ve wholesale ICT’de mevcut olsa da productivity sector extract’inde yoktur; ana matched-sector modeline alınmaz.

## 11.5 2023 sector AI × 2024 sector productivity ortak sample

- Manufacturing: 26
- Construction: 25
- Transportation and storage: 26
- Accommodation and food service: 26
- Information and communication: 25
- Professional/scientific/technical: 26
- Administrative/support: 26
- Real estate: 25

Türkiye productivity nedeniyle tüm sektörlerde dışarıda kalır; bazı sektörlerde ek AI missing de vardır.

---

# 12. ILOSTAT GenAI Exposure — Supplementary Only

**Boyut:** 9.779 satır × 10 sütun  
**Kapsam:** yaklaşık 87 ülke/territory, 1996–2026.

Exposure categories:
- Total
- Gradient 4 highest exposure
- Gradient 3
- Gradient 2
- Gradient 1
- Minimal
- X NEC

Sex:
- Total
- Male
- Female

Ana 27 ülke ile overlap:
- Czechia
- France

**Karar:** Ana country-level modelde, scoring’de veya merge’de KULLANMA. Exposure kavramı raporun literature/policy context bölümünde açıklanabilir ancak “biz exposure’u ölçtük” denmemelidir.

---

# 13. Zaman Eşleştirme Matrisi — KESİN

| Kavram | Kaynak | Ana yıl |
|---|---|---:|
| Enterprise AI adoption | OECD ICT | **2025** |
| Cloud readiness | OECD ICT | **2025** |
| Data analytics readiness | OECD ICT | **2025** |
| ICT specialists | OECD ICT | **2024** |
| ICT training | OECD ICT | **2023** |
| Tertiary attainment | OECD Education | **2024** |
| GDP per capita PPP | WDI | **2024** |
| Services employment share | WDI | **2024** |
| Workforce professional GenAI | Eurostat | **2025** |
| Macro productivity level | OECD Productivity | **2024** |
| Macro lagged AI predictor | OECD ICT AI | **2023** |
| Macro subsequent productivity growth | computed GDP/hour growth | **2024** |
| Sector lagged AI predictor | OECD ICT sector AI | **2023** |
| Sector productivity growth outcome | OECD GVA/hour GY | **2024** |

Bu “mixed-year” tasarım hata değildir; survey availability ve temporal ordering nedeniyle bilinçli olarak kurulmuştur.

---

# 14. Nihai Hipotezler

| Kod | Hipotez | Statü |
|---|---|---|
| H1 | Stronger digital foundation is associated with higher enterprise AI adoption. | ANA |
| H2 | Stronger enterprise skills and general human capital are associated with higher enterprise AI adoption. | ANA |
| H3 | More service-intensive economies exhibit higher enterprise AI adoption. | ANA |
| H4 | AI adoption is higher among large firms than small firms. | ANA |
| H5 | Enterprise AI adoption and professional workforce GenAI use are positively associated. | ANA |
| H6 | Workforce GenAI adoption differs by education, age and, to a lesser extent, gender. | ANA |
| H7 | 2023 enterprise AI adoption is positively associated with 2024 macro labour-productivity growth. | EXPLORATORY |
| H8 | 2023 sector AI adoption is positively associated with 2024 sector GVA/hour growth. | EXPLORATORY |

H7/H8’de **causal language kullanılamaz**.

---

# 15. Değişkenler ve Türetilmiş Göstergeler

## 15.1 Ana değişken isimleri

Önerilen cleaned/master isimler:

```text
country
iso3

enterprise_ai_2025
cloud_2025
data_analytics_2025
ict_specialists_2024
ict_training_2023
tertiary_attainment_2024
gdp_per_capita_ppp_2024
log_gdp_per_capita_ppp_2024
services_employment_share_2024

workforce_genai_work_2025

gdp_per_hour_2023
gdp_per_hour_2024
gdp_per_hour_growth_2024
gva_per_hour_growth_2024

ai_small_2025
ai_medium_2025
ai_large_2025
```

## 15.2 Firm-size gap

```text
sme_ai_gap =
ai_large_2025 - ai_small_2025
```

Ana politika gap’i large vs small’dır.

Cloud/data firm-size gaps supplementary olabilir.

## 15.3 Workforce inclusion gaps

```text
education_gap =
genai_high_education - genai_low_education
```

```text
age_gap =
genai_age_25_34 - genai_age_55_64
```

```text
gender_gap =
genai_male - genai_female
```

Education gap Croatia low-education unreliable/missing nedeniyle n=26 olabilir.

## 15.4 Digital Foundation Index

```text
DigitalFoundation =
mean(
  z(cloud_2025),
  z(data_analytics_2025)
)
```

## 15.5 Skills Readiness Index

```text
SkillsReadiness =
mean(
  z(ict_training_2023),
  z(ict_specialists_2024),
  z(tertiary_attainment_2024)
)
```

## 15.6 AI Readiness Index

```text
AIReadiness =
mean(
  DigitalFoundation,
  SkillsReadiness
)
```

Kural:
- eşit ağırlıklı,
- şeffaf,
- black-box değildir,
- **27 core-country sample** üzerinde standardize edilir,
- aggregate benchmark’lar z-score hesabına girmez.

Uygulama standardı olarak sample standard deviation (`ddof=1`) kullanılabilir; kodda açıkça yazılmalıdır.

## 15.7 Readiness → Adoption Conversion Score

```text
ConversionScore =
z(enterprise_ai_2025) - AIReadiness
```

Yorum:

- yüksek pozitif = readiness seviyesine göre adoption outperformer,
- ≈0 = aligned,
- yüksek negatif = under-converter / latent capacity.

Bu skor nedensel ölçü değildir; relative diagnostic’tir.

## 15.8 Country archetypes — consulting segmentation

Readiness z=0 ve AI adoption z=0 sınırlarıyla:

| Readiness | Adoption | Segment |
|---|---|---|
| High | High | Scaled leaders |
| High | Low | Under-converters |
| Low | Low | Foundation builders |
| Low | High | Adoption outperformers |

Bu bir **istatistiksel clustering algoritması değildir**. K-means ana segmentation olarak kullanılmamalıdır.

## 15.9 Enterprise–Workforce diffusion alignment

Ana analiz:

```text
enterprise_ai_2025 ↔ workforce_genai_work_2025
```

Quadrant framework kullanılabilir:

- High enterprise / high workforce = broad-based diffusion
- High enterprise / low workforce = enterprise-led diffusion
- Low enterprise / high workforce = workforce-led latent potential
- Low / low = low-diffusion economy

Quadrant threshold method AŞAMA 4/5’te açıkça sabitlenmelidir; standardize sample mean (`z=0`) en tutarlı default’tur, fakat final grafik üretilmeden önce kayda geçirilmelidir.

---

# 16. Ana İstatistiksel Tasarım

## 16.1 Country regressions

Örneklem n≈27 olduğu için tek büyük regression **yasaktır**.

### Model 1 — Digital foundation

```text
AI_2025 =
β0
+ β1 Cloud_2025
+ β2 DataAnalytics_2025
+ β3 logGDPpc_2024
+ ε
```

### Model 2 — Skills readiness

```text
AI_2025 =
β0
+ β1 ICTTraining_2023
+ β2 ICTSpecialists_2024
+ β3 TertiaryEducation_2024
+ ε
```

### Model 3 — Economic structure

```text
AI_2025 =
β0
+ β1 ServicesShare_2024
+ β2 logGDPpc_2024
+ ε
```

### Model 4 — Integrated readiness

```text
AI_2025 =
β0
+ β1 AIReadiness
+ β2 logGDPpc_2024
+ ε
```

Regressor’lar katsayı karşılaştırması için z-standardize edilebilir. Outcome percentage point düzeyinde bırakılabilir.

## 16.2 Standard errors

Country-level OLS için:

> **HC3 heteroskedasticity-robust standard errors**

kullanılmalıdır.

Raporlama:

- coefficient
- 95% CI
- robust p-value
- R²
- N

P-value tek başına ana sonuç değildir.

## 16.3 Multicollinearity

Her model öncesi:

- correlation matrix,
- VIF,
- predictor redundancy değerlendirmesi.

Small sample nedeniyle redundant variable’lar aynı modele zorla eklenmemelidir.

## 16.4 Outlier/influence

- Cook’s distance
- leverage
- studentized residual
- leave-one-country-out stability

kontrol edilmelidir.

Outlier görmek otomatik deletion gerekçesi değildir.

---

# 17. Firm-Size Analizi

Ana karşılaştırma:

```text
Large firms vs Small firms
```

Aynı ülke içindeki paired observations kullanıldığı için independent-sample test kullanılmaz.

Ana test:

> **Wilcoxon signed-rank test**

Rapor:

- mean percentage-point gap
- median gap
- Wilcoxon p-value
- rank-biserial effect size
- country distribution

Medium firm grafikte gösterilebilir; ana headline gap large-small.

---

# 18. Workforce GenAI Analizi

## 18.1 Enterprise ↔ workforce

- Pearson correlation
- Spearman correlation
- scatter plot
- country labels yalnızca analytically meaningful outlier/leader’larda tercih edilebilir.

Bu ilişki **same-denominator gap değildir**.

## 18.2 Inclusion tests

Gender, education ve age gaps için paired-country framework.

Ana robust test:
- Wilcoxon signed-rank.

Dağılım uygun ise paired t-test secondary olarak raporlanabilir.

Birden çok subgroup testinde:
- **Holm multiple-comparison correction**.

Önem:
- percentage-point effect,
- distribution,
- CI,
- country heterogeneity

p-value’dan daha önceliklidir.

---

# 19. Macro Productivity Tasarımı

## 19.1 2024 productivity level

`GDP per hour worked 2024`:

- economic performance positioning / benchmark,
- **2025 AI’nin outcome’u gibi modellenmez**.

## 19.2 Lagged exploratory productivity model

```text
ProductivityGrowth_2024 =
β0
+ β1 AIAdoption_2023
+ β2 ln(ProductivityLevel_2023)
+ ε
```

Outcome önceliği:
- GDP/hour growth computed from GDPHRS levels.

Robustness:
- direct OECD GVA/hour growth 2024.

Sample:
- Türkiye eksik → yaklaşık n=26.

Sensitivity:
- Ireland + Luxembourg exclude,
- 2023 AI time-series-break flag’leri (France, Sweden) exclude,
- leave-one-out.

**Sonuç causal değildir.**

Doğru dil:

> Earlier AI adoption is associated with subsequent productivity growth.

Yanlış dil:

> AI caused national productivity growth.

---

# 20. Sector Productivity Tasarımı

## 20.1 Ana ilişki

```text
Sector AI Adoption 2023
        ↓
Sector GVA/hour Growth 2024
```

Ana yedi sector.

İlk aşama:
- sector-by-sector scatter,
- Pearson/Spearman (özellikle Spearman robust alternatif).

Pooled exploratory model:

```text
Growth[c,s,2024] =
β1 AI[c,s,2023]
+ Sector FE
+ ε
```

Robustness:

```text
Growth[c,s,2024] =
β1 AI[c,s,2023]
+ Sector FE
+ Country FE
+ ε
```

Standard errors:
- country-clustered.

Real estate:
- supplementary only.

**National-currency sector levels cross-country karşılaştırılmaz.**

---

# 21. Önceden Belirlenmiş Robustness Protokolü

| Risk | Kural |
|---|---|
| n≈27 | Parsimonious models; HC3 |
| Heteroskedasticity | HC3 |
| Outliers | Cook/leverage + leave-one-out |
| Ireland/Lux productivity distortion | exclusion sensitivity |
| OECD B time-series breaks | main modelde gerekirse tut; exclusion sensitivity |
| Non-normal association | Pearson yanında Spearman |
| Multicollinearity | correlation + VIF + pillar-specific models |
| Multiple subgroup tests | Holm correction |
| Workforce/enterprise denominator difference | literal pp shortfall iddiası yok |
| Observational design | causal wording yok |
| Sector national currency | level değil growth |
| Sector coverage | common/balanced sample robustness |
| ILO services modeled estimate | structural proxy olarak yorumla |
| Missing data | keyfi imputation yok |
| Aggregate OECD/EU | regression observation değil |

---

# 22. Forecasting Kararı

Core study’de forecasting **YAPILMAYACAK**.

Gerekçe:

- güvenilir AI adoption zaman serisi çok kısa,
- 2023–2025 diffusion rejimi çok hızlı değişiyor,
- OECD 2025 enterprise AI adoption’ının 2023’e göre iki kattan fazla arttığını raporlamıştır.

3–4 veri noktasıyla ARIMA/ETS gibi model kullanmak profesyonel görünmek yerine metodolojik olarak zayıf olur.

Appendix’te gerekirse:
- illustrative scenario

üretilebilir; **forecast** denmemelidir.

---

# 23. Preliminary Suitability Diagnostics — Nihai Bulgu Değildir

Aşağıdaki değerler yalnızca veri seçimi / uygunluk kontrolünde hesaplandı. Nihai analitik sonuç olarak rapora doğrudan kopyalanmamalı; AŞAMA 5’te temiz master data üzerinden yeniden üretilmelidir.

27 ülke basit Pearson correlation yaklaşık:

| İlişki | r |
|---|---:|
| Enterprise AI 2025 ↔ Workforce professional GenAI 2025 | 0.79 |
| Enterprise AI ↔ Services share 2024 | 0.73 |
| Enterprise AI ↔ Cloud 2025 | 0.71 |
| Enterprise AI ↔ ICT training 2023 | 0.70 |
| Enterprise AI ↔ log GDPpc 2024 | 0.67 |
| Enterprise AI ↔ Tertiary attainment 2024 | 0.63 |
| Enterprise AI ↔ Data analytics 2025 | 0.53 |
| Enterprise AI ↔ ICT specialists 2024 | 0.52 |

Structural predictor correlations yaklaşık:

- Services ↔ tertiary = 0.80
- Services ↔ log GDPpc = 0.75
- Tertiary ↔ log GDPpc = 0.71
- Cloud ↔ log GDPpc = 0.60

Bu nedenle pillar-specific model tasarımı korunmalıdır.

---

# 24. Veri Yönetimi Kuralları — Kesin

## 24.1 Raw dosyaları değiştirme

Raw CSV’ler immutable kabul edilmelidir.

- kolon silme,
- satır silme,
- isim değiştirme,
- imputation,
- overwrite

raw üzerinde yapılmamalıdır.

Tüm işlemler `clean/` veya `derived/` dosyalarında yapılmalıdır.

## 24.2 Önerilen klasör yapısı

```text
project/
├─ data/
│  ├─ raw/
│  ├─ clean/
│  ├─ derived/
│  └─ metadata/
├─ notebooks/
├─ src/
├─ outputs/
│  ├─ tables/
│  ├─ figures/
│  └─ models/
├─ report/
└─ README.md
```

## 24.3 Önerilen dosya isimleri

```text
oecd_ict_business_raw.csv
eurostat_genai_individuals_raw.csv
oecd_education_attainment_raw.csv
wb_gdppc_ppp_raw.csv
wb_services_employment_raw.csv
oecd_productivity_macro_raw.csv
oecd_productivity_sector_raw.csv
ilostat_genai_exposure_supplementary_raw.csv
```

Temiz dosyalar:

```text
country_core_2025.csv
firm_size_ai_2025.csv
workforce_genai_2025.csv
sector_ai_2023.csv
sector_productivity_growth_2024.csv
country_master.csv
```

## 24.4 Master merge key

Ana country file:
- `iso3` primary key.
- `country` display label.

Sector file:
- `iso3`
- `sector_code` / canonical sector label
- year

Firm-size file:
- `iso3`
- `size_class`
- year

## 24.5 Duplicate rule

Her analytical table için expected grain önceden tanımlanmalıdır.

Örnek:

```text
country_master:
1 row per ISO3
```

```text
sector_panel:
1 row per ISO3 × sector × year
```

Merge sonrası duplicate oluşursa analiz DURDURULUP grain sorunu çözülmelidir. `drop_duplicates()` ile kör biçimde sorun gizlenmemelidir.

---

# 25. AŞAMA 4 — Bundan Sonra Tam Olarak Ne Yapılmalı?

**AŞAMA 4 henüz yapılmamıştır. Başlangıç noktası burasıdır.**

## 25.1 Adım 1 — Raw inventory checksum / shape kontrolü

Her dosya için kaydet:

- filename
- row count
- column count
- source
- last-update metadata varsa
- expected key columns
- current hash/checksum (opsiyonel fakat önerilir)

Beklenen bilinen boyutlar:

| Dosya | Satır × sütun |
|---|---|
| OECD ICT | 5.933 × 34 |
| OECD Education | 193 × 50 |
| Eurostat GenAI | 39.006 × 21 |
| OECD Productivity macro | 573 × 34 |
| OECD Productivity sector | 3.366 × 34 |
| ILO exposure | 9.779 × 10 |
| WDI GDPpc | 265 × 71 |
| WDI services | 265 × 71 |

## 25.2 Adım 2 — Canonical country map oluştur

Tek mapping table:

```text
country_source_name
country
iso2
iso3
source
```

Özellikle:

- Turkiye ↔ Türkiye ↔ TUR
- Greece ↔ EL ↔ GRC
- Slovak Republic ↔ Slovakia display differences
- Eurostat geo codes

manuel ve test edilebilir biçimde çözülmelidir.

## 25.3 Adım 3 — OECD ICT clean tables

Üret:

### `country_readiness.csv`
27 row:
- enterprise_ai_2025
- cloud_2025
- data_analytics_2025
- ict_specialists_2024
- ict_training_2023
- source flags per variable

### `firm_size_ai.csv`
27 × four size class.

### `sector_ai.csv`
Country × sector × 2023/2025 AI as needed.
Ana productivity merge için 2023 kesin tutulmalı.

## 25.4 Adım 4 — Eurostat workforce clean table

Üret:

`workforce_genai_2025.csv`

Kolonlar:
- workforce_genai_work_2025
- female
- male
- low_edu
- medium_edu
- high_edu
- age_16_24
- age_25_34
- age_35_44
- age_45_54
- age_55_64
- reliability flags

Croatia low education missing/unreliable aynen korunmalı.

## 25.5 Adım 5 — Structural controls

OECD education:
- tertiary_attainment_2024

WDI:
- gdp_per_capita_ppp_2024
- log_gdp_per_capita_ppp_2024
- services_employment_share_2024

## 25.6 Adım 6 — Macro productivity

Üret:

```text
gdp_per_hour_2023
gdp_per_hour_2024
gdp_per_hour_growth_2024
gva_per_hour_growth_2024
productivity_status_flags
```

Türkiye missing bırakılmalı.

## 25.7 Adım 7 — Sector productivity

Filtre:

- transformation = Growth rate, over 1 year
- year = 2024
- ana seven sectors

Üret:

`sector_productivity_growth_2024.csv`

## 25.8 Adım 8 — Master country merge

`country_master.csv`:

27 ana country row’u hedeflenir.

Minimum kolonlar:

```text
country
iso3

enterprise_ai_2025
cloud_2025
data_analytics_2025
ict_specialists_2024
ict_training_2023

tertiary_attainment_2024
gdp_per_capita_ppp_2024
log_gdp_per_capita_ppp_2024
services_employment_share_2024

workforce_genai_work_2025

gdp_per_hour_2023
gdp_per_hour_2024
gdp_per_hour_growth_2024
gva_per_hour_growth_2024

all_source_flags...
```

Beklenen:
- readiness/workforce/structural cols: 27 non-missing.
- macro productivity cols: 26 non-missing, Türkiye missing.

## 25.9 Adım 9 — Derived indicators

Master clean olduktan sonra hesapla:

- DigitalFoundation
- SkillsReadiness
- AIReadiness
- ConversionScore
- archetype
- workforce alignment fields

Firm-size ve workforce gap’ler uygun ayrı tablolarda hesaplanabilir.

## 25.10 Adım 10 — QA assertions

Kodda assertion kullan:

```text
core_country_count == 27
unique_iso3 == 27
no_duplicate_iso3_in_country_master
enterprise_ai_2025.notna == 27
workforce_genai_work_2025.notna == 27
tertiary_attainment_2024.notna == 27
log_gdp_per_capita_ppp_2024.notna == 27
services_employment_share_2024.notna == 27
gdp_per_hour_2024.notna == 26
```

Sector:
- Türkiye absence beklenir.
- Real estate ana seven içine girmemelidir.

## 25.11 AŞAMA 4 deliverable’ları

AŞAMA 4 bitmiş sayılmadan önce bulunması gerekenler:

1. `country_master.csv`
2. `firm_size_ai_2025.csv`
3. `workforce_genai_2025.csv`
4. `sector_ai_2023.csv`
5. `sector_productivity_growth_2024.csv`
6. country mapping table
7. data dictionary
8. missingness report
9. flag report
10. merge QA report
11. derived-variable definitions
12. reproducible cleaning script/notebook

---

# 26. AŞAMA 4 Sonrası Yol Haritası

AŞAMA 4 tamamlanmadan EDA veya final model sonuçları “nihai” kabul edilmemelidir.

Önerilen sonraki sıra:

## AŞAMA 5 — EDA ve Descriptive Diagnostics
- distributions
- missingness
- country rankings
- correlation matrix
- scatterplots
- size gaps
- workforce gaps
- sector patterns
- outlier diagnostics

## AŞAMA 6 — Inferential / Model Analysis
- H1–H8 tests
- HC3 regressions
- Wilcoxon tests
- Holm adjustment
- productivity lag models
- sector FE models
- robustness battery

## AŞAMA 7 — Consulting Synthesis
- Readiness index
- ConversionScore
- country archetypes
- enterprise/workforce alignment
- binding constraints
- strategic actions

## AŞAMA 8 — Final Portfolio Deliverables
Muhtemel:
- executive report / memo
- polished charts
- appendix methodology
- reproducible code
- concise presentation
- portfolio README

Her ana aşama kullanıcı talebine uygun olarak **ayrı ayrı tamamlanmalı** ve sonraki ana aşamaya kullanıcı onayı olmadan geçilmemelidir.

---

# 27. Kesin “YAPMA” Kuralları

1. **Exposure’u ana ölçülmüş değişken gibi sunma.**
2. **Workforce disruption/job loss ölçtüğünü iddia etme.**
3. **2025 AI adoption’ı 2024 productivity’nin nedeni gibi modelleme.**
4. **Cross-sectional observational sonuçlarda causal language kullanma.**
5. **2021→2025 AI trendini headline yapma.**
6. **Sector productivity national-currency levels’ı ülkeler arasında karşılaştırma.**
7. **Real estate’i ana sector modeline sokma.**
8. **OECD/EU aggregate’ları regression observation olarak kullanma.**
9. **Raw data’yı overwrite/clean etme.**
10. **Missing Türkiye productivity değerini carry-forward veya impute etme.**
11. **Croatia low-education Eurostat value’sunu impute etme.**
12. **Enterprise ve workforce yüzdelerini aynı denominator gibi yorumlama.**
13. **27 gözlemde çok predictor’lı kitchen-sink regression kurma.**
14. **K-means’i ana country segmentation yapma.**
15. **Kısa AI zaman serisiyle formal forecasting üretme.**
16. **p-value’ı tek başarı ölçütü yapma.**
17. **Time-series-break flag’lerini görmezden gelme.**
18. **Productivity dosyalarının macro ve sector sürümlerini aynı isimle saklama.**

---

# 28. Açık Konular / Henüz Tamamlanmamış Kararlar

Aşağıdakiler yapılmamış veya final üretimden önce netleştirilmelidir:

1. **AŞAMA 4 cleaning code** henüz yazılmadı.
2. Final country master henüz oluşturulmadı.
3. Readiness index gerçek clean data üzerinden henüz hesaplanmadı.
4. Enterprise–workforce quadrant threshold final olarak kayda geçirilmedi; önerilen default z=0.
5. Final regression sonuçları henüz yok.
6. H7/H8 sonuçları henüz test edilmedi.
7. Final visual design / report formatı henüz belirlenmedi.
8. Final country recommendations henüz üretilmedi.
9. 29 Eylül 2026 sonrası OECD education final-2025 release çıkarsa, çalışma hâlâ devam ediyorsa 2025 verinin güncellenip güncellenmeyeceği yeniden değerlendirilmelidir; ana tasarım için 2024 yine yeterlidir.
10. External reproducibility için exact package/environment lock file henüz oluşturulmadı.

---

# 29. Resmî Web Kaynakları / Doğrulama Referansları

Aşağıdaki sayfalar çalışma metodolojisi ve kaynak tanımları için ana dış referanslardır.

## OECD ICT
https://data-explorer.oecd.org/  
Dataset: **ICT Access and Usage by Businesses**  
Dataflow: `OECD.STI.DEP / DSD_ICT_B@DF_BUSINESSES`

## OECD AI adoption context
https://www.oecd.org/en/about/news/announcements/2026/01/ai-use-by-individuals-surges-across-the-oecd-as-adoption-by-firms-continues-to-expand.html

2025 OECD context:
- firm AI adoption 20.2%
- 2024: 14.2%
- 2023: 8.7%
- large firms 52.0%
- small firms 17.4%

Bu değerler global/OECD context içindir; ana sample sonuçlarının yerine kullanılmaz.

## OECD firm AI adoption report
https://www.oecd.org/en/publications/the-adoption-of-artificial-intelligence-in-firms_f9ef33c3-en.html

## Eurostat GenAI
https://ec.europa.eu/eurostat/
Dataset family / online code:
`isoc_ai_iaiu`

Professional-use indicator:
`I_IUAIWP`

## OECD Educational Attainment
https://data-explorer.oecd.org/  
Dataset: **Adults' educational attainment distribution, by age group and gender**  
Dataflow: `OECD.EDU.IMEP / DSD_EAG_LSO_EA@DF_LSO_NEAC_DISTR_EA`

Latest available year values are preliminary; final release date stated by OECD:
**29 September 2026**.

## OECD Productivity
https://www.oecd.org/en/publications/oecd-compendium-of-productivity-indicators-2026_734a5e68-en.html

Macro chapter:
https://www.oecd.org/en/publications/oecd-compendium-of-productivity-indicators-2026_734a5e68-en/full-report/labour-productivity-in-oecd-economies-recent-trends-and-shifting-drivers-of-growth_cd896487.html

Sector chapter:
https://www.oecd.org/en/publications/oecd-compendium-of-productivity-indicators-2026_734a5e68-en/full-report/productivity-patterns-across-industries_8238f2eb.html

OECD 2026 sektör tanımı:
- annual percentage change in GVA per hour worked.

## World Bank GDP per capita PPP
https://data.worldbank.org/indicator/NY.GDP.PCAP.PP.KD

## World Bank Services Employment
https://data.worldbank.org/indicator/SL.SRV.EMPL.ZS

Metadata:
https://databank.worldbank.org/metadataglossary/world-development-indicators/series/SL.SRV.EMPL.ZS

---

# 30. Devralan Kişi / AI İçin Başlangıç Talimatı

Bu projeyi devralıyorsanız:

1. Önce bu belgedeki **Section 24–27 kurallarını** kabul edin.
2. Raw dosyaların tümünün bulunduğunu doğrulayın.
3. Macro ve sector OECD Productivity dosyalarının ayrı olduğundan emin olun.
4. AŞAMA 4’e başlayın; **henüz final EDA/model sonucu üretmeyin.**
5. ISO3 canonical mapping oluşturun.
6. Her source’dan yalnızca burada tanımlanan analytical slices’ı çıkarın.
7. `country_master.csv` üretin.
8. Missing/flag/duplicate QA raporu üretin.
9. 27-country assertions’ı çalıştırın.
10. Türkiye productivity missing’ini olduğu gibi bırakın.
11. Derived readiness skorlarını ancak temiz master doğrulandıktan sonra üretin.
12. AŞAMA 4 çıktıları tamamlanınca ilerlemeyi durdurun ve kullanıcıya raporlayın.
13. Kullanıcı “devam et” demeden sonraki ana aşamaya geçmeyin.

---

# 31. Tek Cümlelik Proje Özeti

> **Çalışma, 27 Avrupa ekonomisinin dijital ve insan sermayesi kapasitesini enterprise AI adoption’a ne ölçüde dönüştürdüğünü; bu adoption’ın firma büyüklüğü ve workforce grupları arasında nasıl yayıldığını; ve daha erken AI adoption’ın sonraki labour-productivity growth ile ilişkili olup olmadığını, küçük örnekleme uygun robust ve nedensellik iddiası taşımayan bir danışmanlık analitiği çerçevesinde incelemektedir.**
