# ADC Nedir?

ADC'ler analog olan sinyali dijitale dönüştüren araçlardır. Gelen sinyalin voltaj değerine göre dijital bir çıktı verir. ADC'lerin hemen hemen hepsi 0-5v aralığında çalışır. Bundan dolayı analog sensörler genelde 0 - 5v aralığındadır. MCU gelen veriyi dijital olarak okuyabildiği için herhangi bir sensörden veri okurken ADC kullanılarak analog olan veri dijitale çevirilerek MCU'ya aktarılır. Basit bir deyişle MCU'nun anlayacağı dilde aktarılır.

# ADC Türleri

- **Çift Eğimli** - Ucuz ve çok yavaş
- **Flaş** - Çok hızlı ama bit çözünürlüğü düşük
- **Boru hattı** - Çok hızlı ama bit çözünürlüğü düşük
- **SAR** - Hızı ve çözünürlüğü iyi (Çok tercih edilen)
- **Delta Sigma** - Hızı ve çözünürlüğü iyi

# Bit Çözünürlüğü

Yüksek bit çözünürlüğünde adım aralıkları daha kısadır. Yani daha hassas ölçümler yapılabilir. Bit çözünürlüğü düştükçe adımların aralığı artacağından gelen verinin hassasiyeti azalır.

# 4-20 mA Protokolü

4-20 mA bir dijital iletişim protokolüdür. Adından da anlaşıldığı gibi 4 ile 20 mA arasında akım değerleriyle haberleşme sağlar. Toplam 16 mA'lık bir aralığı bulunur. 0-5v, 0-10v gibi diğer analog ölçüm çeşitlerine göre avantajları ve dezavantajları vardır. 4 mA en alt seviyeyi, 20 mA ise en üst seviyeyi temsil eder. Sensörden gelen veri tipine bağlı olarak uygun aralıklama yapılır.

4-20 mA akım kaynaklı bir haberleşme çeşidi olduğu için güç kaynağından kesintisiz ve sabit akım alması gereklidir. Bu sağlandığında taktirde veri bozulmadan ve gürültü olmadan uzun mesafelerde yol kat edebilir. Voltaj kaynaklı haberleşmelerde mesafe uzadıkça gürültü artacaktır ve verinin doğruluğu kaybolacaktır.

4-20 mA'da 4 mA altına inme veya 20 mA üstüne çıkma durumu olursa sistemde bir hata olduğuna işaret eder. Gelen veri doğru kabul edilmez.

# 4-20 mA ADC İle Okuma

ADC'lerin büyük bölümü voltaj ile okuma yaparlar. 4-20 mA ise akım ile veri aktarımı sağlar. Bundan dolayı ADC ile bu verinin okunabilmesi için voltaj aralıklarına dönüştürülmesi gereklidir. Veri iletim hattı 4-20 mA protokolü ile ADC'ye kadar gelir. ADC'ye aktarılmadan önce bir direnç devresi kurularak akıma bağlı voltaj değişikliği sağlanır. Bu aşamada genellikle 250 ohm direnç kullanılmaktadır. Bu voltajı ADC okur ve dijitale çevirerek MCU'ya iletir.

