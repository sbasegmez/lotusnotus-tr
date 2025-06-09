---
authors:
  - serdar

title: "Gene Java, gene Türkçe, gene Problem..."

slug: gene-java-gene-turkce-gene-problem...

date: 2011-06-26T00:46:10+02:00

---

Bir Java klasiği daha, bu sefer XPages ile uygulama geliştirirken karşımızda...

Bugün OpenNTF Custom Control yarışması için ikinci kontrolümü tamamladım. Her şeyi toplayıp paketliyordum. Boş bir veritabanı yarattım, her şeyi oraya doldurdum, ACL falan filan derken...
<!-- more -->
XPage'lerin hiç birisi çalışmıyor. Boş yarattıklarım bile aşağıdaki gibi saçma ve bulanık bir hata veriyorlar:

**Error 404**
**HTTP Web Server: Item Not Found Exception**

Sakince düşününce ve biraz Google araması yapınca problemin 'automatic building' ile ilgili olabileceğini düşündüm. Birkaç kombinasyon denedim, sunucuyu, designer'ı, ayrı ayrı ve birlikte restart ettim, kahveme süt koymayı, .çayıma şeker atmayı falan denedim sonuç yok!

İşin garibi, sayfa Notes istemciden açılıyor. Veritabanının XPages olmayan herşeyine tarayıcı üzerinden erişebiliyorum. Gıcıklık yalnızca XPage'lerde.

Süper değil mi? Neyse, çözüm geliyor...

HTTP thread'inde biraz debug yapalım dedim (tell http debug thread on) ve problemi buldum.

25.06.2011 14:16: Exception Thrown
com.ibm.designer.runtime.domino.adapter.util.PageNotFoundException: Cannot find the module: **xınvolve100.nsf**
at com.ibm.domino.xsp.module.nsf.NSFService.doServiceInternal(NSFService.java:451)
at com.ibm.domino.xsp.module.nsf.NSFService.doService(NSFService.java:352)
at com.ibm.designer.runtime.domino.adapter.LCDEnvironment.doService(LCDEnvironment.java:304)
at com.ibm.designer.runtime.domino.adapter.LCDEnvironment.service(LCDEnvironment.java:261)
at com.ibm.domino.xsp.bridge.http.engine.XspCmdManager.service(XspCmdManager.java:291)

Evet, Türkçe yerel ayarlar ve Java birleşince "**I** " harfini "**ı** " olarak küçülten program modülünün tanıdık esintileri bunlar.

15 yıllık profesyonel IT kariyerimde bu problemin çözüldüğünü görmedim, göreceğimi de sanmıyorum.

Günün özeti şu:

#### "Veritabanı isimlerinde büyük harf '**I**' karakteri kullanmayın. Yabancı yazılım alırken de sorun..."

<br />
