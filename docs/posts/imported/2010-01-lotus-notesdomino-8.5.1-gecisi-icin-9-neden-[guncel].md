---
authors:
  - serdar

title: "Lotus Notes/Domino 8.5.1 Geçişi için 9 Neden [güncel]"

slug: lotus-notesdomino-8.5.1-gecisi-icin-9-neden-[guncel]

date: 2010-01-27T16:06:47Z

---

Daha önce Lotus Kullanıcı Grubu'na yazdığım yazıyı yoğun ilgi (!) üzerine yeniliyorum. Upgrade etmeyi düşünenlere yardımcı olmasını umarız...

**1. ID Vault**

ID dosyalarının yönetimi, sistem yöneticileri için en baş ağrıtan süreçlerden birisi olmuştur. ID dosyalarıyla gelen entegre güvenlik sistemi, şifre tabanlı sistemlere göre çok büyük güvenlik üstünlükleri sağlasa da yönetim ve kullanım açısından bazı kısıtlar oluşturmaktadır. Fakat 8.5 itibariyle bu sorunu çözmek için önemli bir aşama kaydedildi. Sunucu tabanlı bir veritabanının ID dosyalarının güvenli kopyalarını tutması temeline dayanan ID Vault sistemi 8.5.1 ile daha stabil bir yapıya kavuşmuş oldu. Ayrıca **Lotus iNotes** ve **Lotus Traveler** gibi ikincil uygulamaların da API düzeyinde ID Vault'u kullanması 8.5.1 ile gelen yeni bir özellik.

Bu özelliği test platformunda kurarsanız epey keyifleneceğinize eminim. Örneğin Lotus Notes client üzerinde id dosyasını siliyoruz. Notes açıldığında sanki ID dosyası varmış gibi şifre soruluyor. Şifre doğru girilirse ve sistem yöneticisi 'ID indirme' hakkı verdiyse kullanıcı normal bir şekilde devam ediyor hayatına. Data klasörünüze baktığınızda silinmiş ID dosyasının geri geldiğini görüyorsunuz... Şifre merkezi olarak sıfırlandığında kullanıcı Notes'unu gene normal olarak açıyor. Yeni şifresini giriyor ve hayatına devam ediyor. Şifresi değişmiş ID otomatikman indiriliyor. Eğer iki farklı PC kullanılıyorsa ikisinde de güncelleme yapılıyor otomatik olarak...
<!-- more -->
ID Vault sayesinde;

* Yetkili kullanıcılar, ID dosyalarının şifrelerini sıfırlayabilir,
* Şifre sıfırlama işlemi programatik olarak gerçekleştirilebilir,
* ID dosyalarının farklı kopyaları arasında senkronizasyon sağlanabilir,
* İsim değişikliği ve anahtar değişimi (key rollover) işlemleri kullanıcı dahil olmadan gerçekleştirilebilir,
* Audit fonksiyonu sayesinde ID dosya içerikleri açığa çıkarılabilir.

<br />

