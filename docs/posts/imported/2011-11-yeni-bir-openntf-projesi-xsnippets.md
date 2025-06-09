---
authors:
  - serdar

title: "Yeni bir OpenNTF projesi: XSnippets"

slug: yeni-bir-openntf-projesi-xsnippets

date: 2011-11-28T08:21:33Z

---

İngilizce kısmı ve PlanetLotus sitesini takip edenler biliyor. Türkçe kısımda da yazmak için biraz olgunlaşmasını bekledim.

Bir süredir [Niklas Heidloff](http://heidloff.net/), [Frank van der Linden](http://www.domino-weblog.nl/) ve [Bruce Elgort](http://bruceelgort.com/) ile yeni bir [OpenNTF](http://www.openntf.org "OpenNTF") projesi olan "[XSnippets](http://www.openntf.org/blogs/openntf.nsf/d6plinks/NHEF-8NNBK7)" üzerinde çalışıyoruz. Geçtiğimiz haftalarda [uygulamanın beta versiyonunu](http://openntf.org/xsnippets) kullanıma açtık. Bu arada [René Winkelmeyer](http://blog.winkelmeyer.com/) de ekibe katıldı ve XSnippets'in en ilginç bölümünü geliştirmeye başladı: [Designer plugin](http://blog.winkelmeyer.com/web/blog.nsf/entry.xsp?permalink=integration-of-xsnippets-into-domino-designer).
<!-- more -->
![A picture named M2](../../images/imported/yeni-bir-openntf-projesi-xsnippets-M2.gif)

XSnippets, daha önce [OpenNTF](http://www.openntf.org "OpenNTF") sitesinde bulunan "Code bin" bölümünün yerini alacak. Büyük ve hazır uygulamalardansa bu bölümde basit birkaç satırlık yararlı kod parçalarına yer veriyoruz. Uygulama, kolay kullanım ve sade bir deneyim oluşturmak adına çok basit tutuldu. Öte yandan bu projenin önemli bir özelliği, veritabanı tasarlamaktan daha fazlasını yapıyor olmamız.

Projenin değişik adımlarında videolar ve bloglar ile uygulama geliştirme sürecimizi de anlatıyoruz. Şu ana kadar edindiğimiz deneyimler çok faydalı oldu.

Karşılaşacağımız zorlukların en başında, dört farklı ülkede (ABD, Hollanda, Almanya ve Türkiye) ve üç farklı zaman diliminde çalışan dört geliştirici olarak nasıl koordine olacağımız sorunuydu. Bu problemi "**LotusLive Activities**" ile çözdük.

OpenNTF projesi: XSnippets" border="0" src="yeni-bir-openntf-projesi-xsnippets.htm/content/M3?OpenElement" /\>

Dört farklı geliştirmeci için bir zorluk da aynı veritabanı üzerinde geliştirme yapmaktı. Bu noktada 8.5.3 versiyonuyla gelen '**Source Code Control**' özelliği imdadımıza yetişti. SVN ile aynı uygulamada versiyonlama destekli bir senkronizasyon yapısı kurduk. Arabirim tasarımlarımızı Bruce'un Mockup çizimleri üzerinde kurguladık ve Skype üzerinden yaptığımız toplantılarda tartışarak son haline getirdik.

Proje henüz beta aşamasında. Hergün yeni bir özellik ekliyoruz. Çok yakında projenin ilk versiyonunu stabil hale getireceğiz ve açık kaynak kodlu olarak yayınlayacağız. XSnippets'in önemli bazı özelliklerini özetlersek;

- Eklenen kodlar, Designer ile aynı görselliğe sahip bir şekilde renklendiriliyor.
- Kopyalanan snippet'ler kayıt altına alınarak 'En popüler' snippetlerin hesaplanmasında kullanılıyor.
- Snippet'lere yıldız verilerebiliyor.
- Widget özelliği ile blog yazarları bu içerikleri sitelerine ekleyebiliyorlar.
- Kullanıcılar, RSS okuyucular kanalıyla yeni eklenen snippet'leri takip edebiliyor.

Şu ana kadar gelen topluluk geribildirimi çok heyecan verici. Birçok kişi; twitter, bloglar ve kişisel konuşmalar kanalıyla projeyi ne kadar beğendiklerini ifade ettiler. İlerisi için çok değişik fikirlerimiz var. Haberdar olmak için bizi izlemeye devam edin :)
