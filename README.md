# HEALER V0.5

**HEALER**, kişisel farkındalık, düzenli takip ve anlamlı öz-gözlem için geliştirilmiş bir kişisel yapay zekâ yardımcı ajanıdır.  
Telegram tabanlı doğal konuşma arayüzünü, uzun dönem hafızayı, kitap destekli RAG altyapısını ve daha geniş bir kişisel yapay zekâ komuta sistemi olan **C-LOPAI** ile kurulan köprüyü bir araya getirir.

Bu proje, her ajanının belirli bir sorumluluğa sahip olduğu daha büyük bir kişisel yapay zekâ ekosisteminin parçası olarak geliştirildi. HEALER’in rolü; kullanıcının düşüncelerini daha net görmesine yardımcı olmak, tekrar eden örüntüleri fark etmek, anlamlı notlar tutmak ve günlük konuşmaları yapılandırılmış kişisel içgörülere dönüştürmektir.

HEALER, genel amaçlı bir chatbot gibi davranmak yerine; bağlamı bilen, geçmişi dikkate alan, önemli örüntüleri hatırlayan ve sakin, dengeli, pratik bir dille yanıt veren odaklanmış bir kişisel destek ajanı olarak tasarlanmıştır.

---

## HEALER Ne Yapar?

HEALER tek bir temel fikir üzerine kuruludur:

> Kişisel bir yapay zekâ yalnızca mesajlara cevap vermemeli.  
> Bağlamı anlamalı, değişimi zaman içinde takip etmeli ve kullanıcının dağınık düşünceden daha net bir bakışa geçmesine yardımcı olmalı.

Mevcut V0.5 sürümünde HEALER şunları yapabilir:

- Telegram üzerinden doğal bir konuşma akışıyla yanıt verir
- Bir mesajın genel sohbet, not, profil sorusu, sistem/meta soru veya kaynak odaklı bir sorgu olup olmadığını ayırt eder
- Yanıtlarını daha tutarlı ve kişisel hale getirmek için yapılandırılmış bir kullanıcı profili kullanır
- Yerel kitap tabanlı bilgi havuzundan destekleyici bağlam alabilir
- Konuşmalar sırasında aktif oturum hafızasını korur
- Uzun dönem notları, oturumları, örüntüleri ve özetleri SQLite üzerinde saklar
- Kullanıcıya dönük ve daha yapılandırılmış raporlar üretebilir
- Daha geniş kişisel yapay zekâ sistemi içinde koordinasyon için C-LOPAI’ye bilgi aktarabilir
- Hassas konular için temel güvenlik sınırları uygular
- Kişisel düşünme/yorumlama süreçleri ile teknik veya sistem sorularını birbirinden ayırır
- Basit bir motivasyon botu gibi davranmak yerine pratik çerçeveleme ve öz-gözlem üzerine odaklanır

---

## Bu Proje Neden Var?

Çoğu yapay zekâ asistanı tepkiseldir. Sorulan şeye cevap verir, ardından daha derin sürekliliği unutmaya meyillidir.

HEALER farklı bir yaklaşımı denemek için geliştirildi:  
Konuşma, hafıza, yapılandırılmış öz-değerlendirme ve bilgi getirme sistemlerini birleştirerek kullanıcıyı zaman içinde destekleyebilen kişisel bir yapay zekâ.

Bu sistem profesyonel desteğin yerine geçmek veya tıbbi kararlar vermek için tasarlanmamıştır. Amacı daha çok özel bir düşünme partneri olmaktır: düşünceleri düzenlemeye, tekrar eden örüntüleri fark etmeye ve dağınık günlük deneyimleri daha anlaşılır, takip edilebilir ve uygulanabilir hale getirmeye yardımcı olan bir araç.

HEALER’in uzun vadeli değeri şu bileşenlerin birleşiminden gelir:

- Kişisel bağlam
- Sakin ve tutarlı yanıtlar
- Yapılandırılmış hafıza
- Seçilmiş okuma materyallerinden bilgi getirme
- Düzenli raporlama
- Daha geniş C-LOPAI ajan ağıyla entegrasyon

---

## Temel Mimari

HEALER, bir VPS üzerinde çalışan Telegram botu olarak kuruludur ve modüler bir Python mimarisi kullanır.

Yüksek seviyede mesaj akışı şu şekildedir:

```text
Telegram Mesajı
    ↓
Güvenlik Katmanı
    ↓
Intent Sınıflandırıcı
    ↓
Yansıtıcı Formülasyon
    ↓
Opsiyonel RAG Bilgi Getirme
    ↓
Yanıt Üretimi
    ↓
Oturum + Uzun Dönem Hafıza
    ↓
C-LOPAI Export / Arşiv
```

