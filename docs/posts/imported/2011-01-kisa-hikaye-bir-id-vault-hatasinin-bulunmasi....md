---
authors:
  - serdar

title: "Kısa hikaye: Bir ID Vault hatasının bulunması..."

slug: kisa-hikaye-bir-id-vault-hatasinin-bulunmasi...

date: 2011-01-12T17:00:43+02:00

---

Müşterilerimde uğraştığım garip problemlerle ilgili yazı yazmayı seviyorum. Umarım bu tip yazılar yeni başlayan admin'ler için bu tip sorunlarla nasıl uğraşılması gerektiğine yönelik ipuçları verir :)
<!-- more -->
Bugün biraz sohbet için bir müşterime uğradım. Bir kaç hafta önce Domino Portal arasındaki bir SSO problemiyle uğraşmıştık. Görünen o ki, SSO işlemlerinden sonra ID Vault'un şifre resetleme işlemleri çalışmamaya başlamış. Bu iki konu arasında herhangi bir bağlantı olamayaca ğını söyledim ve bundan epey emindim :)

Geçen yıl blog'daki en popüler yazım ID Vault sorunlarıyla ilgili olanıydı. Bunun sebebi çok açık: Bazı 'olsa ne güzel olur' özellikler vardır. İnsanlar bu özellikleri test ederler ve bir problem çıkarsa boşverirler. Ama ID Vault vazgeçilemeyecek kadar iyi bir özellik.

Bu problem için de klasik bir sorundur diye düşünüyordum. Public key'lerden ACL ayarlarına kadar herşeyi kontrol ettim, sorun yoktu. Çapraz sertifikasyonları tekrar yarattım, değişik kullanıcıları denedim, aynen devam. ID vault klasik hatasını veriyordu: "**Missing or invalid Password Reset Trust certificate from 'XXX' to 'YYY': Note Item not found** ".

Aslında burada bir farklılık olduğunu gördüm. Klasik hata, '**Entry not found in Index** ' diye biterdi. Çünkü normalde bu tip hatalar gerekli bir dokümanın bulunamamasından ya da kullanıcı kaydına erişememekten oluşurdu.

Ben de bir kaç debug parametresini açtım (Debug_IDV_TrustCert=1; Debug_Namelookup=1) ve problem net bir şekilde göründü :)

Password reset operasyonu için 'reset' yapabilecek her kullanıcı için ayrı bir sertifikasyon dokümanı bulunur. Örneğin sistem yöneticisi (John May/Acme) bir kullanıcının (Mary Jane/Acme) şifresini değiştirecekse, o sistem yöneticisi için bir çapraz sertifika dokümanı (O=Acme \>\> John May/Acme) bulunmalı. Server önce bunu bulacak, daha sonra da organizasyon sertifikasını (certifier) bulup onu karşılaştıracak:

```
[0B30:009A-0CC4] NAMELookup::<lookup> Searching view '($Users)' (1 of 1 views).
[0B30:009A-0CC4] NAMELookup::<lookup> Searching name='O=Acme' (1 of 1 names).
[0B30:009A-0CC4] NAMELookup::<lookup> Searching DBIndex=1.
[0B30:009A-0CC4] NAMELookup::<lookup> NumReturned=0, TotalNumReturned=0 match(es) for name='O=Acme'
```

<br />

<br />

Bu durumda, certifier bulunamıyor (entry not found in index). Ama bizim durumumuzda:

```
[0B30:009A-0CC4] NAMELookup::<lookup> Searching view '($Users)' (1 of 1 views).
[0B30:009A-0CC4] NAMELookup::<lookup> Searching name='O=Acme' (1 of 1 names).
[0B30:009A-0CC4] NAMELookup::<lookup> Searching DBIndex=1.
[0B30:009A-0CC4] NAMELookup::<lookup> NumReturned=2, TotalNumReturned=2 match(es) for name='O=Acme'
```

<br />

<br />

Adres defterinde iki adet sertifika dokümanı bulunuyor ki bunun olmamas ı lazım. Hemen '($Users)' görüntüsüne bakıyoruz ve gerçekten iki tane var. İkincisi 'Short Name' alanında 'O=Acme' yazan bir kullanıcı. Bu bir 'replication conflict' de olabilirdi...

Muhtemelen SSO sırasında bir hata yaptık, fazladan bir enter koyduk. Certifier isminizi bir kullanıcıya 'alias' olarak tanımlamak ölümcül bir hata aslında :)

Neyse, biraz yüzüm kızardı ama problemi çözmüş olduk...
