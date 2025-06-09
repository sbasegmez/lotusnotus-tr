---
authors:
  - serdar

title: "XPages'e geçiş ve 'yetersizlikler' üzerinden geliştirme yapmak..."

slug: xpagese-gecis-ve-yetersizlikler-uzerinden-gelistirme-yapmak...

date: 2012-03-28T08:50:14+02:00

---

Bu yazımı biraz gecikmeli de olsa Türkçe'ye çeviriyorum.

Geçen hafta yirmi kişinin katılımıyla Kullanıcı Grubu'nun ilk XPages Workshop'ını düzenledik. XPages'in genel özelliklerinin yanısıra geleneksel Notes uygulama geliştirmeden gelenlere yönelik bir sunum oldu.

Bir cümleyi daha fazla duymaya başlıyorum:
<!-- more -->
"***XPages'de çok basit şeyleri bile yapamıyorum. Bu yüzden XPages'e geçmeyeceğim!*** "

Geleneksel Notes/Domino geliştiricilerinin XPages'e geçişlerinde başarısız olduklarını çok gördüm. Fakat bu "***XPages patlak*** " edebiyatının bu olaydaki rolü diğer sebeplere yaklaşamıyor bile...

Notes client platformunda uygulama geliştirmeyi çok seviyorum. Çok sağlam uygulamalar geliştirebiliyor ve bunu çok hızlı yapabiliyoruz. Bazı tipte uygulamalar bu platformda diğer platformlara göre %90 daha hızlı geliştirilebilir. Fakat bir gerçekle de yüzleşmemiz gerekiyor: Notes paradigması aslında çok basit şeyleri yapmamıza izin vermiyor. Birkaç örnek vermeye çalışacağım:

Bir doküman yaratmak için form tasarlıyoruz. Dokümanın başka dokümanlarla 1-N ilişkisi var. Örneğin bir satınalma dokümanı ve buna UniversalID ile bağlı 'malzeme/servis' dokümanları olduğunu düşünün. Çok klasik bir örnek değil mi?

Şimdi, bir formun yalnızca bir dokümanla ilişkilendirilebileceğini biliyoruz. Bazı yan yollarla aynı form içerisinde birden fazla doküman yaratabilsek de geliştirme sürecimizi karmaşıklaştırmamak adına genelde formun içerisine bir 'embedded view' yerleştirir ve bir subform'u 'dialog' yardımıyla göstererek ikincil dokümanları yaratır/düzenleriz.

XPages geçişi sırasında birçok geliştirici bu işi Notes'da yaptıkları gibi yapmaya çalışır. Bu 'pattern'i XPages'de (veya herhangi bir web uygulamasında) gerçekleştirmek zordur. Bu yüzden geliştiriciler XPages'in 'çok basit birşeyi bile' ne kadar zor yaptığından bahseder.

Problemin temeline inersek, aslında XPages'te kurgulamaya çalıştığımız (dolayısıyla daha önce Notes'da kurguluyor olduğumuz) bu modelin **yanlış** olduğunu görürüz. Bu kötü alışkanlık, Notes istemcisinin 'aynı form içerisinde iki doküman kullanamaması' yetersizliğinden kaynaklanmıştır. Fakat bu tip yan yolları o kadar uzun zamandır kullanıyoruz ki bize doğrusu buymuş gibi gelmeye başlıyor.

Öte yandan XPages, aynı sayfada istediğimiz kadar veri kaynağına (doküman, view...) erişmemize izin veriyor. Dolayısıyla bu söylediğimizi XPages'de geliştirmemizi sağlayacak çok daha pratik yollar var.

Başka bir örnek, geçen hafta StackOverflow üzerinden sorulan bir [soru](http://stackoverflow.com/questions/9744113/xpages-create-new-copy-of-saved-document-and-open-it-without-saving-it). Aslı biraz daha karmaşık olsa da temel problemi anlatalım. Bir görüntünüz var, buradan bir doküman seçiyor ve bir button'a bastığınızda bu dokümanın yeni bir kopyasının ya da revizyonunun oluşmasını istiyorsunuz. Notes için basit; lotusscript'de yeni bir doküman yaratın, orijinal dokümandaki alanları transfer edin ve UIWorkspace ile yeni dokümanı açın. Bu yolla yeni doküman kaydedilmeden açılacak ve kullanıcının vazgeçme şansı da olacaktır.

Fakat XPages üzerinde bunu kurgulayamazsınız. Herhangi bir XPage, 'in-memory' bir dokümanı kendi 'context'inde yaratabilir, ama kaydedilmemiş bir dokümanı açamazsınız. XPages bu kadar 'basit' birşeyi yapamadığına göre yetersiz olmalı değil mi? :)

