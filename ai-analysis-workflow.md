Bu oturumda, uluslararası danışmanlık portföyü için yürüttüğüm **AI Readiness → Adoption → Workforce Diffusion → Productivity** çalışmasının veri hazırlama ve analiz sürecini birlikte tamamlayacağız.

### Çalışmanın amacı

27 Avrupa ekonomisinin dijital altyapı, işletme becerileri ve insan sermayesini enterprise AI adoption’a ne ölçüde dönüştürdüğünü; AI kullanımının firma büyüklükleri ve çalışan grupları arasında nasıl dağıldığını; ayrıca daha erken AI adoption ile sonraki labour-productivity growth arasında keşifsel bir ilişki olup olmadığını incelemek.

Sonuçlar açıklanabilir, danışmanlık odaklı ve metodolojik olarak savunulabilir olmalı. Observational verilerden nedensellik iddiası üretme.

### Sana sağlayacağım veri kaynakları

1. OECD ICT Access and Usage by Businesses
2. ILOSTAT Employment by sex and generative AI exposure
3. Eurostat Individuals – use of generative AI tools
4. OECD Productivity Database — mevcut 3.366 satırlık extract
5. OECD Educational Attainment
6. World Bank GDP per capita, PPP
7. World Bank Employment in services

Her kaynakla birlikte ya:

* tam ve değiştirilmemiş CSV,
* ya da tam veri setinden **değiştirilmeden seçilmiş structure/sample CSV**
  ve ayrıca veri setinin tam yapısını ve çalışma kurallarını açıklayan bir `.md` bağlam dosyası sağlayacağım.

**Structure sample’lardan final istatistik üretme.** Bunlar yalnızca ana local dosyanın şemasını tanımak, production kodunu geliştirmek ve smoke-test etmek içindir. Final hesaplamalar local bilgisayarımdaki tam veri setlerinde çalıştırılacak.

### Temel çalışma kuralları

* Raw dosyaları değiştirme; tüm cleaning/derived işlemleri ayrı dataframe/dosyalarda yap.
* Dosyaların gerçek sütun adlarını, kodlarını, grain’ini, unit’lerini, flag’lerini ve metadata’sını bağlam dosyalarından doğrula.
* Label yerine mümkün olduğunda source code/ISO3 anahtarlarını kullan.
* Missing değerleri, reliability/time-series-break/estimated flag’lerini sessizce silme veya impute etme.
* Datasetler arasında aynı isimli kavramların aynı denominator/unit’e sahip olduğunu varsayma.
* Aggregate OECD/EU/World Bank region satırlarını ülke gözlemi olarak kullanma.
* Sağlanan metadata ile dosya arasında çelişki görürsen ilerleme; çelişkiyi açıkça bildir.
* Dış kaynak gerekiyorsa yalnızca resmi OECD, Eurostat, ILO veya World Bank dokümantasyonuyla doğrula; sağlanan local verinin yerine başka veri koyma.

### Önce yapılacak iş

Ben tüm veri paketlerini yükleyene kadar master dataset oluşturmaya veya sonuç analizi yapmaya başlama. Her dosyayı şema, grain, coverage, unit, flag ve çalışma rolü açısından incele.

Tüm dosyalar sağlandıktan sonra önce **veri mimarisini tasarla**. Tek bir dev tabloyu varsayma. Çalışmanın ihtiyaçlarına göre:

* tek country-level master,
* firm-size tablosu,
* workforce subgroup tablosu,
* sector/productivity tablosu
  veya daha uygun bir ilişkisel yapı gerekip gerekmediğine karar ver.

İlk değerlendirmende bana yalnızca şunları sun:

1. veri kaynaklarının doğrulanmış envanteri ve rolleri,
2. önerilen master/analytical dataset mimarisi,
3. her tablonun grain’i ve primary/merge key’leri,
4. hangi değişkenlerin hangi kaynaktan/yıldan geleceği,
5. gerekli derived değişkenler,
6. missing/flag/duplicate/outlier yönetim kuralları,
7. merge sırası ve beklenen coverage,
8. uygulanacak QA/assertion kontrolleri,
9. localde üretilecek çıktı dosyaları,
10. varsa çözülmesi gereken belirsizlik veya riskler.

Bu tasarımın **neden mevcut veri yapılarına ve araştırma hedefine en uygun olduğunu** kısaca açıkla. Henüz production koduna geçme. **Onayımı bekle.**

### Onaydan sonraki çalışma biçimi

Süreci küçük ve doğrulanabilir adımlara böl.

Her adımda:

1. o adımın amacı ve beklenen çıktısını belirt,
2. local bilgisayarımda çalıştırabileceğim eksiksiz Python kodunu ver,
3. kodu full local dataset’in gerçek şemasına göre yaz; sample’a özel hard-code üretme,
4. mümkün olduğunca deterministic, yeniden çalıştırılabilir ve assertion içeren kod kullan,
5. oluşturulacak dosya/dataframe’i ve beklenen shape/key/coverage kontrollerini belirt,
6. benden çalıştırma sonucunda yalnızca karar vermek için gereken output’u istemeyi söyle.

Ben sonucu paylaştıktan sonra:

* sonucu değerlendir,
* beklenen QA ile karşılaştır,
* hata/uyumsuzluk varsa önce onu çöz,
* adım başarılıysa bunu açıkça onayla.

**Ben onay vermeden sonraki ana adıma geçme.**

Kod veya sonuç beklediğin durumda tahmin ederek ilerleme. Local çıktıyı benden iste.

### Nihai hedef

Önce güvenilir ve yeniden üretilebilir analytical data architecture oluştur; ardından ancak onay sonrasında EDA, hypothesis testing, robust regressions, firm-size gaps, workforce inclusion, country segmentation/readiness-conversion diagnostics ve sector productivity analizlerine geç.

Teknik karmaşıklığı amaç haline getirme. Her kararın araştırma sorusuna, veri yapısına, küçük örnekleme ve danışmanlık açısından yorumlanabilirliğe hizmet etmesini sağla.

Şimdi veri paketlerini yüklemeye başlayacağım. Dosyaları aldıkça inceleyebilirsin; ancak ben **“tüm veri setleri yüklendi”** demeden master dataset tasarımını başlatma.
