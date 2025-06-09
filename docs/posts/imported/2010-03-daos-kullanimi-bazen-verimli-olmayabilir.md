---
authors:
  - serdar

title: "DAOS Kullanımı Bazen Verimli Olmayabilir"

slug: daos-kullanimi-bazen-verimli-olmayabilir

date: 2010-03-31T10:28:49+02:00

---

DAOS ile %30'lara varan yer kazancımız olacağını söyledik durduk. Fakat bazı özel durumlarda bu güzide özellik ciddi yer kayıplarına neden oluyor.

1 ay önce bir müşterimizde 6-7 sunucu için DAOS özelliğini açmış ve kullanmaya başlamıştık. Dün akşam ne kadar yer kazancımız olduğunu incelediğimizde sürpriz bir sonuçla karşılaştık.
<!-- more -->
Öncelikle standard bir mesajlaşma sunucusuna baktığımızda beklediğimiz değerlere rastladık. 137 kullanıcının mail meritabanlarının mantıksal büyüklüğü 36 GB, fiziksel büyüklükleri ise 15GB iken DAOS klasöründe 9 GB civarında ekli dosya vardı. Bu durumda toplam kazancın %33 civarında olduğunu görüyoruz ki bu da beklentimizi karşılıyor. Öte yandan hub sunucuda DAOS klasöründe 25GB civarında ekli dosya vardı. Yalnızca 20 kullanıcının yer aldığı sunucuda bu kadar büyük bir ekli dosya miktarı, toplamda %90 civarında artışa işaret ediyor.

Müşterimizin topolojisinde kullanılan hub sunucu, dışarıdan içeriye gelen mesajların giriş noktası. Internet üzerinden gelen tüm mesajlar güvenlik katmanından sonra bu sunucuya giriyor. Bu sunucuda mail.box veritabanları DAOS'a dahil edildiğinden dolayı gelen mesajların ekli dosyaları otomatikman DAOS'a alınıyor. Bu mesajlar dağıtıldıktan sonra siliniyorlar fakat 'Deferred deletion interval' olarak tanımlanan süre boyunca DAOS'da tutulmaya devam ediliyor. Bu süre çok uzun tutulduğunda verimsizlik de katlanarak artıyor.

Genel olarak yaptığımız DAOS uygulamalarında 'deferred deletion interval'a karar verirken müşterilerin yedekten geri dönme sıklığını ele alıyoruz. Bu süre, bildiğiniz gibi, işi biten ekli dosyaların ne kadar süre daha sistemde tutulacağını belirliyor. Bu süreyi çok uzun tuttuğunuzda yer kaybına, çok düşük tuttuğunuzda yedekten geri dönüşlerde zorlanmaya neden oluyorsunuz. Diyelim ki silinme süresini 30 gün yaptınız. Kullanıcı 40 gün önce sildiği bir mesaja ulaşmak istediğinde yalnızca veritabanını dönmek yetmiyor, hangi NLO dosyayı geri dönmeniz gerektiğini öğrenip binlerce NLO dosyadan o spesifik dosyayı bulmanız gerekiyor. Bu süreyi hesaplarken belirttiğimiz faktörlerin yanı sıra yedekleme sıklığınızı da göz önüne almanız gerekir.

Başka bir müşterimizde DAOS'u açmış fakat tüm mesaj kutularında aktive etmemiştik. Bu sunucuda da bir kaç mail veritabanı ve mesaj kutularından (mail.box) onlarca gigabyte'lık ekli dosya oluştuğunu gördük. Bu özel durumda tek bir mesajlaşma sunucusunda çok büyük miktarlarda mail veritabanı var. Eğer tüm mail veritabanlarında DAOS aktive edilmezse mail.box veritabanlarından kaynaklanan ekli dosya üretimi gereksiz bir NLO depolamasına neden olmaktadır.

Önerilere gelince;

* Genel topoloji pratiklerinde eğer dağıtık lokasyonlarınız varsa bir adet mesajlaşma noktası kullanmayı öneriyorum. Bu sunucuda mail veritabanı tutulmayacaksa DAOS aktivasyonuna da gerek yoktur. Mail veritabanı kullanacaksanız da mail.box veritabanında DAOS aktivasyonu kullanmayın. Gerçi DAOS ile ilgili IBM'in önerisi mutlaka mail.box'ların DAOS'a aktarılması yönünde. Aksi halde disk kullanımında belirgin bir artış yaşandığı söyleniyor ama mesajlaşma trafiğinin çok yüksek olduğu durumlarda ekstra bir disk kullanımı söz konusu oluyor.
* Eğer sunucunuzda DAOS'u açıyorsanız ve mail.box'larınızda DAOS'u aktive ettiyseniz, mail veritabanlarınızı mümkün olduğu kadar hızlı bir şekilde DAOS'a aktarın. Aksi halde mesajlaşma trafiğinden doğan önemli bir ekli dosya yükünü boş yere depolamış oluyorsunuz.
* 'Deferred deletion interval' süresini çok optimum kullanmak gerekiyor. Bu süre, eğer yedekten geri dönme oranınız düşükse 30 gün veya daha kısa tutulabilir
* DAOS'ta tasarruf edilen disk alanı iki faktör tarafından belirleniyor. Birincisi doküman yönetim sistemleri ve alışkanlıkları. Etkili bir doküman yönetim sistemi ya da dosya sunucusu kullanan şirketler mail veritabanlarında fazla ekli dosya kullanmıyor, dosyalarını mesajlarla transfer etmiyorlar. İkinci faktör ise kullanıcı sayısı. 10-15 kullanıcı için kazancınız %5-6'larda kalabilir ve bu kazanç DAOS'un getirdiği ek yönetim yüküne değmeyecektir. Fakat 500-1000 kullanıcı için %40-50'lere kadar disk alanı kazanmanız hiç de sürpriz olmaz.

<br />

Sizlerden de DAOS tecrubeleri beklediğimi hatırlatmama gerek yok sanırım :)
