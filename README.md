# 💎 Luks Emlak Yapay Zeka Asistanı & CRM Otomasyon Ekosistemi
### Geliştirici: Elif Nur Ayhan | Versiyon: 2.5.0 (Final - Production Ready)

Lüks gayrimenkul sektörünün yüksek prestij ve kurumsal iletişim standartlarına tam uyumlu olarak geliştirilmiş otonom bir **Lead Yönetimi, Yapay Zeka Karar Destek ve CRM Otomasyon Ekosistemidir**. Sistem; Instagram DM, WhatsApp Business API ve Canlı Meta Reklam Altyapısı (Meta Graph API) üzerinden tetiklenen müşteri etkileşimlerini uçtan uca yakalar, Google Gemini LLM motoru ile yapılandırılmamış metinleri anlık anlamlandırır, otonom süreçleri işleterek veriyi HubSpot CRM sistemine entegre eder.

---

## 🏗️ 1. Gelişmiş Sistem Mimarisi ve İstek Akışı

Yazılım mimarisi, harici kanallardan gelen yoğun istek trafiğini sistemi kilitlemeden yönetebilmek amacıyla **FastAPI Asenkron İş Parçacıkları (Background Tasks)** üzerine inşa edilmiştir.

1. **Müşteri Mesajı:** Kullanıcı Instagram DM (ManyChat) veya WhatsApp Business API üzerinden yapılandırılmamış bir talep gönderir.
2. **FastAPI Webhook Girişi:** İstek asenkron olarak backend endpoint'ine (`/api/webhook`) POST edilir.
3. **Gemini AI Analiz Katmanı:** `gemini-2.5-flash` modeli lüks konut segmenti kuralları çerçevesinde mesajı işler; konum, bütçe ve telefon verilerini otonom olarak ayıklar. En az iki kriter doğrulanırsa durum `lead_captured` (kalifiye sıcak lead) seviyesine yükseltilir.
4. **Veri & CRM Senkronizasyonu:** Kalifiye veriler anlık olarak yerel SQLite veri tabanına işlenir ve resmi HubSpot Python SDK'sı üzerinden CRM'e otomatik contact olarak kaydolur.
5. **Otonom Operasyonlar:** Google Drive API ile müşteriye özel izole klasör açılır; Telegram botu üzerinden yöneticiye anlık şık bir Markdown rapor fırlatılır.

---

## 📸 2. Canlı Sistem Testleri ve Ekran Görüntüleri

### 2.1. ManyChat Otomasyon Akışı (Trigger & Action)
Instagram veya WhatsApp üzerinden gelen kullanıcı mesajı **"Bodrum"** gibi kritik segment anahtar kelimelerini içerdiği an otomasyon tetiklenir. Sistem, arka planda LocalTunnel/VPS adresi üzerinden yerel FastAPI webhook endpoint'ine asenkron bir `External Request` (Dış İstek) fırlatır.

### 2.2. Canlı Müşteri Simülasyonu ve Yapayı Zeka İş Mantığı
Instagram DM üzerinden gelen *"Merhaba, Bodrum taraflarında 15-20 milyon TL bütçeyle lüks bir villa arıyorum. Detaylar için bana 0532... numaralı telefondan ulaşabilirsiniz."* ham metni, yapay zeka ayıklama motoru tarafından doğrudan yakalanır. Google Gemini LLM modeli, statik regex kalıplarına bağımlı kalmaksızın **Bölge:** `Bodrum`, **Bütçe:** `15-20 milyon TL` ve **İletişim:** `0532...` verilerini otonom olarak parçalayarak veri tabanına iletir.

### 2.3. Google Drive Otonom Klasör Yapısı
ManyChat'ten kalifiye bir lead düştüğü an, arka plandaki `GoogleDriveService` modülü ve Google Cloud Service Account altyapısı sıfır kullanıcı müdahalesiyle uyanır. Drive üzerindeki ana dizinde müşteri numarasına özel (`1294340325_Emlak_Klasörü`) izole gayrimenkul proje klasörlerini saniyeler içinde otomatik olarak oluşturur.

### 2.4. ManyChat 24 Saat Bariyeri ve Hata Yakalama Kontrolü
Geliştirme aşamasında karşılaşılan `3011` (24 saat etkileşim kuralı engel) hatası, sistem tarafından anlık loglanarak Telegram Botu üzerinden admin paneline aktarılmıştır. Mesajlaşma payload'una mimari seviyede giydirilen kurumsal `HUMAN_AGENT` etiketi (Message Tag) sayesinde bu kural bypass edilmiş ve sistemin kesintisiz çalışması doğrulanmıştır.

### 2.5. Merkezi Telegram Kontrol Paneli Yetenekleri
Telegram botu çift yönlü interaktif bir admin paneli olarak çalışır. Yönetici bot ekranına `/durum` yazdığında sistem SQLite veritabanına anlık ORM sorgusu atarak toplam kullanıcı ve sıcak lead sayılarını analiz raporu olarak basar. `/son_lead` komutu gönderildiğinde ise en son yakalanan müşterinin bütçe, konum ve iletişim verilerini kusursuz bir Markdown kartı olarak yöneticinin önüne serer. `/reklam_analiz` komutu ise Meta Graph API servisinin bütçe optimizasyon döngüsünü manuel/onaylı olarak tetikler.

---

## 🛠️ 3. Çözülen Kronik Sektörel Problemler

* **ManyChat 24 Saat Engelinin Aşılması:** Facebook/Instagram platformlarının 24 saat boyunca etkileşime geçmeyen kullanıcılara mesaj gönderimini engelleme politikası (`3011` hatası), `HUMAN_AGENT` etiketiyle çözülmüştür.
* **HubSpot El Sıkışma Protokolü:** Ham HTTP isteklerinin lokal ağlarda tetikleyebileceği SSL/Proxy (`WRONG_VERSION_NUMBER`) hataları resmi HubSpot Python SDK katmanı entegre edilerek tamamen aşılmıştır.
* **Sıfır Altyapı ve Sunucu Maliyeti:** Tüm ekosistem Docker platformuna taşınmış (`Dockerfile` + `docker-compose.yml`), veritabanı lokalde izole edilmiş ve Google AI Studio'nun ücretsiz geliştirici kotaları kullanılarak projenin bakım maliyetleri sıfıra indirilmiştir.

---

## 🚀 4. Görseller
<img width="1158" height="652" alt="image" src="https://github.com/user-attachments/assets/a6d93ed5-eee4-4e3e-b76f-279d99106f81" />
<img width="1157" height="652" alt="image" src="https://github.com/user-attachments/assets/512a2b16-bd9f-407a-bb7b-050b62866f54" />
<img width="1158" height="655" alt="image" src="https://github.com/user-attachments/assets/c2f9ccf0-8373-4853-a617-dda7bc692f07" />
<img width="1159" height="651" alt="image" src="https://github.com/user-attachments/assets/cf3fc35d-8ed5-41a4-93e3-273b07c17d7f" />
<img width="1160" height="648" alt="image" src="https://github.com/user-attachments/assets/022d6c24-a7f2-4791-886c-7689805c98ef" />
<img width="1159" height="649" alt="image" src="https://github.com/user-attachments/assets/3f5cafa7-7bcf-4a33-a2fd-89fabf17117e" />
