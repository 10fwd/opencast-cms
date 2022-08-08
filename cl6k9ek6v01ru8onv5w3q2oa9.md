## JavaScript Tip Sistemi için 3 İpucu

Yazının orijinali için: [https://medium.com/dailyjs/3-tips-for-javascripts-type-system-2519ba57f954](https://medium.com/dailyjs/3-tips-for-javascripts-type-system-2519ba57f954)

JavaScript esnek olarak yazılan bir dildir, yani bilgilerin ne tür bir değişkende saklanacağını önceden belirtmek zorunda değilsiniz. JavaScript kendisine atadığınız bilgi türüne (ör. Dizge (string) değerlerini belirtmek için ‘’ veya “”) dayalı bir değişkeni otomatik olarak yazar. Java gibi diğer birçok dil, tam sayı (int) ondalıklı sayı (float), mantıksal (boolean) veya dizge (String) gibi bir değişken türünü bildirmeniz gerekir.

Bu hem bir lütuftur hem de bir lanettir.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1659933254163/aRJldyauZ.png)

Photo by [Alex](https://unsplash.com/photos/VxtWBOQjGdI?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/search/photos/ying-yang?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

JavaScript’in tür sistemi çok esneklik verirken, bir nesne (object) için bir tam sayı (int) eklemeye çalıştığınızda size seslenmek için katı tip tanımlamalarından yoksundur; bu da tür hatalarını ayıklamak için saatler harcamanızı önler.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1659933255349/xse-i_5Uv.png)

### #1 typeof

Bir değişkenin türünden şüpheye düştüğünüzde, typeof operatörünü kullanabilirsiniz:

typeof 1 //> “number”  
typeof “1” //> “string”

typeof \[1,2,3\] //> “object”  
typeof {name: “john”, country: “usa”} //> “object”  
  
typeof true //> “boolean”  
typeof (1 === 1) //> “boolean”

typeof undefined //> “undefined”  
typeof null //> “object”

const f = () => 2  
typeof f //> “function”

Temel Çıkarım: Değişken tipinden şüphelendiğinde, typeof kullan.

### #2 Çift Eşittir VS Üç Eşittir

Çift eşittir (==) “tip zorlaması olmayan eşitlik” anlamına gelir. Üç eşitti kullandığınızda ise değerler aynı tür olmalıdırlar.

1 == “1” //> true  
1 === “1” //> false

null == undefined //> true  
null === undefined //> false

‘0’ == false //> true  
‘0’ === false //> false

0 == false //> true  
0 === false //> false, because they are of a different type

Unutmayın, tip eşitliği zorlamasıyla eşitsizliği kontrol etmek için !==(denk değilse) operatörünü kullanabilirsiniz.

1 != "1" //> false  
1 !== "1" //> true

Temel Çıkarım: Her zaman === kullanın, çünkü bu kapsamlı bir kontroldür, sinir bozucu hatalardan kaçınmanıza yardımcı olur.

### #3 Yanlışlıkların Kontrolü

“!” operatörünü kullanarak (“bang” operatörüde denir) yanlışlıkları kontrol edebilirsiniz, aşağıdakileri fark ederiz:

!\[\] //> false  
!42 //> false  
!"hello world" //> false

!null //> true  
!undefined //> true  
!0 //> true  
!"" //> true  
!false //> true

Eğlenceli çünkü d0ru.

`null`, `undefined`, `0`, `“”` ve `false` , `!` operatörünü kullandığınızda true döndürür. Ne zaman ki `!` operatörünü olan bir şeye eklediğimizde, mesela 42 sayısı yada “hello world” dizgesi gibi, o zaman false döndürür.

Bu `null`, `undefined`, `0`, `“”` ve `false` değerlerinin varolmayanı yada false değerini temsil ettiğini gösterir ama aynı şekilde olmadığınıda gösterir. 0 bir sayıdır miktarın bulunmadığını gösterir. “” bir dizgedir ve dizgede maddenin/değerin bulunmadığını temsil eder. Ve son olarak, false bir boolean değer gerçek eksikliği temsil eder. Bu basit bir typeof örneğiyle doğrulanabilir:

typeof 0 //> "number"  
typeof "" //> "string"  
typeof false //> "boolean"

`undefined` ve `null` daha zordur. Aşağıdaki örnekte gösterildiği gibi, bunlar farklı türlerdir, aynı değere sahiptir, ancak`===` (denklik) karşılaştırmasında başarısız olurlar:

typeof undefined //> “undefined”  
typeof null //> “object”

undefined == null //> true  
undefined === null //> false

Çünkü `null` bir nesne, ona sayı ekleyebiliriz. Ancak`undefined` ise bir sayı eklediğimizde `NaN` (Not a Number / Sayı değil) değerini verir.

null + //> 1  
undefined + 1 //> NaN

Bir `null` değere sayı eklemek bazen hoş bir kısayol gibi görünebilir ama yapma!

`null` bir nesne olsa da ona bir sayı eklediğinizde bir sayı alırsınız. Ama ona başka şeyler eklediğinizde, size saçma sapan dizgeler verir:

null + \[1,2,3\]//> "null1,2,3"  
null + \["hello", "world"\] //> "nullhello,world"  
null + {0: "hello", 1: "world"} //> "null\[object Object\]"

**Temel Çıkarımlar:**

*   Doğruluğu kontrol ederken dikkatli olmalısınız. `===` operatörünü kullan potansiyel olarak false olabilecek değerleri kontrol ederken, örneğin, `if(foo === undefined || foo === null) ...` — ki bu oldukça sıkıcı olabilir.
*   `null` ‘a bir şeyler ekleme!
*   Yanlışlığı kontrol etmek için en iyi yol ise `!` operatörünü kullanarak tüm yanlış olabilecek değerleri kontrol etmektir. , Yani, `null`, `undefined`, `0`, `“”` ve `false` için bir operatör.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1659933256286/H5shJfMC0.png)

### Okuduğunuz için teşekkürler!

Eğer bu makaleyi yardımcı bulduysanız, lütfen JavaScript üzerine diğer makalelere ve eğitimlere göz atınız:

*   [Making Sense of JavaScript with Some Examples](https://medium.com/dailyjs/some-examples-to-help-understand-javascripts-closure-372e42fff94d) (İngilizce)
*   [How to refactor code to be more testable](https://medium.com/@xiaoyunyang/how-to-refactor-unwieldy-untestable-code-4a73d75cb80a) (İngilizce)