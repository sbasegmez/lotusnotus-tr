---
authors:
  - serdar

title: "Smart Upgrade paketi oluştururken Türkçe dil sorunu"

slug: smart-upgrade-paketi-olustururken-dil-sorunu

date: 2010-04-10T18:50:51+02:00

---

[](2010-01-lotus-notes-8.5.1-kurulum-problemi.md "Lotus Notes 8.5.1 Kurulum Problemi")Lotus Notes 8.5.1 Kurulum Problemi başlığında bahsetmiş olduğumuz bir problem vardı. Hafta sonu bir upgrade projesi esnasında bu problemle tekrar karşılaştım, fakat farklı bir şekilde.

Hatırlarsanız kurulum uygulaması Türkçe dili seçilmiş işletim sistemlerinde doğrudan Türkçe diliyle açılmayı deniyor ve çalışmıyordu. Biz bu sorunu setup.ini dosyasında küçük bir değişiklik yaparak aşmış ve kullanıcıya dil seçeneğinin sorulmasını sağlamıştık.

Smart Upgrade ya da başka bir yöntemle upgrade işlemlerini otomatikleştirmek istediğimizde 'silent install' seçeneğini kullanmayı tercih ediyoruz. Bu sayede kullanıcıya herhangi bir kontrol olanağı vermeden kurulumu sorunsuz halledebiliyoruz. Fakat aynı hatadan dolayı kurulum gene başarısız oluyor.

Bu sorunu çözmek için epey uğraştıktan sonra;

setup **/L"0x409"** /s ...

parametresiyle kurulumun otomatikman İngilizce başlamasını sağladık. Umarım faydası dokunur.
