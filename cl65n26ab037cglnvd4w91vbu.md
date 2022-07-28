## EdgeDB 2.0: Geleneksel tabanda modern bir veritabanı

Veritabanlarının kendilerini ispat etmeleri, kullanıcılarını rahat hissettirmeleri için birçok değişik yazılımcı aracı kategorisine oranla daha fazla süre aldıkları bir gerçek. Bu nedenle, tahminen bulunduğunuz yazılım ekiplerinde veya yeni proje başlangıçlarında çokça kez veritabanı seçimi konusundaki tartışmalara siz de denk gelmiş veya içinde yer almışsınızdır. Bundan 5-6 yıl önce genel amaçlı uygulamalarda ilişkisel veritabanlarının (RDBMS'ler) yeri tartışılmaz iken; artık döküman tabanlı, graph veritabanları da seçim kümesinde kendilerine yer bulabiliyorlar.

Bilhassa alternatifler arasında MongoDB, Neo4j gibi isimler artık yavaş yavaş eksiklerini kapatıyorken, daha önce Python Core Developer olarak da çalışmış bir ekipten ilişkisel veritabanı esasları ile çalışan, ancak API arabirimlerini SQL'den soyutlayarak graph-tabanlı alternatiflerini aratmayacak bir deneyim sunan EdgeDB duyuruldu. Üstelik bundan 6 ay önce 1.0'ını yeni tanıtmış ekip, bugün 2.0 sürümü ile karşımızda.

Benim henüz deneme fırsatım olmamasına rağmen, bilhassa HTTP katmanı üzerinden haberleşen API'larının "stateless" çalışması, yani başka bir deyişle sürekli ve yönetmeniz gereken açık bir bağlantı ihtiyacı duymaması şimdiden takdir ettiğim özellikleri arasında yer aldı. Bilhassa günümüzün cloud üzerinden ölçeklenebilir olarak tasarladığımız sistemlerinde mimarideki her "stateless" unsur büyük bir yapısal kolaylık anlamına geliyor.

Son olarak ekibin DX (Developer Experience)'a önem verdiği, CLI araçlarının şemalardaki migrationları ilk elden desteklediği, sizi bulunduğunuz platformda çok farklı gönüllü kişilerce tasarlanan ORM/ODM kütüphaneleriyle learning curve'üne teslim etmemesi de pek rastlanılmayan bir özellik.

Eğer şu ana kadar anlatılanlar ilginizi çektiyse, devamı için aşağıdaki linklere bakabilirsiniz:

- https://www.edgedb.com/
- https://www.edgedb.com/blog/edgedb-2-0