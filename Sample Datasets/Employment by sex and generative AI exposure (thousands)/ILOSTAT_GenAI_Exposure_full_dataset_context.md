# ILOSTAT GenAI Exposure — Ana Veri Seti Bağlam ve Kodlama Rehberi

## 1. Kimlik

- **Standart çalışma adı:** ILOSTAT GenAI Exposure
- **Kullanıcının yüklediği dosya:** `Employment by sex and generative AI exposure (thousands).csv`
- **Resmî ILOSTAT tablo adı:** *Employment by sex and generative AI exposure (thousands)*
- **Frekans:** Annual
- **Ana yüklenen extract:** 9,779 veri satırı × 10 sütun
- **Ana extract SHA-256:** `c73982928cd4ed7083ad6bc895864c85eec8fa438cbcae4f505b6fa745d9ee01`
- **Bu structure sample:** 416 veri satırı × 10 sütun
- **Sample SHA-256:** `cf4bf274d6bac257a45e3f497e112323f9d17cc7202c56a39560c1d184add63e`

ILOSTAT'in resmî employment download listesinde bu tablo Annual/Quarterly/Monthly
sürümleriyle yayımlanmaktadır. Kullanıcının yüklediği dosya annual tablodur.

ILO'nun 2025 *Generative AI and Jobs: A Refined Global Index of Occupational Exposure*
çalışması, GenAI exposure'u görev/meslek düzeyindeki **potansiyel maruziyet** olarak ele alır.
Bu ölçüm gerçekleşmiş AI kullanımı, otomasyon, iş kaybı veya gerçekleşmiş workforce
disruption değildir. ILO dört artan exposure gradient'i kullanır; ayrıca minimal exposure ve
not-exposed kavramlarını metodolojide ayrı biçimde tartışır.

## 2. Bu sample'ın amacı

Bu CSV **istatistiksel analiz sample'ı değildir**.

Amaç:
1. Ana CSV'nin gerçek 10 sütunlu şemasını göstermek,
2. Localde tam 9.779 satırlık dosyada çalışacak kodu geliştirmek,
3. `source.label`, sex, exposure classifier, year, status ve note alanlarının gerçek
   formatını göstermek,
4. Embedded newline içeren classifier string'leri dahil gerçek cell value'larla parser ve
   filter kodunu smoke-test etmektir.

### Değişmezlik garantisi

- Sample'da ana dosyanın **10 sütununun tamamı aynı isim ve sırayla** vardır.
- Yeni sütun yoktur.
- Veri değerleri temizlenmemiş, yuvarlanmamış, normalize edilmemiş veya yeniden
  sınıflandırılmamıştır.
- Sample'daki her logical CSV record ana dosyadaki bir record ile **field-by-field birebir
  eşittir**; bu eşitlik yeniden okunarak doğrulanmıştır.
- Ana CSV değiştirilmemiştir.
- Orijinal bazı classifier cell'lerinde gerçek `\n` / `\r\n` karakterleri bulunduğundan,
  sample CSV yeniden serialize edilmiştir; CSV quoting/physical line layout aynı olmak
  zorunda değildir, ancak hücre değerleri aynıdır.

## 3. Sample seçme yöntemi

Sample temsilî istatistik üretmek için değil, **schema ve data-pattern coverage** için
seçilmiştir.

- Her benzersiz
  `sex.label × classif1.label × obs_status.label × note_indicator.label × note_source.label`
  kombinasyonundan en az bir gerçek record seçilmiştir.
- Ana dosyadaki 87 reference area'nın tamamı en az bir kez sample'dadır.
- 39 farklı `source.label` değerinin tamamı sample'dadır.
- 1996–2026 arasındaki 31 yılın tamamı sample'dadır.
- Ana portföy örneklemiyle ortak yalnızca iki ülke olan **Czechia ve France'ın 2024**
  sex × exposure records'larının tamamı özellikle sample'a eklenmiştir.
- Son sample: **416 record**.

Bu seçim nedeniyle sample'daki ülke, yıl ve status dağılımı ana dosyanın dağılımını temsil
etmez. Sample üzerinden country ranking, trend, exposure share, korelasyon veya model sonucu
üretmeyin.

## 4. Tam sütun şeması

