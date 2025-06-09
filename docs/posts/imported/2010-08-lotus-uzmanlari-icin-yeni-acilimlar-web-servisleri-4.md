---
authors:
  - serdar

title: "Lotus Uzmanları için yeni açılımlar: Web Servisleri (4)"

slug: lotus-uzmanlari-icin-yeni-acilimlar-web-servisleri-4

date: 2010-08-23T16:03:36+02:00

---

Aslında yanlış başlık kullandığımın farkındayım... "Web Servisleri" Lotus Domino için yeni bir özellik değil. Fakat Lotus uzmanlarıyla yaptığım konuşmalarda bu özelliğin yeterince kullanılmadığını görüyorum.
<!-- more -->

#### Nedir? Ne işe yarar?

<br />

"Web Servisleri", HTTP protokolü üzerinde çalışan bir kaç teknoloji ve protokolün oluşturduğu bir uygulama arabirimi mimarisini tanımlar. 10 yıldan fazla bir süredir kullanılmaktadır. W3C, web servislerini "*bilgisayarlar arasında ağ üzerinden etkileşimi ve uyumluluğu sağlayacak yazılım sistemi* " olarak tanımlar. Wikipedia makalesinde [daha fazla detay](http://en.wikipedia.org/wiki/Web_service) bulabilirsiniz. Fakat temel felsefe: "**proseslerimizi dağıtık uygulama mimarisinde 'servisler' halinde 'tanımlamak' ve 'kullanıma açmak'** " olarak özetleyebiliriz. (Kötü bir çeviri oldu...)

Milattan önce, uygulama geliştiriciler dış sistemlerde işlem yapmak istediklerinde ya da veri paylaşmaları gerektiğinde 'diğer' uygulama geliştiricileri arar ve temel kurallar üzerinde anlaşmaya çalışırlardı. Danışmanlar bu metodolojiye afilli bir isim bulmakta gecikmedi: "**Electronic Data Interchange** '. EDI, özellikle lojistik sektöründe çok popüler olmasına rağmen müzakerelerde ve değişim yönetimi konusunda bir takım sorunlar yaratıyordu.

![Image:Lotus Uzmanları için yeni açılımlar: Web Servisleri (4)](../../images/imported/lotus-uzmanlari-icin-yeni-acilimlar-web-servisleri-4-M2.png)

2000'lerin başında IBM ve Microsoft bir standardizasyon olanağı gördüler ve (Ariba adlı bir şirketle birlikte) WSDL (Web Services Definition Language) tanımlarının ilk versiyonunu oluşturdular. Bu aşama uygulama geliştirme dünyasında önemli bir açılım yarattı. Sonraki hikayeyi biliyorsunuz: IBM J2EE ile 'çok platform, tek dil' felsefesini benimserken Microsoft 'her dile açığız ama yalnızca Windows severiz' mottosuyla .Net platformunu geliştirdi.

Web servisleri, klasik mimarileri Remote Procedure Call (RPC) metodolojisine dayanmasına rağmen, zaman içerisinde kurumsal sistemlerde Service-Oriented Architecture (SOA) yönüne, Web 2.0 ile de REST mimarilerine doğru evrim geçirdi.

#### Neden?

<br />

Tekrarlamak gerekirse, temel felsefemiz prosesleri değişik uygulamalara dağıtmak. Bir satınalma uygulaması tasarlıyorsak organizasyon yapısına, onay/iş akışı motoruna, depo ve stok yazılımına veya faturalama sistemine dokunmak zorunda kalırız. Tüm bu fonksiyonlar tek bir uygulamada bütünleştirilemeyeceği için gereken servisleri uzman yazılımlardan 'kiralamamız' gerekir.

Tabi bizler ERP uygulaması geliştirmediğimiz için, Domino uygulamalarında neden web servisi kullanmalıyız sorusunu sormalıyız.

Basit bir masraf-onay iş akışı uygulaması tasarladığımızı farzedelim. En basit haliyle düşünürsek, bir view yapıp tüm çalışanları ve onların yöneticilerini koyduk. Masraf kategorilerini de başka bir görüntüye alalım (burada kategoriler masrafın ilişkilendirildiği proje/müşteri/vs. olabilir). Kullanıcı bir doküman yaratıp masraflarını listeler, yöneticisine gönderir. Onay sonrası muhasebeci bu kayıtları muhasebe sistemine dahil eder (personele para göndermek ve proje/müşteri maliyetlerini kayıt altına almak için). Şirketimizin personel bilgilerini SAP HR modülünde tuttuğunu, muhasebe için de kendi geliştirdiği bir .net uygulaması kullandığını varsayıyoruz.

İlk problemimiz, personel listesini almak olacaktır. İK müdürünüze, yaptıkları her tür personel operasyonunu başka bir veritabanına da işlemesi gerektiğini söylemeyi deneyin. Bu mümkün olmayacağından dolayı SAP HR modülüne entegre olmamız gerekiyor. Burada bir kaç alternatifimiz var. SAP ekibinden periyodik bir txt dosya isteyebilir, karmaşık bir SQL kodu alabilir veya bir RPC talep edebiliriz. Hangi metodu kullanırsanız kullanın; gerçek zamanlı veriye ulaşamıyor olacağız ve her iki taraf da epey bir zaman harcayacaktır.

İkinci problem onaylanmış masrafların karşı sisteme gönderilmesi. Veri okumak kolay iş; ama yazmak o kadar kolay olmayacaktır. Bir çok uygulama basit 'insert' operasyonlarıyla yürümez ne yazık ki. Her yeni veri bazı kontrollerden geçer, bir kaç tabloya yazılır ve bir kaç tabloyu da günceller (Logo, Netsis gibi uygulamaları kullananlar iyi bilirler). Dolayısıyla muhasebe uygulamasını geliştiren ekipten ricacı olacağız bu konuda. Gene bir kaç alternatifimiz var: txt dosya gönderebiliriz, 'stored procedure' tasarlatabiliriz, vs. Gene operasyonumuzun gerçek zamanlı olacağı şüphelidir. Bunun en büyük sakıncası, herhangi bir sorun çıktığında bizim uygulamamızın cehaleti olacaktır.

Her koşulda, bu iki sorunu aşabiliriz ve 'operasyonları farklı uygulamalara dağıtmış' olabiliriz. Dolayısıyla soruyu bir daha soracağız. Neden Web Servisleri?

Farzedelim ki biz ya da karşı sistem platform değiştirmeye karar verdi. Mesela .net uygulaması Oracle veritabanına geçti. Ya da bu sistemlerden birisi linux işletim sistemi kullanmaya karar verdi. Bu bizim için bol bol toplantı yapmak anlamına geliyor. Artık karşı sistemin 'değişim yönetimi' takımının değerli bir üyesi haline geldiniz.

Entegrasyon gerçek zamanlı olmayacağı için özellikle bordro geceleri muhasebe departmanı tarafından sıklıkla aranacak ve bir takım agent'ların çalıştırılması için nazik talepler alacaksınız.

Denetim konularından dolayı dijital imzalı bir PDF dosyanın bir yerlere eklenmesi gerektiğinde txt dosyalarla BLOB veri transfer edilemeyeceğini farkedeceğiz. Txt dosyalar validasyondan geçirilemeyeceğinden diğer geliştirici tarafından 'şu data eksik bu data yanlış' gibi sebeplerle sıklıkla aranacaksınız. Oysa web servisi kullanıyor olsaydık gönderdiğimiz XML'lerin 'düzgün' olduğu garanti altına alınacaktı.

En önemli avantaj ise topolojik konularda yaşanacaktır. Dağıtık bir ağ yapınız varsa, hele entegrasyon noktalarının bir kısmı yerel ağınızın dışındaysa, dosya paylaşımı veya veritabanı bağlantılarını güvenlik altına almak HTTP bağlantılarına göre çok daha zor olacaktır.

Tekrar kullanılabilme de web servislerinin arkasında duran önemli motivasyonlardan birisi. Bazen büyük şirketler farklı platformlara dağıtılmış yüzün üzerinde sistem kullanır. Çoğu zaman uygulama geliştiriciler için platform seçme şansı bulunmaz. Muhasebe veritabanınızın sizden başka onlarca uygulamayla aynı amaçla konuşması gerekiyor olabilir. Bu durum uygulama geliştiricide standardizasyon yaklaşımını hakim kılacaktır. İş/süreç mantığına uygun standart bir web servisi tasarlanır ve tüm entegrasyon noktalarının buna uyması beklenir.

#### Nerede kullanmalı?

<br />

Gerçek hayattan bir kaç örnek verelim:

* Bir müşteri için 'Web servisi' tasarlandı. Bu web servisi, müşterinin PHP tabanlı web sitelerinde oluşturulan form bilgilerini güvenli bir kanaldan Domino uygulamasına dahil ediyor, buradan da manual/otomatik işlem için yönlendiriyor.
* "[bestcoder.net](http://www.bestcoder.net/)" blogunun sahibi Ferhat Bulut, web servislerini Blackberry uygulamalarını Domino veritabanlarına entegre etmek için kullanıyor.
* Bir müşterimiz bir self-servis uygulaması tasarlayarak ID Vault kullanarak kullanıcıların kendi şifrelerini sıfırlamalarını sağlıyor. Bu uygulama başka bir .Net uygulamasının web servisini kullanarak oluşturulan rastgele şifreyi kullanıcıya SMS atarak bildiriyor.
* Başka bir müşterimiz SAP HR modülünden personel listesi ve hiyerarşi bilgisini web servisi ile alıyor ve bunları Lotus Workflow organizasyon veritabanına transfer ediyor.
* Başka bir müşteri otel yönetim sistemini domino tabanlı CRM uygulamasına bağlıyor. Otel yönetim uygulaması müşterinin indirim seviyesini uzak sistemden web servisi kanalıyla sorguluyor.

#### Nereden başlamalı?

<br />

Tam kaynağını belirleyemedim ama şu söz çok hoşuma gidiyor: "***Web servisleri lisede seks yapmak gibidir. Herkes bunun hakkında konuşur ama neredeyse hiç kimse, yaptığını iddia edenler bile, nasıl yapılacağını bilmezler*** ". Object-Orientation gibi web servislerini tanımlamak da çok kolay olmaz. Basitten başlar, hata yapa yapa kendi pratiğinizi oluşturursunuz.

Domino üzerinde web servis hizmeti yaratmak ya da başka bir web servisini kullanmak çok kolaydır. Aşağıdaki linklerde başlangıç için güzel kaynaklar var.

* [Lotusphere 2004 : JMP103 - Introduction To Web Services](http://www-10.lotus.com/ldd/sandbox.nsf/ecc552f1ab6e46e4852568a90055c4cd/5171a849ce49f47e85256e2f0055ceca?OpenDocument)
* [Lotusphere 2007: AD509 - Using Web Services Features in IBM Lotus Notes and Domino](http://www-10.lotus.com/ldd/sandbox.nsf/ecc552f1ab6e46e4852568a90055c4cd/7cc00980257e905485257291004c24bb?OpenDocument)
* [Practical Web Services in IBM Lotus Domino 7: What are Web services and why are they important?](http://www.ibm.com/developerworks/lotus/library/web-services1/index.html)
* [Practical Web services in IBM Lotus Domino 7: Writing and testing simple Web services](http://www.ibm.com/developerworks/lotus/library/web-services2/index.html)
* [Practical Web services in IBM Lotus Domino 7: Writing complex Web services](http://www.ibm.com/developerworks/lotus/library/web-services3/index.html)
* [Web Services - What's new? (in 8.5)](http://www-10.lotus.com/ldd/ddwiki.nsf/dx/web-services-whats-new.htm)

<br />

*(Lotus Domino 7 ile 8.x arasında küçük değişiklikler var. Örneğin 7'de doğal yöntemlerle web servisi kullanamıyorduk (consuming). Bu yüzden bazı örnekler Java ve ActiveX uygulamalarına yer veriyorlar, dikkate almayın.)*

Şu aralar bir müşteri için bir kaç entegrasyon noktası için web servisi kullanacak bir uygulama üzerinde çalışıyorum. Bittiğinde örnek uygulama olarak paylaşmayı planlıyorum (ya da umut ediyorum)...
