## Workbox Nedir? Ne işe yarar? Nasıl Kullanılır? | Workbox #1

Photo by [Shane Aldendorff](https://unsplash.com/photos/mQHEgroKw2k?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/search/photos/gear?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

Workbox, [Progressive Web Apps](https://developers.google.com/web/progressive-web-apps/) oluştururken [Service Worker](https://developers.google.com/web/fundamentals/primers/service-workers/) ile ilgili işlevler konusunda size yardımcı olan bir JavaScript kütüphaneleri koleksiyonudur.

### Neden Workbox?

Önceden PWA geliştirirken kullanılan [sw-precache](https://github.com/GoogleChromeLabs/sw-precache) & [sw-toolbox](https://github.com/GoogleChromeLabs/sw-toolbox) kütüphanelerine göre daha küçük boyutlu, daha modüler ve işlevsel, aynı zamanda güçlü bir hata ayıklama desteğini beraberinde getiriyor.

### Peki Ne İşe Yarar?

Workbox genel olarak Service Worker’lar aracılığıyla PWA uygulamanızın yaptığı isteklerini ve varlıklarını (CSS, JS, resim dosyaları vb.) çeşitli stratejilere göre istemci tarayıcının Cache Storage’ında tutup uygulamanızı hızlandırmanızı kolaylaştırır aynı zamanda uygulamanızın kötü internet koşullarında yada çevrimdışı iken kullanıcılarınıza en iyi deneyimi sunmanıza yardımcı olur. Google tarafından geliştirilmektedir.

*   Önbellekleme
*   Çalışma zamanı önbellekleme
*   Stratejiler
*   İstek yönlendirme
*   Arkaplan senkronizasyonu
*   Güçlü hata ayıklama
*   sw-precache ve sw-toolbox’dan daha fazla esneklik ve özellik

### Kimler Workbox’ı Kullanıyor?

*   WIRED
*   Pinterest
*   Starbucks
*   Forbes
*   iHeart Radio
*   BBVA
*   Tinder
*   …

### Başlangıç

Çoğu web uygulaması CSS, JavaScript ve resimler içerdiğinden, bir service worker ve Workbox kullanarak bu dosyaları nasıl önbelleğe alabileceğimizi ve sunabileceğimize bakalım.

#### ⚙ Service Worker Dosyası Oluşturma ve Kaydetme

Workbox’ı kullanmadan önce, bir service worker dosyası oluşturmalı ve web uygulamamıza kaydetmeliyiz.

Uygulamanızın kök dizininde `sw.js` adlı bir dosya oluşturarak başlayın ve dosyaya bir konsol mesajı ekleyin. Bu şekilde yüklendiğini görebiliriz.

```
console.log('Hello from sw.js');
```

Web sayfanızda yeni service worker dosyanızı şöyle kayıt edebilirsiniz:

<script>  
// Service Worker destekleniyor mu?  
if ('serviceWorker' in navigator) {  
  // Sayfanın yüklenme performansını düşürmemek için yüklenme tetikleyicisini kullanın  
  window.addEventListener('load', () => {  
    navigator.serviceWorker.register('/sw.js');  
  });  
}  
</script>

Bu, tarayıcıya bunun web uygulaması için kullanılacak service worker olduğunu söyler.

Sayfanızı yenilerseniz, service worker dosyanızdaki log’u göreceksiniz.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1659933278505/gy3YZaxD6.png)

Chrome DevTools’taki “Application” sekmesine baktığınızda service worker’ın kayıtlı olduğunu görmelisiniz.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1659933279626/5C6OS0EmJ.png)

**Not:** Yeni bir service worker geliştirmeyi kolaylaştırmak için “Update on reload” onay kutusuna tıklayın.

Şimdi kayıtlı bir service worker’ımız olduğuna göre, Workbox’ı nasıl kullanabileceğimize bakalım.

### Workbox’a Başlarken

Workbox’ı kullanmaya başlamak için, yalnızca workbox-sw.js dosyasını service worker’a aktarmanız gerekir.

Service worker’ınızı, aşağıdaki importScripts() fonksiyonunu çağıracak şekilde değiştirin.

importScripts('https://storage.googleapis.com/workbox-cdn/releases/3.6.1/workbox-sw.js');  
  
if (workbox) {  
  console.log(\`Yay! Workbox is loaded 🎉\`);  
} else {  
  console.log(\`Boo! Workbox didn't load 😬\`);  
}

Bununla “Yay” mesajını görmelisiniz, böylece Workbox’ın resmen service worker’a yüklendiğini biliyoruz.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1659933280859/_GRHyWI-m.png)

Şimdi Workbox’ı kullanmaya başlayabiliriz.

**Uyarı:** `**workbox-sw.js**`dosyasını içe aktarmak service worker’ınız içerisinde `[**workbox**](https://developers.google.com/web/tools/workbox/modules/workbox-sw)` [](https://developers.google.com/web/tools/workbox/modules/workbox-sw) nesnesi oluşturacak, ve bu özellik, kullandığınız özelliklere bağlı olarak diğer yardımcı kitaplıkları içe aktarmaktan sorumludur. [Service worker spesifikasyonu](https://www.chromestatus.com/feature/5748516353736704)ndaki kısıtlamalar nedeniyle, bu içe aktarma işlemlerinin bir `**install**` event handler içinde veya service worker’ınızın en üst düzey kodunda aynı anda yapılması gerekir. Daha fazla ayrıntı, geçici çözümler ile birlikte`[**workbox-sw**](https://developers.google.com/web/tools/workbox/modules/workbox-sw#avoid_async_imports)` [dökümantasyonu](https://developers.google.com/web/tools/workbox/modules/workbox-sw#avoid_async_imports)nda bulunabilir.

### Workbox’ı Kullanma

Workbox’ın ana özelliklerinden biri, yönlendirme ve önbellekleme stratejisi modülleridir. Web sayfanızdaki istekleri dinlemenizi ve bu isteğin önbelleğe alınması ve yanıtlanması gerekip gerekmediğini ayrıca nasıl yanıtlanacağını belirlemenizi sağlar.

JavaScript dosyalarımıza bir önbellek fallback’i ekleyelim. Bunu yapmanın en kolay yolu, düzenli bir ifadeyle yapabileceğimiz, istenen “.js” dosyalarıyla eşleşecek olan Workbox’a bir rota kaydetmektir:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1659933282007/F7xe-cI2Q.png)

Bu, Workbox’a, bir istek yapıldığında, düzenli ifadenin URL’in bir parçasıyla eşleşip eşleşmediğini görmesi gerektiğini ve bunu yaparsa bu istekle bir şey yapması gerektiğini söyler. Bu yazı için, “bir şeyler yap” ifadesi, isteği Workbox’ın önbellekleme stratejilerinden biri olacak.

JavaScript dosyalarımızın mümkün olduğunca ağdan gelmesini ancak ağ başarısız olursa önbellek sürümünü kulllanmak istiyorsak, bunu yapmak için “network first” stratejisini kullanabiliriz.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1659933283155/kdF7AUdME.png)

Ham hali: [https://gist.github.com/MrPeker/f1a833ec59a2dafda846b7233f321b82](https://gist.github.com/MrPeker/f1a833ec59a2dafda846b7233f321b82)

Bu kodu service worker’ınıza ekleyin ve sayfayı yenileyin. Web sayfanızda JavaScript dosyaları varsa, buna benzer bazı log’lar görmelisiniz:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1659933284373/0e8bR-uG8.png)

Workbox herhangi bir “.js” dosyası için talebi yönlendirdi ve talebe nasıl cevap verileceğini belirlemek için network first stratejisini kullandı. İsteğin gerçekten önbelleğe alınıp alınmadığını kontrol etmek için DevTools’un önbelleklerine bakabilirsiniz.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1659933285483/LReqckyAG.png)

Workbox, kullanabileceğiniz birkaç önbellek stratejisi sunar. Örneğin, CSS’iniz önce önbellekten sunulabilir ve arka planda güncellenebilir veya resimleriniz bir hafta kadar önbelleğe alınabilir ve kullanılabilir, daha sonra güncellenmesi gerekir.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1659933286750/ppYRwVfUm.png)

