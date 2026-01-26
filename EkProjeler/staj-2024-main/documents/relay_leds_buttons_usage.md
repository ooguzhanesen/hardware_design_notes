# Röle Nedir?
Röle, yüksek akım ve gerilime sahip hatları düşük akımla anahtarlamamızı sağlayan bir devre elemanıdır. İçerisinde bulunan bobin yardımıyla bu anahtarlama işlemi gerçekleşir.

Rölenin NO (Normally Open), NC (Normally Close) ve C (Common) bacakları bulunur. Ayrıca bobini tetikleyebilmek amacıyla bobin bacakları bulunur.
Rölenin NO bacağı, bobine herhangi bir sinyal verilmediğinde açık olan bacaktır. NC bacağı ise, bobine sinyal verilmediğinde kapalı olan bacaktır. Common bacağı ise çıkış yüküne bağlanması gereken ortak bacaktır. Aşağıda rölenin şemasına yer verilmiştir:

![RoleDiyagram](https://github.com/hidroel/staj-2024/raw/main/documents/images/Staj-2024-Role.png)

Kontrol edeceğimiz bileşeni Common ucuna bağlamalıyız. Ardından bu bileşenin sürekli güç alıp almama durumuna göre NO veya NC bacaklarını belirleyip güç kaynağını bu bacaklardan birine bağlamalıyız. Bobin bağlantılarını ise MCU ile denetleyeceğiz.

## MCU İle Röle Bobini Kullanımı
MCU'nun dijital out pini doğrudan bobine bağlanamaz, bu oldukça riskli ve hatalı bir işlemdir. Olası riskler:

-Röle bobininde tersine voltaj dalgalanmaları olabilir ve bu MCU'ya çarparak bozulmasına sebep olur.
-Bobin MCU'nun kaldırabileceğinden daha fazla akım çekebilir ve MCU'yu yakabilir.

Her iki durum da oldukça yaşanması muhtemel durumlardır. Bu sebeple röleyi MCU ile doğrudan kontrol etmeyiz. Öncelikle bir röle sürücü devresi oluştururuz. Bu devre içerisinde transistörler ve diyotlar içerir. Transistör sayesinde yüksek akım çekilme ihtimalini ortadan kaldırırız. Diyot ise tek yönlü geçişe izin verdiği için tersine olan tüm dalgalanmaları emecek ve MCU'yu koruyacaktır.

![RoleDriverDiyagram](https://github.com/hidroel/staj-2024/raw/main/documents/images/Staj-2024-RoleDriver.png)


Yukarıdaki gibi bir sürücü devresi oluşturulduğu zaman MCU ile güvenli bir şekilde röle kontrolü yapılabilir.


**Not:** Kullanılacak diyot ve dirençler MCU'ya göre ve projenin diğer bileşenlerine göre değişkenlik gösterir. 

# MCU ile LED Kontrolü

LED'ler 5v, 3.3v gibi değerlerle çalışabilirler, çektikleri akım ise fazla yüksek değildir. Ancak buna rağmen doğrudan MCU ile LED sürmeye çalışmak sağlıklı bir yöntem değildir. Bu yüzden LED kontrollerinde de doğrudan MCU'ya bağlamak yerine bir sürücü devresi oluşturarak bağlantı sağlarız. Bu sürücü devresi röle kadar karmaşık değildir, bir mosfet kullanarak bu işlem sağlanabilir. Aşağıda LED sürmek için ideal bir devre şemasına yer verilmiştir.

![LEDDriverDiyagram](https://github.com/hidroel/staj-2024/raw/main/documents/images/Staj-2024-LEDDriver.png)

Buradaki amaç, LED'in MCU'dan değil güç kaynağından beslenmesidir. MCU yalnızca aradaki anahtarlamayı sağlayan çok düşük akımlı sinyali mosfete göndermektedir.

# MCU ile Buton Okuma
MCU'ya fiziki olarak müdahale edeceğimiz durumlar varsa butonlara ihtiyacımız var demektir. Butonlar, aslında mekanik anahtarlardır. Aktif duruma getirildiğinde anahtar kapanarak üzerinden yük geçişine izin verir. Yükteki değişimi kontrol ederek buton yardımıyla MCU'ya talimatlar verebiliriz.

Butonları devreye bağlama şeklimize göre veya butonun çeşidine göre pull up veya pull down olarak yönetebiliriz. Detaylara bakacak olursak;

## Pull Up Buton
Pull up buton, butona basılı değilken MCU'ya sürekli 1 sinyalini gönderen butondur. Dijital olarak aktif 1 gönderir. Butona basıldığı taktirde sinyal kesilir.
## Pull Down Buton
Pull down buton, pull up butonun tam tersi mantık ile çalışır. Butona basılı değilken MCU'ya herhangi bir şey göndermez. Başka bir değişle 0 olarak okuyabiliriz. Butona basıldığı anda sinyal gönderir.

Projenin kullanım alannıa göre butonlar pull up veya pull down olarak kullanılabilir. Butondan gelen hat, MCU'nun herhangi bir GPIO pinine bağlanarak dijital okuma sağlanabilir.

Bu projede pull down buton kullanmak ihtiyacımızı karşılayacaktır. Pull down butonun şeması aşağıdadır:

![ButtonDiyagram](https://github.com/hidroel/staj-2024/raw/main/documents/images/Staj-2024-Buton.png)

Şekilde gördüğümüz R1 direnci VCC'ye göre belirlenmelidir. MCU'nun 3.3v maksimum çalışma gerilimine sahip olduğunu düşünürsek, giriş voltajı kesinlikle 3.3 voltu geçmemelidir. VCC MCU'nun kendisinden alınabileceği gibi, güç kaynağından da alınabilir. Ancak butonlarda yüksek akıma ihtiyaç olmadığı için VCC hattını doğrudan MCU'dan çekmek mantıklı bir seçenektir.

**Önemli Not:** VCC gerilimi MCU'nun kabul edeceği seviyede olsa bile direnç kullanılması zorunludur. Aksi taktirde buton aktif hale getirilse bile akım dirençsiz yoldan geçeceği için MCU tarafından okuma sağlanamayacaktır.

## Debounce Nedir?
Mekanik butonlar, fiziksel olarak iki temas yüzeyinin birbirine dokunması ve sonra ayrılmasıyla çalışır. Butona basıldığında, temas noktaları bir süreliğine geçici olarak açılıp kapanabilir. Bu durum, birkaç mikrosaniyelik titreşimlere neden olur ve "bouncing" olarak bilinir. Bouncing, bir butona basıldığında veya bırakıldığında, temas noktalarının birkaç kez açılıp kapanmasına yol açar. Bu da MCU yazılımının kararsız kalmasına ve hatalı işlem yapmasına sebep olur. Bu durumu gidermek için bazı yöntemler bulunmaktadır. İşte bu yöntemler:

- Yeteri kadar büyük bir direnç kullanmak. Direnç kullanılarak gürültüler önemli ölçüde azaltılabilir. 
- Kapasitör kullanmak. Butonla MCU arasındaki hatta kapasitör ekleyerek dalgalanmaların önüne geçilerek düzgün bir voltaj sağlanabilir.
- Yazılım çözümleri. Firmware yazılımında sinyalin belli bir süre stabil gelmesinden sonra doğru kabul edileceğine yönelik eklemeler yapılarak çözüm bulunabilir.

Yukarıdaki yöntemlerin tümünü aynı anda kullanmak en efektif sonucu verecektir. Yine de proje durumuna göre yalnızca bir tanesi de kullanılabilir. 

Bouncing durumunun ölçüm cihazlarıyla kaydedilmiş görselleri:
![BouncingImg](https://github.com/hidroel/staj-2024/raw/main/documents/images/Staj-2024-Bouncing1.png)
![BouncingImg](https://github.com/hidroel/staj-2024/raw/main/documents/images/Staj-2024-Bouncing2.png)


