---
authors:
  - serdar

title: "Lotus Notes'dan Exchange'e geçiyormuşuz..."

slug: lotus-notesdan-exchangee-geciyoruz-diyolar...

date: 2010-05-26T20:08:00+02:00

---

**Lotus Evangelist** olarak bildiğimiz **Keith Brooks** , geçenlerde güzel bir blog yazmıştı. "[A CIO asked about Exchange, so I told him the truth](http://lotustech.blogspot.com/2010/05/cio-asked-about-exchange-so-i-told-him.html)" başıklı yazısını kendisinin de izniyle blog'uma taşımak istiyorum.
<!-- more -->
Keith de bir çok Lotus iş ortağının yaşadığı '***Exchange'e geçiyoruz, neden mi? Öyle istediler!*** ' sohbetini anlatmış.

IT departmanlarının derinlemesine maliyet-fayda analizi yapmaktan çoğu zaman yoksun olduğu bilinen bir gerçek. Bunun temel sebebinin Türkiye'de IT yöneticiliğinin doğasından kaynaklandığını düşünüyorum. Bürokratik şirket yapılarımız (kemikleşmiş holding yapıları, örneğin), IT yönetimini mali işler kökenli çalışanlara emanet etmekte. Bu çalışanların finansal konulara yatkınlığı ve yaygın iş modalarına dirençli olması önemli bir avantaj oluştursa da üst yönetimle ilişkilerdeki yaklaşımları, teknoloji seçimindeki tutuculukları ve son kullanıcılarla kuramadıkları iç müşteri bağlantısı önemli sorunlara neden oluyor. Daha yenilikçi şirketler ise kariyer yönetiminde ülke standardını aşamayan bir çizgi izliyorlar. Nedense bir satış uzmanının satış pazarlama müdürü olma sürecinde MBA yapması, konusuyla ilgili rotasyonlara ve özel eğitimlere tabi tutulması son derece doğal karşılanırken bir IT şefinin IT müdürü, sonrasında direktörü olması sürecinde bu yol izlenmiyor. Interpro'ya danışmak lazım; **bilgi işlem departmanlarından sorumlu kaç üst düzey yönetici hem teknoloji hem de iş yönetimi (finans/organizasyon/insan kaynağı yönetimi) konusunda eğitimlidir** ?

Bir çok şirketi bu kapsamın dışında bırakıyorum. Görüşme yaptığım şirketlerde, küçük şirketlerde bile, eğitim eksikliklerine rağmen bu konuda kendisini epey geliştirmekte ve rasyonel yatırım stratejileri oluşturmakta olan yöneticiler görüyorum. Fakat tahmin bile edemeyeceğiniz şirketlerde yukarıdaki diyalogla karşılaşabiliyorum.

Dönelim bu Exchange hayranlığına. Türkiye'de (ve Avrupa'nın bir kısmında) IBM Lotus'un önemli bir sorununun son kullanıcıyı hedef alan bir halkla ilişkiler ve pazarlama operasyonu yürütmediğini daha önce de eleştirmiştim. Bununla ilgili Avrupa'dan gelen üst düzey IBM yöneticileriyle de zaman zaman tartışma olanağı buluyoruz. Kısa vadede IBM'den bu konuda bir gelişme beklemek hayaldir. Bu noktada eksik kalan noktaları biz iş ortaklarının doldurması gerekir. Satış konusunda daha agresif ve geniş çerçeveli hareket etmemiz gerekiyor. Bunun neden olmadığı/olamadığı ayrı bir konu.

Fakat bu eksiklik, son kullanıcıda **Lotus kakadır, Outlook iyidir diye bir algı** oluşmuş durumda. Son kullanıcıdaki bu imaj en küçük bir problemde '*eski şirketimde outlook kullanıyorduk, süperdi* ' dedikodularıyla üst düzey yönetime kadar geliyor. Kimse sormuyor '*Kaç kez PST dosyanız çöktü ve tüm mesajlarınız kaybettiniz?* ' diye...

Ayrıca birbiriyle karşılaştırılamayacak iki üründen bahsettiğimizi unutmamalıyız. Bildiğiniz gibi Microsoft Exchange bir **mesajlaşma ürünü** yken Lotus Notes/Domino bir '**groupware** ', hatta '**collaboration** ' ürünü. Lotus platformunda geliştirilecek uygulamaları Microsoft tabanlı platformlarda **geliştiremiyoruz** . Dikkat edin, geliştirmek pahalı, uzun süreli ya da zor demiyoruz. Sadece geliştiremiyoruz.

Microsoft platformlarında Lotus yazılımlarıyla örtüşen tekil ürünler var. Fakat, esnek ve (ilişkisel veritabanlarının aksine) yarı-yapılandırılmış (semi-structured), replikasyon mekanizmasına uygun şekilde optimize edilmiş, bağlantısız (offline) çalışmaya uygun ve hızlı geliştirme sunan bir veritabanı sistemi bu platformda bulunmuyor.

Exchange'e geçiş yapmayı planlarken bu uygulamaları da planlamak gerekiyor. Outlook kullanmaya başladıktan sonra uygulamaları yavaş yavaş geçireceğiz diyerek başarısız olan, şimdilerde **uygulamalar için Lotus Notes, mesajlaşma için Outlook** kullanan şirketler var. Bunu başaramayacağını anlayıp uygulamaları web platformuna taşıyan, bu yüzden hem Lotus Domino, hem de Exchange lisanslarına katlanan şirketler de biliyoruz. Bu geçişi planlarken antivirus yazılımından yedekleme yazılımına; faks sunucusundan uzak ofis bağlantılarına kadar bir dizi sorunu çözmeyi 'unutan'lar da olabiliyor.

Upgrade maliyetleri? Son durum nedir bilmiyorum iş hayatımda bir kaç kez Exchange versiyon geçişi gördüm. Bir dizi danışman, günlerce çalışıp domain'i, active directory'yi ve exchange sunucusunu peşpeşe yükseltip haftalar süren uzun ve maliyetli süreçlerden geçiyorlar. Biraz sarkastik olacak ama, benim sunucu upgrade'lerimin en uzunu 3 saat sürdü. Bu kadar uzamasının sebebi, müşterimin uzak lokasyona kurulum dosyalarını göndermeyi unutmasıydı :) 2.5 saat dosyaların indirilmesini bekledim, yedekleme de 20 dakika sürmüştür. Kalan uzun dakikalar boyunca sunucu versiyonunu yükselttik!

Sonuç olarak konuya Lotus iyidir, Exchange kötüdür gibi bakan bir yazı yazmış bulundum. Benim şahsi fikrim bu konuda taraflıdır. **Fakat eleştirilmesi gereken esas nokta IT yöneticilerinin bu konuda tavrıdır** . Aynı şeyi bir Microsoft Exchange hayranı Outlook kullanan bir şirketin Lotus Notes'a geçmek istemesi hakkında da yazabilir. '*Yönetim böyle istedi* ', '*kullanıcılar böyle talep ediyor*' gibi yaklaşımlar yönetim kademesinden bir alt seviyeye inmemelidir bile...
