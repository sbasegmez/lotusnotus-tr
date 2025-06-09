---
authors:
  - serdar

title: "Lotus Workflow: Efsane Geri Dönecek mi?"

slug: lotus-workflow-efsane-geri-donecek-mi

date: 2010-02-21T12:42:14+02:00

---

2002 yılında kendim için sürpriz bir kararla iş değiştirmiş ve Superonline'da MIS uzmanı olarak yeni bir kariyere başlamaya karar vermiştim. Çeşitli nedenlerle bu işte yalnızca bir sene kaldım ve 2003'te kendi işimi kurarak girişimcilik dünyasına adım attım. Superonline'da işe başladığım hafta [**SWAP**](http://www.developi.com/tr/projects.asp?section=swap)(Superonline Workflow Automation Platform) projesinin içine 'düştüm'.

SWAP, Lotus Workflow ile form-bazlı akışların web ortamına aktarılmasını amaçlayan önemli bir projeydi. İlk fazı bir ayda bitirerek basit bir arabirimle açtığımız SWAP, kısa sürede Superonline'ın belkemiği uygulamalarından birisi haline geldi. Kullanıcı kabullenmesiyle ilgili problemler yaşıyorduk ve bunların ağırlıklı olarak kullanıcı arabiriminden kaynaklandığını farkediyorduk.

İlk fazın ardından kapandık ve Lotus Workflow'u baştan yazmaya karar verdik. Bir kaç temel problem farkediyorduk.
<!-- more -->
1) Kullanıcı arabirimi çok kötüydü. Arabirim R5 versiyonundan kalmaydı. Domino'nun standart Java action'ları, outline objeleri ve view görünümleri hem yavaş, hem de kullanışsız bir deneyim sunuyordu. Bu yüzden arabirimi profesyonel bir web geliştirme ekibiyle sıfırdan yazdık. Javascript ile derli toplu bir UI kütüphanesi oluşturduk.

2) Workflow Engine üzerinde bir takım varsayımsal sorunlar bulunuyordu. Örneğin işi başlatan kişi işe bir isim vermek durumundaydı. İşler belirli bir numaralama uygulanmadan yaratılıyordu ve evrak bağlantılarında problemler oluşuyordu. Tüm bunların yanında ufak tefek bug'lar da tespit ediyorduk. Yeni versiyonda engine üzerinde onlarca düzeltme yaptık. Bu düzeltmeleri ne kadar kolay yaptığımızı farkettikçe daha çok geliştirme yapıyorduk.

3) Organizasyonla ilgili kabuller Türk şirketlerine uymuyordu. Gevşek bir matris organizasyon yapısı sunan LWF, bizim değişken hiyerarşik yapımızda sürekli problemler çıkartıyordu. Son olarak organizasyon yapısını geniş ve değişken hiyerarşileri destekleyecek şekilde yeniden modelledik.

İki ay içerisinde LWF üzerinde özelleştirmediğimiz bölüm bırakmamıştık. Projenin ismi de "*SWAP Next Generation* " olarak belirlendi. Süreç sahibi olarak adlandırdığımız ve orta kademe yöneticilerden oluşan geniş bir ekibin de desteğiyle harika bir proje ortaya çıktı. Öyle ki yeni bir akışın sisteme entegre edilmesi 2-3 gün gibi rekor sürelerde gerçekleştiriliyordu. Superonline bünyesinde her yıl gerçekleşen yapısal organizasyon değişikliklerine bile uygulama yapısına dokunmamıza gerek kalmadan adapte oluyorduk.

Superonline'dan ayrıldıktan sonra kendi şirketim üzerinden SWAP üzerinde çalışmaya devam ettim. Geçen yıl Superonline'ın Tellcom'a devrinden sonra SWAP, 7 yaşını doldurarak kapandı. Uygulamanın kullanıcı gözündeki başarısı o kadar yüksekti ki, halen eski Superonline çalışanları tarafından referans gösterilmekteyiz. Ara zamanda kapatılıp açılanlarla 60 civarında iş akışı yürüten uygulamanın başarısında Lotus Workflow'un esnek ve güçlü yapısının yanında SWAP'ın aldığı üst düzey yönetim desteğinin de önemli payı olmuştur.

Çok güçlü bir yapıya sahip Workflow motoru pek çok noktada özelleştirilebilmektedir. Bir çok parçası açık kod olarak tasarlandığından özelleştirmeler ürünün çekirdek yapısıyla çelişmeyecek şekilde gerçekleştirilebilmektedir. Zaman içerisinde benzer iş akışı platformları oluşturmaya çalışsam da LWF kadar esnek ve sağlam bir motor yazmanın çok zor olduğunu söyleyebilirim.

Lotus Workflow 7 versiyonundan sonra minor/major hiç bir geliştirme görmemesi tüm müşterilerde '*acaba tedavülden kalkacak mı* ' kaygısı yaratmıştı. Her IBM toplantısında bu ürünün geleceğini sorguladık ve aldığımız cevap netti: "*Lotus Workflow çok önemli bir ürün. Kaldırmayı düşünmüyoruz. Yeni versiyon yakında çıkacak...* ". Küçük kardeşi Domino.Doc'un portföyden çıkacağı ve Lotus Quickr tarafından ikame edileceği anlaşıldığında bu kaygılar iyice artmıştı.

Son Lotussphere organizasyonundan çıkan haberlerse umut verici. Kesin olmamakla birlikte Lotus Workflow'a güçlü bir **Java API** yazılmakta olduğu söyleniyor. Bu yeni API sayesinde arabirimin **XPages** , **Portal** ve **Composite Applications** üzerinden kullanılabileceği söyleniyor. Güçlü iş akışı motoru da yeni Domino mimarisine göre tekrar şekillendirilecek muhtemelen.

Bunlar yalnızca ayaküstü konuşmalardan gelen duyumlar. Fakat Lotus Workflow 7 Nisan ayı itibariyle son dönemece giriyor ve tahmin ediyorum bu tarihe kadar resmi açıklama gelir.

Segmentinde rakipsiz ve alternatifsiz olan Lotus Workflow, Lotus yazılımları arasında efsanevi bir yere sahiptir. Umarım yakın zamanda efsane geri döner...
