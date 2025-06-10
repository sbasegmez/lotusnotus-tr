---
authors:
  - serdar

title: "Lotus Notes/Domino 8.5.3 geliyor... Hazır mısınız?"

slug: lotus-notesdomino-8.5.3-geliyor...-hazir-misiniz

date: 2011-09-28T12:01:41+02:00

---

Belki farkındasınızdır, blog'lar ve tweet'ler bu olaya kilitlendi. Önümüzdek salı (4 Ekim'de) Lotus Notes/Domino 8.5.3 versiyonuyla ilgili bir dizi yenilik duyurulacak.
<!-- more -->
Geçen sefer 8.5.2 için bloglardan derleme bir yazı yazmıştık, gene yapalım. Fakat başlamadan önce birkaç detay var:

Öncelikle yasal uyarılar: Bu yazdıklarım söz verilmiş veya garantilenmiş değiller, değişebilirler ve beta programındakilerin yazılarına dayanmaktadır falan filan :)

Ayrıca salı günü yalnızca yeni versiyon duyurulmayacak, daha fazlası var. Tüm lisanslama baştan yazıldı. Sadeleştirmelerle birlikte [express lisanslamadaki kısıtlamaların değiştirilmesi](http://www.edbrill.com/ebrill/edbrill.nsf/dx/domino-express-restrictions-in-853) gibi bazı değişiklikler de duyacağız.

IBM, Lotus topluluğunu dikkatle dinledi ve **önümüzdeki hafta yeni bir ürün duyurusu** yayınlayacak. Kısıtlı bir telekonferansa katıldım ve ürünle ilgili detayları öğrendim. Bunları paylaşamıyorum, fakat aklımızı biraz karıştıracak da olsa pazardaki önemli bir boşluk doluyor bu yeni ürünle \[fragmanlar burada bitiyor\] :)

Neyse, blogları özetlemeye başlayalım:

1. [Julian Buss](http://xpageswiki.com/web/youatnotes/wiki-xpages.nsf/dx/Whats_new_in_Domino_8.5.3) yeni XPages özelliklerini de içine alan geniş bir wiki yayınladı.

2. [Darren Duke](http://blog.darrenduke.net/darren/ddbz.nsf/dx/domino-and-notes-8.5.3-has-reached-code-drop-5-that-means-the-embago-is-over-so-what-is-new.htm), [Mary Beth Raven](http://www.notesdesignblog.com/NotesDesignBlog/NDBlog.nsf/dx/a-few-of-the-things-coming-in-notes-8.5.3.htm) ve [Marie Scott](http://crashtestchix.com/2011/08/04/good-news-new-8-5-3-imap-commandsfeatures/) genel yenilikleri özetliyor:

* Sunucudaki full-text indeksleri başka bir sürücüye taşıma
* Bilgisayara özel policy'ler
* 'Purge Interval' kontrollü replikasyon
* 'Re:' ve 'Fwd' önekleri konuya göre sıralandığında yoksayılacak.
* Yeni mesaj uyarısı değişti (slide-in alerts).
* Okunmayan mesajların renginde tam kontrol
* Birden fazla imza kullanabilme
* 'Recent Contacts' ile ilgili daha geniş kontroller
* Sametime embedded 8.5.1 ve Symphony 3.0 geliyor yeni istemciyle.
* Single-user kurulumunu Multi-user'a çeviren bir araç geliyor.
* Windows Vista ve Windows 7 destekleyen Smart Upgrade
* ID Vault Citrix XenApp ile de çalışıyor
* IMAP üzerinde yeni komutlar
* Mesajları sağ tuş menüsünden alıcıya veya konuya göre arayabilme

<br />

3. [Declan Lynch](http://www.qtzar.com/blogs/qtzar.nsf/Blog.xsp?entry=1wdacr5ugwf0g), [Eric Brooks](http://www.bleedyellow.com/blogs/erik/entry/8_5_3_app_dev_keeps_moving_forward?lang=en) ve [Niklas Heidloff](http://heidloff.net/home.nsf/dx/09272011023837AMNHE9T8.htm) Domino Designer 8.5.3 hakkında yeniliklerden bahsediyor:

* Source Control Enablement - Domino Designer'la SVN gibi sistemleri kullanabilirsiniz.
* Designer daha stabil ve çevik (!).
* Java elementi ile java class'larını doğrudan ekleme (daha önce package explorer kullanmak zorunda kalıyorduk.)
* Eclipse üzerinde yeni XPages perspektifi
* Javascript editöründe geliştirmeler.
* Design elementlerini listeleyen görüntülere 'Sign' tuşu eklendi.
* Info-box'ların otomatik fırlamasını kontrol edebiliyoruz.
* F2 tuşuyla design elementlerin isimlerini ve 'alias'larını değiştirebilme

<br />

4. [Darren Duke](http://blog.darrenduke.net/darren/ddbz.nsf/dx/domino-and-notes-8.5.3-has-reached-code-drop-5-that-means-the-embago-is-over-so-what-is-new.htm), [Niklas Heidloff](http://heidloff.net/home.nsf/dx/09272011023837AMNHE9T8.htm), [Eric Brooks](http://www.bleedyellow.com/blogs/erik/entry/8_5_3_app_dev_keeps_moving_forward?lang=en), [Julian Buss](http://www.juliusbuss.de/web/youatnotes/blog-jb.nsf/dx/huge-starting-time-improvement-for-xpages-applications-in-the-notes-8.5.3-client.htm), [David Marko](http://blog.tcl-digitrade.com/blogs/tcl-digitrade-blog.nsf/dx/14.07.2011111755DMACWS.htm), [John Jardin](http://jvjardin.wordpress.com/2011/09/12/notesdomino-8-5-3-launch-date-and-xpages-release-notes/) ve [Declan Lynch](http://www.qtzar.com/blogs/qtzar.nsf/Blog.xsp?entry=1wdacr5ugwf0g) (bir de [bu](http://www.qtzar.com/blogs/qtzar.nsf/Blog.xsp?entry=mfr6u1708ow0)) XPages geliştirmelerini özetlemiş:

* Full-text aramalarında sıralama yapabilme
* XPages kontrollerinde HTML5 özellikleri eklendi.
* XPages uygulamaları sunucu ve istemci tarafında önyükleme ile süratleniyor.
* JS ve CSS dosyaları sunucu düzeyinde birleştirilip sıkıştırılıyor
* Dojo 1.6.1 versiyonu geliyor.
* i18n desteği kolaylaşıyor
* Extension Library ve OSGI plugin'lerin yüklenmesi kolaylaşıyor.
* Bazı kontrollerin HTML tag üretmesi kısıtlanabiliyor (repeat, panel gibi)
* 'Disable' edilmiş kontrollerin yalnızca okuma modunda da gösterilebilmesi
* Kontroller için yeni Dojo özellik paneli ile Dojo parametrelerini daha kolay girebilmek
* 'Evaluate entire page on refresh' ile performans arttırımı.
* View'lar için de 'Show XPages instead' seçeneği
* fileDownload kontrolünde görsel değişiklikler ve silme fonksiyonu
* view.postScript() event'i sayesinde tarayıcı tarafında full/partial update'ler sonrası javascript fonksiyonu çalıştırma
* OneUI 2.1 versiyonu.
* Extension Library ile birlikte ilişkisel veritabanı erişimi
* (Bu arada, Extension Library 8.5.3 versiyonu için de derlendi)

<br />

5. [Ulrich Krause (Eknori diye de bilinir)](http://www.eknori.de/2011-06-11/lnt-8-5-3-new-widgets-for-android/) ve [Paul Mooney](http://www.pmooney.net/2011/06/lotus-traveler-8-5-3-approving-devices-to-access-data/) (bir de [bu](http://www.pmooney.net/2011/08/traveler-whats-coming-with-8-5-3/)) Traveler ile ilgili yenilikleri yazdı:

* Android üzerinde bir sürü geliştirme var:
* Mesajlar ve takvimler için yeni widget'lar.
* Çok satırlı signature desteği
* Takvimle ilgili geliştirmeler
* Takvimlerde 'Tap-to-Dial'
* Mesajlarla ilgili geliştirmeler
* Android 3.0 desteği
* Android kurulumunda geliştirmeler
* Name-lookup geliştirmeleri
* Toplantı sahibi için ek işlevler
* Android 3.0.x tablet menüleri
* Android için şifreli mesaj desteği
* Apple'larda Reply/Forward ikonları
* Apple'lar için hangi uygulamaların senkronizasyonuna izin verileceğinin belirlenmesi
* Yeni bağlanacak cihazların onaylanmasını sağlayacak güvenlik politikası
* Symbian\^3 desteği (cihaz şifreleme zorunluluğuyla birlikte)
* Lotus Traveler sunucusunda mail routing ayarı yapmaya gerek olmayacak
* Mobil cihazdan gönderilen toplantı uyarılarının göndereni düzeliyor
* Name-lookup, kullanıcının mail sunucusundan yapılacak
* Apple cihazlarda uzaktan silme fonksiyonu yalnızca Traveler verilerini silecek şekilde kullanılabiliyor
* Domino Mail-in database ve group adreslerine lookup yapılabilecek.


Daha fazlasını da görebiliriz, hatta kalın :)