1. `ref_area.label`
2. `source.label`
3. `indicator.label`
4. `sex.label`
5. `classif1.label`
6. `time`
7. `obs_value`
8. `obs_status.label`
9. `note_indicator.label`
10. `note_source.label`

## 5. Veri grain'i

Ana extract'te gözlem grain'i:

`ref_area.label × source.label × indicator.label × sex.label × classif1.label × time`

Bu grain üzerinde duplicate sayısı: **0**.

`source.label` grain'in bir parçasıdır. Aynı ülke/yıl için farklı source olasılığını kodda
görmezden gelmeyin.

## 6. Indicator ve birim

Ana dosyada tek indicator:

- `Employment by sex and generative AI exposure (thousands)`

`obs_value` birimi **thousands of employed persons**'dır.

- `obs_value = 100` → yaklaşık 100 bin kişi.
- Yüzde değildir.
- Exposure share gerekiyorsa uygun `Exposure gradient: Total` denominator'ına bölünerek
  ayrıca türetilmelidir.
- `obs_value` non-missing değerlerinin tamamı numeric parse edilebilir:
  parse failure = 0.
- Missing `obs_value`: **13 record**.
- Missing değerler 0 olarak doldurulmamalıdır.

## 7. Sex değerleri

- `Female` — 3,257 satır
- `Male` — 3,257 satır
- `Other` — 8 satır
- `Total` — 3,257 satır

`Other` yalnızca 8 record'da görülür ve Bangladesh 2023/2024 kaynaklıdır; bazı değerleri
Unreliable ve/veya missing'dir. Main male/female comparison yapılacaksa `Other` otomatik
olarak Male/Female'e dağıtılmamalıdır.

## 8. Exposure classifier — raw string'ler kritik

Ana dosyada 7 classifier vardır:

- Raw: `Exposure gradient: 1 - Low exposure, high task \nvariability`  
  Okunabilir: **Exposure gradient: 1 - Low exposure, high task variability** — 1,396 satır
- Raw: `Exposure gradient: 2 - Moderate exposure, high \ntask variability`  
  Okunabilir: **Exposure gradient: 2 - Moderate exposure, high task variability** — 1,396 satır
- Raw: `Exposure gradient: 3 - Significant exposure, high \ntask variability`  
  Okunabilir: **Exposure gradient: 3 - Significant exposure, high task variability** — 1,396 satır
- Raw: `Exposure gradient: 4 - Highest exposure, low task \r\nvariability`  
  Okunabilir: **Exposure gradient: 4 - Highest exposure, low task variability** — 1,395 satır
- Raw: `Exposure gradient: Minimal exposure, \nmoderate task variability`  
  Okunabilir: **Exposure gradient: Minimal exposure, moderate task variability** — 1,396 satır
- Raw: `Exposure gradient: Total`  
  Okunabilir: **Exposure gradient: Total** — 1,400 satır
- Raw: `Exposure gradient: X - Not elsewhere classified`  
  Okunabilir: **Exposure gradient: X - Not elsewhere classified** — 1,400 satır

### Kritik whitespace uyarısı

`classif1.label` değerlerinin bazılarında hücrenin içinde gerçek newline (`\n`) ve bir
değerde `\r\n` vardır.

Bu nedenle production kodunda aşağıdakine benzer şekilde **raw sütunu bozmadan türetilmiş
bir canonical comparison field** oluşturmak güvenlidir:

```python
df["classif1_canonical"] = (
    df["classif1.label"]
      .str.replace(r"\s+", " ", regex=True)
      .str.strip()
)
```

Raw `classif1.label` sütunu korunmalıdır.

### `X - Not elsewhere classified` için yorum kuralı

Raw dataset'te kategori adı açıkça `X - Not elsewhere classified`'dır.

ILO'nun 2025 methodology metni `Not Exposed` kavramını ayrıca tanımlar; fakat bu CSV'de
ayrı bir `Not Exposed` label'ı yoktur. Bu nedenle `X - Not elsewhere classified` kategorisi
**explicit ILO codebook mapping doğrulanmadan `Not Exposed` diye yeniden adlandırılmamalıdır**.