Ham hali: [https://gist.github.com/MrPeker/00617c8b0f536360600a92270ffa0c96](https://gist.github.com/MrPeker/00617c8b0f536360600a92270ffa0c96)

### 🛠 Workbox API’ı Nasıl?

Aşağıda, geliştiricilerin service worker’lara uyguladıkları ortak yaklaşımların bazılarını gösteren Workbox API’ya birkaç örnek bulunmakta.

#### 📄 Web Uygulamanızdaki Google Fonts’un Önbelleklenmesi

Kullanıcınız uygulamanızı ziyaret ettikten sonra çevrimdışı olduğunda Google Fonts’a güvenmek ister miydiniz? Önbellekten onlara sunmak için basit bir kural ekleyebilirsiniz.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1659933288056/WP3kb3ruH.png)

Ham hali: [https://gist.github.com/MrPeker/a3dec2158c91be91f975ad2c7015ee7d](https://gist.github.com/MrPeker/a3dec2158c91be91f975ad2c7015ee7d)

#### 🔥 JavaScript ve CSS Dosyalarının Önbelleklenmesi

Bir sonraki kullanım için arka planda güncelleyip JS ve CSS varlıklarınızı önbellekten servis ederek daha hızlı hale getirin.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1659933289290/sAILxf3Cc.png)

