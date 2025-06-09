---
authors:
  - serdar

title: "Disclaimer Ekleme ve Mesajlarda Türkçe Karakter Sorunları"

slug: disclaimer-ekleme-ve-mesajlarda-turkce-karakter-sorunlari

date: 2010-04-02T16:07:35+02:00

---

Bir süre önce müşterilerden birinden ilginç bir hata gelmişti. Müşterinin sistemi çok kompleks olduğundan (DAMO/POP3/IMAP/iNotes/Notes Client opsiyonlarından tamamını kullanıyorlar) problemi çözmek biraz vaktimi almıştı.

Problem, bazı mesajlarda Türkçe isimli çalışanların gönderen alanında Türkçe karakterler bozulması olarak geldi. Yani benim attığım mesajlarda:

**From: Serdar Başeğmez**

yerine

**From: Serdar Ba?e?mez**

gibi bir görüntü oluşuyordu.

<!-- more -->
Biraz daha karıştırınca sorunun konu alanında da tekrarlandığını ama her zaman olmadığını gördük. Biraz daha fazla karıştırınca sorunu tekrar etmeyi başardık. Mesajın 'header' kısmında (From, To, CC, BCC, Subject, vs.) Türkçe karakter varsa fakat 'body' kısmında yoksa Türkçe karakterler bozuluyordu. Giden mesajın header alanlarının sunucuda **router görevi tarafından** değiştirildiğini farkettik. Örneğin normalde;

**Subject: =?windows-1254?Q?Denemeþþþþþ?=**

olarak kodlanması gereken konu satırı (encoding tipi ve sonrasında ş harfi yerine geçen 'þ' kodu) bozulan mesajlarda şöyle bir satır oluşuyor:

**Subject: =?windows-1252?Q?Deneme=3F=3F=3F?=**

Windows-1254 Türkçe kodlama, 1252 ise ingilizce kodlamayı temsil ediyor. Bu yüzden de mesaj bozuk görünüyor. Uzun çabalardan sonra sorunun nereden kaynaklandığını bulmuştuk. Disclaimer ekleme seçeneğini konfigürasyon dokümanında iptal ettiğimizde sorun düzeldi.

O gün için problemi müşterinin karmaşık yapıdaki ortamına bağlamıştım. Fakat bugün problemi ben de yaşayınca buraya yazmak istedim.

Disclaimer ekleme iki şekilde gerçekleşebilir: Server üzerinde ya da client üzerinde. Dolayısıyla konfigürasyon dokümanında bu seçeneği kaldırarak disclaimer seçeneğini iptal etmiş olmuyorsunuz. Yine mail policy üzerinden "Notes Client can add disclaimers" seçeneğini kullanabilirsiniz. Bu şekilde Lotus Notes, mesajı gönderirken disclaimer'ı mesajın altına ekleyecektir.

Sorunu 8.5, 8.5.1.x versiyonlarında tekrarlayabildim. Başka versiyonlarda aynı problemi yaşarsanız yorum yaparak paylaşabilirsiniz.
