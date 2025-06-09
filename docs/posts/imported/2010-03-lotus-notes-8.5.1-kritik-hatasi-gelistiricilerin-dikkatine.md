---
authors:
  - serdar

title: "Lotus Notes 8.5.1 Kritik Hatası: Geliştiricilerin dikkatine"

slug: lotus-notes-8.5.1-kritik-hatasi-gelistiricilerin-dikkatine

date: 2010-03-07T11:15:53Z

---

Bugün bloglarda dolaşırken rastladığım bir yazı, Lotus Notes 8.5.1 versiyonunda oluşan ve önemli olduğunu düşündüğüm bir hatadan bahsediyordu. Bleed Yellow sitesindeki blogunda Eric Brooks, konuyu "[8.5.1 FAIL. Your code may just break](http://www.bleedyellow.com/blogs/erik/entry/8_5_1_fail_your_code_may_just_break19)" konusuyla açıklıyor.

Olay 8.5.1 upgrade'inden sonra ortaya çıkıyor. **NotesView.GetDocumentByKey, NotesView.GetAllDocumentsByKey, NotesView.GetEntryByKey or NotesView.GetAllEntriesByKey** rutinlerinde standart bir lookup yaparken zaman zaman "**The collection has become invalid.**" hatasıyla karşılaşabiliyoruz. Hata her zaman çıkmadığı için belirlemek de oldukça zor. Zaten yorum yapanlar da bunu özellikle belirtiyor.
<!-- more -->
Eric, problemi tekrarlayabilir hale gelmiş ve destek kaydı açabilmiş. Hata sürekli olmuyor, bunun nedeni normal davranışın "**View.AutoUpdate=True** " komutuyla değiştirilebilirken artık değiştirilemiyor oluşu. Eski versiyonlarda view üzerinde bir değişiklik varsa, komutun çalışmasından önce indeksler otomatik olarak güncellenirdi. Yeni versiyonlarda yapılan değişiklik sonrası güncelleme yapılmıyor ve hata verip kodun çalışması durduruluyor.

Özellikle yoğun işlem yapılan veritabanlarında sorun olduğu söyleniyor.

Yazıya yapılan yorumları incelerseniz destek ekibinden Chad Scott, konuyu çözdüklerini ve 12 Mart itibariyle düzeltmenin hazır olacağını bildiriyor. Verilen SPR numaralarıyla destek kaydı açılırsa hotfix edinilebilir.

Son olarak şunu söylemek isterim. Eric, hatayı blog'unda ele aldıktan sonra Eric'i takip eden Ed Brill'den başlayan hızlı bir yayılım oluyor. 4 gün içerisinde 20 kişi yorum yapıyor. Destek ekibi de bir şekilde işe dahil edilerek fix'in takvimi açıklanıyor.

Lotus yazılımlarıyla ilk çalışmaya başladığımda bu tip durumlarda yapılabilecek tek şey destek kaydı açıp olayı forumlara yansıtmak ve aynı hatayla başka bir kişinin de karşılaşmış olmasını beklemek olurdu. Tabi bu kişinin cevap yazması da gerekirdi. Bu şekilde aylarca tekrar edilemediği için bekleyen nice hatalarla karşılaşırdık. Oysa sosyal medyanın yaygınlığı, bu tip hatalara bloglardan da bolca cevap bulunabilmesini sağlıyor. Forumlardan farklı olarak blog'ların diğer kullanıcılar tarafından sürekli izlenmesi paylaşımı oldukça kolaylaştırıyor.
