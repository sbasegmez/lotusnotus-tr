---
authors:
  - serdar

title: "Lotus Notes 8.5.1 Yeni Kullanıcılarda Password Policy Sorunu"

slug: lotus-notes-8.5.1-password-policy-sorunu

date: 2010-02-23T18:46:03+02:00

---

Bugün bir müşterimde karşılaştığım problemden sonra okuyucularımı da bilgilendireyim dedim.

Lotus Notes 8.5.1 kullanıyorsanız ve kullanıcılarınızı security policy ile yaratıyorsanız, yeni kullanıcılarla kurulum sırasında problem yaşayabilirsiniz.

Client kurulumu sonrasında konfigürasyon sihirbazı sırasında ID şifresi sorulduktan sonra "**Your password has expired. You cannot access this server until you change it.** " hatası alıyoruz. Sorun muhtemelen ID vault'a aktarılan ID dosyasının expired olması. ID şifresinin değiştirilmesi için client kurulumunun tamamlanması gerekiyor. Fakat sihirbaz tamamlanamayınca bu da gerçekleşmiyor.

Sorunu çözmek için öncelikle kurulumu temizlememiz gerekiyor. Notes.ini dosyasını beşinci satırdan itibaren temizlemek yeterli olacaktır.

Daha sonra client için FP1 yüklüyor ve konfigürasyon sihirbazını baştan başlatıyoruz.

Alternatif olarak security policy'yi registration sırasında uygulamamak çözüm olabilir fakat bu bana pek pratik gelmiyor.

Hata 8.5.2 versiyonunda da düzelmiş olacak. Technote'un [linki](http://www.ibm.com/support/docview.wss?uid=swg21413465) burada...
