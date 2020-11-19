# III-hafta-odevi

- :heavy_check_mark: .Net kodu nedir ve nasıl derlenir?

- :heavy_check_mark: Roslyn compiler ne işe yarar?

- :heavy_check_mark: Restful servisler nasıl çalışır? Alternatifleri nelerdir ve nasıl çalışırlar?

- :heavy_check_mark: Extension method nedir? Nasıl yazılır?

- :heavy_check_mark: MVC'nin alternatifleri nelerdir?

- :heavy_check_mark: Architectural pattern nedir? Neden ihtiyaç duyuyoruz?

- :heavy_check_mark: ViewData, ViewBag, TempData farkları nelerdir? Çalıştığımız proje üzerinde başka bir branch açarak bunları deneyiniz?

## .Net Kodu Nasıl Derlenir ve Roslyn Compiler 

Roslyn takma adı ile de bilinen .Net Derleyici Platformu, Visual Basic ve C# dilleri için .Net açık kaynak derleyici ve kod analizi API'sidir.  

Özellikler **C#** programlama dilinin geleceği ile ilgili araştırmalar yaptıysanız **Compiler as a Service(CaaS)** konseptiyle mutlaka karşılaşmışsınızdır. İşte **Roslyn** projesinin temel amacı da bu. **Compiler as service**, yani compiler’ın bir **API** vasıtasıyla servis olarak dışarıya açılması amaçlanmaktadır.

## Extension metod 

Extension metodlar herhangi bir yeni nesne oluşturmadan, üzerinde işlem yaptığınız nesne üzerinden çağrılabilen "genişletilmiş" manasına gelen çok pratik metodlardır. Bu metodları kullanarak hem extra iş yükünden kurtulmuş olursunuz, hem de sürekli aynı kodları yazmak zorunda kalmazsınız.

Extension metodlar statik metodlar ve statik classlardan oluşmaktadır. Fakat referans olarak oluşturduğunuz obje üzerinden çağrılırlar. Extension metodların aldığı ilk parametre, bu metodun hangi nesne üzerinde çalışacağını belirtir. Ve alacağı ilk parametrenin önüne "this" anahtar kelimesi getirilir. Böylece metodun bu nesne üzerinde işlem yapacağı belirtilmiş olur.

## Restful Servisler 

Web servis geliştirmek için günümüzde iki farklı metodoloji kullanılıyor. Bunlardan birisi **RESTful**(Representation State Transfer), diğeri de **SOAP**(Simple Object Access Protocol) metodolojisidir.

SOAP protokolü, veri formatı olarak XML’i kullanır. Oysa RESTful servislerde veriler XML formatında da iletilebiliyor olmalarına rağmen daha kompakt olan **JSON** formatı tercih edilmektedir. Aynı veri JSON formatında serialize edildiğinde XML’e göre çok daha küçük boyutlara inmektedir. Bu nedenle iletimi çok daha kolay, parse edilmesi ise çok daha hızlıdır.

### Rest neden tercih edilmeli?
- Basit yapılar

- Farklı dillerde yazılımcılar tarafından anlaşılması istenen entegrasyonu sağlar. Örneğin: Python, Ruby, PHP, C tarafında client yazmak daha kolaydır.

- JSON kullanmanın çok avantajlı olması. Ör: Web sitesi arayüzü veya mobil uygulama tarafından kullanılacak bir servis.

## MVC Alternatifleri

### HMVC - Hierarchical Model-View-Controller
MVC yapılarında bir çok controller ayrı ayrı işler yapıp hepsinin birbirine bağımlılığı söz konusudur. Ayrı ayrı bağımsız geliştirmelerin ihtiyaç olduğu bu yapıda yardıma HMCV yapısı yetişiyor. HMVC yapısını aşağıdaki hiyerarşide daha rahat anlayabilirsiniz.

