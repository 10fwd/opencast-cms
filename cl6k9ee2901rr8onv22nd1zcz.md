## 5 Dakikada CSS Değişkenlerini Öğren!

#### Nasıl başlayacağınızı gösteren hızlı bir eğitim.

Yazıya başlamadan önce belirtmek isterim ki bu yazı [https://medium.freecodecamp.org/learn-css-variables-in-5-minutes-80cf63b4025d](https://medium.freecodecamp.org/learn-css-variables-in-5-minutes-80cf63b4025d) bu adresteki yazının tarafımca Türkçe çevirisidir. İngilizce okumak isterseniz linke tıklayabilirsiniz.

Evet başlayalım :)

CSS Özel Özellikler (CSS Custom Properties) (ayrıca değişkenler olarak bilinir) front-end geliştiriciler için büyük bir kazançtır. Bu değişkenlerin gücünü CSS’e getirir, daha az tekrarlama, daha iyi okunabilirlik ve daha fazla esneklik ile sonuçlanır.

Ayrıca, CSS önişlemcilerinin değişkenlerinden farklı olarak, CSS değişkenleri, aslında bir çok yararı olan DOM’un bir parçasıdır. Bu nedenle, aslında steroidler üzerindeki SASS ve LESS değişkenleri gibiler. Bu yazıda, bu yeni teknolojinin nasıl çalıştığına dair yoğun kurs vereceğim.

### **Niçin CSS Değişkenleri öğrenmeliyiz?**

CSS’de değişkenleri kullanmak için bir çok neden var. En ilgi çekici olanlarından biri stil sayfalarınızdaki tekrarlamayı azaltıyor olmasıdır.

The old way: Eski Yol, Your main red color: Senin ana kırmızı rengin

Yukarıdaki örnekte, #ffeead rengini için tekrarlamak yerine bir değişken oluşturmak daha iyidir, burada yaptığımız gibi:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1659933243097/GHZdI00Ay.png)

The new way: Yeni yol, Declaring a variable: Değişken tanımlama, Referencing it: Referans olarak

Bu sadece kodunu daha okuması kolay yapmakla kalıyor, aynı zamanda bu rengi değiştirmek istediğinizde size daha fazla esneklik kazandırır.

Bu SASS ve LESS değişkenleri ile yıllardır mümkündü. Şimdi bununla birlikte CSS Değişkenlerinin birkaç büyük yararı var.

1.  Tarayıcıya özgü olduğu için herhangi bir dönüştürücü (transpiling) çalışması gerekmez. SASS ve LESS ile yaptığımız gibi başlangıç için herhangi bir kuruluma ihtiyaç yok.
2.  DOM’da yaşıyorlar, bu da makalede ve orjinal yazının yazarının yaklaşmakta olan dersinde geçireceği bir ton fayda sağlamaktadır.

Şimdi CSS değişkenleri öğrenmeye başlayalım!

### İlk CSS Değişkenini tanımlama

Değişken tanımlamak için öncelikle değişkenin hangi etki alanı (scope) nda yaşaması gerektiğini belirlemelisin. Eğer istersen global bir şekilde erişebilir yapabilirsin, basitçe değişkenini pseudo sınıfı olan :root da tanımla. Belge ağacınızın kök öğesiyle eşleşir (genellikle <html> etiketi).

Değişkenler devralınca, tüm DOM öğeleriniz <html> etiketinin soyundan olduğu için değişkeninizi uygulamanızın tamamında kullanılabilir hale getirecektir.

:root {  
  --main-color: #ff6f69;  
}

Görebildiğiniz gibi, herhangi bir CSS özelliğini ayarladığınız gibi bir değişkeni bildirirsiniz. Bununla birlikte, değişken iki çizgi ile başlamalıdır.

Bir değişkene erişmek için `var()` fonksiyonunu kullanmanız ve değişken ismini parametre olarak girmeniz gerekir.

#title {  
  color: var(--main-color);  
}

Ve bu başlığınıza`#f6f69` rengini verecektir:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1659933244245/DPMbb2jH0.png)

