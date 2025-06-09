---
authors:
  - serdar

title: "Ekspress lisanslamada kümeleme (cluster) desteği..."

slug: ekspress-lisanslamada-kumeleme-cluster-destegi...

date: 2010-12-09T18:12:29+02:00

---

Lotus Domino sunucularda cluster yaratmak çok basit. Yarattığınız aktif/pasif cluster sunucularla sunucularınızı daha verimli kullanabilir, yüksek erişilebilirlik sağlayabilir, felaket anlarında süreklilik sağlayabilirsiniz.
<!-- more -->
Sistem basit. Aralarında hızlı bir ağ bağlantısı bulunan iki sunucuyu bir cluster olarak tanımlıyorsunuz. Bu cluster'a dahil etmek istediğiniz veritabanlarını seçiyorsunuz. Sunucu bu veritabanlarında yapılan güncelleme işlemlerini anında diğer sunucuya aktarıyor. Lotus Notes istemcileri de bağlı oldukları sunucuların cluster bilgilerini bir kenara yazıyor. Eğer çalışılan sunucu cevap vermiyorsa ya da çok yoğunsa (neye göre ayarladıysanız) diğer sunucuya geçiş yapıyor.

Cluster tanımladıktan sonra kullanıcıların yarısının 'home server'larını diğer sunucuya yönlendirirseniz alın size güzel bir yük dengeleme metodu. Bu iki sunucunun önüne bir de ICM (Internet cluster manager) kurarsanız benzer özellikleri web uygulamaları için de kullanabilirsiniz.

Dilerseniz ikinci sunucuyu pasif tutarsınız. Kullanıcılar yalnızca ilk sunucu çökerse burayı kullanırlar. Bu sayede, örneğin dilediğiniz zaman ikinci sunucuyu kapatıp yedek alabilirsiniz. İkinci sunucuyu analiz, raporlama ya da çok CPU tüketen agent'lar için kullanabilirsiniz.

Yaratıcılığın sınırı yok :)

Daha önce Cluster mekanizması ekspress lisanslı kullanıcılarda desteklenmiyordu. Şimdi, resmi açıklama da geldi; artık mümkün.

1 Ocak 2011 itibariyle Domino Collaboration Express lisansına sahip şirketler cluster desteğinden faydalanabiliyor olacaklar. Resmi duyuru [burada](http://www-01.ibm.com/common/ssi/ShowDoc.jsp?docURL=/common/ssi/rep_ca/2/631/ENUS310-292/index.html&breadCrum%C3%9ET001PT022&url=buttonpressed%C3%9ET002PT005&specific_index%C3%9ET001PEF502&DET015PGL002%C3%9ET001PEF011&submit.x=7&submit.y=8&lang=en_US)...
