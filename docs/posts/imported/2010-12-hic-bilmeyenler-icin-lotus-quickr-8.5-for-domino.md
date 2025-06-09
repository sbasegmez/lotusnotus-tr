---
authors:
  - serdar

title: "Hiç bilmeyenler için Lotus Quickr 8.5 for Domino"

slug: hic-bilmeyenler-icin-lotus-quickr-8.5-for-domino

date: 2010-12-24T18:30:00+02:00

---

Konferans falan derken ihmal ettik blog yazmayı...

Bu aralar gündemimde Lotus Quickr 8.5 for Domino ve Sametime 8.5 var. Sametime'ı başka zaman yazarız ama Quickr için taze bilgilerimi aktarayım. Kullanıcı Grubu sitesini de buraya taşımayı düşünüyoruz. Sertifika sahibi de olduğuma göre soruları yanıtlamaya başlayabilirim sanırım :)
<!-- more -->
**Lotus Quickr nedir, ne işe yarar?**
Lotus Quickr, basit anlatımıyla, ekip birlikteliği için kullanılabilecek ortak bir arabirim sunmakta. Sosyal yazılım kategorisine girmek için dikey mekanizmalara (yorumlama, paylaşma vs.) sahip yapısıyla son derece kolay kullanılabilir ve öğrenilebilir bir uygulama. Ağırlık noktası doküman yönetimi olarak görülüyor ama daha geniş perspektifte içerik yönetimi diyebiliriz.

Quickr, bize 'Place' adında bir içerik havuzu sunuyor. Bir place, içeriklerin yerleştirilebileceği bir kutu aslında. İçerik, bir web sitesi bağlantısı, görev (task), takvim girdisi, doküman(lar), form verisi, liste veya HTML/zengin metinli içerik gibi biçimlerde olabiliyor. Place'ler, bu değişik tipte içerikleri gerektiği gibi görmemizi sağlıyor.

Quickr kullanarak bir ekibin tüm dokümanlarını yönetebilir, ortak bir takvim kullanabilir, forumlar yapılandırabilir, listeler oluşturabilir, basit onay zincirleri kurgulayabiliriz.

**Domino versiyonu nedir? Portal versiyonu nedir?**
Bu kısım en kafa karıştırıcı olanı.

Bildiğiniz gibi Lotus Quickr, Lotus Quickplace'in devamıydı. Fakat 8.0 versiyonu itibariyle hem Domino hem de Websphere Portal versiyonu çıktı. O dönemde, açıkçası, Domino versiyonunun kapatılacağını, yalnızca Portal versiyonunun kalacağını öngörüyorduk. Hatta bu öngörüye dayanarak Kullanıcı Grubu web sitesini Portal versiyonu üzerinde kurgulamıştık.

Zaman içerisinde beklentimizin aksine, Domino versiyonu Portal tarafından daha hızlı gelişti. 8.5 versiyonunda Portal arabirimi değiştirilerek klasik Quickplace'den gelen dikey navigasyona dönüştürüldü. Bu da aslında Domino versiyonunun zannettiğimiz gibi yetim kalmayacağını gösterdi bize.

Resmi öneri, hangi platformu biliyorsanız onu kullanın şeklinde. Fakat aralarında önemli farklar bulunuyor.

