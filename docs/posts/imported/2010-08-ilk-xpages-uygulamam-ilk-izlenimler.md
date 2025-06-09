---
authors:
  - serdar

title: "İlk XPages uygulamam: İlk izlenimler"

slug: ilk-xpages-uygulamam-ilk-izlenimler

date: 2010-08-01T15:55:00+02:00

---

Geçen hafta, [](2010-07-ilk-xpages-uygulamam.md)ilk XPages uygulamam hakkında bir yazı yazmıştım. Bu alana yeni girenler için ilk izlenimlerimi ve tavsiyelerimi derleyip toparlamak istiyorum...
<!-- more -->
**1. Farklı bir yaklaşım gerekiyor**

Domino platformunda klasik uygulama mimarilerini bir kenara koymak gerekiyor. Bunları kullanmak çok kolay olmayacak XPages üzerinde. Öncelikle **başlamadan önce düşünmek** gerekiyor. Tabi uygulama yazmadan planlama yapmak geliştiricilerin temel düsturudur fakat Lotus uygulamaları genellikle plansız programs ız da yapılabiliyor. Bir şey yapıp üzerine koya koya ilerliyebiliyorsunuz.

Klasik web uygulamalarında (Domino platformunda) iki farklı tasarım yapmaya meyilliyiz. Birincisi notes uygulamalarından alışık olduğumuz standart metod. Bir form ve iki agent tasarlarız (QueryOpen ve QuerySave). İkinci tasarım, daha çok CGI deneyimi olanlar tarafından sevilir. HTML formu üreten bir agent hazırlarız, bu formun çıktılarını işleyen başka bir agent da kalan işleri yapar.

Öte yandan, XPages üzerinde arabirim daha büyük önem kazanıyor. Tüm ekranlarda kullanılacak bir iskelet tasarlamamız işlerimizi epey kolaylaştıracaktır. Ben ilk aşamada burada hata yaptım. Klasik düşünceyle her ekran i çin ayrı bir XPage hazırladım. Sonuçta veri bağlantıları, belirli event'leri takip etme gibi konularda aynı işleri tekrar tekrar yapmak zorunda kald ım. Bu da epey verimsiz bir iş oldu benim için. Normal uygulamalarda subform ve script library yapılarını daha etkin kullanabiliyorsunuz. Fakat dikkat edilmesi gereken noktalardan birisi, XPages üzerinde Custom Control yapılarının subform'ların bire bir eşleniği olmadığı.

CGI uygulamalarına gelince, XPage'leri bu şekilde kurgulamak hiç doğru bir yaklaşım değil. CGI, stateless (durumsal olmayan) mimariye sahip. XPage'lerin tersine, herhangi bir CGI yordamı kendi durumu haricinde bir şey bilmek zorunda değil. Onlar girdileri çıktıya dönüştüren birer kara kutu.

Öncelikli iş, bir kağıt kalem edinmek. Uygulamanın tüm aşamalarını ve ekranlarını çizip, bunlar arasındaki gidiş gelişleri haritaland ırmak ve ortak noktaları belirlemek. Daha sonra tüm bu ortak noktaları yöneten bir custom control hazırlamak ve tüm sayfalara yerleştirmek doğru bir yaklaşım olacaktır.

**2. XPages'in doğrulama (validation) yöntemleri muhteşem!**

Validasyon (doğrulama demeyi sevmiyorum, özür dilerim.) gerçekten çok kolay. Çok detaylı istekleriniz olmadığı sürece (başka bir yerden veri al, çarp böl karşılaştır gibi şeyler yapmıyorsanız) bir kaç parametreyi ayarlıyorsunuz ve işte!

Bu uygulamada client-side (istemci tarafında) validasyon kullandım. Bir isme, doğru bir e-mail adresine, geçerli bir içerik seçimine ve kullanım servisleri onayına ihtiyaç duyuyordum. Validasyon ayarlarını yaptım, javascript tarafını o halletti :)

Bir ayrıntı, listbox gibi bazı kontrollerin validasyon ayarları özellikler sayfasında görünmüyor. Onları 'All Properties' üzerinden ayarlamak gerekiyor. Karşılaştığım tek zorluk Captcha testindeydi, ona da geleceğim.

**3. Checkbox ve Radio kullanımı biraz problemli**

Mevcut versiyonda, checkbox'lar ve radio'lar tekil obje olarak algılanıyor. Bunları gruplamak için 'Other Controls' altında farklı kontroller var. Fakat dokümantasyon yetersiz olduğu için kullanmak biraz zor. Ayrıca bunları oluştururken koda girmek gerekiyor. Umarım önümüzdeki versiyonlarda bunlar düzeltilir.

Bu kontrollerin validasyonu da problemli. Blog'larda güzel örnekler var. PlanetLotus.org üzerinden bir arama yapmanızı öneririm.

**4. Çoklu dil desteği sunmak çok kolay ama biraz sabredin!**