Ham hali: [https://gist.github.com/MrPeker/8b3a025acd74f243b1a39a550034951d](https://gist.github.com/MrPeker/8b3a025acd74f243b1a39a550034951d)

#### 🌅 Resimlerin Önbelleklenmesi

Resimler bir web sayfasının boyutunun çoğunu oluşturur. Kullanıcılarınızın depolama alanını tüketerek onları **süresiz önbelleklemediğinizden** emin olarak önbellekten hızlı bir şekilde sunmak için bu kuralı kullanabilirsiniz.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1659933290458/vDcLvpF23.png)

Ham hali: [https://gist.github.com/MrPeker/e1ba598b455358d2b73dd887d046a64a](https://gist.github.com/MrPeker/e1ba598b455358d2b73dd887d046a64a)

#### 📈 Çevrimdışı Google Analytics

Çevrimdışı PWA’nız için çevrimdışı analizler mi istiyorsunuz? Sorun değil.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1659933291537/Ent9e4mTn.png)

Ham hali: [https://gist.github.com/MrPeker/68692edf01aa6eaaf2dc759c85f4ca5b](https://gist.github.com/MrPeker/68692edf01aa6eaaf2dc759c85f4ca5b)

Gördüğünüz gibi oldukça kolay ve temiz bir kullanımı var, Workbox kullanmadan bu işlemleri yapmak için yüzlerce satır kod yazmak gerekecekti (Google Dev Summit’in yalancısıyım, “Kaynaklar” bölümünde ilgili sunumu bulabilirsiniz)

Peki her şey iyi, hoş, güzel de şu stratejilerde neyin nesi?

### Workbox Önbellekleme Stratejileri

Çoğu istek, Workbox’ta yerleşik önbellekleme stratejilerinden biriyle ele alınabilir. Özel durumlarda kendi önbellekleme stratejilerinizi de oluşturabilirsiniz.

#### Stale While Revalidate

Bu strateji, bir istek için önbelleğe alınmış bir yanıtı kullanacak ve arka planda önbelleği ağdan gelen bir yanıtla güncelleyecektir. (Önbelleğe alınmamışsa, ağ yanıtını bekleyecek ve onu kullanacaktır). Bu, kullanıcıların önbelleklerini düzenli olarak güncelledikleri anlamına gelen oldukça güvenli bir stratejidir. Bu stratejinin dezavantajı, kullanıcının bant genişliğini kullanarak her zaman ağdan bir varlık talep etmesidir.

**Örnek Kullanım Alanları:**

*   CSS dosyaları
*   JavaScript dosyaları
*   Web uygulamanızdaki gerçek zamanlı olmayan ama sıklıkla güncellenen API sorguları, örneğin haftalık trendler.

#### Network First

Bu, önce ağdan bir istek almaya çalışacaktır. Bir yanıt alırsa, bunu tarayıcıya iletir ve ayrıca bir önbelleğe kaydeder. Ağ isteği başarısız olursa, son önbelleğe alınmış yanıt kullanılacaktır.

**Örnek Kullanım Alanları:**

*   Kullanıcı profilleri
*   Konular
*   Yazılar vb.
*   Bu strateji uygulamanızın internet erişimi olduğu sürece daima kullanıcının güncel veriye erişmesini, çevrimdışı olduğu zamanda en son önbelleklenmiş olan veriyi sunmak istediğiniz durumlarda oldukça kullanışlıdır.

#### Cache First

Bu strateji, önbelleği ilk önce bir yoklar ve varsa bunu kullanır. İstek önbellekte değilse, ağ kullanılacak ve tarayıcıya iletilmeden önce önbelleğe herhangi bir geçerli yanıt eklenecektir.

**Örnek Kullanım Alanları:**

*   Yazı tipi dosyaları
*   Resimler

#### Network Only

Yanıtı ağdan gelmeye zorlar.

**Örnek Kullanım Alanları:**

*   Giriş yapma
*   Kayıt olma
*   Uygulamanızın internet erişimi varken erişilebilir olmasını, önbelleklenmemesini, çevrimdışı durumlarda erişilebilir olma*ma*sını istediğiniz bölümleri

#### Cache Only

Yanıtı önbellekten gelmeye zorlar.

**Örnek Kullanım Alanları:**

*   Tarayıcı bazlı kişiselleştirmeler, örneğin gece modu
*   Önbellekte bulunduğu sürece erişmek istediğiniz, olmaması durumunda edinmeye ihtiyaç duymadığınız veriler

Bu stratejileri, işleyici olarak kullanabilirsiniz:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1659933292694/AuOhyiXJz.png)