![HMVC](https://enesgur.com.tr/wp-content/uploads/mvc-hmvc-1.png)

### MVVM - Model-View-ViewModel

MVVM bir projenin “sorumlulukların ayrıştırılması” esasına göre geliştirilmesi temeline dayanan bir tasarım kalıbı sunmaktadır. Sorumlulukların ayrıştırılması, yani meslek hayatımızda kullandığımız karşılığıyla **Separation of Concerns(SoC).** MVVM bir yazılımı **Model**, **View** ve **ViewModel** adında üç farklı yapıda geliştirmemizi tavsiye etmektedir.

**Model:** Veritabanından, web servislerinden ya da herhangi bir veri kaynağından gelen verilerimizi temsil etmek için kullanılan POCO ya da entity sınıflarından oluşmaktadır. Ayrıca veri tutarlığını ve doğruluğunu kontrol eden iş kuralları da burada yer almaktadır.

**View:** Bu kısım verilerimizi son kullanıcılara aktardığımız görsel arayüzdür. Son kullanıcı ile uygulama arasında bir köprü görevi görür.

**ViewModel:** ViewModel ise görsel arayüz ile model arasında köprü görevi görmektedir, yani Model’i View’a bağlayan yapıdır. View ile Model arasında doğrudan bir etkileşim yoktur. View, ilgili işlemleri ViewModel üzerinden yapmaktadır. ViewModel’ın View’a direkt erişimi yoktur ve View ile ilgili hiçbir şey bilmez.

![MVVM](http://devnot.com/wp-content/uploads/2015/01/mvvm-pattern.gif)

### MVP - Model-View-Presenter

**Model**: Kullanıcı arayüzünde (view) görüntülenecek veya başka bir şekilde davranacak verilerin işlendiği kısımdır (event gönderme vb.). Presenter’ın ihtiyaç duyduğu bilgileri sağlar. İş mantığı bu kısımda ele alınır.

**View**: Verilerin görüntülendiği ve işlem yapmak için kullanıcı ile etkileşime geçilen kısımdır. Activity, fragment, dialog vb.

**Presenter**: Model ile View arasındaki bağlantıyı sağlayan kısımdır. Verileri modelden alır ve UI mantığını uygular. Ayrıca View’dan gelen kullanıcı etkileşimlerine tepki verir.

![MVP](https://miro.medium.com/max/875/1*TuWeZzR14MmB-RBbjtZl-A.png)

### RMR - Resource-Method-Representation

RMR mimarisinde, uygulamanızı daha sonra kullanıcıya temsil edilen kaynaklar (resource) üzerindeki HTTP yöntemlerine göre yapılandırırsınız. Böylece MVC Modelleri resource haline gelir (REST kaynaklarıyla 1: 1 eşlenirler). Controller bir "Metod" nesnesi haline gelir ve View, Representation olur.

### ADR - Action-Domain-Responder

Action-Domain-Responder(kısaca ADR), [Paul M. Jones](http://paul-m-jones.com/) tarafından 2014 yılında yayınlanmış, MVC’ye dair bir iyileştirme vaat eden bir teklif. ADR, MVC’nin modern web uygulamalarını açıklamada yetersiz kaldığını savunarak bir çözüm getiriyor. Aynı MVC’de olduğu gibi, kesin bir implementasyon belirtmiyor ancak MVC kadar da muğlak kalmamaya çalışıyor.

**Domain**, MVC’deki modelin aynısıdır. Sadece bahsettiğim “Model” kelimesinin anlam değişmesine son vermek için yeniden isimlendirilmiştir.

**Action**, HTTP requestlerini karşılayan ve uygulamadaki bir aksiyonu niteleyen elemandır. Tek görevi gelen request’i ilgili domain’e iletmek, domain’den gelen cevabı da uygun responder’a göndermektir. Action’da domaine dair bir validasyon bile yapılması önerilmiyor, ne kadar uygulamadan habersiz ve aptal olursa o kadar iyi. Bu kullandığımız framework’ün domain’e sızmaması, framework bağımsız kod yazabilmemiz için önemli.

**Responder,** MVC’deki view katmanına benzer ancak sadece HTML veya JSON içerikten ibaret değildir. Action’dan aldığı domain cevabı ile bir HTTP response oluşturur. Headerlar ve HTTP durum kodları dahil olmak üzere HTTP response’u oluşturmak tamamen responder’ın sorumluluğudur.

![ADR](https://i1.wp.com/blog.cemunalan.com.tr/wp-content/uploads/2019/10/resim.png?resize=740,360&ssl=1)

## Mimari Örüntüler (Architectural Patterns)

Mimari örüntüler gerçek mimariden örnek alarak ortaya çıkmıştır. Mimaride hep aynı desenlerin tekrar ettiğini görebilirsiniz. Sütunlar, sütunların üzerindeki şekiller hep birbirinin tekrarı olacak şekilde tasarlanmıştır. Bu şekilde yapmanın avantajı her bir bileşenin bağımsız olarak geliştirilip sorunsuz bir şekilde birleştirilebilmesidir.

Yazılımlarda bu mimari yapılara çok benzer. Bileşen, Servis, vb yapılarından oluşan uygulamaların aşağıdaki özellikler benzer problemler oluşturur. Bu problemleri gidermek için kullanılan, sistemin tamamında benzer örneklerin görüldüğü çözümlere/yapılara  **Mimari örüntüler**  denir.

-   Yapısı
-   Davranış Şekilleri
-   Birbirleri İle İletişim Şekilleri

Mimari örüntülerin, tasarım örüntülerinden farkı, belli bir alanda, belli bir kapsamdaki problemi çözmek yerine uygulamanın her yerinde geniş alana yayılan problemi çözmeyi hedeflemesidir. Gelin aşağıda yer alan mimari örüntüleri inceleyelim;

-   [Microservices](https://medium.com/architectural-patterns/microservice-nedir-73bdfddad197)
-   [Microfrontends](https://medium.com/architectural-patterns/micro-frontends-hakk%C4%B1nda-konu%C5%9Fulanlar-e178b73cd1c3)
-   [Service-oriented architecture (SOA)](https://medium.com/architectural-patterns/soa-service-orietented-architecture-nedir-75092cd90d61)
-   [Serverless Mimarisi](https://medium.com/cloud-and-servers/serverless-architecture-faas-2e5804ececd9)
-   [Layers, Multi tier Katmanlı Uygulama Mimarisi](https://medium.com/architectural-patterns/katmanl%C4%B1-uygulama-mimarisi-f517b03b050e)
-   [Flux Patten (Redux, vb…)](https://medium.com/architectural-patterns/flux-mimari-%C3%B6r%C3%BCnt%C3%BCs%C3%BC-a9b2198e3cfa)
-   [MVC (Model View Controller) Örüntüsü](https://medium.com/architectural-patterns/mvc-model-view-controller-80e395179ab0)
-   [Broker Pattern](https://medium.com/architectural-patterns/yaz%C4%B1l%C4%B1m-mimarisinde-brokerlik-9677be6dfa5a)
-   [Event-Driven Architecture](https://medium.com/architectural-patterns/event-driven-architecture-7d0a7fb57db8)
-   [Blackboard System](https://medium.com/architectural-patterns/veri-merkezli-mimariler-data-centered-e3d6ad7e5f94)
-   [Pipe and filter architecture](https://medium.com/architectural-patterns/pipe-and-filters-mimarisi-fee576ef6fb0)

## ViewData, ViewBag, TempData

### ViewData
- ViewData, ViewDataDictionary sınıfından türetilir ve temelde bir Dictionary nesnesidir, yani Anahtarların Dize olduğu Anahtarlar ve Değerler, Değerler ise nesneler olacaktır.
 
- Veriler, ViewData'da Nesne olarak saklanır.

- Verileri alırken, veriler nesne olarak saklandığından ve ayrıca geri getirilirken NULL kontrolleri gerektirdiğinden, orijinal türüne Type Cast olması gerekir.

- ViewData, Controller'dan View'a değer iletmek için kullanılır.

- ViewData yalnızca Mevcut İstek için kullanılabilir. Yönlendirme üzerine imha edilecek.

### ViewBag
- ViewBag, ViewData etrafında oluşturulmuş bir Sarmalayıcıdır.

- ViewBag dinamik bir özelliktir ve C # 4.0 dinamik özelliklerinden yararlanır.

- Alma sırasında Tip Döküm verisine gerek yoktur.

- ViewBag, Controller'dan View'e değer geçirmek için kullanılır.

- ViewBag yalnızca Mevcut Talep için kullanılabilir. Yönlendirme üzerine imha edilecek.

### TempData
- TempData, TempDataDictionary sınıfından türetilir ve temelde bir Dictionary nesnesidir, yani Anahtarların Dize olduğu Anahtarlar ve Değerler, Değerler ise nesneler olacaktır.

- Veriler, TempData'da Nesne olarak saklanır.

- Verileri alırken, veriler nesneler olarak saklandığından ve ayrıca geri getirilirken NULL kontrolleri gerektirdiğinden, orijinal türüne Type Cast olması gerekir.

- TempData, Controller'dan View'a ve ayrıca Controller'dan Controller'a değer geçirmek için kullanılabilir.

- TempData, Geçerli ve Sonraki İstekler için kullanılabilir. Yönlendirme sırasında imha edilmeyecektir.


### Kaynak

- https://www.ilkayilknur.com/the-roslyn-project-5n1k-neneredene-zamannasilnedenkim

- http://www.yavuzaydogan.com/c-sharp/extension-metod-nedir-nasil-yazilir-nasil-kullanilir-147

- https://medium.com/@yasinmemic/web-servis-nedir-soap-restful-9f6369edfe0a

- https://blog.ircmaxell.com/2014/11/alternatives-to-mvc.html 

- https://blog.cemunalan.com.tr/2019/10/17/adr-bir-mvc-alternatifi/ 

- http://devnot.com/2015/mvvme-hizli-bir-giris/ 

- https://www.c-sharpcorner.com/blogs/main-difference-between-viewdata-vs-viewbag-vs-tempdata-in-asp-net-mvc
