# Eurostat Workforce GenAI — Ana Veri Seti Bağlam ve Kodlama Rehberi

## 1. Kimlik

- **Standart çalışma adı:** Eurostat Workforce GenAI
- **Kullanıcının yüklediği dosya:** `Eurostat Individuals – use of generative AI tools.csv`
- **Eurostat dataset title:** `Individuals - use of generative AI tools`
- **Eurostat dataset / online code:** `isoc_ai_iaiu`
- **CSV structure ID:** `ESTAT:ISOC_AI_IAIU(1.0)`
- **Ana yüklenen extract:** 39,006 veri satırı × 21 sütun
- **Ana extract SHA-256:** `078b7864e32ab144a158297c207aef7d44598313130d693f77074f72446e4271`
- **Bu structure sample:** 429 veri satırı × 21 sütun
- **Sample SHA-256:** `b2493081670c7be2324aac4578fe2174cb8638e2443dd8de97171b6fd6ba5802`
- **Time coverage:** yalnızca 2025
- **Frequency:** Annual

Eurostat'ın 2025 yayınlarında bu veri seti, EU survey on the use of ICT in households and
by individuals kapsamında kullanılır. GenAI soruları, anketten önceki **son 3 ay** içindeki
kullanımı referans alır. Eurostat bir generative AI tool'u prompt/input üzerinden text,
image, programming code, video veya başka yeni içerik üretebilen araç olarak açıklar.

## 2. Bu sample'ın amacı

Bu CSV **final analiz için örneklem değildir**.

Amaç:
1. Localdeki 39.006 × 21 tam CSV'nin gerçek şemasını modele göstermek,
2. 104 `ind_type` kodunun yapısını tanıtmak,
3. dört GenAI indicator'ını ve üç denominator/unit türünü doğru ayırt ettirmek,
4. `u = low reliability` flag handling kodunu test etmek,
5. ana portföy filtrelerinin local full CSV'de hatasız uygulanmasını sağlamaktır.

### Değişmezlik garantisi

- Ana dosyanın **21 sütununun tamamı aynı isim ve sıradadır**.
- Yeni sütun eklenmemiştir.
- Rename/recode/rounding/normalization yoktur.
- Sample'daki her data row ana dosyadan **byte-for-byte aynı fiziksel CSV satırı** olarak
  kopyalanmıştır.
- Ana dosya değiştirilmemiştir.
- Sample istatistiksel olarak representative değildir.

## 3. Sample seçme yöntemi

Sample schema/code-development amacıyla seçilmiştir:

- Ana çalışma için gereken 27 core geography'nin tüm
  `I_IUAIWP + PC_IND` professional-use satırları şu breakdown'larda eksiksiz sample'a
  alınmıştır:
  - `SAL_SELF_FAM`
  - `F_Y16_74`, `M_Y16_74`
  - `I0_2`, `I3_4`, `I5_8`
  - `Y16_24`, `Y25_34`, `Y35_44`, `Y45_54`, `Y55_64`
- Ana dosyadaki **104 `ind_type` kodunun tamamı** en az bir kez temsil edilmiştir.
- Mevcut tüm `indic_is × unit × OBS_FLAG` yapıları temsil edilmiştir.
- **37 geography** kodunun tamamı en az bir kez temsil edilmiştir.
- EU27 benchmark için `IND_TOTAL` satırları indicator/unit çeşitliliğini göstermek üzere
  eklenmiştir.
- Son sample: **429 satır × 21 sütun**.

Bu sample üzerinde final mean, ranking, country comparison, correlation veya regression
hesaplanmamalıdır. Production kod localde tam CSV'ye uygulanmalıdır.

## 4. Tam sütun şeması

1. `STRUCTURE`
2. `STRUCTURE_ID`
3. `STRUCTURE_NAME`
4. `freq`
5. `Time frequency`
6. `ind_type`
7. `Individual type`
8. `indic_is`
9. `Information society indicator`
10. `unit`
11. `Unit of measure`
12. `geo`
13. `Geopolitical entity (reporting)`
14. `TIME_PERIOD`
15. `Time`
16. `OBS_VALUE`
17. `Observation value`
18. `OBS_FLAG`
19. `Observation status (Flag) V2 structure`
20. `CONF_STATUS`
21. `Confidentiality status (flag)`

## 5. Veri grain'i

Full dataset'te unique observation grain:

`freq × ind_type × indic_is × unit × geo × TIME_PERIOD`

Bu grain üzerinde duplicate sayısı: **0**.