Ham hali: [https://gist.github.com/MrPeker/c5c513d11ec4abe76a4e1c8a3f5c14e0](https://gist.github.com/MrPeker/c5c513d11ec4abe76a4e1c8a3f5c14e0)

Herhangi bir stratejiyi kullanırken önbellek adı tanımlayabilir ve/veya eklenti kullanabilirsiniz.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1659933293938/es88DSdij.png)

Ham hali: [https://gist.github.com/MrPeker/0655ba33feb124ca99e7a7d19b1b799f](https://gist.github.com/MrPeker/0655ba33feb124ca99e7a7d19b1b799f)

Bu seçeneklere, istekleri önbelleğe alırken daha güvenli hale getirmek için sık sık ihtiyaç duyulur (yani, önbellekleme sürelerinin sınırlandırılması veya bir cihazda kullanılan verilerin sınırlı olduğundan emin olunması).

### İsteğin Özel Bir Strateji İle Yönetilmesi

İsteğinize kendi stratejinizle farklı bir talebe cevap vermek istediğiniz ya da basitçe talep edilen service worker tarafından şablonlama yaparak üretmek istediğiniz senaryolar olabilir. Bunun için bir işlev sunabilirsiniz ve bu, url ve FetchEvent isteklerini içeren bir nesne ile çağrılır.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1659933295040/nKspXisi7.png)

