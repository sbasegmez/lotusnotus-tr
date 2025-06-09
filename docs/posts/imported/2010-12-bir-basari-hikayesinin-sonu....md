---
authors:
  - serdar

title: "Bir başarı hikayesinin sonu..."

slug: bir-basari-hikayesinin-sonu...

date: 2010-12-03T18:01:41+02:00

---

2003 yılında, bir müşterimden oldukça zorlu bir talep geldi. Web siteleri için bir içerik yönetim sistemi gerekiyordu. İçerikler hem şirket içindeki çalışanlar, hem de şirket dışındaki ajanslar tarafından yönetilebilecekti.

Önce bir Notes veritabanı yaptık. Fakat o kadar çok ziyaret oluyordu ki web sitesine, bir süre sonra sunucunun performansı yerlere iniyordu. Fakat domino'dan vazgeçemezdik. Çünkü içerikler çok farklı lokasyonlarda düzenleniyordu. Replikasyonun yanı sıra veri esnekliği bizim için vazgeçilmezdi.
<!-- more -->
Neyse ki, IBM'den güzel bir haber geldi. Websphere Application Server yazılımının kısıtlı kullanımı Domino sunucularıyla veri alışverişi yapmak kaydıyla serbest bırakılmıştı. Veriye nasıl ulaşacağımız belliydi ama onu nasıl göstereceğimizi çözmek biraz zaman aldı.

Günler geceler süren çalışmalardan sonra JSP'lerden ve J2EE kütüphanelerinden oluşan büyük bir sistem tasarladık. Veri altta NSF veritabanlarında tutuluyor, güncellemeler Notes üzerinden yapılıyordu. Üst tarafta bir Java Bean (fasülye !) kütüphanesi oluşturduk. DIIOP protokolü üzerinden verileri çekiyor ve cache'liyorduk. Onlarca JSP sayfa kullanarak web sitesinin önyüzünü de tasarlıyorduk. Zaman içerisinde 8 farklı web sitesi bu uygulama üzerine taşındı. Tasarladığımız 'in-memory caching' algoritması sayesinde performans inanılmazdı. Sistem ayrıca çok stabil (aylarca restart etmeden) ve güvenli (hiç bir DOS saldırısına maruz kalmadan) bir şekilde çalışıyordu.

Bu yetmedi, yaklaşık bir yıl sonra daha fazla talep geldi. Müşteri, ziyaretçi verilerinin CRM uygulamasına yapıştırılmasını istiyordu. Web sitesinden form dolduran ziyaretçinin kim olduğunu çözüp marka ile olan etkileşimini kayıt altına almamız gerekiyordu. Java bean'lerimizi bu yönde genişleterek toplanan verinin CRM alt sistemine entegre olmasını da sağladık.

Fakat zaman içerisinde dünya değişti... Şimdi, sosyal medyanın hükmettiği bir dönemdeyiz ve web siteleri eskisi kadar stabil değil. Her ay yeni bir mikro site tasarlanıyor. Stabil, performanslı ve ölçeklendirilebilir yapısına rağmen bizim JSP uygulamamızın bir gediği vardı. JSP ve Domino bilgisine haiz bir geliştirici olmadan yeni tasarımların aktarılması mümkün olmuyordu. Bir kaç kez ajansların HTML kodcularını kullanmak istedik, felaketle sonuçlandı. Bunun yanında müşterimiz tüm içeriği değişik ajanslara yıkmaya başladı. Artık NSF veritabanı bize yük olmaya başladı. Çünkü ne zaman yeni bir ajansla çalışmaya başlanılsa, yeni kullanıcıları Notes üzerinde çalışan karmaşık bir içerik yönetim sistemi için eğitmek durumunda kalıyorduk.

Geçen yıl bir çıkış planı yaptık. Web siteleri teker teker dışarı taşındı. CRM entegrasyonunu web servisleri kullanarak tekrar tasarladık. Ve yarım saat kadar önce, son modülü kapattım. Sanırım haftaya sunucunun fişini çekiyor olacağız.

Bu projeye harcadığım 7 yıl boyunca çok değişik uygulama geliştirme teknikleri öğrendim. Ama üzerinde uzun zaman uğraştığınız bir projeye bağlanmış hissettiniz mi? Ben hissettim :)))

İşin iyi tarafı, bu deneyimlerimi XPages üzerinde kullanıyorum. JSP (ve JSF) kullanmak, geleneksel web uygulama geliştirmekten (asp, php ya da agent'lar) çok farklıdır. Eğer alt tarafta ne döndüğüne dair bilginiz varsa adapte olmak daha kısa sürer.