Primary code columns:
- `freq`
- `ind_type`
- `indic_is`
- `unit`
- `geo`
- `TIME_PERIOD`

Value:
- `OBS_VALUE`

Quality:
- `OBS_FLAG`
- `CONF_STATUS`

Descriptive label columns aynı code'ların açıklamasıdır; production filtering/merge'de
mümkün olduğunca code columns kullanılmalıdır.

## 6. Full-dataset temel yapı

- Rows: 39,006
- Columns: 21
- `freq`: yalnızca `A`
- `TIME_PERIOD`: yalnızca `2025`
- Distinct `ind_type`: 104
- Distinct `indic_is`: 4
- Distinct `unit`: 3
- Distinct `geo`: 37
- Blank `OBS_VALUE`: 3,196
- `OBS_FLAG = u`: 6,699
- Blank `OBS_FLAG`: 32,307
- `CONF_STATUS`: full extract'te tamamı blank (39,006 satır)

## 7. Indicator kodları

### Information society indicators

| Code | Label | Full-data rows |
|---|---|---:|
| `I_IUAI` | Use of generative AI tools: in the last 3 months | 7,128 |
| `I_IUAIFE` | Use of generative AI tools: for formal education | 10,626 |
| `I_IUAIPR` | Use of generative AI tools: for private purposes | 10,626 |
| `I_IUAIWP` | Use of generative AI tools: for professional (work) purposes | 10,626 |

Ana portföy indicator'ı:

> `I_IUAIWP` — Use of generative AI tools: for professional (work) purposes

`I_IUAI` ise herhangi bir GenAI aracının son 3 ayda kullanılmasıdır; private/work/formal
purpose indicator'larıyla aynı kavram değildir.

## 8. Unit / denominator — EN KRİTİK KURAL

### Unit / denominator

| Code | Label | Full-data rows |
|---|---|---:|
| `PC_IND` | Percentage of individuals | 14,256 |
| `PC_IND_IU3` | Percentage of individuals who used internet in the last 3 months | 14,256 |
| `PC_IND_IUAI` | Percentage of individuals who have used any generative AI tools in the last 3 months | 10,494 |

Bu üç unit birbirine karıştırılmamalıdır.

### `PC_IND`
Denominator = ilgili `ind_type` popülasyonunun tamamı.

Örneğin:

`SAL_SELF_FAM + I_IUAIWP + PC_IND`

= employees/self-employed/family workers grubunun tamamı içinde work-purpose GenAI kullanan
kişilerin yüzdesi.

**Ana workforce değişkeninde kullanılan unit budur.**

### `PC_IND_IU3`
Denominator = son 3 ayda internet kullanan ilgili gruptaki kişiler.

Eurostat bazı 2025 yayınlarında country GenAI adoption sonuçlarını internet users denominator
üzerinden sunar; bu nedenle bu değerler `PC_IND` ile aynı sayı olmak zorunda değildir.

### `PC_IND_IUAI`
Denominator = son 3 ayda herhangi bir GenAI tool kullanmış kişiler.

Bu unit özellikle “GenAI kullanıcılarının hangi amaçla kullandığı” sorusunu yanıtlar.
Örneğin Eurostat'ın EU 2025 purpose-by-age grafiğinde professional/private/formal education
payları **GenAI users** tabanında verilmektedir.

**Kural:** Unit filtering yapılmadan aynı indicator'ın değerlerini karşılaştırmayın.

## 9. Geography kodları

### Geographies

| Code | Label | Full-data rows |
|---|---|---:|
| `AL` | Albania | 935 |
| `AT` | Austria | 1,130 |
| `BA` | Bosnia and Herzegovina | 902 |
| `BE` | Belgium | 1,133 |
| `BG` | Bulgaria | 1,112 |
| `CH` | Switzerland | 957 |
| `CY` | Cyprus | 1,124 |
| `CZ` | Czechia | 1,124 |
| `DE` | Germany | 1,001 |
| `DK` | Denmark | 1,089 |
| `EA` | Euro area (EA11-1999, EA12-2001, EA13-2007, EA15-2008, EA16-2009, EA17-2011, EA18-2014, EA19-2015, EA20-2023, EA21-2026) | 1,121 |
| `EE` | Estonia | 1,001 |
| `EL` | Greece | 1,001 |
| `ES` | Spain | 1,133 |
| `EU27_2020` | European Union - 27 countries (from 2020) | 1,121 |
| `FI` | Finland | 1,130 |
| `FR` | France | 1,111 |
| `HR` | Croatia | 1,001 |
| `HU` | Hungary | 1,124 |
| `IE` | Ireland | 1,078 |
| `IT` | Italy | 1,133 |
| `LT` | Lithuania | 998 |
| `LU` | Luxembourg | 1,001 |
| `LV` | Latvia | 1,094 |
| `MK` | North Macedonia | 957 |
| `MT` | Malta | 1,001 |
| `NL` | Netherlands | 1,133 |
| `NO` | Norway | 1,083 |
| `PL` | Poland | 1,121 |
| `PT` | Portugal | 990 |
| `RO` | Romania | 998 |
| `RS` | Serbia | 915 |
| `SE` | Sweden | 1,133 |
| `SI` | Slovenia | 1,119 |
| `SK` | Slovakia | 1,099 |
| `TR` | Türkiye | 946 |
| `XK` | Kosovo* | 957 |