Ham hali: [https://gist.github.com/MrPeker/e218c6fd517c2b3c94a1286b22092c9f](https://gist.github.com/MrPeker/e218c6fd517c2b3c94a1286b22092c9f)

Unutulmaması gereken şey, `match`callback’inde bir değer döndürürseniz, `handler`callback’ine `params` argümanı olarak geçirileceğidir.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1659933296213/8ECk8DMVu.png)

Ham hali: [https://gist.github.com/MrPeker/619bfa1c95115c6210e70cc2ce33d178](https://gist.github.com/MrPeker/619bfa1c95115c6210e70cc2ce33d178)

URL’de, *match* callback’inde bir kez ayrıştırılabilecek ve *handler*’ınızda kullanılabilecek bilgi parçaları varsa, bu yararlı olabilir.

#### Kaynaklar:

Workbox konusunda yararlı bir yazı, göz atmanızı öneririm:

[**A 5 minute intro to Workbox 3.0**  
*Workbox is a collection of JavaScript libraries that help you with service worker related functionalities when you’re…*medium.com](https://medium.com/google-developer-experts/a-5-minute-intro-to-workbox-3-0-156803952b3e "https://medium.com/google-developer-experts/a-5-minute-intro-to-workbox-3-0-156803952b3e")[](https://medium.com/google-developer-experts/a-5-minute-intro-to-workbox-3-0-156803952b3e)

[**Workbox | Google Developers**  
*Workbox is a set of service worker libraries that making build progressive web apps easy.*developers.google.com](https://developers.google.com/web/tools/workbox/ "https://developers.google.com/web/tools/workbox/")[](https://developers.google.com/web/tools/workbox/)

[**Get Started | Workbox | Google Developers**  
*Get Started with Workbox.*developers.google.com](https://developers.google.com/web/tools/workbox/guides/get-started "https://developers.google.com/web/tools/workbox/guides/get-started")[](https://developers.google.com/web/tools/workbox/guides/get-started)

[**Route Requests | Workbox | Google Developers**  
*A guide on how to route requests with Workbox.*developers.google.com](https://developers.google.com/web/tools/workbox/guides/route-requests "https://developers.google.com/web/tools/workbox/guides/route-requests")[](https://developers.google.com/web/tools/workbox/guides/route-requests)

### Chrome Dev Summit 2017 Workbox Sunumu:

<iframe src="https://www.youtube.com/embed/DtuJ55tmjps?feature=oembed" width="700" height="393" frameborder="0" scrolling="no"></iframe>

Sunum İngilizce, İngilizce altyazı var.

Bu sunumda Jeff Posnick, Workbox’ın önbellekleme stratejileri, ön-önbellekleme (precaching) ve gezinme isteklerini yönetme konusundaki desteğine genel bir bakış sunuyor. Pinterest ve WIRED gibi şirketlerin Workbox’ı canlıda nasıl kullandıklarına dair gerçek dünya örnekleriyle dolu.

Workbox’a genel olarak baktık, birkaç örnek ile ne işe yaradığına dair zihnimizde bir şeyler oluştu. Bu Workbox üzerine olacak bir serisinin ilk yazısıydı, umarım size bir şeyler katabilmişimdir.

Sorcial’ı geliştirirken karşılaştığımız maceraları yazıya dökeceğimiz bu blogu takip edebilirsiniz :)

Hoşunuza gittiyse birkaç 👏 fena olmaz gibi :)

Sorularınız ve fikirleriniz bizim için değerli, yorum atarak bildirirseniz seviniriz.

Bana ulaşmak için Sorcial profilime göz atabilirsiniz:

[**Mehmet Ali Peker 👨‍💻 | Sorcial**  
*Head of Dev. at @sorcial & @acafine With Sorcial, you can publish all your social media links on your profile page and…*sorcial.com](https://sorcial.com/mr "https://sorcial.com/mr")[](https://sorcial.com/mr)

### 👋 ***Hoşçakalın***