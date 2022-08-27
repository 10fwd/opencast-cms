## Deno 1.25, Yol Haritası ve Rakipleri

Yeni bir "JavaScript Runtime"ını değerlendirirken, elbette ilk yaptığımız değerlendirme çoğunlukla bu runtime'ı Node.js ile karşılaştırıp farkları anlamaya çalışmak üzerinden ilerliyor. 

Ancak Deno projesi oldukça sakin ve uzun vadeye yayılmış bir oyun planı ile ilerleyeceğini, bir Node.js drop-in replacement'ı olmayacağını ilk günlerinde çok net bir mesaj olarak bizlere iletti. Açıkçası çıkar çıkmaz benimsemediğimiz ama zamanla hayatımızda yer eden bu gibi birçok teknoloji olduğu için, bu stratejiyi daha olgun buluyorum. Aksi takdirde Deno'nun hype cycle'dan geçen teknolojiler kervanına katılıp hızlıca şişip sonra da parlaklığının kaybolmamasını izliyor olabilirdik.

Deno açıkçası bir "deneyim" projesi olduğu için, ilk günlerinden bu yana Node.js'in yolda vermiş olduğu "yanlış" kararları vermekten ve bu yanlış kararların üzerine bir yapı inşa etmekten kaçınıyor.

Bu nedenle ilk çıkışı esnasında hali hazırda Node.js kullanıcılarının bir şeyleri sıfırdan oluşturmadan geçiş yapabileceği bir geliştirme ortamı sağlamazken, bilhassa yatırım aldıktan ve daha fazla yazılımcıya daha iyi "developer experience" nasıl sağlanabileceğine yönelik uzun süren tartışmalardan sonra, bugün Deno "kendi yoluyla" geriye doğru uyum çalışmalarını arttırmaya başladı.

Bunların detaylarından yazının devamında bahsetmeye çalışacağım.

## Deno 1.25 Yenilikleri

- `deno init` komutu
- deneysel npm desteği
- daha hızlı bir HTTP sunucusu
- daha hızlı başlangıç süresi
- FFI (foreign function interface) üzerine geliştirmeler

detaylar: https://deno.com/blog/v1.25


## Deno'nun Yol Haritası

Deno'nun geliştirme bloğunda [Deno'nun önündeki büyük değişiklikler](https://deno.com/blog/changes) başlığı ile yayınlanan yazıyı biraz özetlersek;

**Node ve NPM Desteği**  
Deno önümüzdeki 3 ay içerisinde npm paketlerinin 80-90% gibi bir çoğunluğunu kapsayacak şekilde çalıştırabilir olmak için çalışmalarına devam ediyor.

"node compat mode" ve "experimental npm support" özellikleri bugün dahi deneyebileceğiniz durumda.

örneğin bugün `import express from "npm:express"` komutu ile express'i deno üzerinde kullanabilir duruma geliyorsunuz.

**En hızlı JavaScript Runtime'ı**  
Deno'nun -kendi iddialarına göre- hedefi Deno'yu en hızlı JavaScript runtime'ı yapmak. Bunu da, sonraki sürümde Deno'nun barındıracağı HTTP server'ın yapılmış en hızlı JavaScript web sunucusu olduğunu örnekleyerek anlatıyorlar.

**Kurumsal Destek**  
Deno'nun büyük şirketlerdeki geliştiricilerce kullanımı ve yaygınlığı için "Deno'yu kurumsal dünya kurgusuna uyarlamak" gibi bir başlıkla ofis saatleri başlatarak kurumsal-Deno işbirliğinin başlayacağı ifade ediliyor.

**En Rahat Geliştirici Deneyimi (DX)**  
Deno kullanıcılarına yaptığı ankette en büyük avantajının TypeScript'i runtime ile birlikte getirmesi olduğu bulgusuna erişmiş. Yine kendi içerisinde gelen lint, format, test, benchmark, dokümantasyon araçları ile Deno bu alanda en iyi developer experience (DX)'ı sağlamaya devam edeceğini iddia ediyor.

**Ekosistem**   
Deno bu yazının yazıldığı tarihte GitHub üzerinden 4.1 milyon download'ı geçmiş, aylık 250 bin aktif kullanıcıya sahip. Hedef ise bu sayıları arttırmak.


## Deno, Node.js ve Bun Rekabeti

Bu kısmı genelde [sunumlarımda](https://speakerdeck.com/eser) daha kapsamlı anlatsam da, ufak bir temel fikri burada da paylaşmak isterim.

Aslında Deno, her iki runtime'ın da geliştiricisi olan Ryan Dahl'ın "Node.js'i geliştirirken yaptığı tasarımsal yanlışlar"ı değerlendirip, bu yanlışların olmadığı bir runtime oluşturmaya çalışması ile ortaya çıkmış bir ürün. 2009'da ilk sürümünü çıkartmış olan Node.js'in, bugün yeniden yorumlanması neticesinde Deno'nun Node.js'den çok daha iyisini sağlayabileceğini söylemek ilginç olmaz. Düşünürsek, Web API'ların olgunluğundan tutalım, cloud/bulut mimarisinin, JavaScript'in, diğer alternatif backend ve frontend platformlarının, yazılım pratiklerinin değiştiği bir dünyada bugün Deno standart kütüphanesinden tutalım, beraberinde getirdiği tooling'e kadar Node.js'den ayrışıyor.

Bununla birlikte düne kadar TC39 gibi JavaScript standartlarını belirleyen bir konsorsiyum'un kararlarını bile çok yavaş adapte eden, hatta ES Modules gibi 2015'den bu yana hayatımızda olan bir standarta rağmen kendi modül sistemini devam ettirmek konusunda ayak direyen bir Node.js Deno'nun varlığı ile artık eksiklerini tamamlamaya başladı diyebiliriz. Elbette bu rekabet kullanıcıların lehine sonuçlanıyor.

Bun'ın ortaya çıkışı ise ayrı bir hikaye. Bun da Deno'nun bugüne kadar odaklanmadığı Node.js kullanıcılarına sorunsuz geçiş olanağı ve daha hızlı performans konusunda Deno'yu zorluyor ve hareket etmeye mecburi bırakıyor gibi görünüyor.

---

Tüm bu durum yıllarca yaşadığımız Browser Savaşlarının bir benzerini acaba Runtime Savaşları olarak görür müyüz sorusunu aklıma getiriyor. Siz ne dersiniz?