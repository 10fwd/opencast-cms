# OAuth güzel. Peki Ethereum’u denediniz mi?

Web uygulamalarının temel ihtiyaçlarının başında kaçınılmaz olarak kimlik doğrulama `Authentication` gelmekte. Kısaca web uygulamamızla iletişime geçen kullanıcının gerçekten de iddia ettiği kullanıcı olduğundan emin olmak istiyoruz. Başlangıçta e-posta adresi/kullanıcı adı ve parola ikilileri ile bu problemi çözdük.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1659933045808/AOy90lPhl.png)

HackerNews Giriş Ekranı

Ancak genel olarak parolalar biraz *şeydiler* yani bilirsiniz, *şey.* Uzun ve güçlü bir kombinasyona sahip olmalıdırlar ki hacklenmeyesiniz. Her sitede farklı parola kullanmalısınız ki parolanızı girdiğiniz site hacklenirse hacklenmeyesiniz. Bunu yaparken de tonla parola aklınızda tutamayacağınızdan bir *parola yönetici* kullanmalısınız ki onun da oradan al, oraya yapıştır, yeni siteye kaydolurken umarım eklenti düzgün kaydeder vs. Bir de onun güvenliği var ki ayrı dert. Parola yöneticisine de güvenmiyorsanız `two-blind` yöntemini kullanmanız lazım önemli siteler için. Dediğim gibi, parolalar biraz *şeyler*.

### OAuth / Social Login

Genel olarak paroladan kurtulmamızı sağlayan bir çözümle karşılaştık. Çoğumuzun her gün kullandığı devasa şirketlerin logolarını içeren butonlar hayatımıza girdi. Kullanıcı için birkaç tık ile giriş yapma kolaylığını sağlayan bu butonlar, website sahiplerine de kullanıcı tabanlarını çok daha hızlı genişletme imkanını tanıyordu.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1659933046995/y0rct5tnv.png)

Popüler üçüncü parti giriş yapma yöntemleri

Dikkatinizi çekmek isterim ki buradaki email *(link gelmesi durumunda)* ve telefon numarası da aslında üçüncü parti bir giriş yapma yöntemi *–emailinizi kendi sunucunuzda barındırmıyor veya GSM operatörü sahibi değilseniz.* Şahsen Google ile giriş yapmayı severek kullanıyorum ancak bu tip yöntemlerin barındırdığı kimi riskler bulunmakta. Hesabınıza erişirken kullandığınız anahtarların başkasının kontrolünde olması gibi.

Bunu biraz şuna benzetebiliriz, bir eviniz var ve anahtarını başkasına veriyorsunuz. Evinize her girmek istediğinizde ise ondan izin almak zorundasınız. “*Bugün olmaz, yarın gel”* dediğinde yapabileceğiniz pek de bir şey yok.

> Bu yazıya başladıktan sonra Facebook ve diğer uygulamalarıyla servislerine yaklaşık 7 saat boyunca dünya genelinde erişilemedi. Diğer websiteleri ve uygulamalara Facebook ile kayıt olmuş kullanıcılar hesaplarına erişim sağlayamadı. Ayrıca Facebook, 2019 yılında da 24 saatten uzun bir süre offline olmuştu.

### Web Authentication

Webin gelişimi ile birlikte alternatif yöntemler de implemente edildi. Bunlardan biri `Web Authentication` veya kısaca `[WebAuthn](https://webauthn.guide/)` 2019'dan beri popüler tarayıcılarda destekleniyor. Bu yöntem de OAuth gibi şifresiz bir giriş imkanı tanıyor. Bunu `public-private key` şifreleme mekanizmasıyla gerçekleştiriyor. Kullandığınız web sitesinin implementasyonuna göre aşağıdaki yöntemlerden bir veya birkaçını kullanarak bu sefer kullanıcı doğrulaması cihaz üzerinde gerçekleştiriliyor.

*   Hardware Authenticator örneğin Yubikey
*   Software Authenticator örneğin telefondaki bir uygulama
*   Platform Authenticator örneğin Windows Hello, Face ID, hesap şifreniz ile cihazınızın kendisi

