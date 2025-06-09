---
authors:
  - serdar

title: "Domino'yu alt versiyona geçirdikten sonra çıkan XPages sorunu..."

slug: dominoyu-alt-versiyona-gecirdikten-sonra-cikan-xpages-sorunu...

date: 2011-02-27T16:29:45+02:00

---

Bir sunucuyu Domino 8.5.2'den 8.5.1 versiyonuna indiriyoruz. Biraz aptalca bir sebebimiz var, çünkü Lotus Quickr 8.5.1 eski versiyonu kullanabiliyor.

Hep upgrade'lerde problem olmayacak ya, bu sefer de downgrade problemi oldu. XPages sayfalarında Dojo problemleri oluşmaya başladı. Problemi ilk farketmem tarih alanlarındaki takvim ikonunun kaybolması...
<!-- more -->
Test sunucusuyla karşılaştırınca bir şey farkettim: hatalı XPage'ler dojo objelerini 'dojo-1.4.3' klasöründen alıyorlar. Bu son dojo versiyonu 8.5.2 ile geliyor.

Problem şu: HTTP çalışırken en son Dojo versiyonu hangisiyse onu kullanıyor. XPages ayarlarında '8.5.1 versiyonunu kullan' demeniz bir işe yaramıyor. Sunucudaki 'domino/js' klasörüne bakınca üç dojo versiyonunun da olduğunu görüyoruz: '**dojo-1.3.2** ', '**dojo-1.3.3** ' ve '**dojo-1.4.3** '. Domino 8.5.1 ile gelen dojo-1.3.2 varsayılan versiyon. Ben de geri kalan iki klasörü sildim, HTTP görevini tekrar başlattım ve şimdi, olması gerektiği gibi çalışıyor...

Downgrade, normalde tüm klasörleri boşaltmaz. Belki uygulamayı kaldırsak ve tekrar kursak bu problem olmazdı ama alışkanlık işte...