[*Daha fazlası...*](http://www-10.lotus.com/ldd/dominowiki.nsf/dx/12162008022843PMNEKQT7.htm)

**2. DAOS: Domino Attachment and Object Service**

Daha önce sunulan Shared Mail (veya SCOS: Single Copy Object Store), R8.5 itibariyle kaldırılıyor. **DAOS** servisinin SCOS üzerine çok önemli avantajları bulunuyor.

* SCOS, birden fazla kişiye atılan mesajları depoluyordu. DAOS, attachment bazında çalıştığından daha etkin bir optimizasyon sunuyor,
* DAOS, depoladığı objeleri ve dosyaları bir .nsf dosyaya kaydetmiyor. Bu sayede performans avantajı sunduğu gibi **incremental** yedeklemede kolaylık sağlıyor,
* DAOS yalnızca E-posta'lar üzerinde değil **tüm veritabanlarında** çalışıyor.

<br />

Lotus Domino 8.5.1 ile gelen en önemli yenilik DAOS'un **replication düzeyine** indirgenmesi. 8.5.1 öncesinde veritabanındaki ekli dosyalar DAOS'ta tutuluyordu. Fakat replication esnasında DAOS'tan çıkartılıyordu. Eğer bir attachment 5 veritabanında bulunuyorsa ve bu 5 veritabanı ikinci bir sunucuya (örneğin **cluster**) replicate ediliyorsa bu attachment 5 kez transfer ediliyordu. Artık Replicator önce DAOS kopyasını gönderiyor, daha sonra DAOS ticket'larını. Özellikle cluster'larda çok önemli bir performans arttırımı söz konusu.
[*Daha Fazlası...*](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/topic/com.ibm.help.domino.admin85.doc/DOC/H_ATTACHMENT_CONSOLIDATION_OVER.html)

[*Örnek Başarı...*](http://www.edbrill.com/ebrill/edbrill.nsf/dx/yet-another-daos-success-story-from-darren-duke)

**3. Lotus Notes Traveler 8.5.x**

R8 itibariyle sunulan Traveler, yeni versiyonda da bir çok yenilik sunuyor:

* Nokia S60 desteği ve iPhone desteği (8.5.1 ile),
* Remote Wipe ile kaybolan telefondaki bilgileri uzaktan silebilme,
* Windows Mobile 6 telefonlar için rich text desteği,
* Windows Mobile cihazlar için dijital imza desteği,
* iPhone üzerinde şifreli mesaj desteği (Lotus Traveler 8.5.1.1 ve Lotus Traveler Companion ile. İlgili yazı [](2010-01-lotus-notes-traveler-companion.md "Lotus Notes Traveler Companion")burada...),
* iPhone üzerinde takvim geliştirmeleri (Lotus Traveler 8.5.1.1 ve Lotus Traveler Companion ile. İlgili yazı [](2010-01-lotus-notes-traveler-companion.md "Lotus Notes Traveler Companion")burada...).

<br />

[*Daha Fazlası...*](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/topic/com.ibm.help.lnt85.doc/What%27s_new_in_Lotus_Notes_Traveler_8_5.html)

**4. Yeni iNotes 8.5.x**

R8.5 itibariyle web arayüzünde devrimsel bazı değişiklikler yapıldı:

* Merkezi olarak yönetilebilen widget desteği,
* Lotus Quickr entegrasyonu ve yerel Quickr sunucuları için HTTP proxy servlet,
* Mail ve desktop policy desteği,
* Ultra-lite Edition ile geliştirilmiş iPhone desteği,
* 'External Calendar Overlay' ile farklı takvimlerin eklenebilmesi,
* Mesajlarda disclaimer desteği (8.5.1 ile)

<br />

[*Daha Fazlası...*](http://www.ibm.com/developerworks/lotus/library/inotes-full/)

**5. XPages**

Web arayüzünde değişim zamanı gelmişti. XPages, [JSF](http://en.wikipedia.org/wiki/JavaServer_Faces) temelli [Web 2.0](http://en.wikipedia.org/wiki/WEB_2.0)uygulamaları geliştirmek amacıyla kurgulanan tasarım elemanlarıdır.

* Önceden hazırlanmış web kontrolleriyle kolay sayfa tasarımları,
* Kompozit temelli genişletilebilir hazır kontroller,
* CSS desteği,
* İleri düzey web kontrolleri (tabbed panel gibi...),
* Client-side ve Server-side Javascript desteği,
* Sunucu üzerindeki Java kütüphanelerine doğrudan erişim,
* Ajax desteği (Kısmi sayfa yenilemesi, type-ahead kullanımı gibi...),
* Notes platformu desteği ([8.5.1 ile](http://www.lotusturkiye.org/lotus/myquickr/blogspace/blog/!ut/p/c1/04_SB8K8xLLM9MSSzPy8xBz9CP0os_gAN8ugEFN_YwMDcwtDAyMvQwtHbw9vAwNfY6B8pFm8AQ7gZEBAdzjIPjwqDCDy-MzHJ-9ooO_nkZ-bqh-pH2WO0xZXM_3InNT0xORK_RD9SA_9gtwIg8yAjEQAtj-oHA!!/dl2/d1/L2dJQSEvUUt3QS9ZSnB3L3djbTo4NjEwMjA4MDRlMTNhYzI0Yjk5NWI5NjMwMzYyOTE1NQ!!/)),
* Offline uygulama desteği (8.5.1 ile),
* Component geliştirme desteği ile composite uygulama ve Lotus Mashup entegrasyonu (8.5.1 ile),
* Theme desteği (8.5.1 ile).

<br />

[*Daha Fazlası...*](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/topic/com.ibm.designer.domino.xpages_ug.doc/wpd_forms_working_with.html)

**6. Lotus Domino Designer 8.5.1**

Eclipse tabanlı yeni Designer, uygulama geliştirmeciler için pek çok yenilik içeriyor. İlk versiyonda bazı sorunlar olsa da artık eclipse tabanlı modern bir platforma geçmenin zamanı gelmişti.

Lotus Domino Designer 8.5.1 ile gelen yeniliklere bakarsak;

* En önemli yenilik; artık Lotus Domino Designer 8.5.1'in **ücretsiz** olarak dağıtılması,
* Eclipse tabanlı Lotusscript editörü Script Library ve Agent tasarlarken bize çok büyük bir yenilik sağlıyor. Alışmak biraz zaman alsa da eskisinden çok daha rahat olduğunu söyleyebilirim,
* Symphony, Portal gibi yeni bileşenlerle geliştirilmiş 'Composite Application Editor',
* Working Set'lerle daha organize çalışmayı sağlayan uygulama navigasyonu,
* Geliştirilmiş arama fonksiyonu.

<br />

[*Daha Fazlası...*](http://www-10.lotus.com/ldd/ddwiki.nsf/archive?openview&title=Domino%20Designer%208.5&type=cat&cat=null&tag=Domino%20Designer%208.5)

**7. Domino Configuration Tuner**

R8.5 itibariyle gelen DCT, sunucu konfigürasyonunuzu inceleyip daha verimli bir sistem için gereken değişiklikleri önermektedir.

[*Daha Fazlası...*](http://www-01.ibm.com/support/docview.wss?uid=swg24019358&rs=0&cs=utf-8&context=SWA00&dc%C3%9400)

**8. Diğer Sistem Yönetim yenilikleri**

8.5 ve 8.5.1 ile gelen bazı yenilikler 'neden daha önce yapmadılar ki' dedirtecek cinsten. Bir kaçını özetlemek gerekirse;

* Lotus Notes Standard Configuration, artık MacOS platformlarında da çalışıyor,
* Router'da önemli tasarım değişiklikleri yapıldı. Mesaj transferleri bu versiyonlar itibariyle belirgin bir şekilde hızlanmış oldu,
* Windows Single Sign-on özelliğiyle web kullanıcıları kendi bilgisayarlarında bir Active Directory'ye bağlılarsa tekrar şifre girmeden giriş yapabiliyorlar (8.5.1 ile),
* 'Notes Shared Login' ile Single-log-on servisinin yarattığı güvenlik açığı kapatılmış oldu,
* Auto-populated grup kavramı 8.5 itibariyle sunuluyor. Bu özellik sayesinde belirli bir sunucuda ikamet eden kullanıcıların otomatik olarak gruplanması sağlanıyor. Bu özellik daha geliştirilecek gibi görünüyor,
* 'Dynamic Policy' ile policy yönetimi epey iyileştirildi. Bu sayede policy'ler grup bazında tanımlanabiliyor,
* Policy'ler ve install paketleriyle sertifika dağıtımı mümkün hale geliyor (8.5.1 ile). Daha önce programatik olarak çözülmesi gereken bir sorun da policy'ler yardımıyla çözüldü. Sistem yöneticisi, seçtiği sertifikaları (cross certification, internet certifier, trusted root certifier...),
* 8.5 itibariyle yeni ve gelişmiş bir '**Roaming User**' desteği sunuluyor. Hatta 8.5.1 ile birlikte kullanıcının workspace ikonları bile gezicilik kapsamına alındı.


**9. Geriye Doğru Uyumluluk**

Tüm bu yeni özelliklere rağmen eskiden yazdığınız tüm uygulamaları rahatlıkla kullanabilirsiniz. Hatırlattığı için **Atilla Öztürk**'e teşekkürler :)