### Ana 27-country mapping açısından kritik kodlar

- Greece = `EL` (ISO2 `GR` değildir)
- Türkiye = `TR`
- Czechia = `CZ`
- Slovak Republic / Slovakia = `SK`
- EU benchmark = `EU27_2020`
- `EA` euro-area aggregate'tır; ana regression observation değildir.

Ana portfolio geography listesi:

`AT, BE, BG, HR, CZ, DK, EE, FI, FR, DE, EL, HU, IE, IT, LV, LT, LU, NL, NO, PL, PT, RO, SK, SI, ES, SE, TR`

Full dataset ana 27 ülkenin tamamını içerir.

## 10. Individual-type breakdowns — 104 kod

### Individual-type breakdowns — tüm 104 kod

| Code | Label | Full-data rows |
|---|---|---:|
| `CB_EU_FOR` | Individuals who are born in another EU Member State | 297 |
| `CB_EXT_EU` | Individuals who are born in non-EU country | 308 |
| `CB_FOR` | Individuals who are foreign-born | 396 |
| `CB_NAT` | Individuals who are native-born | 396 |
| `CC_EU_FOR` | Nationals of another EU-Member State | 294 |
| `CC_EXT_EU` | Nationals of non-EU country | 319 |
| `CC_FOR` | Non-nationals | 404 |
| `CC_NAT` | Nationals | 407 |
| `EMPL_UNE` | Individuals in the labour force (employed and unemployed) | 407 |
| `F_I0_2` | Females with low formal education | 404 |
| `F_I0_2_75_89` | Females 75-89 with no or low education | 192 |
| `F_I3_4` | Females with medium formal education | 407 |
| `F_I3_4_75_89` | Females 75-89 with medium education | 213 |
| `F_I5_8` | Females with high formal education | 407 |
| `F_I5_8_75_89` | Females 75-89 with high education | 219 |
| `F_Y16_19` | Females, 16 to 19 years old | 407 |
| `F_Y16_24` | Females, 16 to 24 years old | 407 |
| `F_Y16_29` | Females, 16 to 29 years old | 407 |
| `F_Y16_74` | Females, 16 to 74 years old | 407 |
| `F_Y20_24` | Females, 20 to 24 years old | 407 |
| `F_Y25_29` | Females, 25 to 29 years old | 407 |
| `F_Y25_34` | Females, 25 to 34 years old | 407 |
| `F_Y25_54` | Females 25 to 54 years old | 407 |
| `F_Y25_64` | Females, 25 to 64 years old | 407 |
| `F_Y35_44` | Females 35 to 44 years old | 407 |
| `F_Y45_54` | Females 45 to 54 years old | 407 |
| `F_Y55_64` | Females 55 to 64 years old | 407 |
| `F_Y55_74` | Females 55 to 74 years old | 407 |
| `F_Y65_74` | Females 65 to 74 years old | 407 |
| `F_Y75_89` | Females 75-89 | 225 |
| `I0_2` | Individuals with no or low formal education | 407 |
| `I3_4` | Individuals with medium formal education | 407 |
| `I5_8` | Individuals with high formal education | 407 |
| `IND_DEG1` | Individuals living in cities | 396 |
| `IND_DEG2` | Individuals living in towns and suburbs | 385 |
| `IND_DEG3` | Individuals living in rural areas | 396 |
| `IND_TOTAL` | All individuals | 407 |
| `ISCO0_5` | Non-manual including the armed forces | 385 |
| `ISCO6_9` | Manual | 374 |
| `ISCO_ICT` | ICT professionals | 385 |
| `ISCO_ICTX` | Non ICT professionals | 396 |
| `M_I0_2` | Males with low formal education | 407 |
| `M_I0_2_75_89` | Males 75-89 with no or low education | 190 |
| `M_I3_4` | Males with medium formal education | 407 |
| `M_I3_4_75_89` | Males 75-89 with medium education | 222 |
| `M_I5_8` | Males with high formal education | 407 |
| `M_I5_8_75_89` | Males 75-89 with high education | 225 |
| `M_Y16_19` | Males, 16 to 19 years old | 407 |
| `M_Y16_24` | Males, 16 to 24 years old | 407 |
| `M_Y16_29` | Males, 16 to 29 years old | 407 |
| `M_Y16_74` | Males, 16 to 74 years old | 407 |
| `M_Y20_24` | Males, 20 to 24 years old | 407 |
| `M_Y25_29` | Males, 25 to 29 years old | 407 |
| `M_Y25_34` | Males, 25 to 34 years old | 407 |
| `M_Y25_54` | Males 25 to 54 years old | 407 |
| `M_Y25_64` | Males, 25 to 64 years old | 407 |
| `M_Y35_44` | Males 35 to 44 years old | 407 |
| `M_Y45_54` | Males 45 to 54 years old | 407 |
| `M_Y55_64` | Males 55 to 64 years old | 407 |
| `M_Y55_74` | Males 55 to 74 years old | 407 |
| `M_Y65_74` | Males 65 to 74 years old | 407 |
| `M_Y75_89` | Males 75-89 | 225 |
| `RETIR_OTHER` | Individuals who are retired or not in the labour force (excluding students) | 407 |
| `SAL_SELF_FAM` | Employees, self-employed, family workers | 407 |
| `STUD` | Students | 407 |
| `UNE` | Unemployed | 407 |
| `Y0_15` | Individuals, 15 years old or less | 11 |
| `Y16_17` | Individuals, 16 to 17 years old | 363 |
| `Y16_19` | Individuals, 16 to 19 years old | 407 |
| `Y16_24` | Individuals, 16 to 24 years old | 407 |
| `Y16_24HI` | Individuals aged 16-24 with high formal education | 407 |
| `Y16_24LO` | Individuals aged 16-24 with low education | 407 |
| `Y16_24ME` | Individuals aged 16-24 with medium formal education | 407 |
| `Y16_29` | Individuals, 16 to 29 years old | 407 |
| `Y16_29HI` | Individuals aged 16-29 with high formal education | 407 |
| `Y16_29LO` | Individuals aged 16-29 with low formal education | 407 |
| `Y16_29ME` | Individuals aged 16-29 with medium formal education | 407 |
| `Y20_24` | Individuals, 20 to 24 years old | 407 |
| `Y25_29` | Individuals, 25 to 29 years old | 407 |
| `Y25_34` | Individuals, 25 to 34 years old | 407 |
| `Y25_54` | Individuals, 25 to 54 years old | 407 |
| `Y25_54HI` | Individuals aged 25 to 54 with high formal education | 407 |
| `Y25_54LO` | Individuals aged 25 to 54 with low formal education | 407 |
| `Y25_54ME` | Individuals aged 25 to 54 with medium formal education | 407 |
| `Y25_64` | Individuals, 25 to 64 years old | 407 |
| `Y25_64HI` | Individuals aged 25 to 64 with high formal education | 407 |
| `Y25_64LO` | Individuals aged 25 to 64 with low formal education | 407 |
| `Y25_64ME` | Individuals aged 25 to 64 with medium formal education | 407 |
| `Y25_64_EMPL_UNE` | Individuals aged 25 to 64 who are in the labour force (employed and unemployed) | 407 |
| `Y25_64_RETIROTH` | Individuals aged 25 to 64 who are retired or not in the labour force (excluding students) | 407 |
| `Y25_64_SALSELFFAM` | Individuals aged 25 to 64 who are employees, self-employed or family workers | 407 |
| `Y25_64_UNE` | Individuals aged 25 to 64 who are unemployed | 407 |
| `Y35_44` | Individuals, 35 to 44 years old | 407 |
| `Y45_54` | Individuals, 45 to 54 years old | 407 |
| `Y55_64` | Individuals, 55 to 64 years old | 407 |
| `Y55_74` | Individuals, 55 to 74 years old | 407 |
| `Y55_74HI` | Individuals aged 55 to 74 with high formal education | 407 |
| `Y55_74LO` | Individuals aged 55 to 74 with low formal education | 395 |
| `Y55_74ME` | Individuals aged 55 to 74 with medium formal education | 407 |
| `Y65_74` | Individuals, 65 to 74 years old | 407 |
| `Y75_89` | All persons 75-89 | 225 |
| `Y75_89HI` | Persons aged 75-89 with high education | 225 |
| `Y75_89LO` | Persons aged 75-89 with no or low education | 201 |
| `Y75_89ME` | Persons aged 75-89 with medium education | 222 |