Öncelikle, doküman yönetim altyapısı tamamen farklı. Portal versiyonu, doküman yönetimi için Java tabanlı özel bir yapı kullanıyor. Kullanılan yapı Domino versiyonundan daha esnek aslında. Karmaşık metadatalar tanımlayabiliyoruz. Metadata tanımlama konusunda Domino 8.5 versiyonunda epey bir ilerleme olsa da Portal'in yetenekleri benim daha çok işime geliyor. Örneğin Domino tarafında standart bir Powerpoint dosyasını koyup 'hadi bakalım versiyonla' demek çok kolay değil. Buna 'explicit' versiyonlama deniyor. Yani dokümanı alıyorsunuz, mevcut halini eski versiyon olarak işaretleyip yeni versiyon oluşturuyorsunuz. Bunun tersi, 'implicit' versiyonlama ki, bunu Domino versiyonunda aktif hale getirmek için biraz takla atmak gerekiyor. Domino tarafında 'implicit' versiyonlamayı form'lar için kullanabiliyoruz. Formlar tanımlanmış metadatalara bilgi girmemizi sağlayan yapılar ([örnek video](http://www-10.lotus.com/ldd/lqwiki.nsf/xsp/.ibmmodres/domino/OpenAttachment/ldd/lqwiki.nsf/F1D9ECD5BB4BF4968525779D00727DBE/attach/QD%208.5%20-%20Creating%20Custom%20Forms.mp4)). Bu formlara ekli dosya(lar) dahil edebiliyoruz.

ECM (Enterprise Content Management) entegrasyonu 8.5 öncesi Domino versiyonlarında yoktu. Artık arkada Filenet kullanıyorsanız Domino versiyonundan ECM bağlantıları kurabilirsiniz. Bu yetenek, özellikle doküman yükü çok yüksek olan finans gibi sektörler için çok önemli. Çünkü Filenet'in arabirimi pek kullanıcı dostu değil. Quickr, bu tip büyük doküman yönetim sistemlerinin önyüzü olarak konumlandırılıyor.

İçerikler Domino versiyonunda NSF veritabanlarında tutuluyor. Bu önemli bir avantaj, çünkü DAOS kullanabiliyoruz ve replikasyon özelliğinden faydalanabiliyoruz. Bu noktada içerik yapılarının ne derece değiştirilebildiği (örneğin forum içeriğine bir kategori ekleyip onu da folder üzerinde gösterebilmek) benim için kapalı kutu. Bunun için geliştirilmiş bir sistem mevcut fakat henüz o kısma gelemedim.

Öte yanda Portal versiyonu içerikleri WCM üzerinde tutuyor. Eski, hantal ve karmaşık bir yapı da olsa, WCM sayesinde epey geliştirme yapabiliyorsunuz. Bunun için biraz JSP bilmeniz gerekiyor. Ben bir kaç deneme yapmıştım fakat çok karmaşık bir sistem olduğunu söylemem gerekiyor.

Portal versiyonunda 'teorik' olarak portlet kullanabiliyorsunuz. 'Teorik olarak' dememin nedeni kullanacağınız portletlerin lisans olarak uygun olması gerektiğinden. Standart bir Websphere Portal portleti alıp koymanız yasak (teknik olarak mümkün ama lisans olarak yanlış).

Bir de Domino tarafının 'offline' kullanım desteği sunuyor olmasını (8.5.1 itibariyle) ve placebot adında bir yapı (agent fonksiyonu gibi düşünülebilir) kullanabildiğinizi atlamayalım.

**Ücretsiz olan Quickr Entry?**
Artık Quickr Entry önermiyoruz. Bu ürün 8.2 versiyonunda takıldı. 8.5 versiyon itibariyle entry sürümü gelmiyor. Daha önce [](2010-11-iyi-haber-lotus-quickr-entry-tarih-oldu....md)bahsettiğim gibi, daha iyisi yolda... Bekliyoruz :)

Gene de öğrenmek isteyenler için bilgi verelim, Entry versiyonu kişisel 'place'ler yaratmanıza imkan veriyor. Kullanıcı kişisel alanına kişisel dosyalarını yüklüyor ve diğer kullanıcılara adres bilgisini gönderiyor ve bu dokümanları paylaşmış oluyor.

Burada paylaşılan dosyalarla ilgili kısıtlı bir güvenlik olduğunu hatırlatalım. Dosyalarınızı gizleyebiliyorsunuz, bu yolla yalnızca link adresini bilenlerin bu dosyalara erişmesini sağlıyorsunuz. Fakat link'i bir şekilde öğrenen başka kullanıcılar dosyayı indirebiliyor. Dolayısıyla bu imkan, kişisel bir doküman yönetimi değil, dosya sunucularındaki 'Genel' klasörlerinin yerini alabilecek bir uygulama.

**Peki Quickr Connector nedir?**
Quickr Connector, Quickr'da yarattığınız içeriklere ulaşabilmenizi sağlayan ek bir uygulama. Connector sayesinde dokümanlarınıza Windows Explorer, Lotus Notes, Lotus Symphony, Outlook, MS Office ve Lotus Sametime üzerinden erişebiliyorsunuz.

Connector, Quickr'ın olmazsa olmaz bir parçası. Örneğin MS Excel ile yarattığınız dokümanı doğrudan kullandığınız 'place'in kütüphanesine yerleştirebiliyorsunuz. Herhangi bir içeriğin eski versiyonlarına erişebiliyor, yeni versiyon yaratabiliyorsunuz. Lotus Notes ile aldığınız ve gönderdiğiniz dokümanları Quickr'a aktarıp büyük büyük dosyaları göndermek yerine onların bağlantı adreslerini paylaşabiliyorsunuz.

**Lotus Quickr 8.5 diye bir şey var?**
Lotus Quickr 8.5 for Domino, çok önemli yeniliklerle geldi. Bunların kısa bir özetini geçersek;

* Artık çoklu dil desteği tek sunucuda mümkün. Daha önce her sunucunun ayrı dili oluyordu. Hem Türkçe hem İngilizce kullanmak istiyorsanız iki ayrı sunucu kurmanız gerekiyordu.
* List fonksiyonu geldi. Müthiş yararlı bir özellik. Demosunu [buradan](http://www-10.lotus.com/ldd/lqwiki.nsf/xsp/.ibmmodres/domino/OpenAttachment/ldd/lqwiki.nsf/F1D9ECD5BB4BF4968525779D00727DBE/attach/QD%208.5%20-%20Lists.mp4) izleyebilirsiniz.
* 'What's New' sayfası geldi (RSS destekli). Bu sayede üç gün uğramadığınız bir 'place'de neler olmuş diye bakabilirsiniz.
* Lotus Quickr takvimi Lotus Notes takvimine eklenebiliyor.
* Yeni zengin metin düzenleyici (Rich Text Editor) adapte edildi. İçeriklerde Word ve Symphony metinlerini formatları bozulmadan yapıştırabilmenizi sağlıyor bu editor.
* Son kullanıcının ActiveX kullanmasına gerek kalmadı. Bu sayede platform desteği arttığı gibi activex yükleme derdi de ortadan kalkmış oldu.
* Yeni eklenen çöp kutusu sayesinde silinen içerikler geri getirilebiliyor.
* Klasör düzeyinde erişim kontrolü yapabiliyoruz.
* IBM FileNet ve IBM Content Manager için ECM desteği sunuluyor.
* Sunucu için SUSE Linux platformu destekleniyor.

<br />

**Nasıl deneyebilirim?**
En güzeli [Greenhouse](http://greenhouse.lotus.com/) sitesini kullanmak... Bu sitede Lotus portföyünde bulunan bir çok ürün ücretsiz olarak kullanıma sunuluyor. Buradan Lotus Quickr'ın hem portal, hem de domino versiyonlarını inceleyebilirsiniz. Kurmak çok zor değil ama Domino versiyonu için 4-5 saat, Portal versiyonu için 7-8 saatlik bir çalışma gerekiyor. Hazırı varken değmez bence...

**Evde denemek isteyenlerin en sık yaptığı hatalar:**

* Mutlaka LDAP kullanın. Bu sayede SSO, Sametime entegrasyonu gibi konularda sorun yaşamazsınız.
* Quickr'ı mutlaka ayrı bir sunucuya kurun. Hatta mümkünse farklı bir Notes domain kullanabilirsiniz. Bunun bir kaç nedeni var. Örneğin versiyon bağımlılığını düşünmek gerekiyor. Mevcut versiyon 8.5.1, Lotus Domino 8.5.2 ile kullanılamıyor. Web site ayarlarında kendi yaptığınız login form'larınızı kullanamıyorsunuz. UTF-8 kullanmak zorunlu. Zaten LDAP kullanacağınız için adres listesine (names.nsf) ihtiyaç duymayacaksınız. Domino kurulumu sırasında mevcut Certifier ID'nizi ve Admin ID'nizi kullanarak 'First Standalone Server' seçeneğini seçerseniz sertifikasyon sorunlarıyla da uğraşmazsınız.
* Bu 'Login Form' meselesi önemli. Sunucunuzda 'Multi-server SSO' kullanacaksınız. Bildiğiniz gibi bu ayarı yaptığınız zaman 'domcfg.nsf' isimli bir veritabanı oluşturup login için kullanılacak formu burada tanımlamanız lazım. Lotus Quickr, kullanılan kullanıcı dizininin haricinde tekil üye alabiliyor (yani LDAP'a kayıtlı olmayan ama yalnızca bir place'e erişim yetkisi olan kullanıcı). Bu üyelerin giriş yapabilmesi için ayrı bir login formu kullanılıyor.
* İlk yarattığınız Admin kullanıcısına dikkat etmek gerekiyor. Bu kullanıcının LDAP dizininde olmaması tavsiye ediliyor.
* Quickr'a yüklenecek dosyaların boyutu varsayılan olarak 10 MB ile sınırlandırılmış. Bunu arttırmak için iki farklı alanı değiştirmeniz gerekiyor. Birisi Quickr içinde, diğeri Domino sunucusunda. Buna dikkat etmenizi tavsiye ederim.
* Ölçek önemli bir seçim kriteri. Quick for Domino, yaklaşık olarak 800-900 kullanıcı için tasarlanmış. Bu kısıtlamanın sebebi, place kullanıcılarının veritabanlarındaki ACL kayıtlarında yeralıyor olması. ACL kayıtlarında da sınırlama var. Eğer 'Expanded Membership' adlı bir mekanizmayı aktif hale getirirseniz Quickr, dizin üzerinde otomatik yönetilen gruplar tanımlar. ACL'lere de doğrudan bu gruplar yerleştirilir. 'Expanded Membership', 4000 civarında kullanıcı desteklemenizi sağlasa da, belli noktalarda bazı [kısıtlamalar](http://www-10.lotus.com/ldd/lqwiki.nsf/dx/Expanded_membership_qd85) içerir.

<br />

<br />

Şimdilik bu kadar. Quickr 8.5 itibariyle ürün dokümantasyonunun Infocenter'dan [wiki tarafına taşındığı](http://www-10.lotus.com/ldd/lqwiki.nsf/xpViewCategories.xsp?lookupName=Lotus%20Quickr%208.5%20for%20Domino%20documentation) bilgisini de verelim. Bir kaç [video linkini](http://www-10.lotus.com/ldd/lqwiki.nsf/dx/Quickr_8.5_Videos) de paylaşalım ve diğer soruları alalım :)))