Tam ve non-missing bloklarda `Total`, altı non-total classifier'ın toplamıyla yalnızca
yayın yuvarlaması düzeyinde farklılaşmaktadır. Kontrol edilen **1.388/1.388** blokta mutlak
fark **0,005 bin kişinin altında**dır; gözlenen maksimum fark yaklaşık **0,002 bin kişi
(~2 kişi)**dir. Production QA'da tam floating-point eşitliği yerine bu tür küçük bir
rounding tolerance kullanılmalıdır.

## 9. Exposure kavramının doğru yorumlanması

ILO'nun resmi 2025 metodolojisine göre:

- Gradient 4: highest exposure, low task variability.
- Gradient 3: significant exposure, high task variability.
- Gradient 2: moderate exposure, high task variability.
- Gradient 1: low exposure, high task variability.
- Minimal exposure: low exposure, moderate task variability.

ILO, bu sınıflandırmanın **potential exposure** olduğunu ve gerçekleşmiş employment impact
olmadığını açıkça belirtir. Bir occupation'ın exposed olması işin ortadan kalkacağı anlamına
gelmez.

Bu nedenle raporda:
- `exposure` ≠ `AI adoption`
- `exposure` ≠ `automation rate`
- `exposure` ≠ `job displacement`
- `exposure` ≠ `job-loss forecast`

## 10. Observation status

- `(blank)` — 8,620 satır
- `Break in series` — 1,088 satır
- `Unreliable` — 71 satır

Ana yorum:
- blank = ayrı bir problem flag'i belirtilmemiş.
- `Break in series` = time comparison için dikkat.
- `Unreliable` = ana sonuçlarda dikkat / mümkünse exclusion sensitivity.

`obs_status.label` boşluğu “missing observation” demek değildir; observation değeri ayrıca
`obs_value` üzerinden kontrol edilmelidir.

## 11. Indicator notes

- `(blank)` — 8,666 satır
- `Break in series: Methodology revised` — 1,071 satır
- `Employment definition: Excluding own-use production workers` — 21 satır
- `Employment definition: Excluding own-use production workers | Break in series: Methodology revised` — 21 satır

Methodology break note'larını trend kodunda kaybetmeyin.

## 12. Source notes

- `Repository: ILO-STATISTICS - Micro data processing` — 9,044 satır
- `Repository: ILO-STATISTICS - Micro data processing | Age coverage - maximum age: 64 years old` — 21 satır
- `Repository: ILO-STATISTICS - Micro data processing | Age coverage - maximum age: 74 years old` — 189 satır
- `Repository: ILO-STATISTICS - Micro data processing | Age coverage - maximum age: 75 years old` — 21 satır
- `Repository: ILO-STATISTICS - Micro data processing | Age coverage - minimum age: 16 years old` — 147 satır
- `Repository: ILO-STATISTICS - Micro data processing | Age coverage - minimum age: Less than or equal to 9 years old` — 21 satır
- `Repository: ILO-STATISTICS - Micro data processing | Data reference period: First quarter` — 21 satır
- `Repository: ILO-STATISTICS - Micro data processing | Data reference period: First semester` — 21 satır
- `Repository: ILO-STATISTICS - Micro data processing | Data reference period: Noncalendar year` — 126 satır
- `Repository: ILO-STATISTICS - Micro data processing | Data reference period: October` — 63 satır
- `Repository: ILO-STATISTICS - Micro data processing | Data reference period: Second quarter` — 105 satır

Tüm record'larda `note_source.label` doludur. Age coverage veya reference-period farkları
cross-country/year comparison'ın metadata'sıdır; sample hazırlanırken kaldırılmamıştır.

## 13. Source types — tam 39 değer