Bu katmanlı yapı sayesinde HEALER her mesajı aynı şekilde ele almaz.  
Kısa bir not, kişisel bir düşünce paylaşımı, kaynak odaklı bir soru ve sistem düzeyinde bir teknik soru farklı biçimde işlenir.

---

## Ana Bileşenler

### Telegram Arayüzü

HEALER kullanıcıyla Telegram üzerinden iletişim kurar.  
Bu sayede deneyim günlük hayata yakın ve basit kalır: kullanıcı doğal şekilde yazabilir, kısa notlar gönderebilir, rapor isteyebilir veya ayrı bir panel açmadan devam eden bir konuşmayı sürdürebilir.

### Kişisel Profil Katmanı

HEALER, kullanıcının geçmişini, tekrar eden temalarını, tercih edilen tonu ve önemli sınırları anlamak için yapılandırılmış bir profil dosyası kullanır.

Bu profil, sistemin genel ve yüzeysel cevaplar vermesini engeller.  
HEALER, boş bir chatbot gibi yanıt vermek yerine kullanıcının gerçek geçmişi ve hedefleriyle daha uyumlu, bağlam farkındalığı yüksek cevaplar üretebilir.

### RAG Bilgi Havuzu

HEALER; psikoloji, kişisel gelişim, dikkat, duygu düzenleme ve öz-gözlem alanlarında seçilmiş kitaplardan oluşan yerel bir bilgi getirme sistemi içerir.

Kitaplar parçalara ayrılarak yerel bir ChromaDB vektör veritabanında saklanır.  
Gerekli olduğunda HEALER, ilgili bağlamı getirerek yanıtlarını destekleyebilir.

Buradaki amaç kitapları mekanik şekilde alıntılamak değildir. Asıl amaç, kaliteli okuma materyallerinin asistanın akıl yürütmesini arka planda güçlendirmesidir.

### Oturum Hafızası

HEALER aktif konuşmaları takip eder ve ilgili oturum verilerini saklar.  
Bu sayede konuşmalar kopuk ve parçalı değil, daha devamlı hissedilir.

Sistem, son konuşma akışını hatırlayabilir, mevcut mesajları önceki bağlama bağlayabilir ve her mesajı tamamen izole şekilde ele almaktan kaçınır.

### Uzun Dönem Hafıza

Önemli notlar, oturum özetleri, tekrar eden örüntüler ve yapılandırılmış gözlemler SQLite üzerinde saklanır.

Bu yapı HEALER’e uzun dönem takip için temel sağlar.  
Zaman içinde asistan daha yararlı hale gelebilir; çünkü yalnızca mevcut mesaja yanıt vermekle kalmaz, tekrar eden örüntüleri de gözlemlemeye başlar.

### Raporlar

HEALER, saklanan verilerden raporlar üretebilir.  
Bu raporlar, yakın dönemdeki örüntüleri, anlamlı notları ve genel yönelimi daha yapılandırılmış biçimde özetlemek için tasarlanmıştır.

Amaç, kişisel ilerlemeyi uzun sohbet geçmişinin içinde kaybolmaktan çıkarıp daha kolay gözden geçirilebilir hale getirmektir.

---

## C-LOPAI Köprüsü

HEALER aynı zamanda daha geniş kişisel yapay zekâ ekosisteminin ana koordinasyon ajanı olan **C-LOPAI** ile bağlantılıdır.

C-LOPAI merkezi komuta ve arşiv katmanı gibi çalışır.  
HEALER’in görevi yalnızca kullanıcıya yanıt vermek değil, aynı zamanda C-LOPAI’nin daha geniş koordinasyon için kullanabileceği yapılandırılmış özetler üretmektir.

Bu köprü dosya tabanlı export ve arşiv güncellemeleriyle çalışır.  
HEALER haftalık veya yapılandırılmış özetler hazırlayabilir ve bunları C-LOPAI’nin okuyabileceği ortak bir hafıza alanına yazabilir.

Bu yapı basit ama güçlü bir mimari oluşturur:

```text
HEALER
  → kişisel düşünme ve gözlem süreçlerini takip eder, özetler

C-LOPAI
  → HEALER özetlerini okur
  → önemli bağlamı arşivler
  → daha geniş ajan sistemiyle koordinasyon kurar
```

Bu köprü, projenin en önemli parçalarından biridir. Çünkü HEALER’i tek başına çalışan bir bottan çıkarıp daha büyük bir kişisel yapay zekâ işletim sisteminin bileşenlerinden biri haline getirir.

---

## Ana Komutlar

HEALER doğrudan etkileşim için çeşitli Telegram komutları içerir:

