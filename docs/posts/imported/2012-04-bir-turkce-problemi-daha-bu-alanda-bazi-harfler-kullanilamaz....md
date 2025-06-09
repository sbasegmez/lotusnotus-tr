---
authors:
  - serdar

title: "Bir Türkçe problemi daha: \"Bu alanda bazı harfler kullanılamaz...\""

slug: bir-turkce-problemi-daha-bu-alanda-bazi-harfler-kullanilamaz...

date: 2012-04-20T16:09:52+02:00

---

Dün benim için biraz talihsiz bir gündü. Sabah 9:00'da başlayan maraton süresince dokunduğum herşeyi 'kırdım'... Dün bütün günümü beta testleri için harcasaydım herkes için en yararlı gün olurdu muhtemelen :)

Böyle bir günde XPages tasarlamaya kalkarsanız başınıza gelecek şey, gene abuk bir hatayla karşılaşmak olacaktır.
<!-- more -->
Java varoldukça bazı problemler giderilemeyecek. Bu seferki hatamız gene Türkçe ile ilgili. Fakat bu sefer işletim sistemi dili denklemin içinde yeralmıyor. Sorunumuz doğrudan iki güzide karakterimizle ilgili. Videoyu seyredin ve ne demek istediğimi anlayın:

<iframe width="750" height="515" src="http://www.youtube.com/embed/S8sJUlLoVGY" frameborder="0" allowfullscreen></iframe>

Videoda gördüğünüz Extension Library ile gelen basit bir Dojo Button. Bu button için "Label" girmeye çalıştığınızda Türkçe karakterler bozuk çıkıyor, fakat iki spesifik karakter büyük "Ş" ve büyük "Ğ" harfleri hiç gösterilmiyor. Bunlar ekranda görünmediği gibi, bu şekilde kaydettiğiniz XPages kodunu bir daha açamıyorsunuz. Önce XSP Editörü çöküyor, ısrar ederseniz Designer'ınız kilitleniyor :)

Kazara bu hataya düşerseniz Package Explorer'dan custom control ya da XPage'inizi bulup sağ tuşa basın ve "Open with\\XML Editor" seçeneğiyle açıp sorunu düzeltin.

Bu arada sorun sadece dojo button'da değil. Extension Library ile gelen ve girdiğiniz değerleri XPages Design görüntüsünde gösteren tüm kontroller için geçerli. Dojo Button, Dojo Radio, Dojo Checkbox, Form Table, vs. benim test ettiklerim (Form Table'ıma "Şirket" diye bir başlık atmaya çalışınca farkettim zaten)...

Konunun Extension Library'den kaynaklandığını düşündüğüm için bir hata kaydı yarattım. Siz de aynı problemden muzdaripseniz [buraya](http://www.openntf.org/internal/home.nsf/defect.xsp?action=openDocument&documentId=53C3401374B636A3862579E500672952) bir cevap ekleyin ki çözüme öncelik verilsin...

Blog'a henüz yazmadım, çok da duyurusunu yapmadım ama yeri gelmişken belirtmek istedim.

Nisan ayı itibariyle şirketim Developi, **IBM Lotus Notes/Domino** yazılımlarının **Design Partner** programına seçildi. Bu program, Managed Beta programının bir seviye ilerisi. Program dahilinde yeni ürünlere ve versiyonlara erken fazda erişebiliyor, bunlarla ilgili geribildirimlerde bulunabiliyoruz. Haftada iki saatlik bir toplantıya katılmamız gerekiyor ve Beta testleri epey zaman alıyor. Fakat keyifli bir iş...

Umarım, özellikle Türkçe karakter problemleri sayısında küçük bir azalma yaşarız :)

Bu konuda herkesin katılımına açığım. Gördüğünüz Türkçe çeviri hataları veya Türkçe karakter problemlerini beklerim. Doğru kişilere doğru geribildirimler yapıldığında problemler çözülebiliyor. Örneğin birçok kişinin muzdarip olduğu ama nedense kimsenin destek kaydı açmadığı [script library problemi](2011-11-gene-java-gene-turkce-error-loading-use-or-uselsx-module.md "gene-java-gene-turkce-error-loading-use-or-uselsx-module.htm") çözüldü ve en yakın release'de yayınlanmak üzere sıraya girdi. Şu anda haber beklediğim konuysa iNotes'daki "Yeni Klasör" tuşundaki çeviri hatası.

Bir sonraki Türkçe hatasına kadar iyi çalışmalar :)