- `HIES - Harmonized Survey on Household Living Conditions` — 42 satır
- `HIES - Household Budget Survey` — 21 satır
- `HIES - Household Income and Expenditure Survey` — 189 satır
- `HIES - Household Socio-Economic Survey` — 63 satır
- `HIES - Living Conditions Monitoring Survey` — 21 satır
- `HIES - Living Standards Survey` — 42 satır
- `HIES - National Household Survey` — 42 satır
- `HIES - National Panel Survey` — 21 satır
- `HIES - Survey on Living Conditions` — 42 satır
- `HS - Continous Multi-Purpose Household Survey` — 84 satır
- `HS - Continuous National Household Sample Survey` — 294 satır
- `HS - Multi-Topic Household Survey` — 126 satır
- `HS - Multi-purpose Household Survey` — 273 satır
- `HS - National Survey on Socio-Economic Conditions` — 42 satır
- `LFS - Continous Household Survey` — 273 satır
- `LFS - Continuous Employment Survey` — 189 satır
- `LFS - Continuous Multi-Objective Survey Employment and Labor Market Statistics` — 21 satır
- `LFS - Continuous National Labour Force Survey` — 231 satır
- `LFS - Employment Survey` — 441 satır
- `LFS - Employment and Unemployment Survey` — 84 satır
- `LFS - Employment, Unemployment Survey` — 21 satır
- `LFS - Integrated Household Survey` — 84 satır
- `LFS - Integrated Labour Force Survey` — 21 satır
- `LFS - Integrated Regional Survey on Employment and Informal Sector` — 21 satır
- `LFS - Labor Market Panel Survey` — 21 satır
- `LFS - Labour Force & Household Survey` — 63 satır
- `LFS - Labour Force Sample Survey` — 399 satır
- `LFS - Labour Force Survey` — 5,411 satır
- `LFS - Labour Market Survey` — 63 satır
- `LFS - National Employment Survey` — 105 satır
- `LFS - National Labor Force Survey` — 21 satır
- `LFS - National Labour Force Survey` — 84 satır
- `LFS - National Occupation and Employment Survey` — 294 satır
- `LFS - National Population and Employment Survey` — 21 satır
- `LFS - National Survey on Employment, Unemployment and Underemployment` — 273 satır
- `LFS - Permanent Employment Survey, National` — 84 satır
- `LFS - Unemployment, Under-employment Watch` — 21 satır
- `PC - Population Census` — 210 satır
- `PC - Population and Housing Census` — 21 satır

Ana çoğunluk:
- `LFS - Labour Force Survey`: 5,411 record.

Ancak local kodda yalnızca bu source'a filtrelemek genel olarak doğru değildir; ülkelere göre
resmî source label farklılaşır. `source.label` korunmalı ve ülke-yıl benzersizlik kontrolünde
grain'in bir parçası olarak ele alınmalıdır.

## 14. Time coverage — tam extract

- Minimum year: **1996**
- Maximum year: **2026**
- 31 distinct year

- 1996: 21 satır
- 1997: 21 satır
- 1998: 21 satır
- 1999: 21 satır
- 2000: 21 satır
- 2001: 21 satır
- 2002: 21 satır
- 2003: 21 satır
- 2004: 21 satır
- 2005: 42 satır
- 2006: 42 satır
- 2007: 42 satır
- 2008: 63 satır
- 2009: 105 satır
- 2010: 84 satır
- 2011: 189 satır
- 2012: 294 satır
- 2013: 378 satır
- 2014: 420 satır
- 2015: 462 satır
- 2016: 546 satır
- 2017: 651 satır
- 2018: 630 satır
- 2019: 861 satır
- 2020: 798 satır
- 2021: 861 satır
- 2022: 903 satır
- 2023: 908 satır
- 2024: 801 satır
- 2025: 489 satır
- 2026: 21 satır

2026 record'ları yalnızca **Mexico** için vardır; bunu tüm dataset'in “2026 coverage”ı gibi
yorumlamayın.

Bir country trend'i üretilmeden önce o ülkenin actual year coverage'ı ve break notes/status
kontrol edilmelidir.

## 15. Reference area coverage — 87 alan