| Komut | Amaç |
|---|---|
| `/start` | Botu başlatır ve kullanıcı bağlamını yükler |
| `/end` | Aktif oturumu kapatır ve özet kaydeder |
| `/rapor` | Yakın dönem kullanıcı raporu üretir |
| `/klinik_rapor` | Daha yapılandırılmış bir rapor üretir |
| `/clopai` | C-LOPAI için yapılandırılmış bilgi export eder |
| `/profil` | Profil tabanlı özet gösterir |
| `/not` | Doğrudan not kaydeder |

Bu komutlar sistemi pratik tutmak için tasarlanmıştır.  
Kullanıcı ister doğal şekilde konuşabilir, ister daha yapılandırılmış bir işlem için açık komut kullanabilir.

---

## Mevcut Sürüm: V0.5

V0.5, HEALER’in çekirdek zekâ katmanının ilk sağlam sürümünü temsil eder.

Bu aşamada projede şunlar bulunmaktadır:

- Telegram bot entegrasyonu
- Modüler Python backend
- Gemini tabanlı model yönlendirme
- Intent sınıflandırma
- Yansıtıcı formülasyon katmanı
- Yanıt üretim katmanı
- Yerel RAG entegrasyonu
- ChromaDB vektör veritabanı
- SQLite hafıza
- Oturum takibi
- Uzun dönem notlar
- Rapor üretimi
- C-LOPAI export köprüsü
- Temel güvenlik sınırları
- Profil farkındalığı olan yanıtlar

V0.5 nihai ürün değildir.  
Ancak güçlü bir çalışma temelidir: sistemin basit bir bottan çıkıp gerçek bir kişisel yapay zekâ modülüne dönüşmeye başladığı noktadır.

---

## Tasarım İlkeleri

HEALER birkaç temel ilke üzerine tasarlanmıştır:

### 1. Genel Tavsiyeden Çok Bağlam

Sistem, onu kullanan kişiyi anlamalıdır.  
Genel tavsiye üretmek kolaydır; kişisel fayda ise bağlamdan doğar.

### 2. Sakin, Net ve Dengeli Ton

HEALER abartılı tepki vermemeli, dramatize etmemeli veya boş motivasyon üretmemelidir.  
Tonu sakin, pratik ve dengeli olmalıdır.

### 3. Hafıza Önemlidir

Kişisel bir yapay zekâ, değişimi zaman içinde takip edebildiğinde daha değerli hale gelir.  
HEALER’de hafıza sonradan eklenen bir detay değil, temel özelliklerden biridir.

### 4. Bilgi Desteklemeli, Baskın Gelmemeli

RAG sistemi, yanıtları seçilmiş bilgi kaynaklarıyla güçlendirmek için vardır.  
Asistanı kuru bir ders kitabı gibi konuşturmamalıdır.

### 5. İnsan Kontrolü Önceliklidir

HEALER bir destek aracıdır.  
Kullanıcının daha net düşünmesine, organize olmasına ve daha bilinçli hareket etmesine yardımcı olurken önemli kararları insan kontrolünde bırakmalıdır.

---

## Teknoloji Yığını

| Katman | Teknoloji |
|---|---|
| Arayüz | Telegram Bot |
| Backend | Python |
| LLM Sağlayıcısı | Google Gemini |
| Vektör Veritabanı | ChromaDB |
| Uzun Dönem Depolama | SQLite |
| Bilgi Getirme Yöntemi | Retrieval-Augmented Generation |
| Dağıtım | Linux VPS |
| Entegrasyon | Dosya tabanlı C-LOPAI köprüsü |

---

## Proje Durumu

HEALER V0.5, arkasında gerçek bir mimari bulunan çalışan bir kişisel yapay zekâ destek modülüdür.

Şu anda şunları yapabilir:

- bağlam farkındalığı olan konuşmalar yürütebilir,
- kişisel profil kullanabilir,
- destekleyici bilgiyi yerel bilgi havuzundan getirebilir,
- notları ve oturumları kaydedebilir,
- raporlar üretebilir,
- C-LOPAI ile yapılandırılmış bilgi paylaşabilir.

Proje bilinçli şekilde adım adım geliştirilmektedir. Öncelik; kararlılık, mahremiyet ve dikkatli iterasyondur.

---

## Son Not

HEALER, daha kişisel bir yapay zekâ asistanı oluşturma denemesidir.

Genel amaçlı bir chatbot değildir.  
Basit bir günlük uygulaması değildir.  
Yalnızca bir LLM sarmalayıcısı değildir.

HEALER; konuşma, hafıza, seçilmiş bilgi kaynakları ve sistem düzeyinde koordinasyonu birleştiren odaklı bir ajandır.

V0.5, temelin artık yerli yerine oturduğu noktayı temsil eder:  
HEALER dinleyebilir, yansıtabilir, hatırlayabilir, özetleyebilir ve daha geniş C-LOPAI ekosistemiyle iletişim kurabilir.

Projenin özü budur.
