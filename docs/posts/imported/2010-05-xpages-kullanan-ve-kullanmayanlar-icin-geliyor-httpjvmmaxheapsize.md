---
authors:
  - serdar

title: "XPages Kullanan ve Kullanmayanlar için geliyor: HTTPJVMMaxHeapSize"

slug: xpages-kullanan-ve-kullanmayanlar-icin-geliyor-httpjvmmaxheapsize

date: 2010-05-26T11:18:15+02:00

---

Geçen hafta IBM'in yayınladığı önemli bir [technote](http://www-01.ibm.com/support/docview.wss?uid=swg21377202) var...

Özellikle sunucuda kısıtlı hafızalarla uğraşan sistem yöneticileri Java Virtual Machine tarafından kullanılan hafıza miktarıyla oynayabiliyorlar. Daha önemlisi bu hafıza miktarı 8.5.2 itibariyle düşürülüyor. Bu yüzden önceden önlem almak iyidir...
<!-- more -->
8.5.1 itibariyle HTTPJVMMaxHeapSize notes.ini parametresi kullanılabilir durumda. 32-bitlik işletim sistemi kullanan ve hafıza kullanımı 2GB sınırına dayanan (32-bit için sınır değer) sunucularda bu parametreyle oynanması gerekebilir. Daha önceki versiyonlarda bu değer 64 MB iken, 8.5.1 versiyonunda 256 MB oldu. Bu da versiyon yükseltme sonrası performans sorunu yaratabilir.

Eğer XPages kullanmıyorsanız, varsayılan olarak 256 MB olan bu değeri 64 MB'a çekerek önemli bir kazanç elde edebilirsiniz. Bunun için notes.ini'ye "HTTPJVMMaxHeapSize=64M" satırını eklemelisiniz/güncellemelisiniz.

Eğer XPages kullanıyorsanız bu parametreyi yine de 256 MB olarak ayarlayın. Çünkü 8.5.2'de bu değer varsayılan olarak 64 MB'a çekilecek, bu da olası bir versiyon geçişinde XPages uygulamalarında yavaşlığa neden olacaktır.

Notes.ini parametresini değiştirdikten sonra HTTP işlemini yeniden başlatmanız gerekir.

Eğer Java gibi bir altyapı kullanıyorsanız yüksek hafıza gereksinimi içerisindesiniz demektir. Bu tip sunucuları mutlaka 64 bit altına geçirmenizi tavsiye ederim. Bildiğiniz gibi 32-bit sunucular belirli bir hafızanın üzerini adresleyemezler. Dolayısıyla hafızanın arttırılması, belirli bir limitten sonra performans geliştirmesi sunmayacaktır.

Bir öneri daha: Eğer XPages kullanıyorsanız Lotus Domino sunucunuzu sürekli son sürümde (Fix Pack'ler de dahil) tutun. Yeni bir teknoloji olduğundan sürekli düzeltme ve geliştirmeler yapılıyor. Örneğin 8.5 ile 8.5.1 arasında performans ve ölçeklendirme adına inanılmaz farklılıklar var.