- Afghanistan — 21 satır; latest 2021
- Angola — 168 satır; latest 2025
- Bahamas — 63 satır; latest 2024
- Bangladesh — 92 satır; latest 2024
- Barbados — 126 satır; latest 2024
- Belarus — 189 satır; latest 2024
- Belize — 42 satır; latest 2016
- Bhutan — 153 satır; latest 2025
- Bosnia and Herzegovina — 315 satır; latest 2025
- Botswana — 126 satır; latest 2024
- Brazil — 294 satır; latest 2025
- Burundi — 21 satır; latest 2020
- Cambodia — 84 satır; latest 2025
- Cape Verde — 21 satır; latest 2009
- Chile — 42 satır; latest 2022
- Colombia — 84 satır; latest 2025
- Cook Islands — 42 satır; latest 2023
- Costa Rica — 189 satır; latest 2025
- Czechia — 294 satır; latest 2024
- Dominican Republic — 231 satır; latest 2025
- Ecuador — 273 satır; latest 2025
- Egypt — 105 satır; latest 2024
- El Salvador — 273 satır; latest 2025
- Eswatini — 63 satır; latest 2023
- Ethiopia — 21 satır; latest 2021
- Fiji — 21 satır; latest 2024
- France — 294 satır; latest 2024
- Gambia — 42 satır; latest 2025
- Georgia — 126 satır; latest 2025
- Ghana — 21 satır; latest 2017
- Grenada — 105 satır; latest 2023
- Guinea-Bissau — 42 satır; latest 2022
- Guyana — 105 satır; latest 2024
- Honduras — 84 satır; latest 2025
- Indonesia — 21 satır; latest 2023
- Iraq — 42 satır; latest 2021
- Kiribati — 42 satır; latest 2023
- Kosovo — 126 satır; latest 2024
- Kyrgyzstan — 84 satır; latest 2023
- Lao People's Democratic Republic — 21 satır; latest 2017
- Lebanon — 21 satır; latest 2019
- Lesotho — 21 satır; latest 2024
- Malawi — 21 satır; latest 2024
- Maldives — 42 satır; latest 2019
- Mali — 21 satır; latest 2022
- Marshall Islands — 21 satır; latest 2021
- Mexico — 294 satır; latest 2026
- Mongolia — 315 satır; latest 2025
- Montserrat — 21 satır; latest 2020
- Myanmar — 105 satır; latest 2020
- Naoero — 42 satır; latest 2021
- Nepal — 21 satır; latest 2017
- Nigeria — 21 satır; latest 2024
- Niue — 21 satır; latest 2022
- North Macedonia — 357 satır; latest 2025
- Pakistan — 168 satır; latest 2025
- Palau — 21 satır; latest 2020
- Panama — 63 satır; latest 2025
- Peru — 84 satır; latest 2025
- Philippines — 147 satır; latest 2023
- Rwanda — 42 satır; latest 2021
- Samoa — 63 satır; latest 2022
- Sao Tome and Principe — 21 satır; latest 2017
- Senegal — 105 satır; latest 2024
- Serbia — 189 satır; latest 2019
- Seychelles — 42 satır; latest 2020
- Sierra Leone — 21 satır; latest 2014
- Sri Lanka — 252 satır; latest 2024
- Sudan — 21 satır; latest 2022
- Suriname — 21 satır; latest 2016
- Switzerland — 630 satır; latest 2025
- Tajikistan — 21 satır; latest 2016
- Tanzania, United Republic of — 21 satır; latest 2020
- Thailand — 273 satır; latest 2025
- Timor-Leste — 84 satır; latest 2022
- Tokelau — 21 satır; latest 2022
- Tonga — 63 satır; latest 2023
- Tunisia — 21 satır; latest 2019
- Tuvalu — 42 satır; latest 2022
- Uganda — 105 satır; latest 2021
- United Arab Emirates — 105 satır; latest 2022
- United Kingdom of Great Britain and Northern Ireland — 441 satır; latest 2025
- Uruguay — 273 satır; latest 2025
- Vanuatu — 63 satır; latest 2025
- Viet Nam — 294 satır; latest 2024
- Wallis and Futuna — 21 satır; latest 2019
- Zambia — 189 satır; latest 2024

## 16. Ana portföy çalışmasıyla uyumluluk

Portföyün ana 27-country örneklemi ile bu extract'in ortak ülkeleri:

- **Czechia**
- **France**

Overlap: **2/27**.

Bu nedenle bu veri seti ana country-level merge, readiness index, regression veya 27-country
segmentation için uygun değildir.

### Kesin çalışma statüsü

**SUPPLEMENTARY / CONTEXTUAL ONLY**

Uygun kullanım örnekleri:
- exposure kavramını açıklamak,
- iki ortak ülke üzerinde yalnızca illustrative check,
- ILO methodology/context,
- kadın/erkek exposure farklarının küresel literatürünü desteklemek.

Uygun olmayan kullanım:
- 27 ülke için exposure variable yaratmak,
- missing 25 ülkeyi impute etmek,
- exposure'u workforce GenAI use yerine kullanmak,
- exposure'u gerçekleşmiş disruption olarak yorumlamak.

