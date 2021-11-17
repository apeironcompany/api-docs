# Mikroservis Nedir?

### **Mikroservis Nedir?**

Mikroservis en kısa tabiriyle , küçük , otonom ve bir arada çalışan servislerdir.  Yazılım projesine yeni fonksiyonellikler eklendikçe , kodlar büyür.  Bir zaman sonra,  projeye hakim olmak, eklentiler yapmak ve karşımıza çıkan sıkıntıları çözmek zor bir hal almaya başlar. Normalde, monolitik bir proje içerisinde , bu gibi problemlerle mücadele edebilmek için kodumuzda olabildiğince soyutlamalar ve modüller oluştururuz.

![Untitled](Mikroservis%20Nedir%203f296d5e1c4a4d689dce721649e969d5/Untitled.png)

Yukarıdaki resimde de görüldüğü üzere monolitik bir uygulamada tüm uygulama direkt olarak tek bir database’e bağlıdır ve bu birazdan bahsedeceğimiz büyük sorunları da beraberinde getirir. Mikroservis mimarisinin yaptığı, uygulamamızı olabildiğince ufak ve kendi database’ine sahip servislere bölmek ve bu şekilde çalıştırmaktır.  Servis ne kadar küçük olursa, mikroservis mimarisinin faydalarını en üst düzeye ve olumsuz etkilerini de en alt düzeye indirmiş oluruz.  Her bir mikro servis ayrı bir varlıktır. Servisler birbirinden bağımsız olarak değiştirilebilmelidir. Burada altın kural , bir servisteki değişikliği ve deployu yaparken başka bir serviste de değişiklik yapma ihtiyacı duyuyor muyuz?

### **Mikroservis Mimarisinin Sağladığı Faydalar**

### ** 1. Teknoloji Çeşitliliği**

Çoklu, işbirliği yapan mikro servislerden oluşan bir sistemle, her birinin içinde farklı teknolojiler kullanmaya karar verebiliriz. Bu, her bir iş için doğru aracı seçmemize olanak tanır. Teknoloji seçiminde genellikle en düşük ortak paydaya dönüşen ve daha standartlaştırılmış seçimler yapmak doğru değil.

Örneğin, bir sosyal ağ için, kullanıcılarımızın bir sosyal grafiğin birbiriyle bağlantılı doğasını yansıtacak şekilde grafik odaklı(graph based) bir veritabanında etkileşimlerini saklayabiliriz, ancak kullanıcıların kullandıkları yayınlar da belge odaklı bir veri deposunda saklanabilir.

![Untitled](Mikroservis%20Nedir%203f296d5e1c4a4d689dce721649e969d5/Untitled%201.png)

Mikroservis ile, teknolojiyi daha hızlı bir şekilde benimseyebiliriz ve yeni ilerlemelerin bize nasıl yardımcı olabileceğini görebiliriz. Yeni teknolojiyi denemek ve benimsemek için en büyük engellerden biri, projede o kısım ile ilişkili kısımların olması ve bir yere dokunulduğunda arkasının da geleceği riskidir. Monolitik bir uygulama ile, eğer yeni bir programlama dili, veritabanı veya framework denemek istersek, herhangi bir değişiklik sistemin büyük bir kısmını etkileyebilir. Birden fazla servisten oluşan bir sistemle, yeni bir teknolojiyi denemek için birden fazla yeni yer vardır. Muhtemel en düşük riskli bir hizmeti seçilebilir ve olası olumsuz etkileri sınırlanabileceği bilinerek, oradaki teknoloji kullanılabilir.

### **2. Esneklik**

Bir sistemin bir componenti fail olabilir bu doğal bir durumdur ancak bir componentin fail olmasıyla başka componentler de fail olursa sıkıntı baş göstermeye başlar . Monolitik bir uygulamada, servis başarısız olursa, her şey çalışmayı durdurur. Böyle bir sistemle, hata şansımızı azaltmak için birden fazla makinede çalışabiliriz, ancak mikro servislerle, hizmetlerin toplam başarısızlığını ele alan ve buna bağlı olarak işlevselliği bozan sistemler oluşturabiliriz.

### **3. Ölçekleme**