Bu zenginlik nedeniyle tüm breakdown'ları ana rapora sokmak scope creep yaratır.
Ana çalışmanın kesinleşmiş demographic set'i aşağıdadır.

## 11. Ana workforce variable — KESİN

Local full CSV filtreleri:

```python
main = df[
    (df["indic_is"] == "I_IUAIWP") &
    (df["ind_type"] == "SAL_SELF_FAM") &
    (df["unit"] == "PC_IND") &
    (df["geo"].isin(core_geo)) &
    (df["TIME_PERIOD"].astype(str) == "2025")
]
```

Tanım:

> Percentage of employees, self-employed and family workers who used generative AI tools
> for professional/work purposes in the last 3 months.

Analytical variable:
`workforce_genai_work_2025`

Coverage:
- rows = 27/27
- geographies = 27/27
- missing values = 0
- low reliability (`u`) = 0

Bu 27-country ana workforce variable tam ve clean'dir.

## 12. Gender analysis — ANA

Filtre:
- `indic_is = I_IUAIWP`
- `unit = PC_IND`
- `ind_type in ["F_Y16_74","M_Y16_74"]`
- core 27

Coverage:
- 54/54 expected rows
- missing = 0
- low reliability = 0

Derived:
```text
gender_gap = male_work_genai - female_work_genai
```

