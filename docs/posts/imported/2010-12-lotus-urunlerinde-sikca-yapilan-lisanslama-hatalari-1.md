---
authors:
  - serdar

title: "Lotus ürünlerinde sıkça yapılan Lisanslama hataları (1)"

slug: lotus-urunlerinde-sikca-yapilan-lisanslama-hatalari-1

date: 2010-12-12T19:39:31+02:00

---

Haftasonu [Sapanca](http://maps.google.com/maps?f=q&source=s_q&hl=tr&geocode=&q=Sapanca,+T%C3%BCrkiye&sll=40.688969,30.262527&sspn=0.062999,0.133896&ie=UTF8&hq=&hnear=Sapanca/Sakarya,+T%C3%BCrkiye&ll=40.695347,30.263386&spn=0.062993,0.133896&z=13&iwloc=A)'da partner toplantısındaydım. Fırtına ve şiddetli yağmura rağmen Esra ve yerel IBM ekibi sayesinde güzel bir mikro haftasonu geçirdik.

Son tartışmamızda konuştuğumuz gibi, her geçen gün daha fazla lisanslama sorusuyla karşılaşıyorum. Bunları CEE (Orta/Doğu Avrupa) takımına çokça sormuş olmalıyım ki kanal müdürümüz Maciej, kısa bir lisanslama sunumu yaptı. Umarım yakın bir zamanda bir müşteri aktivitesi de yapılır bu konuda.
<!-- more -->
Şimdi müşteriler ve iş ortakları tarafından sıkça yapılan hataları listeleyeceğim:

#### Lotus Domino Designer bedava ama uygulamayı yerleştirmek değil!

<br />

Eğer Collaboration Express ya da utility server modellerini kullanıyorsanız, Lotus Domino Enterprise Server kurabilir ve bu sunucuda uygulama kullanabilirsiniz.

Yalnız uygulamalarınızı sunucuya gönderen her kullanıcı (basitçe her uygulama geliştirici) için ek "Lotus Domino Enterprise CAL" lisansı almanız gerekiyor. Eğer kendi uygulama geliştiriciniz yoksa serbestsiniz :)

#### 'Authenticated User' nasıl sayılıyor?

<br />

Çoğu müşterimin kullanıcı sayısını names.nsf'deki person dokümanlarını sayarak hesapladığını görüyorum. Bu tamamen yanlış!

Şu durumlar için kullanıcı lisansına ihtiyacınız yoktur:

* Yaratılan Jenerik administrator hesapları
* Test Kullanıcısı hesapları
* Yalnızca E-posta adresi olsun diye eklenen hesaplar
* ID yaratsanız da yaratmasanız da, departman ya da görevler için yaratılan jenerik e-posta hesapları (satis@domain.com, bilgi@domain.com gibi).

<br />

Fakat şu durumlarda ayrı lisanslara ihtiyacınız olacak.

* İki farklı kullanıcı tek ID dosyasını paylaşıyorlarsa (departman posta kutusu ya da yardım masası gibi) iki CAL gerekiyor.
* Bu ID dosyasını farklı zamanlarda (örneğin iki farklı mesaide) paylaşıyor olmak farketmez. Kullanıcı demek yetkili giriş yapan gerçek insan demektir.
* Üçüncü parti bir uygulama sunucuya bağlanıp kaynak kullanıyorsa ek bir lisans gerekir.
* Kendi authentication sisteminizi yapmak ve anonim kullanıcıya bu yolla isim/şifre girişiyle servis veriyor olmak lisans durumunu değiştirmez. Örneğin bir extranet uygulamanız var ve kullanıcıları names.nsf üzerinde tanımlamadan kendi yazılımınızla (örneğin session cookie kullanarak) içeri alıyorsunuz. Kullanıcılar anonim giriş yapsalar da lisans gerektirir. En iyi çözüm, bu tip durumlar için uygun bir utility express sunucu lisansı almak olacaktır.

<br />

#### PVU demek çekirdek sayısı çarpı 50 demektir...

<br />

Hayır! Bu, PVU hesaplamasında en sık yapılan hatadır.

"Processor Value Unit", server ürünlerinin lisanslamasında kullanılan ve çekirdek sayısına orantılı fiyatlama yapmayı sağlayan bir ölçü sistemi. PVU'nun arkasındaki felsefe performans oranında lisans yatırımı yapmak. Fakat, bütün işlemciler aynı performansı vermiyor. Dolayısıyla bazı işlemcileri kullanmak daha pahalı. [Şu sayfadan](https://www-112.ibm.com/software/howtobuy/passportadvantage/valueunitcalculator/vucalc.wss) ne kadar PVU gerektiği konusunda hesaplama yapabilirsiniz...