Büyük, Monolitik bir uygulamada, her şeyi birlikte ölçeklemek zorundayız. Bazen ölçekleme amacımız projenin  küçük bir  kısmı içindir ve buna rağmen genel sistemimizi ölçeklendirmeliyiz. Daha küçük hizmetlerle, ölçeklendirmeye ihtiyaç duyan hizmetleri ölçeklendirebiliriz. Farklı sistemler ve platformlarda çalışabilen farklı servisler olarak geliştirildikleri için, ihtiyaça göre genişletilebilirler. Mesela yoğun “memory” kullanan bir servis ile yoğun I/O işlemi yapan bir servisi farklı şekillerde “scale” edip, kaynak kullanımını optimize etmek oldukça kolay olacaktır.

### **4. Deployment Kolaylığı**

Monolitik bir uygulamada belki bir satırlık değişikliğin deployu ve release işlemi için tüm uygulamanın deploymenta ihtiyacı vardır. Mikroservis mimarisi ile , yaptığımız her değişiklik kendi işi için  özelleştirilmiş servislerin içerisinde olacağından , bu servisin deployu çok daha kolay ve sistemin geri kalanından bağımsız olacaktır. Bu da bizim için deployment sürecini hızlandıracaktır. Eğer bir problem meydana gelirse problemin meydana geldiği bağımsız serviste problem kolayca çözülebilecek ve hızlı bir şekilde rollback yapılma imkanı doğar.

![Untitled](Mikroservis%20Nedir%203f296d5e1c4a4d689dce721649e969d5/Untitled%202.png)

### **5. Organizasyonların Düzenlenmesi**

Mikroservisler, mimarimizi organizasyonumuza daha iyi uydurmamızı sağlar ve herhangi bir kod tabanında çalışan kişi sayısını minimize etmemize yardımcı olur. Ayrıca, ekiplerin hizmetler arasında sahipliğini tek bir hizmet alanında çalışan kişileri tutmaya çalışacak şekilde değiştirebiliriz. Ayrıca ekibe sonradan katılan bir kişinin bu kadar büyük bir yapıya, mimariyi öğrenmesi yerine, bu kişinin hangi dilde ve hangi DB ortamında işi yapmasını biliyor ise bu ortamda bu ufak iş mantığını geliştirme imkanı vermeyi sağlar.

### **6. Reuseability’i Optimize Etme**

Her projede kimsenin dokunmak istemediği , proje için hayati öneme sahip bölümler mevcuttur ve bu bölümler eski teknolojilerle hayata geçirilmiş ve yaşam ömrünü yıllar önce kaybetmiş makinelerde çalışıyor olabilir. Peki bunlar neden değiştirimez. Cevabı basit, bu değiştirme ve geçiş işlemi çok büyük ve riskli bir iş.

Mikroservis mimarisi ile bağımsız servisler küçük boyutlarda olduğundan, bunların yerine daha iyi bir uygulama ile yer değiştirme, dönüştürme ya da bunları tamamen silme maliyetini yönetmek daha kolaydır.  Mikroservis yaklaşımlarını kullanan ekipler, gerektiğinde hizmetlerin tamamen yeniden yazılabilmesinde ve artık ihtiyaç duyulmadığında bir servisi yok etmekte eskiye kıyasla sıkıntı yaşamazlar.

*Mikroservis Mimarisine Geçilirken Karşılaşılabilecek Bazı Sıkıntılar…*

- Önceki sistemde RDBMS kullanılıyorsa çoğu sorgunun değişmesi gerekebilir. Örneğin, her servisin kendi database’i olacağından join kullanımını önceki sistemdeki halinden farklılaştırılmak zorunda kalınacaktır.
- Kullanıcı session yönetimi yapısı farklılaştırılmak zorunda kalınabilir.
- Servisler farklı platformda ve ortamlarda çalışabileceğinden, bunların yönetim ve monitoring maliyeti doğacaktır.
- Fazlaca database ve transaction yönetimi zor olabilir.

Geçiş sırasında mikroservisin getirdiği faydalar ve sıkıntılar bir teraziye konup kıyaslandığında hangi tarafın ağır basacağı görülüp ihtiyaçlara göre karar verilmesi doğru olacaktır.