Bu yalnızca descriptive/paired-country gap'tir; causal gender effect değildir.

## 13. Education analysis — ANA

Codes:
- `I0_2` — no or low formal education
- `I3_4` — medium formal education
- `I5_8` — high formal education

Coverage:
- 81/81 expected records
- missing = 1
- low reliability = 1

Known issue:
- **Croatia (`HR`) + `I0_2`**: `OBS_VALUE` blank and `OBS_FLAG = u`.

Bu değer:
- 0 değildir,
- impute edilmemelidir,
- main high-vs-low education gap hesabında Croatia dışarıda kalabilir → n=26.

Derived:
```text
education_gap = high_education - low_education
```

## 14. Age analysis — SECONDARY but approved

Ana yaş kodları:
- `Y16_24`
- `Y25_34`
- `Y35_44`
- `Y45_54`
- `Y55_64`

Coverage:
- 135/135
- missing = 0
- low reliability = 0

Ana age-gap önerisi:
```text
age_gap = GenAI_work_25_34 - GenAI_work_55_64
```

`Y16_24` descriptive grafikte kullanılabilir ancak tüm grubun labour-force içinde olmadığı
unutulmamalıdır.

## 15. OBS_FLAG ve reliability

Full dataset:
- blank = 32,307
- `u` = 6,699 — **low reliability**

`Observation status (Flag) V2 structure` label sütunu da `u` için `low reliability` yazar.

Kural:
- `u` observation otomatik olarak zero yapılmaz.
- Missing ve unreliable ayrı durumlar olarak korunur.
- Ana variable clean olsa bile alt breakdown'larda flag kontrolü her filtre sonrası yapılır.

## 16. `CONF_STATUS`

`CONF_STATUS` ve label full extract'te boş.

Kolonlar sample'dan veya production load'dan silinmek zorunda değildir; fakat current
extract'te analitik bilgi taşımazlar.

## 17. Enterprise vs workforce karşılaştırması — denominator uyarısı

OECD Business ICT enterprise variable:

> percentage of enterprises using AI.

Eurostat workforce variable:

> percentage of individuals in the `SAL_SELF_FAM` group using GenAI for work.

Dolayısıyla:

```text
enterprise_ai_2025 - workforce_genai_work_2025
```

hesaplanabilir ancak aynı denominator/population'da bir percentage-point “shortfall” değildir.

Yalnızca:
> relative enterprise–workforce diffusion alignment indicator

olarak yorumlanabilir.

Ana ilişki:
- Pearson correlation
- Spearman correlation
- scatter / quadrant framework

Causal language kullanılmaz.

## 18. Eurostat yayınlarıyla denominator farkını doğrulama

Eurostat'ın 2025 kaynakları iki farklı presentation kullanır:

