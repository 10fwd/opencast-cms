# EdgeDB 2.0: Geleneksel tabanda modern bir veritabanı

Veritabanlarının güvenilirlik açısından kendilerini ispat etmeleri diğer yazılımcı araçlarına oranla daha fazla süre aldığı, hepimizin veri kaybına ve risklere yönelik temkinli olduğumuz bir gerçek. Bu nedenle, tahminen bulunduğunuz yazılım ekiplerinde veya yeni proje başlangıçlarında çokça kez veritabanı seçimi konusundaki tartışmalara siz de denk gelmiş veya içinde yer almışsınızdır. Bundan 5-6 yıl önce genel amaçlı uygulamalarda ilişkisel veritabanlarının (RDBMS'ler) yeri tartışılmaz iken; artık döküman tabanlı, graph veritabanları da seçim kümesinde kendilerine yer bulabiliyorlar.

Bilhassa alternatifler arasında MongoDB, Neo4j gibi isimler artık yavaş yavaş eksiklerini kapatıyorken, daha önce Python Core Developer olarak da çalışmış bir ekipten ilişkisel veritabanı esasları ile çalışan, ancak API arabirimlerini SQL'den soyutlayarak graph-tabanlı alternatiflerini aratmayacak bir deneyim sunan EdgeDB duyuruldu. Üstelik bundan 6 ay önce 1.0'ını yeni tanıtmış ekip, bugün 2.0 sürümü ile karşımızda.

Benim henüz deneme fırsatım olmamasına rağmen, özellikle HTTP katmanı üzerinden haberleşen API'larının "stateless" çalışması, yani başka bir deyişle sürekli ve yönetmeniz gereken açık bir bağlantı ihtiyacı duymaması şimdiden takdir ettiğim özellikleri arasında yer aldı. Kuşkusuz günümüzün cloud üzerinde ölçeklenecek şekilde tasarladığımız sistemlerinde, mimarideki her "stateless" unsur büyük bir yapısal kolaylık anlamına geliyor.

Ayrıca ekibin DX (Developer Experience)'a önem verdiği, CLI araçlarının şemalardaki migrationları ilk elden desteklediği, sizi bulunduğunuz platformda çok farklı gönüllü kişilerce tasarlanan ORM/ODM kütüphaneleriyle learning curve'üne teslim etmemesi de pek rastlanılmayan bir özellik.

Yine, EdgeDB 2.0 sürümü ile birlikte bir de arabirim sağlamaya başlamış:

![EdgeDB UI](https://cdn.hashnode.com/res/hashnode/image/upload/v1659049852834/w-Z8Fino8.webp align="left")

Peki EdgeDB'e güvenmek mümkün mü? Yani veritabanlarındaki veri kayıpları geri dönülemez hasarlar bırakırken, henüz 6 ay önce kendisine "1.0" diyebilmiş bir yazılıma güvenebilir miyiz? Elbette, bu tarz riskler her zaman baki olmak koşuluyla, EdgeDB aslında tüm bu özelliklerini PostgreSQL üzerine inşa etmiş durumda. Ve yine PostgreSQL gibi [100% açık kaynak bir yazılım](https://github.com/edgedb) kimliğinde.

EdgeDB'nin SQL kullanmadığından bahsettik, yerine EdgeQL isimli bir dil kullanıyor. EdgeQL ile ilgili örneklere gelirsek...

## Deklaratif Şema Tanımları

```
type User {
  required property email -> str {
    constraint exclusive;
  }
}

type BlogPost {
  required property title -> str;
  required property published -> bool {
    default := false
  };
  link author -> User;

  index on (.title);
}
```

## Yalın Sorgulama Dili

```
select BlogPost {
  title,
  trimmed_title := str_trim(.title),
  author: {
    email
  }
}
filter not .published
```




Eğer şu ana kadar anlatılanlar ilginizi çektiyse, devamı için aşağıdaki linklere bakabilirsiniz:

- https://www.edgedb.com/
- https://www.edgedb.com/blog/edgedb-2-0
- https://www.edgedb.com/docs/edgeql/index
- https://github.com/edgedb