Açıkçası etkileyici bir çözüm olsa da anladığım kadarıyla `Hardware Authenticator` kullanmadığınız sürece genel kullanıcı kitlesine erişimi kolay olan `Platform Authenticator` yönteminde kullandığınız cihazı kaybetmeniz durumunda giriş yaptığınız web sitelerine [erişiminiz de yok oluyor](https://charliedigital.com/2021/06/17/web-identity-showdown-ethereum-vs-webauthn/#:~:text=WebAuthn%3A%20the%20device%20dependency.%20Because%20the%20private%20keys%20are%20device%20specific%2C%20loss%20of%20the%20device%20equates%20to%20irrecoverable%20loss%20of%20access%20without%20an%20alternate%20mechanism.) *–ilgili sitede farklı bir kurtarma yöntemi yoksa.* `Hardware Authenticator` larda ise cihazlar/platformlar arası kimliğinizi taşımanız kolayken, ilgili cihazı *(örn. Yubikey)* kaybettiğinizde yine benzer bir durumla karşılaşıyorsunuz.

### Favorim: Ethereum ile Giriş

Öncelikle biraz Ethereum’dan bahsedelim. Nedir Ethereum? Ethereum’a sadece bir kriptoparadır demek Ethereum’un hakkını yemek olur. 2017'den beri Ethereum’a benzer bir göz ile baktığımdan ancak 2021'de treni yakalayabildim.

Hadi Ethereum’un kendini nasıl tanımladığına bakalım.

> Ethereum, geçmişiniz veya konumunuz ne olursa olsun, herkes için dijital paraya ve veri dostu hizmetlere açık erişimdir. Kripto para birimi etherinin (ETH) ve bugün kullanabileceğiniz binlerce uygulamanın arkasında topluluk tarafından oluşturulmuş bir teknolojidir.

Ethereum en temelinde Ethereum blokzinciri ve üzerinde oluşan ekosistemi temsil eder. Ethereum blokzincirini üzerine kendi programlarınızı yazabileceğiniz kalıcı, herkese açık ve merkeziyetsiz bir veritabanı olarak düşünebilirsiniz. Tabii ki bir çok detayı bulunmakta ancak bu yazının konusu değil. Kendiniz araştırmanızı tavsiye ederim, keşfettikçe insanı heyecanlandıran bir ekosistem. *DYOR.*

Son kullanıcı olarak Ethereum ağına dahil olabilmek için bir [hesaba](https://ethereum.org/en/developers/docs/accounts/) ihtiyacımız var. Hesaplar genel olarak şu iki seye sahiptir, adres ve bakiye. Bakiyenin nasıl belirlendiği oldukça bariz, peki adres nasıl oluşuyor?

Bir Ethereum hesabını oluşturan iki şey vardır, `public key` ve `private key`. Aslında SSL/TLS'den aşina olduğumuz benzer bir yapı burada bulunmakta. Hesabınızın adresi sahip olduğunuz public keyden üzerinden üretilir. Public keyiniz de hesabınıza ait private keyden üretilir. Private keyinizi evde kendiniz de yapabilirsiniz ancak lütfen bunu yapmayın.

Belki bunun nereye gittigini görmüş olabilirsiniz. Elimizdekilere bakalım:

*   Bir tanımlayıcı/`identifier` (address)
*   Herkese açık bir doğrulama anahtarı (public key)
*   Şifrelemek/imzalamak için kullanılan özel bir anahtar (private key)

Gördüğünüz üzere aslında güvenli bir kimlik doğrulama mekanizması için gereken neredeyse her şeye sahibiz. Peki, eksik ne?

Eksik… mesaj! Özellikle her seferinde farklı olan bir mesaj veya bir diğer deyişle `payload` buradaki eksiğimiz. Bunu da kendimiz belirleyebiliriz. O zaman **Ethereum ile girişi** genel şemasını oluşturalım.

*   Sunucu kullanıcıya imzalaması için bir mesaj gönderir.
*   Kullanıcı bu mesajı hesabının private keyi ile imzalar.
*   İmzalanmış mesajı ve adresini sunucuya gönderir.
*   Sunucu imzalanmış mesajı ve istediği mesajı kullanarak public keyi ve public key üzerinden de adresi çıkartır.
*   Sunucu çıkartılan adres ile iddia edilen adres aynı mı diye kontrol eder.
*   Ve tada ?

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1659933048258/ES6bL9ck2.png)

Konuşması kolay, kodu göster :) | [https://stickker.net/urun/talk-is-cheap-show-me-the-code/](https://stickker.net/urun/talk-is-cheap-show-me-the-code/)

Öncelikle geliştirme ortamımızı hızlıca hazırlayalım. Node.js ve NPM’in kurulu olduğunu varsayıyorum. Proje klasörümüzü ve express API’mızı oluşturalım.

```
mkdir eth-sign-in && cd eth-sign-in  
npx express-generator --no-view  
npm install  
npm install ethers uuid  
npm start
```

Ardından [http://localhost:3000](http://localhost:3000/) adresinde Express yazısı bizi karşılıyor olacak.

### Cüzdan Kurulumu

Ethereum ağıyla etkileşime geçebilmek için bir *hesaba* ihtiyacımız olduğundan bahsetmiştim. Sahip olduğumuz hesapları kullanmayı, saklamayı, ağ ile iletişime geçmeyi kolaylaştıran uygulamalara ise *cüzdan* deniliyor. En popüler cüzdanlardan biri olan MetaMask işinizi görecektir. MetaMask tarayıcınıza eklenti olarak kurulup, ziyaret ettiğiniz web sitelerine Ethereum API’nı enjekte ediyor.

[Metamask Web Sitesi](https://metamask.io/)’nden tarayıcınıza yükledikten sonra sizi şu ekran karşılayacak:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1659933050305/pasKhAmNN.png)

Create a Wallet diyerek devam ediyoruz. Ardından bir parola belirlememizi istiyor. Parolamızı belirledikten sonra Ethereum hesabımıza herhangi bir zamanda herhangi bir yerden erişebilmemizi sağlayan “Secret Recovery Phrase” bizi karşılıyor. Bu kelimelere sahip herhangi biri hesabınıza erişebilir. Güvenli bir şekilde saklamanız önemli. [Daha fazla bilgi.](https://metamask.zendesk.com/hc/en-us/articles/360060826432)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1659933052187/TL98ElLNx.png)

xkcd: Security — [https://xkcd.com/538/](https://xkcd.com/538/)

Kurulumu bitirdikten sonra artık bir Ethereum hesabına ve cüzdanına sahibiz! Aşağıdakine benzer bir ekran sizi karşılayacak. Sağ üstten bağlı olduğunuz blokzincir ağını görebilirsiniz. Örneğin kendi bilgisayarınızda çalışan bir blokzincire de MetaMask cüzdanınızla bağlanmanız mümkün. *How cool is that!*

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1659933054611/i67guKvYb.png)

Artık kodlamaya geçebiliriz! Öncelikle sayfamıza bir buton ekleyelim. Ardından tıklanıldığında cüzdandaki hesap adreslerine erişim isteyelim.

// public/index.html

<button onclick="signIn()">Ethereum ile Giriş Yap</button>

<script>  
  async function signIn () {  
    // Cüzdandaki hesap adreslerine erişim isteyelim.  
    const accounts = await ethereum.request({ method: 'eth\_requestAccounts' })  
    console.log(accounts)  
  }  
</script>

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1659933056897/j5N_Isu-s.png)

Butona tıkladıktan sonra çıkan popupı onaylayınca consoleda Ethereum hesap adresinizi görebilirsiniz. Şimdi sunucudan imzalanması gereken mesajı almamız gerekiyor. Bunun için endpointimizi oluşturalım.

```
// app.js
```

```
// 18. satır sonrasına  
const { v4: uuidv4 } = require('uuid');  
  
// Şimdilik veritabanı olarak düşünelim  
const addressNonceMap = {}   
  
app.post('/auth/ethereum/message', (req, res) => {  
  // Kullanıcının Ethereum adresi  
  let { address } = req.body  
  address = address.toLowerCase()  
  
  // Tek kullanımlık kod yoksa adrese ait, oluşturalım  
  addressNonceMap[address] = addressNonceMap[address] ?? uuidv4()   
  
  const nonce = addressNonceMap[address]  
  
    const message = `Welcome to there's no place like 127.0.0.1!\nClick "Sign" to sign in.\nWallet address: ${address}\n\nNonce: ${nonce}`  
      
  res.send({  
    message  
  })  
})
```

Şimdi ise butona tıklanıldığında sunucuya istek atıp gelen cevap ile imza isteği oluşturalım.

```
// public/index.html
```

```
<button onclick="signIn()">Ethereum ile Giriş Yap</button>  
  
<script src="https://cdn.ethers.io/lib/ethers-5.2.umd.min.js" type="application/javascript"></script>  
  
<script>  
  async function signIn () {  
    // Cüzdan erişimi isteyelim  
    const accounts = await ethereum.request({ method: 'eth_requestAccounts' })  
    console.log(accounts)  
	  
    // Daha kolay işlem yapabilmek için ethers kütüphanesine Web3 Provider olarak MetaMask'in sunduğu Ethereum Provider'ını veriyoruz  
    const provider = new ethers.providers.Web3Provider(window.ethereum)  
      
    // Signerı hesap olarak düşünebilirsiniz. Ethereum ağında veya dışında hesabınızla yaptığınız her işlemde bir veri imzalanır.  
    const signer = provider.getSigner()  
    console.log(signer)  
  
    // Sunucuya hesap adresini göndererek imzalanması gereken mesajı alalım.  
    const response = await fetch('/auth/ethereum/message', {  
      method: 'POST',  
      headers: {  
        'content-type': 'application/json',  
      },  
      body: JSON.stringify({ address: accounts[0] })  
    })  
  
    const { message } = await response.json()  
	  
    // Signer'dan imzalamasını isteyelim.  
    const signature = await signer.signMessage(message)  
    console.log(signature)  
  }  
</script>
```

Terminalde tekrardan npm start yapıp sayfayı yeniledikten sonra Ethereum ile Giriş Yap dediğinizde MetaMask sizden mesajı imzalamanızı isteyecek.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1659933059202/2nCoG5Ezv.png)

Ardından consoleda Ethereum adresinizle imzalanmış mesajı görebilirsiniz. Artık bu imzayı sunucuya gönderip kontrol etmek kaldı. Bu kontrolü yapan endpointimizi yazalım.

```
// app.js
```

```
const ethers = require('ethers')  
  
app.post('/auth/ethereum/verify', (req, res) => {  
  let { address, signature } = req.body  
  address = address.toLowerCase()  
  
  const nonce = addressNonceMap[address]  
  
  const message = `Welcome to there's no place like 127.0.0.1!\nClick "Sign" to sign in.\nWallet address: ${address}\n\nNonce: ${nonce}`  
  
  // Istenilen mesaj ile imzalanmış mesajı kullanarak imzalayan adresi çıkart  
  const recoveredAddress = ethers.utils.verifyMessage(message, signature)  
  
  // Iddia edilen adres ile imzadan çıkartılan adres eşleşiyor mu?  
  if (address === recoveredAddress.toLowerCase()) {  
    res.json({  
      status: true  
    })  
  } else {  
    res.json({  
      status: false  
    })  
  }  
})
```

—

```
// public/index.html - signIn fonksiyonu devamı
```

```
// Signer'dan imzalamasını isteyelim  
const signature = await signer.signMessage(message)  
console.log(signature)  
  
// Imzayı sunucuya gönderelim  
const verifyResponse = await fetch('/auth/ethereum/verify', {  
    method: 'POST',  
    headers: {  
        'content-type': 'application/json',  
    },  
    body: JSON.stringify({ address: accounts[0], signature })  
})  
  
const { status } = await verifyResponse.json()  
  
let authMessage;  
  
if (status) authMessage = `Auth successful! Welcome <pre>${accounts[0]}</pre>`  
else authMessage = `Auth failed. Please try again later or contact with us.`  
  
document.querySelector('h1').innerHTML = authMessage
```

Ethereum ile giriş özelliğini implemente ettik! Expressi yeniden başlatıp sayfayı yenilediğinizde artık siz de cüzdanınızla giriş yapabilirsiniz!

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1659933061276/hc2dNv9k3.png)

Açıkçası kodda bulunan `Auth failed.` mesajını UI'ı kullanırken almanız oldukça güç. Sonuç olarak herhangi bir kullanıcı adı veya parola girmiyorsunuz :)

Demoyu olabildiğince basitleştirmek için veritabanı, `Auth token` gibi yapıları eklemedim. `Verify` edildikten sonra halihazırda yaptığınız şekilde bir Cookie veya `JWT token` istemciye sağlayabilirsiniz.

Sunucudan gönderdiğiniz mesajda `nonce` olması önemli. Statik bir mesaj üzerinden de adres doğrulaması yapmak mümkün ancak imzalanmış mesaj herhangi bir şekilde başka birine geçmesi durumunda aynı siteye bu signature kullanılarak defalarca giriş yapabilir. Aynı zamanda da aynı mesajı imzalatan diğer websitelerine de bu imzalanmış mesajı göndererek giriş yapabilir. Nonce önemli.

GitHub üzerinden koda ulaşabilirsiniz.

[**GitHub - MrPeker/eth-sign-in: Sample code for ETH Sign In**  
*Sample code for ETH Sign In at https://acik-kaynak.org/oauth-guzel-peki-ethereumu-denediniz-mi/ The related code for…*github.com](https://github.com/MrPeker/eth-sign-in "https://github.com/MrPeker/eth-sign-in")[](https://github.com/MrPeker/eth-sign-in)

Twitter: [https://twitter.com/peker\_eth](https://twitter.com/peker_eth?ref_src=twsrc%5Egoogle%7Ctwcamp%5Eserp%7Ctwgr%5Eauthor)