![4-20ma Görseli](https://www.hgsind.com/sites/default/files/content_images/Currentloop_Figure1b.jpg)

# 0-5v Protokolü
0-5v protokolü, gerilim ile veri iletimi sağlayan bir protokoldür. Sensörden çıkan gerilim 0 ile 5v arasında olmak zorundadır. Sensörün ölçüm aralığına göre 0-5v arasında bir gerilim çıkışı yapar ve bu ADC tarafından okunur. Örneğin 0-100 derece arasında sıcaklık ölçen bir sıcaklık sensörü 0-5v protokolü kullanıyorsa 0 derece 0 volta, 50 derece 2,5 volta, 100 derece ise 5 volta karşılık gelecektir. ADC'ler gerilim kaynaklı okuma yaptığı için ekstra herhangi bir dönüşüm yapmaya gerek kalmamaktadır.

# 0-10v Protokolü
0-10v protokolü 0-5v ile aslında birebir aynıdır. Çalışma prensibinde hiçbir farklılık yoktur. Aradaki tek fark aralığın daha geniş olması yani 0-10v arasında olmasıdır. Bu sayede daha fazla parçalama yapılabilir ve ölçüm hassasiyeti artırılabilir. Tabii bu hassasiyet için ADC'nin çözünürlüğünün de buna uygun olması gereklidir.

![0-5v Görseli](https://www.researchgate.net/profile/Viorel-Miron-Alexe/publication/322087251/figure/fig4/AS:667627429048361@1536186191791/Representation-of-the-sensors-analog-signal-offsetted-to-25V-DC-with-the-voltage.ppm)

![0-5v 0-10v Farkı](https://andykong.org/static/analogscalinggraphic.png)

# Diferansiyel ve Tek Uçlu Bağlantılar
Tek Uçlu (Single-Ended) Bağlantı: Bu bağlantı türü, bir analog sinyalin referans olarak ortak bir toprak hattına (GND) karşı ölçüldüğü bir yöntemdir. Tek bir giriş hattı ve bir toprak hattı kullanılır. Bu, basit ve yaygın olarak kullanılan bir yöntemdir, ancak gürültüye karşı hassas olabilir.

Diferansiyel Bağlantı: Diferansiyel bağlantıda, iki giriş hattı (pozitif ve negatif) kullanılır ve sinyal bu iki hat arasındaki fark olarak ölçülür. Bu yöntem, ortak mod gürültüsünü (örneğin elektromanyetik girişim) ortadan kaldırarak daha güvenilir ve doğru ölçümler sağlar. Özellikle uzun mesafelerde veya gürültülü ortamlarda tercih edilir.

# Çoklama
Analog Multiplexer (Çoklayıcı): Çoklayıcılar, tek bir ADC (Analog to Digital Converter) kullanarak birden fazla analog sinyali okumanın bir yolunu sunar. Çoklayıcı, giriş sinyalleri arasında hızla geçiş yaparak birden fazla kaynaktan gelen verileri tek bir ADC üzerinden işler. Bu, çok kanallı sistemlerde maliyetleri düşürmek için kullanılır.
# Paralel Bağlantılar

Paralel bağlantı, aynı anda birden fazla sinyalin iletilmesi için kullanılır. Bu yöntemde, her bir sinyalin kendi hattı vardır, bu da daha hızlı veri iletimine olanak tanır, ancak daha fazla kablo gerektirir.

# Aktif Pasif Filtreleme
Aktif Filtreleme: Bu yöntemde, sinyal işlemeyi geliştirmek için aktif bileşenler (örneğin, op-amp'ler) kullanılır. Aktif filtreler, belirli frekanslardaki gürültüyü azaltarak sinyal kalitesini artırabilir ve sinyalin daha hassas bir şekilde işlenmesini sağlar.

Pasif Filtreleme: Pasif bileşenler (dirençler, kapasitörler, indüktörler) kullanılarak yapılan filtreleme, genellikle daha basittir ve güç gerektirmez. Pasif filtreler, istenmeyen frekansları ve gürültüyü bastırmak için kullanılır, ancak aktif filtreler kadar esnek değildirler.

# Analog Demodülasyon
Analog sinyallerin farklı taşıyıcı frekanslar üzerine bindirilip, daha sonra demodüle edilerek asıl bilgiye erişildiği bir yöntemdir. Bu, özellikle radyo frekansı iletişimlerinde kullanılır.

# Zaman Bölmeli Çoklama
Birden fazla analog sinyalin, belirli zaman dilimlerinde sırayla tek bir hat üzerinden iletilmesi yöntemidir. Her sinyal belirli bir zaman aralığında gönderilir ve bu zaman dilimleri arasında geçiş yaparak birden fazla sinyalin tek bir hat üzerinden iletilmesi sağlanır.

# ADC Bit Çözünürlüğü Önemi

ADC'ler 8 bit, 10 bit, 16 bit gibi birçok farklı bit çözünürlüğüne sahiptir. Bit çözünürlüğü kullanım alanına göre oldukça önemlidir. Bit çözünürlüğü ADC'nin dijital adım sayısının belirtir. 2 üzeri bit sayısı şeklinde adım sayısı bulunur. Örneğin 8 bitlik bir ADC 256 adım aralığına sahiptir. 16 bitlik bir ADC 65536 adım sayısına sahiptir. Adım sayısı sensörlerden okunan verinin hassasiyetini belirler. Örneğin 0-256 PSI aralığında basınç ölçen bir sensördeki veri 8 bitlik bir ADC ile okunursa basınç değişimleri 1 PSI olarak değişir, ara değerler ölçülemez. Bu sensördeki veri 16 bitlik bir ADC ile okunursa 0,01 PSI gibi küçük değerlerin değişimi bile dijital olarak okunabilir.

Bir sensörden veri okunduğunda ADC bunu dijital bir sayısal değere çevirerek MCU'ya aktarır. Bu sayede MCU tarafından sensörden gelen veri doğru bir şekilde yorumlanabilir.

# STM32 İle ADC Kullanımı

ADC, STM32 ile denetleyicilerin üzerinde dahili olarak bulunmaktadır. Seçilen MCU modeline göre ADC'nin kaç bit çözünürlüğe sahip olduğu öğrenilmelidir.

Kullanılan MCU'nun datasheet'inde hangi pinlerin ADC olarak kullanılabileceği belirtilmiştir. Öncelikle buradan pin seçimi yapılmalıdır. Ardından bu pin STM32Cube ile ADC olarak yapılandırılmalıdır. Sonrasında ADC'nin çözünürlüğü (bit) yapılandırılmalıdır. Daha sonra Hz cinsinden örnekleme hızı yapılandırılmalıdır. Bu örnekleme hızı ADC'nin saniyede kaç kere analog veriyi dijitale çevireceğini belirler. Projenin ihtiyacına göre burada frekans ayarlaması yapılır.

İlgili sensörün standart VCC GND bağlantıları yapıldıktan sonra analog çıkışı STM32'nin ADC olarak belirlenen pinine bağlanır. Gerekli diğer ayarlar da yapıldığı için bu aşamadan sonra ADC belirtilen sürelerde sensörden gelen analog veriyi dijitale yani sayısal bir biçime çevirerek MCU'ya aktarır. Sensörün ölçüm aralığına göre dijital aralıkların karşılığı hesaplanır ve istediğimiz birimde ölçüm sonucunu alabiliriz. Bu aşamadan sonra MCU'nun sensörden gelen veriye göre ne yapacağı projeye göre belirlenebilir.

Eğer projede birden fazla analog veri toplanacaksa MCU'nun diğer GPIO pinleri de ADC olarak tanımlanıp her birinden farklı kanallar üzerinde veri toplanabilir. Bu sayede tek bir MCU ile birden fazla sensörden veri alınarak yorumlanabilir.

> Not: STM işlemciler genellikle SAR tipi ADC kullanmaktadır.

# ADC'yi Verimli Kullanmak İçin Yapılabilecekler

- ADC pinlerinin girişinde çok küçük (0,1 uF) kapasitörler koyularak gürültü azaltılır.
- Analog veri hattı mümkün olduğunca kısa tutularak gürültü azaltılır.
- Analog veri hattı manyetik alan üreten bileşenlerden uzak tutularak manyetik gürültüden korunur.
- Analog sinyal yolları dijital sinyal yollarıyla çok yakın olmamalıdır.


# Tarım Sulama Sistemi Ek Modülü ADC Kullanımı
Projemizde kullandığımız basınç sensörünün analog çıkış gerilimi 0.5v ile 4.5v arasındadır. ADC olarak MCU üzerindeki dahili ADC'yi kullanacağımız için bu aralık ihtiyacımızı karşılamamakta. MCU üzerindeki dahili ADC maksimum 3.3v gerilime kadar desteklediği için sensörün kendi aralığını kullanamıyoruz. Bundan dolayı, bu gerilim aralığını 0 - 3.3v aralığına düşürmemiz gerekiyor. Gerilimi istediğimiz aralığa düşürmek için iki adet yöntem bulunuyor.

## Gerilim Bölücü Kullanımı

Gerilim bölücü basit bir devre ile sağlanmaktadır. Bu devre en temel ohm yasasına göre, gerilimin dirençle orantılı geçeceğine dayanarak kurulur. Bu sayede gerilim oransal olarak azaltılabilir. Aşağıda gerilim bölücü devresinin şemasını görebilirsiniz.

![GerilimBolucuDiyagram](https://github.com/hidroel/staj-2024/raw/main/documents/images/Staj-2024-GerilimBolucu.png)

Şekilde ifade edilen R1 ve R2 dirençleri ihtiyaca uygun şekilde belirlenmelidir. Bunu hesaplamak için genel bir formül bulunmaktadır.

Bu formüller esasında V = I * R formülünden türetilmektedir. Şimdi gerilim bölücünün genel formülüne bakalım.

Vout = Vin * (R2/R2+R1)

Bu formülde gerekli yerleştirmeler yapılarak giriş voltajı istenilen çıkış voltajına getirilebilir. Ancak projemizde sabit bir gerilim değil, değişken bir gerilim var. Çünkü sensörden analog veri okuması yapacağız. Bu durumda belli bir aralığa düşürecek şekilde bir çözüm uygulamamız gerek. Bunu da şu şekilde yapabiliriz:

Vin aralığı: 0.5v - 4.5v
Vout aralığı: 0v - 3.3v 

Voutmax / Vinmax hesaplamasını yaptığımız 0.733 oranına ulaşıyoruz. Bu, gelen her değeri 0.733 ile çarparak düşürmemiz anlamına geliyor. Gerilim düşürmesini ise gerilim bölücü devresi ile sağlayacaktık. Yani, Vin değerini çarpmamız gereken sayıyı bulmuş olduk. Ana formüle baktığımızda Vin'in R2/R2+R1 ile çarpıldığını görüyoruz. Öyleyse;

R2/R2+R1 = 0.733
Gerekli matematiksel işlemler yapıldığında R2/R1 oranı yaklaşık olarak 2.74 yapmaktadır. Bu oranı sağlayacak 2 adet direnç değeri belirleyerek gerilim bölücü devresini tamamlayabiliriz. Örneğin;

R1 = 1k Ohm
R2 = 2,74k Ohm 

Özetle, projemiz için gerilim bölücü devresi kullandığımızda R1 direnci 1k Ohm, R2 direnci 2,74k Ohm kullanılarak 0.5v - 4.5v aralığı 0 - 3.3v aralığına uygun hale gelecektir. Örneğin 4.5v olan maksimum sensör verisi, ADC'ye girerken 3,2985 yani 3.3v gibi bir değerle girecektir. 

**Not:** Kullanılacak direnç değeri tam olarak bulunmaz ise seri bağlantı yapılarak birden fazla dirençle tek bir R1 direnci veya R2 direnci üretilebilir. Ancak dirençlerin sapma aralıklarının iyi ölçülmesi gereklidir.

Gerilim bölücülerin en büyük dezavantajı analog verideki hassasiyetin azalmasıdır. Geniş aralıkta olan veriyi dirençler kullanarak dar aralığa düşürdüğümüz için aralıklar azalacak yani hassasiyet azalacaktır. Büyük hassasiyet gerektiren projeler için gerilim bölücü devresi kullanmak uygun bir yöntem değildir. Bu projede bu kadar ciddi hassasiyete ihtiyaç duymadığımız için gerilim bölücü devresini rahatlıkla kullanabiliriz.

## Op-Amp Kullanımı

Gerilimi istediğimiz aralığa düşürmenin bir diğer yolu da Op-Amp kullanmaktır. Op-Amp gerilim bölücüye kıyasla daha maliyetli ancak daha hassas sonuçlar veren bir çözümdür. Gerilim bölücünün yaptığı işin aynısını başka methodlar ile yapmaktadır. Op-Amp görseli aşağıdadır: 

![OpAmpDiyagram](https://github.com/hidroel/staj-2024/raw/main/documents/images/Staj-2024-OpAmp.jpg)

Op-Amp'ın kullanımına gelecek olursak;

 +Giriş (Non-Inverting Input):

Op-amp'in bu pinine uygulanan voltaj, çıkış voltajını belirleyen ana sinyaldir. Bu pin, sinyalin doğrudan amplifiye edildiği giriştir. Eğer op-amp'in çıkış voltajını belirlemek için sinyali bu pin aracılığıyla verirsen, op-amp bu voltajı amplifiye eder ve çıkışta uygun gerilimi sağlar.
-Giriş (Inverting Input):

Bu pin, op-amp'in giriş voltajlarının ters yönlü etkisini ifade eder. Non-inverting pin ile bu pin arasındaki fark, op-amp'in çıkışını belirler. Eğer bu pinin voltajı artırılırsa, çıkış voltajı azalır ve tam tersi.Eğer Op-amp'in çıkış voltajını bu pin ile geri besleyerek, sinyali ters yönde kontrol edebilir veya belirli bir kazanç ayarı yapabiliriz.

+Vss (Pozitif Besleme Voltajı):

Op-amp'in çalışması için gerekli pozitif besleme voltajını sağlar. Op-amp'in çalışma aralığını belirler ve çıkış voltajının üst sınırını belirler. Op-amp'in doğru şekilde çalışabilmesi için yeterli pozitif besleme voltajı sağlamalıyız.

-Vss (Negatif Besleme Voltajı):

Op-amp'in çalışması için gerekli negatif besleme voltajını sağlar. Çıkış voltajının alt sınırını belirler. Negatif besleme voltajı, op-amp'in sinyalleri doğru şekilde işleyebilmesi için gereklidir. 

Çıkış (Output):
Op-amp'in işlem sonucunda elde ettiği amplifiye edilmiş voltajı bu pin üzerinden dışarıya verir. Bu pin, diğer devre elemanları ile bağlantı kurarak, işlem sonucunu sağlar. Çıkış voltajı, op-amp'in amplifiye ettiği sinyal olup, bu voltajı ADC'ye bağlayabiliriz.

Op-Amp kullanımında gain yani kazanç hesaplaması yapılarak yükseltme ve düşürme uygulanabilir. Op-Amp genellikle yükseltme işlemlerde daha sık tercih edilir ancak düşürme için de kullanılabilmektedir. Kazanç aslında pozitif bir terimdir ancak kazancı 1'den küçük bir değer olarak belirlediğimizde düşürme işlemi için Op-Amp kullanabiliriz.

**Not:** Inverting Amplifier voltaj yükseltme anlamına gelmektedir.
**Not:** Non-Inverting Amplifier voltaj düşürme anlamına gelmektedir.