Aslında Notes istemcisinde kurguladığımız bu sahne, çok temel bir yetersizlikten kaynaklanıyor. Formlar normalde parametre alamazlar. Örneğin "CopyFrom=UNID" şeklinde bir parametre alabilseydik ve formun event'lerinde gereken hazırlıkları (veri kopyalama vs.) yapabilseydik çok daha iyi olmaz mıydı? Böylece 'yeni doküman yaratma' ile ilgili tüm kodlarımız tek bir yerde olacaktı. Daha temiz ve şık bir programlama pratiği...

Hey! Biz bunu XPages'de yapabiliriz! Herhangi bir XPage arkaplandan ya da açıktan parametre alabilir ve bundan daha iyisi event'ler veri kaynağı bazında tanımlanabilir (Notes'un başka bir sorunu. Event'ler Notes'da form bazında tanımlanır, doküman bazında değil).

Son bir örnek... Bu daha çok MVC (Model-View-Controller) pattern'iyle ilgili. Notes istemci paradigmasında MVC uygulamak, yani model, view ve controller seviyelerini farklı katmanlar olarak kurgulamak çok zordur. Bunu daha doğru ifade etmek gerekirse, Notes üzerinde MVC uygulamamak çok daha kolaydır :)

Bir iş akışı uygulamanız var ve formun içinde de bir 'Onayla' tuşu. Kullanıcı bu tuşa bastığında ondan bir açıklama alıyor, bir sonraki aşamada ne yapılacağını öğreniyor (bir sonraki onay veya formu sahibine gönder gibi), bir e-mail atıyor ve dokümanın statüsünü değiştiriyoruz. Basit değil mi? Birkaç formula yazarsınız o kadar!

XPages'de durum biraz farklı. Çünkü server-side JavaScript formüllerinde içinde bulunduğunuz 'context'i terkedemezsiniz. Oysa seçeneklerinizin neler olduğuna bakmanız, kullanıcıyla etkileşime girmeniz ve iş akışıyla ilgili birkaç işlem yapmanız gerekecektir. Yani sunucu tarafına, istemci tarafına ve tekrar sunucu tarafına gitmeniz gerekecek. Bu da XPages'de çok zor olduğuna göre XPages yetersizdir değil mi?

Tamamen yanlış!

Verinizle ne işlem yaptığınız, 'context'inizi nasıl kontrol ettiğiniz ve kullanıcıyla nasıl etkileşime girdiğiniz tamamen ayrı katmanlarda düşünülmesi gereken konular. 'Onayla' tuşunun yapması gereken tek birşey var, kullanıcıyla etkileşime girmek ve iş akışının devamı için gereken bilgiyi almak. Dokümanda değişiklik yapmak ve e-mail atmak bambaşka hikayeler. XPages'de veri kaynağı bazında 'event' tanımlayabildiğinizden bahsetmiş miydik?

Dolayısıyla yapmanız gereken şu: Kullanıcıya ne yapılması gerektiğini sorun. Aldığınız cevabı diğer 'context'e aktarın (scope değişkenleri, event parametreleri, veri kaynağı, vs) ve bir sonraki işlemin gerçekleştirilmesini tetikleyin (örneğin veri kaynağını kaydedin). Gerisi veri kaynağı içerisinde ele alınmalıdır. Bu paradigma çok daha doğru bir programlama yaklaşımıdır.

**Sonuç**

XPages geçişi bir paradigma değişimidir. Biz Notes istemci programlama modeline ve onun yetersizliklerine o kadar alışmışız ki orada yarattığımız 'çöpü' XPages uygulamalarına taşımaya çok hevesliyiz. Oysa paradigma değişimi uygulama deneyimini sıfırdan planlamamızı gerektiriyor. Böylece web uygulama modeline deha uyumlu uygulamalar tasarlayabiliriz.

Business Logic'imizi veya veri modelimizi koruyabilir, tekrar kullanabiliriz. Formlarımız ve alanlarımız değişmiyor, Lotusscript kodumuz Notes agent'ları içine aktarılabilir ve formula'larımız belli oranda SSJS formatına çevirilebilir. Fakat uygulama deneyimini tekrar kullanamayız...