### Yerel bir değişken tanımlama

Yerel değişkenler de oluşturabilirsiniz, bu değişkenler yalnızca çocukları ve bildirilen element tarafından erişilebilir durumdadır. Bu yalnızca bir değişkenin uygulamanızın belirli bir bölümünde (veya bölümlerinde) kullanılacağını biliyorsanız bunu yapmak mantıklı olur.

Örneğin, uygulamanın başka yerlerinde kullanılmayan özel bir renk türünü kullanan bir kutu uyarısı olabilir. Bu durumda onu global kapsam bırakmak mantıklı olabilir:

.alert {  
  --alert-color: #ff6f69;  
}

Bu değişken artık çocuk elementleri tarafından kullanılabilir:

.alert p {  
  color: var(--alert-color);  
  border: 1px solid var(--alert-color);  
}

Eğer denersen alert-color değişkenini uygulamanın herhangi bir yerinde kullanmayı örneğin navbarda, basitçe çalışmayacak. Tarayıcı sadece bu CSS satırını yoksayardı.

### Değişkenlerle daha kolay cevap verme

CSS Değişkenlerinin büyük bir avantajı, DOM’a erişimi olmasıdır. Değişkenleri normal CSS’ye göre derlendiğinden, LESS veya SASS’de durum böyle değildir.

Uygulamada, örneğin ekranın genişliğine bağlı olarak değişkenleri değiştirebileceğiniz anlamına gelir:

:root {  
  --main-font-size: 16px;  
}

media all and (max-width: 600px) {  
  :root {  
    --main-font-size: 12px;  
  }  
}

Ve bu basit dört satırlık kodla, küçük ekranlarda görüntülendiğinde tüm uygulama boyunca ana font boyutunu güncellediniz. Oldukça zarif, di mi?

### JavaScript ile değişkenlere nasıl erişilir

DOM’da yaşamanın diğer bir avantajı, JavaSCript ile değişkenlere erişebilmeniz ve bunları örneğin kullanılan etkileşimlere dayalı olarak güncelleyebilmemizdir. Kullanıcılarınıza web sitenizi değiştirme (yazı tipi boyutunu ayarlama gibi) izni vermek istiyorsanız bu mükemmel bir seçenektir.

Bu makalenin başından itibaren örnek üzerinde devam edelim. JavaScript’te bir CSS değişkenini değiştirme üç satırlık kod alır.

var root = document.querySelector(':root');  
var rootStyles = getComputedStyle(root);  
var mainColor = rootStyles.getPropertyValue('--main-color');

console.log(mainColor);   
\--> '#ffeead'

CSS Değişkeni’ni güncellemek için değişkenlerin bildirildiği öğedeki setProperty yöntemini çağırın ve değişken adını ilk parametre olarak, yeni değeri ikinci olarak girin.

root.style.setProperty('--main-color', '#88d8b0')

Bu ana renk, uygulamanızın görünümünü değiştirebilir; bu nedenle, kullanıcıların sitenizin temasını ayarlamalarına izin vermek için mükemmeldir.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1659933246371/pq4Gu40UM.gif)

Tek bir değişkeni güncellediğinizde, navbarın, metnin ve öğelerin rengini değiştirebilirsiniz.

### Tarayıcı desteği

Şu anda, global web sitesi trafiğinin yüzde 87.19'u CSS Değişkenlerini destekliyor ve ABD’de neredeyse yüzde 91.2'lik bir oran. Kullanıcını çok iyi bilgili olduğu ve çoğunlukla modern tarayıcıları kullanan Scrimba.com’da zaten CSS Değişkenleri kullanıyoruz. Türkiye’de bu oran 88.87%. (Veriler 24 Şubat 2018 tarihinde alınmıştır)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1659933248109/QjpiIODUp.png)

Tamam, işte bitti. Umarım bir şey öğrenmişsindir!

Tam olarak çeviremediğim bazı kelimelerin parantez içinde ingilizcelerini verdim umarım iyi bir anlatım olmuştur :)