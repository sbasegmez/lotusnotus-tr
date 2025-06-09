---
authors:
  - serdar

title: "Lotus uzmanları için yeni açılımlar: Bilgi Güvenliği (3)"

slug: lotus-uzmanlari-icin-yeni-acilimlar-bilgi-guvenligi-3

date: 2010-06-27T12:33:47+02:00

---

Sabah gazetesinin [haberi](http://www.sabah.com.tr/Gundem/2010/06/27/tapuda_ulusal_guvenlik_skandali), İstanbul iline ait tapu bilgilerinin bulunduğu TSM uygulamasına ait veritabanlarının çalındığını ve çeşitli emlakçılara pazarlandığını iddia ediyor. Haber başka kaynaklara sıçramadığından detayları ve doğruluğu konusunda çok emin olamıyoruz. Ama haberi okuduğumda uygulama geliştiricilerin önemli bir problemi aklıma geldi: **Bilgi güvenliği** .
<!-- more -->
Bizim sektörümüz uygulama geliştirme konusunda bir hayli 'alaylı' ve 'teoriden uzak' çalışan bir sektör. Bu durum dolaylı olarak gözü kapalı ve çeşitli ezberlere dayalı pragmatik bir uygulama modeli oluşturuyor her sektörde. Bu uygulama modeli, bilginin sürecin önüne geçtiği uygulamalarda '**erişim güvenliği** 'nin ön planda olduğu bir güvenlik modelini tercih ediyor.

Erişim güvenliği, hangi bilgiye kimin erişeceğini tanımlayan yapısal bir tasarım. Lotus dünyamızdan örnek verirsek, çok katmanlı bir güvenlik yapımız olduğunu hatırlayalım. Öncelikli olarak ID tabanlı bir '**erişim kontrolü** ' (authentication) sistemi kullanıyoruz. Daha sonra veritabanlarımızda ACL ile kişi ve grupların ne yapabileceklerine karar veriyoruz. Bu kişiler yeni kayıt yaratabilsin, bunlar silebilsin gibi... Bir alt katmanda doküman bazında 'Reader' ve 'Author' alanlarıyla daha mikro kontroller yapıyor, alan bazında şifreleme kullanarak belirli bir dokümanın alanlarını 'kişilere özel' kılabiliyoruz.

Bir örnek verirsek, üye takip uygulamasına sahip olduğumuzu düşünelim. Müşteri bilgileri bizim için önemli. Bu veritabanına her çalışanın erişebilmesini istemeyiz. Satış ekibimiz, müşteri temsilcilerimiz, muhasebe çalışanlarımız bu kayıtlara erişebilsin yeterli (ACL). Fakat belirli bir müşterinin kaydına, potansiyel bir üye ise yalnızca satış ekibi tarafından, aksi halde ilgili müşteri temsilcisi ve muhasebe çalışanı tarafından erişilebilsin isteriz (Reader/Author alanları). Müşteri temsilcisinin kredi kartı numarasını görmesine gerek yoktur. Dolayısıyla bu alanı (field encryption ile) yalnızca muhasebe çalışanı görebilsin istiyoruz. Buraya kadar iyi bir 'erişim kontrolü' sistemi kurduk.

'Bilgi güvenliği', erişim kontrolünü de içine alan kapsamlı bir yapı. Müşteri temsilcisinin kredi kartı alanını görmemesi bu kapsamda değerlendirilebilir. Fakat bir adım ötesini de düşünmek gerekiyor. Muhasebe çalışanının kredi kartı bilgisini görebilme yetkisi bu kişinin fonksiyonel ihtiyacından (tahsilat yapma) kaynaklanır. Fakat kötü niyetli bir çalışanın, görme yetkisine sahip olduğu bilgiyi kötü amaçla kullanma ihtmalini ortadan kaldırmak gerekir. Bu örnekte kredi kartı bilgilerinin şifrelenmesi ve tahsilatın yazılım tabanlı POS sistemleriyle yapılması çözüm olarak önerilir. Bu sistem büyük alışveriş siteleri tarafından tercih edilen bir methodoloji. Kredi kartı numaraları, banka tarafından oluşturulan bir şifreleme anahtarı ile şifrelenerek depolanır ve tahsilatlar şifreli kart numaralarıyla bankaya transfer edilir. Banka haricinde kimse bu bilgilere erişemez.

Bu konuda temel prensip, görmeye izin veriyorsanız çalınmasına da imkan verirsiniz olarak algılanıyor. Biliyoriz ki bütün bilgiler şifrelenemez ve fonksiyon sahiplerinden gizlenemez. Örneğin kötü niyetli bir satış yetkilisi rakip firmaya giderken sahip olduğunuz tüm potansiyel müşteri kayıtlarını taşıyabilir. Bu noktada düşünülmesi gereken bir kaç bilgi güvenliği önlemi daha var.

Öncelikle en büyük kaçak noktası 'toplu miktarda bilgi transferi'dir. Eğer uygulamanız tüm müşterilerin iletişim bilgilerini Excel'e transfer etme olanağı veriyorsa ciddi bir probleminiz var demektir. Bu tip açıkları engellemenin bir kaç pratik noktası vardır. Örneğin Notes üzerinde uygulama açılırken notes.ini'deki tüm 'Export' parametrelerini kaldırmak pratik bir önlem içerir. Gereken bilgileri görüntüler üzerine yerleştirmemek bir başka yöntem olabilir. Eğer çok ciddi bir önleme ihtiyaç duyuyorsanız, (işinizi biraz kompleks hale getirir ama) iletişim bilgilerini başka kayıtlarda saklarsınız. XPages gibi teknolojilerde bu güvenlik açıklarının sayısının epey azaldığını düşünüyorum.

İkinci bir yöntem izlemenin (monitoring) etkin kullanılması. Bir kullanıcı, yaptığı işin gerektirmediği düzeyde bir aktivite gerçekleştiriyorsa, örneğin günde 15-20 müşteri temasında bulunan bir müşteri temsilcisi o gün içinde 500 kişinin kaydına ulaştıysa bir terslik vardır ve alarmlar çalmalıdır. Doğrusu bu teknoloji ilişkisel veritabanlarında daha aktif olarak kullanılmaktadır. Ama Lotus üzerinde bu tipte eklentiler olduğunu biliyorum.

Bu anlattıklarımız uygulama düzeyinde. İşin bir de uygulama dışında boyutları var.

Bazı danışmanlık şirketlerinde analiz raporları binlerce dolar karşılığı satılmaktadır. Denetim firmalarında üretilen dokümanlar, müşterinin çok üst düzeyde gizli verilerini içerirler. Bu bilgilerin şirket dışına çıkarılmaları ölümcül sonuçlar doğurabilir. Bilgi güvenliği üzerine çalışan uygulamalar, önemli verileri içeren dokümanları özel içerik kontrolünden geçirerek giriş çıkışları kontrol altına alırlar. Websense'in ürün tanıtım [video](http://connect.websense.com/mbh)'su bu konuda çok güzel bir örnek. Bu tip ürünlerle önemli dokümanlar özel yöntemlerle indeksleniyor; isim değişikliği, kopyala yapıştır veya yazdırma gibi yöntemlerle bile şirket dışına çıkarılamıyor.

Disket sürücülerin kaldırılması veya usb'lerin devre dışı bırakılması çok eskide kaldı. Bilgi güvenliği, kurumsal bilgi sistemlerinde önemli bir başlık altında yeralıyor artık. Telekom şirketleri, finans kuruluşları, denetim firmaları gibi bir çok kurum, bilgi güvenliğini de ön plana koyan bir dizi uygunluk (compliance) kurallarına adapte olmak zorundalar. Dolayısıyla bu başlık, kurumsal bilgi sisteminin önemli bileşenlerinden biri haline gelen Lotus uygulamalarının da hayati yanlarından birini oluşturacak.