Ana workforce adoption kaynağı Eurostat'tır; ILOSTAT bunun yerine geçmez.

## 17. Eğer supplementary exposure share hesaplanacaksa

Local full-data üzerinde, **aynı**
`ref_area.label × source.label × sex.label × time`
bloğunda denominator:

`Exposure gradient: Total`

olmalıdır.

ILO 2025'in “one of the four exposure gradients” kavramına yakın bir türetilmiş share için
Gradient 1–4 numerators toplamı / Total hesaplanabilir.

Minimal exposure ayrıca tutulmalıdır.

`X - Not elsewhere classified` raw adıyla korunmalı; `Not Exposed` olarak otomatik rename
edilmemelidir.

Örnek formül:

```text
four_gradient_exposure_share =
100 * (G1 + G2 + G3 + G4) / Total
```

Bu türetilmiş yüzde **ana CSV'de mevcut değildir**; kodla üretilecek derived field'dır.

## 18. Missing / reliability kuralları

- `obs_value` missing record: 13.
- Missing değer = 0 değildir.
- `Unreliable` record: 71.
- `Break in series` record: 1088.
- İmputation yapılmamalıdır.
- Trend analizi break status / methodology note olmadan yapılmamalıdır.
- Source/reference-period/age-coverage notes kaybedilmemelidir.

## 19. Local production code için minimum QA

```python
assert df.shape == (9779, 10)
assert list(df.columns) == ['ref_area.label', 'source.label', 'indicator.label', 'sex.label', 'classif1.label', 'time', 'obs_value', 'obs_status.label', 'note_indicator.label', 'note_source.label']

grain = [
    "ref_area.label",
    "source.label",
    "indicator.label",
    "sex.label",
    "classif1.label",
    "time",
]
assert not df.duplicated(grain).any()

assert df["indicator.label"].nunique() == 1
assert df["indicator.label"].iloc[0] == (
    "Employment by sex and generative AI exposure (thousands)"
)

assert df["ref_area.label"].nunique() == 87
assert df["source.label"].nunique() == 39
assert df["sex.label"].nunique() == 4
assert df["classif1.label"].nunique() == 7
assert df["time"].astype(int).min() == 1996
assert df["time"].astype(int).max() == 2026
assert df["obs_value"].isna().sum() == 13
```

CSV reader'a göre empty strings pandas'ta default olarak NaN olabilir; QA kodunda load
ayarına göre `isna()` / empty-string kontrolü uyarlanmalıdır.

## 20. AI/model'e yüklerken önerilen açıklama

> `ILOSTAT_GenAI_exposure_unchanged_structure_sample.csv`, localde bulunan tam
> `Employment by sex and generative AI exposure (thousands).csv` dosyasından seçilmiş
> schema/structure sample'dır. Sample'daki tüm sütun ve hücre değerleri ana record'lardan
> değiştirilmeden alınmıştır; sample istatistiksel olarak representative değildir ve final
> analiz sample üzerinde yapılmayacaktır. Production Python/R kodunu sample üzerinde
> geliştirip localdeki 9.779 × 10 tam CSV'ye uygula. `classif1.label` içinde embedded
> newline'lar vardır; raw alanı koru ve filtering için derived whitespace-normalized field
> oluştur. `obs_value` bin kişi birimindedir, yüzde değildir. `source.label` grain'in
> parçasıdır. Break/Unreliable status ve note alanlarını kaybetme. Bu kaynak ana 27-country
> portfolio sample'ıyla yalnızca Czechia ve France'ta örtüştüğü için ana modelde kullanılmaz;
> supplementary/contextual source olarak kalır. Exposure'u gerçekleşmiş AI adoption,
> automation veya job loss olarak yorumlama.

## 21. Kullanım sınırı

Bu sample yeterlidir:
- parser/schema tanıma,
- multiline cell handling,
- source-aware filtering,
- classifier normalization code,
- status/note handling,
- reshaping/pivot code,
- derived share code smoke-test'i.

Bu sample yeterli değildir:
- final country estimates,
- final trend,
- global exposure statistics,
- final sex-gap calculations,
- portfolio main model.

Final hesaplar local tam dosyada yapılmalıdır.