1. **All individuals 16–74** tabanlı yayında GenAI kullanım/purpose payları population
   percentage olarak gösterilir.
2. **GenAI users** tabanlı purpose analizinde private/professional/formal-education oranları
   GenAI kullananların içindeki pay olarak verilir.

Bu raw CSV'deki `PC_IND` ve `PC_IND_IUAI` unit ayrımıyla uyumludur.

Production kodunda unit explicit filtrelenmelidir.

## 19. Main-study dışına alınacak breakdown'lar

Full dataset'te ayrıca:
- citizenship,
- country of birth,
- degree of urbanisation,
- occupation / ICT professional status,
- labour-force status,
- detailed sex×age,
- sex×education,
- 75–89 yaş özel breakdown'ları

bulunur.

Ana çalışma için **otomatik kullanmayın**. Bunlar yalnızca yeni bir araştırma sorusu
açıkça kabul edilirse local full CSV'den alınmalıdır.

## 20. Local production code için minimum QA

```python
assert df.shape == (39006, 21)
assert list(df.columns) == ['STRUCTURE', 'STRUCTURE_ID', 'STRUCTURE_NAME', 'freq', 'Time frequency', 'ind_type', 'Individual type', 'indic_is', 'Information society indicator', 'unit', 'Unit of measure', 'geo', 'Geopolitical entity (reporting)', 'TIME_PERIOD', 'Time', 'OBS_VALUE', 'Observation value', 'OBS_FLAG', 'Observation status (Flag) V2 structure', 'CONF_STATUS', 'Confidentiality status (flag)']

grain = ["freq","ind_type","indic_is","unit","geo","TIME_PERIOD"]
assert not df.duplicated(grain).any()

assert set(df["freq"].unique()) == {"A"}
assert set(df["TIME_PERIOD"].astype(str).unique()) == {"2025"}
assert df["ind_type"].nunique() == 104
assert df["indic_is"].nunique() == 4
assert df["unit"].nunique() == 3
assert df["geo"].nunique() == 37

assert set(df["indic_is"].unique()) == {
    "I_IUAI","I_IUAIFE","I_IUAIPR","I_IUAIWP"
}
assert set(df["unit"].unique()) == {
    "PC_IND","PC_IND_IU3","PC_IND_IUAI"
}
assert set(df["OBS_FLAG"].dropna().unique()).issubset({"u"})
```

CSV load ayarına göre blank string'ler pandas tarafından NaN olabilir; QA kodu buna göre
uyarlanmalıdır.

Main-filter assertions:

```python
assert len(main) == 27
assert main["geo"].nunique() == 27
assert main["OBS_VALUE"].notna().all()
assert main["OBS_FLAG"].isna().all()  # default pandas NA handling ile
```

## 21. AI/model'e yüklerken önerilen açıklama

> `Eurostat_GenAI_unchanged_structure_sample.csv`, localde bulunan tam
> `Eurostat Individuals – use of generative AI tools.csv` dosyasından seçilmiş,
> değiştirilmemiş schema/structure sample'dır. Sample final istatistik üretmek için değil,
> full 39.006 × 21 CSV üzerinde çalışacak production Python/R kodunu geliştirmek için
> kullanılacaktır. Her sample row ana CSV'den byte-for-byte kopyalanmıştır. Filtering'de
> `ind_type`, `indic_is`, `unit`, `geo`, `TIME_PERIOD` code columns kullan. En kritik nokta
> `unit` denominator'ıdır: `PC_IND`, `PC_IND_IU3`, `PC_IND_IUAI` birbirinden farklıdır.
> Ana portfolio workforce variable `I_IUAIWP + SAL_SELF_FAM + PC_IND + 2025`'tir.
> Gender `F_Y16_74/M_Y16_74`, education `I0_2/I3_4/I5_8`, age
> `Y16_24/Y25_34/Y35_44/Y45_54/Y55_64` kullanılır. Croatia low-education professional-use
> observation missing + low-reliability'dir ve impute edilmemelidir. `u` flag'lerini koru.
> Final calculations local full CSV'de yapılacaktır.

## 22. Kullanım sınırı

Bu sample yeterlidir:
- exact schema/parser,
- denominator-aware filtering,
- 104 breakdown code handling,
- geography mapping,
- reliability handling,
- pivot/reshape code,
- main/subgroup filter smoke tests.

Bu sample yeterli değildir:
- final country values,
- final demographic gaps,
- final correlations,
- rankings,
- regressions,
- report findings.

Final hesaplamalar local tam CSV üzerinde yapılmalıdır.