Uygulamam Türkçe ve İngilizce dil desteğine sahip. Fakat benim yapt ığım hata acele etmek oldu. Formu tasarlayıp hemen dil dokümanlarını kurcaladım. Daha sonra farkettim ki, ben alanlarda değişiklik yaptıkça dil dok ümanı da değişiyor.

Benim önerim, tüm uygulamayı bitirip testlerini yaptıktan sonra dil dokümanlarını bir kerede değiştirin.

**5. Türkçe dilden başlayın**

İlk başladığımda arabirimi İngilizce olarak tasarlamaya giriştim. Fakat dil dokümanlarını düzenlerken farkettim ki buralarda Türkçe karakter kullanamıyoruz. Onları unicode olarak (\\uXXXX) değiştirmek gerekiyor. Bunun yerine Türkçe'yi varsayılan dil yaparsanız Designer bunları unicode olarak oluşturuyor. İngilizce'ye dönüştürmek daha kolay.

**6. CAPTCHA testi**

Captcha, doldurulan formun robotlar tarafından değil de gerçek insanlar tarafından doldurulduğunu anlamamıza yarayan küçük testler. Bir çok web sayfasında 'gördüğünüz karakterleri/sayıları giriniz' sorusuna eşlik eden yamultulmuş resimler karşımıza çıkar.

Internet'de ücretsiz olarak bulabileceğiniz bir çok versiyonu var bunların. Fakat çoğu sunucu tarafında kodlama gerektiriyor. Ben daha basit bir test tasarladım. Form iki sayının çarpımını soruyor. Başlangı çta sessionScope'da belirlenen iki sayıyı alıp bunları validasyon esnasında kontrol ediyorum. Eğer bu forma özel bir robot tasarlanırsa elbette kolayca kırılabilecek bir test, ama hiç yoktan iyidir.

Captcha testinin validasyonu biraz karmaşık, çünkü custom validation hakkında dokümantasyon çok zayıf. Bloglardan birinde (yazardan özür dilerim, unuttum...) bir kod bulmuştum, ipucu olarak onu vereyim. Ekteki kod custom validation script'lerine yerleştiriliyor.

![Image:İlk XPages uygulamam: İlk izlenimler](../../images/imported/ilk-xpages-uygulamam-ilk-izlenimler-M2.gif)

```

result=getComponent("fieldToBeValidated");

// Testimizi yapıyoruz...

if(testFailed) {
    result.setValid(false);  // Validasyonu başarısız olarak ayarlıyoruz
    return "Test başarısız! biraz matematik öğren de gel!";        // Hata mesajını döndürüyoruz
}

```

<br />

**7. Dokümantasyon zayıf (yok da denebilir)**

XPages'in en zayıf yanı dokümantasyon meselesi. Neredeyse yok denecek kadar az... Designer'ın yardım bölümü obje yapılarını ve referanslarını veriyor ki zaten çoğunu biliyoruz.

Kontrollerin özelliklerinin tanımları, event hiyerarşileri, farklı validasyon teknikleri, objeler arası bağlantılar, dojo gibi bazı kısımlar eksik. Wiki çoğu zaman yardımcı olamıyor. En yararlı kaynak blog'lar. PlanetLotus.org burada kurtarıcınız olacaktır.

Ek olarak, JavaScript ve el altından JSF (J2EE tabanlı) kullandığınız göz önüne alınırsa bunlarla ilgili referanslardan bir kitaplık oluşturmanız yararlı olacaktır. Örneğin facesContext objesi çeşitli J2EE objelerine ulaşmanızı sağlayacak ve alt seviye bazı işlemleri yapmanızı kolaylaştıracaktır. Herhangi bir noktada başka bir XPage'e gitmek için "context.redirectToPage(someXPage)" komutunu kullanabilirsiniz fakat XPage olmayan başka bir sayfaya gitmek isterseniz biraz Java kullanmalısınız: "facesContext.getExternalContext().redirect(someURLString)". ExternalContext, JSF context'inin J2EE karşılığı gibi düşün ülebilir.

**8. JavaScript öğrenin!**

Daha önceki yazılarımda söylediğim gibi, JavaScript, XPages'in altında yatan kilit teknoloji.

Ben bu konuda çok şanslıydım. Bir kaç yıl önce, temelinde çok karmaşık bir JavaScript iskeletin kullanıldığı bir projede rol almış ve prototype programlamayı konusuna çok hakim birinden öğrenme fırsatı bulmu ştum.

Benim eksik yanım Dojo oldu. Henüz öğrenmedim ama istemci tarafında programlama için çok önemli. Neyse ki internet üzerinde yüzlerce örnek bulabiliyorsunuz.

**9. Tarayıcı testlerine önem verin**

Değişik tarayıcılara uyumlu uygulama geliştirmenin ne kadar sinir bozucu olduğunu tüm Web uygulamacıları bilirler. Ben her zaman W3C standartlarına uymak gerektiğini düşünürüm ama bazen Mozilla Firefox bile bu standartları yıkacak işler yapıyor.

