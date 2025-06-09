---
authors:
  - serdar

title: "Sebepsiz yere çöken sunucuyu nasıl düzelttik?"

slug: sebepsiz-yere-coken-sunucuyu-nasil-duzelttik

date: 2010-08-31T15:30:51+02:00

---

Bir müşterinin uzak lokasyondaki sunucusu bir kaç haftadır sebepsiz yere çöküyordu. Neden çöktüğüne dair bir sebep bulamadık ama sorunu düzeltmeyi başardık.

Bu vakayı özetleyerek deneyimsiz sistem yöneticileri için bu tür durumlarda ne yapılacağına dair bazı ipuçları vermek istiyorum.
<!-- more -->
Sunucumuz ara sıra (ve rastgele zamanlarda) çöküyordu. "**Automatic Server Recovery** " özelliği sayesinde sunucu kendi kendine yeniden başlıyor ve ayağa kalkıyordu. Bir çok kullanıcı durumun farkına varmadı. Ayrıca "**transaction logging** " sayesinde herhangi bir veritabanı bozulması veya veri kaybı yaşamadık bu süreçte.

İpucu: Sunucu dokümanında "Automatically Restart Server After Fault/Crash" özelliğini devreye alın. Sunucu gecenin bir yarısı çökebilir ve kullanıcılar sizin uyanmanızı bekleyecek kadar sabırlı davranmayacaktır :)

İpucu: "Transaction Logging" özelliğini kullanmanızı öneririm. Bu özellik çoğu durumda performansı arttırır ve veritabanlarının daha dayanıklı olmasını sağlar.

<br />

Hemen "**IBM_TECH_SUPPORT** " klasöründeki **NSD** dosyalarını inceledik. Çoğu zaman birden fazla çökme yaşandığında, NSD dosyalarında tekrarlı bir takım durumlar görürüz. Bir kaç örnek verelim:

* Çökmelerin '**ne zaman**' olduğu önemlidir. Her akşam 20:00'da meydana gelen 3-4 çökme vakası tesadüf olamaz. O saatte çalışan agent'lar, replikasyonlar, yedekleme ve diğer 'task'ler incelenmelidir.
* NSD dosyaları **hangi prosesin çöktüğü** hakkında bilgi verir (FATAL THREAD kelimelerini aratın). Aynı prosesin bir kaç kez çökmesi, iyi bir başlangıç noktasıdır.
* Her çökme sonrası NSD, problem yaratan işlemin hafıza içeriğini bir dosyaya yazar (**Memory Dump** dosyası: \*.dmp). Bu dosya, çöken prosesin en son ne yaptığına dair bazı işaretler taşır. Örneğin yapısal olarak bozuk bir veritabanı replikasyon sırasında 'REPLICA' işlemini, view güncellemeleri sırasında 'UPDATE' prosesini çökertebilir.
* Bazen, sunucunun patlamasından saniyeler önce konsol loguna yazdığı son cümleye dikkat etmek gerekir. Örneğin belli bir kullanıcıya mesaj dağıtıldığını söyleyen bir cümle bir kaç çökmede son yapılan işlerden birisi ise o kullanıcının veritabanını, kurallarını, varsa pre-delivery agent'larını incelemekte fayda vardır.
* Web logları da önemli bilgiler verebilir. Bir defasında bu tip rastgele çökmelerde web loglarının son satırının hep aynı olduğunu farketmiştim. R7'nin alt versiyonlarından birisinde kullanıcılar iNotes üzerinden adres defterini açtıklarında sunucu çöküyordu.

İpucu: Sunucu dokümanında "Run NSD To Collect Diagnostic Information" seçeneğinin aktif olduğundan ve "Cleanup Script / NSD Maximum Execution Time" seçeneğinde makul bir süre ayarlandığından emin olun. Varsayılan değer (300 saniye) yüksek hafızalı meşgul sunucularda yetersiz kalabilir.

İpucu: Elinizden geldiğince (sistemi yavaşlatmadan) log tutun. Neye ne zaman ihtiyaç duyacağınızı bilemezsiniz...

<br />

Bizim durumumuzda ne yazık ki tekrarlı bir desen yoktu. Bütün çökmeler farklı saatlerde ve farklı proseslerde oluşuyordu. Üstelik bir kaç durumda NSD dosyaları, süre yetersizliğinden, tam olarak oluşamamıştı. Dolayısıyla ikinci adıma geçtik: **Araştırma** .

IBM destek kaynaklarını (Support portal, fixlist veritabanı, knowledge base, vs.) kullanarak aynı versiyonda oluşmuş değişik çökme vakalarını inceledik. 8.5.1 FP1 versiyonunda bir kaç benzer örnek bulunca en son fix pack olan FP4'ü yüklemeye karar verdik. Bir kaç günlük sessizlikten sonra yine bir çökme yaşadık.

İpucu: Genellikle en son fix pack'i yüklemek mantıklıdır. Minor yükseltmeleri (8.5.1, 8.5.2 gibi) yapmadan önce iki kez düşünürüz çünkü gelen bazı değişiklikler hakkında hazırlık yapmamız gerekebilir. Fakat fix pack'lerin güvenli olduğunu söyleyebiliriz...

<br />

En sonunda PMR yaratmadan önce bir kaç şey daha denemeye karar verdik.

* **Names.nsf** ve **admin4.nsf** veritabanlarının sıfır replikalarını bir client üzerine aldık ve sorunlu sunucudakilerin yerine koyduk (sunucu bu sırada kapalıydı tabi). **Log.nsf** ve **mail(n).box** veritabanılarını sildik. Bu veritabanları sunucu çalışıyorken sürekli meşgul verir. Deneyimlerime göre bu veritabanlarındaki bozukluklar tespit edilmesi en zor sorunlardır...
* **Daoscat.nsf** veritabanını sildik ve sunucu açıkken '**resync**' komutuyla DAOS indekslerini sıfırladık. 8.5.x serisinin erken versiyonlarında DAOS ile ilgili bir çok problem rapor edilmiştir.
* ".ft" uzantılı klasörleri silerek sunucunun full-text indekslerini tekrar oluşturmasını sağladık. Full-text indeksler (özellikle ekli dosyalar) sunucu arızalarında sık karşılaşılan nedenlerdendir. Yalnız bu işlemin çok zaman alacağını hatırlatırım.
* Konsoldan "**fixup -J**" komutuyla tüm veritabanlarını kontrol ettik (-J seçeneği transaction logged veritabanlarında kullanılır).
* Konsoldan "**updall -R**" komutuyla tüm view indekslerini yeniden güncelledik (-R seçeneği view indekslerini rebuild etmeye yarar).

<br />

Tüm bu işlemler için sunucuyu iki saat kadar kapatmamız gerekti. Ek olarak fixup ve updall işlemleri daha uzun süreceğinden sabaha kadar bariz bir yavaşlık hissedildi. Dolayısıyla bu tür işlemleri hafta sonuna denk getirmek mantıklı bir hareket olacaktır.

Sonunda sorunumuz çözüldü. Bugün çökme yaşamadığımız sekizinci gün. Halen sorunun kaynağını bilmiyoruz fakat önemli olan sorunu düzeltmek değil miydi?

Daha fazla detay için IBM'in hazırladığı bu harika dokümanı inceleyebilirsiniz: [Troubleshooting Lotus Domino hangs and crashes](http://www.ibm.com/developerworks/lotus/library/domino-server-crashes/)