Örnek olarak standart intel tabanlı Xeon işlemcilerini (3000-3399, 5000-5499 veya 7000-7499 serileri) düşünürsek, her çekirdek 50 PVU demektir. Öte yandan daha hızlı bir Xeon ailesi olan ve 1-2 soket içeren (6500-6599 veya 7500-7599 serileri) işlemcilerde, bir çekirdek 70 PVU olacaktır...

#### Cluster sunucusu için ayrı lisans almama gerek yok!

<br />

Cevap: **Duruma göre değişir** ...

Eğer aktif olarak kullanılmayan bir sunucunuz varsa (yedek cihaz gibi), ek lisansa gerek yok. Fakat aktif cluster sunucusu (yüksek erişilebilirlik ve yük dengelemesi için kullanılan) için lisans almalısınız. Aynı kural geliştirme ve test sunucuları için de geçerlidir.

#### Lisans maliyetlerimi düşük tutmak için Partitioning özelliğini kullanmıyorum.

<br />

Bunu bir müşterimden duymuştum. Partitioning, aynı sunucu üzerinde birden fazla sunucu çalıştırmamızı sağlıyor (VM ile karıştırmamak lazım, tek işletim sistemi var bu durumda). Sözkonusu olan tek makine olduğu sürece birden fazla partition sunucusu çalıştırabilirsiniz.

Peki neden kullanayım partition sunucuları? Çok örneği var bu durumun. Değişik bölümleri (departman, iş birimi, marka gibi) ayırmak isteyebilirsiniz, güvenli bir alan yaratmak isteyebilirsiniz (ID Vault sunucusu gibi) ya da ek bir cluster sunucusunu aynı makinede yaratabilirsiniz. Partition sunucular neredeyse tamamen ayrı çalışırlar: Farklı data klasörlerini kullanırlar, birisi çökse de diğeri çalışabilir, bağımsız bir şekilde kapatılıp açılabilir gibi...

#### Express lisansım var ve Domino sunucumu tepe tepe kullanıyorum...

<br />

Bir çok müşteri Express lisanslama modelinin kısıtlamalarını bilmiyor. Şu özellikleri kullanamazsınız:

* Gelişmiş erişim kontrolleri (*Extended Access Control Lists*)
* Katmanlı dizinler (*Cascading Directories*)
* Dizin katalogları (*Directory Catalogs*)
* Ek dizin desteği (*Directory Assistance*)
* Merkezi Dizin - Kullanıcısız adres defteri (*Central Directory - userless names and address book*)

<br />

Bir çok express lisans kullanıcısı dizin directory catalog ve directory assistance özelliklerini bilerek ya da bilmeyerek kullanıyorlar.

#### Domino Enterprise CAL lisansım olduğuna göre kendi Lotus Mobile Connect altyapımı kurabilirim!

<br />

... LMC sunucu lisanslarını alır almaz... Evet, Enterprise CAL lisansı kullanıcılarınıza LMC software kullanmanıza izin verir ama yalnızca istemci için. PVU tabanlı sunucu lisanslarını ayrıca almanız gerekiyor.

#### Peki yazdığım uygulamayla 'Software as a Service' hizmeti sunabilir miyim?

<br />

Bu daha çok Utility server lisanslarıyla ilgili bir durum. Ama lisans anlaşmalarına göre lisanslı bir domino sunucuda uygulama kiralama yapamazsınız. Örneğin bir e-ticaret sitesi yürütebilirsiniz fakat kullanıcı ya da fonksiyon tabanlı bir SaaS veya bulut uygulaması yapmak için ayrı bir lisans modeli gerekiyor.

Ayrıntılı bilgiye Partnerworld sitesinden ulaşabilirsiniz...

#### Sanal makineler için nasıl bir PVU hesabı yapmalıyım?

<br />

Bu, bir sonraki yazım için reklam :) Hatta kalın, abone olun, öğreneceksiniz...

Bu arada şu linklerde bol bilgi var bu konularda...

[Notes/Domino Licensing Sıkça Sorulan Sorular](http://www.ibm.com/software/lotus/notesanddomino/licensing.html)
[Lisans Anlaşmaları](http://www.ibm.com/software/sla)
[Passport Advantage Anlaşmaları (giriş yapmanız gerekiyor)](http://www-01.ibm.com/software/howtobuy/passportadvantage/pao_customers.htm)