Uygulamanızı değişik aşamalarda farklı tarayıcılarla test edin. Son test çoğu zaman hayal kırıklığı yaratabiliyor. Uygulama bittikten sonra çok kilit bir noktanın bir tarayıcıda çalışmadığını farkederseniz her şey için çok geç olabilir. Bu yüzden ne kadar sık test ederseniz bazı sorunları o kadar erken farkedebilirsiniz.

**10. Hata kontrolü yapın**

Domino'da geliştirme yapan web'ciler bilir ki, hata ayıklamak zor iştir. XPages için de geçerli bu durum. Standart geliştirme ortamında varsayılan hata sayfaları hata ayıklama için gereken bilgiyi sunarlar fakat ger çek platformda kullandığınız script'leri gösterdikleri için önemli bir tehlike oluştururlar.

Çözüm, tüm hataları kontrol edip kendi hata izleme yöntemlerinizi oluşturmak. Try-catch blokları bu açıdan çok yararlıdır.

**11. Güvenlik çok da farklı değil**

XPages üzerinde standart güvenlik sorunları aynen geçerli. View'lar ı web platformundan gizlemeniz, doğru bir ACL yapısı oluşturmanız ve önemli bilgileri Reader alanlarıyla gizlemeniz gerekir. Kullanıcılarınızla ilgili şu temel kuralları unutmayın:

- Uygulamanızı kırmak için yeterli zamanları ve yeterli motivasyonları vardır.
- Lotus hakkında her şeyi bilirler.
- Uygulama mimarinize ait her şeyi bilirler.
- İhtiyaç duydukları her araç ellerinin altındadır (sniffers, brute-force attackers vs.)
- Sosyal mühendislik konusunda ustadırlar.

**12. Geleceği de düşünün**

Bugüne kadar benim için çalışanlar da dahil olmak üzere bir çok Domino programcısını inceleme fırsatı buldum. Genel bir eğilim var. Öğrenme aşamasında beceriksiz ve amatörce uygulamalar üretiliyor. Bu konuda bir şeyler öğrenen geliştirici, daha güzel, verimli ve dayanıklı uygulamalar oluşturmaya başlıyor. Gerçek bir usta olduğunda ise artık kendine ait bir tarz oluşturuyor, subform ve script library gibi esnek öğeleri ba şarıyla kullanmaya başlıyor. Bugüne kadar bu modüler yapıyı baştan kullanmaya başlayan notes/domino geliştiricisi görmedim.

XPages üzerinde custom control yapısı subform'lardan daha kolay ve daha esnek bir kullanım sunuyor. Çünkü genellikle ana XPage'den bağımsız davranıyorlar. Öte yandan Script library'ler çok benzer. Onları etkin olarak kullanmanın yolu prototype programlamadan ve dojo'dan geçiyor.

**13. Son sözler: Yol Haritası**

Şimdi XPages yetkinliğinizi planlama zamanı. İlk kural sabırlı olmak. Gerçek bir uygulamaya dalmak için acele etmeyin.

* İlk olarak basit teknolojiler konusunda bilgilerinizi tazeleyin. **HTML** ve **CSS** , **Ajax** , **JavaScript** , **XML** vs.
* **Web 2.0** için hazırlanmakta fayda var. Bu yeni mimari klasik yaklaşımdan biraz farklı. Bunlar hakkında bir kaç makale okumakta fayda var. Aslında XPages ile klasik uygulama yazmak web 2.0 kodlamaktan daha zor diyebilirim.
* Bir kaç workshop (çalıştay demeyeceğim) alın. Eğer bir iş ortağı için çalışıyorsanız ParnerWorld sitesinde **VIC (Virtual Innovation Centers)** üç günlük bir XPages eğitimi sunuyor. Yerel IBM yetkiliniz belki bu tip bir eğitim organize edebilir. Alternatif olarak D8L55 kodlu bir sunuş eğitimi yetkili eğitim merkezlerinde sunuluyor.
* Bu sunuş eğitiminde gördüklerinizi uygulamakla başlamanızda fayda var. Gerçek eğitime gittiğinizde karmaşanın içinde kaybolabilirsiniz. Bunun yerine 40-50 saatlik bir boğuşma, size hangi konuda eksiklik yaşadığınızı gösterecek, esas eğitimde daha bilinçli olmanızı sağlayacaktır.
* Şimdi esas eğitim için hazırsınız. Yetkili eğitim merkezleri "**D8C51: IBM Lotus Domino Designer 8.5x: Introduction to Application Development (5 gün)** " veya daha yenisi "**D8C55: Building XPage Applications with IBM Domino Designer 8.5.1 (4 gün)** " eğitimlerini sunuyorlar. [Sibnet](http://www.sibnet.com.tr/)'ten Kenan Yılmaz'la sık sık görüşüyorum ve bu eğitimi en az iki ayda bir açıyorlar.
* Artık gerçek uygulama tasarlamaya başlayabilirsiniz. Ama gene de **planetlotus.org** üzerinden çeşitli XPages blog'lar ını incelemeye devam edin. Onlara abone olup önemli yazıları kenara ayırın. Zaman içerisinde çok yararını göreceksiniz...
