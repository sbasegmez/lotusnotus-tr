---
authors:
  - serdar

title: "ID Vault ve Upload/Download Problemleri"

slug: id-vault-ve-uploaddownload-problemleri

date: 2010-03-22T19:50:46+02:00

---

ID Vault, 8.5 versiyonunun en önemli özelliklerinden birisi. Bir çok sistem yöneticisinin nefret ettiği ID ve şifre yönetimi konusunda çok önemli kolaylıklar getiren Vault özelliğiyle ilgili bir yazı yazmak istedim. Bu yazıda vault mekanizmasından kısaca bahsedeceğim ama özellikle sıklıkla karşılaşılan **download/upload** konularıyla ilgili bazı ipuçları vermek istiyorum. Çok yeni bir özellik olduğundan versiyona özel bir takım sorunlar sıklıkla yaşanıyor. Yazıyı okurken farkedeceksiniz ki bu özelliği kullanacaksanız hem client'larınızı hem de server'larınızı 8.5.1 FP1 versiyonuna getirmek fena bir fikir olmayacak.
<!-- more -->

ID Vault özelliğinden uzun uzun bahsetmek istemiyorum. Daha detaylı bilgi isteyenler developerWorks sitesindeki [Domino Security Wikis](http://www.lotus.com/ldd/dominowiki.nsf/xpViewCategories.xsp?lookupName=Domino%20security) sayfalarını inceleyebilir.

ID Vault, temel olarak kullanıcılara ait ID dosyalarını güvenli bir şekilde depolayan merkezi bir yapı. Daha önce kullanıcının ID dosyasıyla katılımını zorunlu kılan bir takım operasyonlar (Şifre değişiklikleri, anahtar yenilemeler ve re-sertifikasyonlar gibi) bu yöntemle kullanıcısız bir şekilde gerçekleştirilebiliyor. Ayrıca yapı yönetimsel işlemlerin katmanlı bir şekilde delege edilebilmesini sağlıyor. Örneğin farklı sertifika gruplarında (organizasyonel birimler düzeyinde) farklı şifre sıfırlama operatörleri atanabiliyor. Self servis uygulamalarla kullanıcıların kendi şifrelerini resetlemesi sağlanabiliyor.

ID Vault sisteminize tanımlandıktan ve policy kanalıyla kullanıcılara tanıtıldıktan sonra 8.5 ve üstü client kullanan tüm kullanıcıların id dosyaları vault'a gelmeye başlar. ID Vault veritabanını doğrudan açarsanız bunları görebilirsiniz. Policy'de vault ayarlarını yaptıktan sonra yarattığınız kullanıcılar için id dosyaları otomatikman vault'a yüklenecektir. Bu işlemlere 'ID Upload' diyoruz.
Bir şifre resetleme yaptığınızda; client tarafında id dosyası bozulur/kaybolursa veya birden fazla client kullanan kullanıcı bir tarafta şifre değiştirip öbür tarafta sisteme girdiğinde ID dosyası vault'dan client'a indirilir. Bu olaya da 'ID Download' diyeceğiz.

Tüm bu işlemler Vault sunucusunun **log.nsf** veritabanında '**Security Events** ' bölümünde görülebilir. Log'larla ilgili bir bilgi vereyim: Genelde bir kullanıcının ID dosyası vault'da bulunamadığında "*Error: Entry not found in index* " gibi bir hata görüyorsunuz. Hemen ardından "*ID successfully synchronized with vault* " mesajı çıkıyor. Buradaki hata mesajını dikkate almaya gerek yok.

Soru cevap kısımlarına geçmeden önce iki küçük hatırlatma daha: Birincisi yeni problemler ve/veya çözümlerle karşılaştıkça bu yazıyı güncelleyeceğim. İkincisi ise bunların dışında problemlerle karşılaşırsanız beni bilgilendirin, burayı güncellerim. Yorum yapabilir ya da mesaj atabilirsiniz.

**#### 1. ID Upload Problemleri**
**1.1.Kullanıcı ID Vault'a tanımlandı, policy'si güncellendi, 8.5 ve üstü client'dan giriş yaptı ama ID dosyası vault'a henüz gelmedi.**

Bu konu ilk zamanlar benim epey zamanımı almıştı. Farkettikten sonra ilgili dokümantasyonu gördüm. Vault sunucuda yük dengelemesi yapılması amacıyla Upload işlemleri biraz rastgele bir şekilde yapılıyor. Örneğin cluster yapısında iki sunucuda da Vault tanımlıysa rastgele birisi deneniyor, başarısız olma durumunda diğeri denenmeden önce biraz daha bekleniyor.

Özellikle birden fazla ID aynı client'ta kullanılırsa bu 'denemeler arası bekleme zamanları' problem yaratıyor. Genelde test etme aşamasında yaşanılan bu problemlerde 'notes.ini' dosyasında 'IDVault' ile başlayan satırları silip yeniden başlatmayı deniyorum ve kısa zaman içinde problemin çözüldüğünü görüyorum.

İki önemli noktanın kontrol edilmesi gerekiyor. Birincisi kullanıcının lokasyon dokümanındaki 'home server' alanı doğru olmalı. İkincisi log incelenerek (hem lokal, hem sunucuda security events bölümleri) deneme yapılıp yapılmadığı, yapıldıysa ne hata oluştuğu belirlenmeli.

Örneğin IBM'in technote'larında kullanıcının adres defteri (names.nsf) versiyonunun kontrol edilmesi ve policy ayarlarının kontrol edilmesi öneriliyor. Notes.ini dosyasındaki 'KeyFileName' kaydının doğru id dosyasını göstermesi gerekiyor. Bazı durumlarda kullanıcının id dosyasının isminin 'user.id' şeklinde olması gerektiği öneriliyor.

**1.2.Yeni kullanıcı yaratıyoruz ve ID Upload edilemedi hatasıyla karşılaşıyoruz.**

En sık karşılaştığım problem. Registration esnasında mekanizma şu şekilde çalışıyor. Admin client yeni ID dosyasını temp klasörüne yaratıyor. Bir an için bu yeni ID dosyasını kullanarak sunucuya giriş yapıyor ve senkronizasyon gerçekleştiriliyor.

Bu tip bir hata oluştuğunda genelde person dokümanı oluşuyor, mail veritabanı yaratılıyor (ya da yaratılması için request oluşuyor) ve grup üyeliği oluşturuluyor. Fakat ID dosyası oluşmadığı için işlemler yarım kalıyor. Yeniden denemeden önce bunların temizlenmesi gerekiyor.

IBM'in bir technote'una göre antivirüsler bazen bu klasörde kısıtlama uygulayabiliyor. Antivirüs loglarını incelemek bir adım olabilir.

Lotus Domino 8.5 versiyonunda eğer "Compare public key \> Enforce key checking for all Lotus Notes users and Lotus Domino servers" seçeneğini kullanıyorsanız bu hata oluşuyor. Sunucu anahtar kontrolü yapmaya çalıştığında 'Person' kaydı olmayan yeni kullanıcının giriş yapmasını engellemeye çalışıyor. 8.5.1 versiyonunda bu problem düzeltildi. Hemen upgrade yapmayı düşünmüyorsanız "Compare public key \> Enforce key checking for Notes users and Domino servers listed in trusted directories only" seçeneği sorunu düzeltecektir.

Gene Lotus Domino 8.5 versiyonunda eğer 'Certification Authority' kullanıyorsanız ID dosyası upload edilemiyor ve log dosyasında "Error: Your certificate has not yet been signed by the Certificate Authority. Try again later." gibi bir hata oluşuyor. Bildiğiniz gibi CA kullanıldığında oluşturulan sertifikanın Administration Request kanalıyla onaylanması gerekiyor. IBM'in technote'una göre bu sorun da 8.5.1 versiyonunda düzeltilmiş. 8.5 kullanıyorsanız hatayı gözardı edebilirsiniz, kullanıcı ilk giriş yaptığında ID dosyası güncellenecektir.

Lotus Notes 8.5 versiyonunda bizim rastladığımız bir sorun da kullanıcıyı yaratan sistem yöneticisinin lokasyon ayarlarından kaynaklanıyordu. Lokasyon ayarlarında 'Mail File Location' bölümü 'on server' seçili değilse bu geçici giriş yapılamıyor ve upload gerçekleşemiyordu. Lotus Notes 8.5.1 versiyonunda bu sorun düzeltildi.

Başka bir müşterimde daha önce aynı isimde yaratılmış ve daha sonra silinmiş bir kullanıcının benzer bir hataya sebep olduğunu gördük. ID upload işlemi gerçekleşmiyor ve log dosyasında 'Note Item Not Found' hatası oluşuyordu. Aynı isimde yaratılan kullanıcının ID dosyası Vault üzerinde 'Inactive' olarak duruyordu. Bu kaydı sildiğimizde sorun düzeldi.

**#### 2. ID Download Problemleri**
**2.1.Yeni kullanıcı yarattık, kullanıcının client kurulumu sırasında "Your password has expired. You cannot access this server until you change it" hatası alıyoruz.**

Daha önce [](2010-02-lotus-notes-8.5.1-password-policy-sorunu.md "Lotus Notes 8.5.1 Yeni Kullanıcılarda Password Policy Sorunu")yazmıştık. Lotus Notes 8.5.1 versiyonunda böyle bir sorun var. Sorunu düzeltmek için FP1 yüklüyoruz, notes.ini dosyasını temizleyerek wizard'ı baştan başlatıyoruz.

**2.2.Yeni kullanıcı yarattık, kullanıcının client kurulumu sırasında ekran dondu ve ilerlemiyor.**

Kendi testlerim sırasında karşılaştığım bir sorun daha. Gene Lotus Domino 8.5 versiyonunda eğer ID dosyası yalnızca vault'da bulunuyorsa fakat ID download konusunda kısıtlama getirildiyse hiç bir hatayla karşılaşmıyorsunuz ama işlem de ilerlemiyor. Sorun 8.5.1 versiyonunda düzeltildi. Geçici çözüm olarak kullanıcıya ID download hakkı verip tekrar deneyebilirsiniz.

**2.3.Kullanıcı şifresini resetlediğimiz halde bilinmeyen bir sebeple ID dosyasını indiremiyor.**

Bir müşterimizde kullanıcının şifresini bir kaç kez yanlış girdiğini tespit ettik. ID Vault belirli bir sayıda yanlış şifreden sonra o kullanıcının bir günlük download haklarını kaldırır. Şifreyi tekrar resetlemek sorunu çözüyor.

Şimdilik bu kadar. İlerleyen zamanda eklemeler olacaktır umarım...
