# 🚀 Apollo CR3BP — Kısıtlı Üç-Cisim Yörünge Simülasyonu

Bu proje; Dünya, Ay ve bir uzay aracı arasındaki kütleçekim dinamiklerini modelleyen, **Kısıtlı Dairesel Üç-Cisim Problemi (CR3BP)** tabanlı interaktif bir astrodinamik simülasyonudur.

Herhangi bir harici grafik veya fizik kütüphanesi kullanılmadan; saf JavaScript (Vanilla JS) ve HTML5 Canvas API ile tek dosya üzerinden geliştirilmiştir.

---

## 📌 Projenin Amacı ve Kapsamı

İki cisimli Kepler modelleri, birden fazla kütleçekim kuyusunun bulunduğu ortamlarda yetersiz kalır. Bu projede:
* Uzay aracının hem Dünya hem de hareketli Ay kütleçekimi altındaki bileşke ivmesi,
* Doğru bir Ay transferi (TLI) için fırlatma zamanlaması (faz açısı / lead angle),
* Ay etrafında stabil bir yörüngeye oturmak için gereken otonom frenleme (LOI - Lunar Orbit Insertion) manevrası,
* Sayısal entegrasyonda enerji korunumunu sağlayan algoritmalar görselleştirilmiştir.

---

## 🧮 Astrodinamik ve Fiziksel Modelleme

### 1. Kısıtlı Üç-Cisim Problemi (CR3BP)
Uzay aracının kütlesi ihmal edilebilir kabul edilir ($m \ll M_{Moon} < M_{Earth}$). Aracın maruz kaldığı net ivme, iki gök cisminin çekim ivmelerinin vektörel toplamıdır:

$$\vec{a}_{net} = -\frac{\mu_E}{|\vec{r} - \vec{r}_E|^3}(\vec{r} - \vec{r}_E) - \frac{\mu_M}{|\vec{r} - \vec{r}_M|^3}(\vec{r} - \vec{r}_M)$$

* $\mu_E \approx 3.986 \times 10^{14} \text{ m}^3/\text{s}^2$ (Dünya Çekim Parametresi)
* $\mu_M \approx 4.904 \times 10^{12} \text{ m}^3/\text{s}^2$ (Ay Çekim Parametresi)

### 2. Ortak Kütle Merkezi (Barycenter)
Sistem, Dünya merkezinden yaklaşık 4.671 km uzaklıkta bulunan ortak kütle merkezi etrafında döner:

$$R_{bary} = D_{EM} \cdot \left(\frac{M_M}{M_E + M_M}\right) \approx 4{,}671 \text{ km}$$

Bu merkez Dünya yüzeyinin altında kaldığı için Dünya uzayda sabit durmaz; ortak kütle merkezi etrafında hafif bir yalpalama hareketi sergiler.

### 3. Euler-Cromer Sayısal Entegrasyonu
Klasik açık Euler yöntemi enerji korunumunu sağlayamadığı için yörüngelerde yapay sapmalara yol açar. Simülasyonda semi-implicit yapıda çalışan **Euler-Cromer** yöntemi ve alt adımlama (*sub-stepping: dt = 0.25 s*) kullanılmıştır:

$$v(t + \Delta t) = v(t) + a(t) \cdot \Delta t$$
$$x(t + \Delta t) = x(t) + v(t + \Delta t) \cdot \Delta t$$

### 4. TLI ve Faz Açısı Zamanlaması
Translunar Injection (TLI) hızı yaklaşık $10.83 \text{ km/s}$ olarak ayarlanmıştır. Aracın Ay mesafesine ulaşması ~3 gün sürer. Bu süreçte Ay da açısal olarak ilerleyeceği için Ay, fırlatma anında buluşma noktasının gerisinde (3. bölge, $\approx 220^\circ$) başlatılmıştır.

### 5. LOI (Lunar Orbit Insertion) Frenlemesi
Araç Ay'a 9.000 km yaklaştığında teğetsel hız vektörü tersine işletilerek Ay'ın dairesel yörünge hızına ($v = \sqrt{\mu_M / r}$) eşitlenir ve stabil bir Ay uydusu haline gelir.

---

## 🛠️ Teknik Özellikler

* **Çekirdek:** Saf JavaScript (ES6+), HTML5 Canvas
* **Görsel Efektler:** Radyal gradyan atmosfer parlaması, dinamik şeffaflaşan yörünge izi ve derin uzay yıldız alanı
* **Arayüz:** Gerçek zamanlı telemetri paneli ve dahili dokümantasyon modalı
* **Dağıtım:** Bağımlılıksız (Zero-dependency), GitHub Pages uyumlu

---

## 💻 Canlı Demo ve Çalıştırma

* **Canlı Simülasyon:** `https://<kullanici-adiniz>.github.io/<repo-adiniz>/`
* **Yerel Çalıştırma:** Projeyi indirip `index.html` dosyasını herhangi bir web tarayıcısında çift tıklayarak açabilirsiniz.

---

## 🧠 Geliştirme Yaklaşımı

Bu proje, astrodinamik kurallarının kod tabanına dönüştürülmesi sürecinde problem analizi, hata tespiti (orbital rezonans, faz açısı kaymaları, integrasyon kararlılığı) ve yönlendirmelerin insan vizyonuyla yapıldığı; kod iskeletinin yapay zeka eşli programlama (*AI pair-programming*) desteğiyle oluşturulduğu bir mühendislik çalışmasıdır.
