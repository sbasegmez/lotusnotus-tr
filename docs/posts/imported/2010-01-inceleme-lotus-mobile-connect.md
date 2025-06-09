---
authors:
  - serdar

title: "İnceleme: Lotus Mobile Connect"

slug: inceleme-lotus-mobile-connect

date: 2010-01-25T09:15:13Z

---

Bugün zor şartlar altında karlı yollara çıktım. TEM'de giderken ön camımın buz tutması ve sileceklerimin iptal olmasına bir de yoldaki donmalar eklenince geri dönmem gerektiğine karar verdim. Kendimi ilk alışveriş merkezine attım ve sıcacık bir Starbucks bulup TTNet Wi-Fi üzerinden işlerimi yapmaya başladım.

İşte böyle zamanlarda [Telecommuting](http://en.wikipedia.org/wiki/Telecommuting) (evden çalışma, ofis dışından iş yapabilme) şansına sahip olmanın ne kadar güzel olduğunu farkediyorum. Bunları düşünürken küçük bir Lotus Mobile Connect incelemesi yapmanın iyi bir fikir olduğunu hissediyorum :)
<!-- more -->
Lotus Mobile Connect (LMC), IBM'in mobil VPN uygulaması. Daha önceleri Websphere Everyplace Connection Manager ismiyle anılan pahalı bir yazılımken bir kaç yıl önce Lotus ürün ailesine katıldı. Sadece istemci lisansları ise bu yıl başlayan yeni lisanslama modeliyle ücretsiz hale getirildi. Hemen belirtmek lazım; [bu haktan](http://www-01.ibm.com/software/lotus/notesanddomino/additionalswentitlements.html) "IBM Lotus Domino Enterprise Client Access License" lisansına sahip olan müşterilerimiz yararlanabilecek.

LMC öncelikle standart VPN uygulamalarının sahip olduğu özelliklerin dışında önemli bazı eklentiler sunuyor. '**Client-less access** ' sayesinde iNotes gibi web uygulamaları için tarayıcı-tabanlı giriş olanağı sunuyor. Ekstra firewall ayarları yapmadan NAT ve topoloji değişikliklerine izin veren yönetim yazılımı, **dinamik oturum ayarları** yla uzaktan konfigürasyon değişikliklerine de izin veriyor. Mobil istemcilerde **Symbian** ve **Windows Mobile** desteğinin yanısıra masaüstü platformlarda Windows ve MacOS desteği sunuyor. Benim için en favori özelliklerden birisi olan '**Seamless Roaming** ' sayesinde, örneğin, büyük bir dosya yüklerken WiFi bağlantınız kesildiğinde yükleme kesilmeden GPRS'e geçmenizi sağlıyor. İstemciler sunucuya normal HTTP portundan bile erişebiliyorlar. Bu sayede özellikle port kısıtı bulunan ağlarda bağlantı problemi yaşamıyoruz. LMC, **Lotus Traveler** ve **Lotus Sametime** gibi mobil ürünlerle entegre çalışıyor.

Bunların dışında şifreleme ve bağlantı özellikleri daha detaylı olarak bu [linkten](http://www-01.ibm.com/software/lotus/products/mobileconnect/features.html) ve bu [linkten](ftp://ftp.software.ibm.com/software/lotus/lotusweb/product/mobileconnect/datasheet.pdf) incelenebilir.

Daha önceki [](2010-01-lotus-notes-traveler-companion.md "lotus-notes-traveler-companion.htm")blogda anlattığım gibi, 2008 yılında LMC ve Traveler kullanarak gerçekleştirdiğimiz bir projeyle **IBM Lotus Yazılımları Yılın Projesi** ödülü kazanmıştık. Bu projede çalışanların Symbian ve Windows Mobile tabanlı cep telefonlarının mesaj ve takvim bilgilerine erişmesini sağlamıştık.

Traveler'ın alternatif ürünlere göre en önemli eksikliğinin kendi güvenlik altyapısının bulunmaması olduğunu yazmıştık. Normal şartlarda Traveler, güvenlik ve gizlilik yönünden SSL'e dayanmaktadır. Fakat SSL ne derece güvenli görünse de yerel ağınızı Internet'e açmanız anlamına geliyor. Bu riskin dışında bazı ihtiyaçlarımızı sadece bağlantı güvenliğiyle aşamıyoruz. Örneğin cihazını kaybeden bir kullanıcının sisteme tekrar bağlanmasını engellemeyi bu topolojide başaramıyorsunuz. Benzer şekilde kullanıcının şifresi kötü niyetli kişiler tarafından elde edilirse ruhumuz duymadan çok önemli risklerle karşı karşıya kalıyoruz. Oysa LMC ile kullanıcının sadece belli bir cihazdan bağlanmasını garanti altına alabiliyorsunuz.

Lotus Domino sistemiyle de iyi bir entegrasyon yeteneğine sahip olan LMC, bu sayede LTPA Token paylaşmaktan tek noktadan kullanıcı yönetimine kadar bir çok kolaylık sağlıyor. Robust yapısıyla VPN altyapısı olmayan küçük ve orta boyutlu tüm işletmelerde rahatlıkla kullanılabilecek bir yazılım.

Görüşmek üzere...
