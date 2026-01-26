# Power Devresi Nedir?
Power devresi, bir elektronik sistemin tüm bileşenlerine gerekli enerjiyi sağlamak için tasarlanmış bir devredir. Elektronik cihazların düzgün ve güvenilir bir şekilde çalışabilmesi için doğru voltaj ve akım değerlerinin sağlanması kritik öneme sahiptir. Power devresi, bu ihtiyacı karşılamak için güç kaynaklarını düzenler, dönüştürür ve filtreler. Kart üzerindeki en önemli devredir ve sistemin işleyişi için hayati önem taşır. Power devresinde kullanılan bileşenler şunlardır:

- Güç Kaynağı: Sistemin ana gücünü aldığı ekipmandır. Adaptör, akü, pil, batarya gibi herhangi bir şey olabilir.
- Dönüştürücüler: Sistemdeki bileşenlerin ihtiyacı olan voltaj her zaman güç kaynağı ile aynı değildir. Bu nedenle voltajı istenilen seviyelere çevirmek için dönüştürücüler kullanılır. Ayrıca, AC güç kaynağı varsa DC'ye çevirir.
- Filtreler: Gürültü ve dalgalanmaları azaltarak stabil bir güç sağlar. Kapasitörler ve indüktörler ile oluşturulan filtre devreleri ile bu sağlanır.
- Koruma Devreleri: Aşırı akım çekme, yüksek voltaj, kısa devre gibi durumlarda sistemin korunabilmesi için koruma devresi oluşturulur. Sigorta gibi bileşenlerle sistemin güvenliği sağlanır.

# Filtreler
Elektronik bileşenlerin sağlıklı çalışabilmesi için parazitlerden mümkün olduğunca uzak olması gereklidir. Buna power devresi de dahildir. Güç kaynağından gelen gerilim genellikle parazitli gelmektedir. Bu da diğer bileşenlerin sağlıklı çalışmasına engel olmaktadır. Bu nedenle, power devresinde çeşitli filtreler uygulamak zorundayız.

## LC ve CL Filtreleri

LC ve CL filtreleri paraziti azaltmak ve kesintisiz bir gerilim sağlamak amacıyla kullanılır. L, indüktörü C ise kapasitörü temsil eder. LC ve CL olarak ayrılmasının sebebi ise bağlantı şekillerinin farklı olmasıdır. İhtiyaca göre LC olarak veya CL olarak kullanılırlar. 

Filtrelerde alçak geçiş filtreleri ve yüksek geçiş filtreleri olarak iki ana çeşit bulunmaktadır. Düşük geçiş filtresi, belirli bir kesim frekansının altındaki sinyalleri geçiren, kesim frekansının üstündeki sinyalleri ise bastıran bir filtre türüdür. Yüksek geçiş filtresi ise belirli bir kesim frekansının üstündeki sinyalleri geçiren, kesim frekansının altındaki sinyalleri ise bastıran bir filtre türüdür. Projemizin power devresini yaparken aküden çıkan gerilimi sabit halde alabilmek için kullanacağımız filtre alçak geçiş filtresi olacaktır. Alçak geçiş filtrelerinin çeşitlerine şematik olarak bakalım.

#### CL Tipi Filtre
![CLFilter](https://github.com/hidroel/staj-2024/raw/main/documents/images/Staj-2024-CLFilter.png)
Giriş empedansı yüksek, çıkış empedansı düşük olduğunda kullanılır.
#### LC Tipi Filtre
![LCFilter](https://github.com/hidroel/staj-2024/raw/main/documents/images/Staj-2024-LCFilter.png)
Giriş empedansı düşük, çıkış empedansı yüksek olduğunda kullanılır.
#### Pi Tipi Filtre
![PiFilter](https://github.com/hidroel/staj-2024/raw/main/documents/images/Staj-2024-piFilter.png)
Giriş empendansı ve çıkış empadansı yüksek olduğunda kullanılır.
#### T Tipi Filtre
![TFilter](https://github.com/hidroel/staj-2024/raw/main/documents/images/Staj-2024-TFilter.png)
Giriş empendansı ve çıkış empadansı düşük olduğunda kullanılır.

İhtiyaca göre bu filtrelerden herhangi birisi kullanılabilir. Bu projenin power devresinde 12v çıkışı için pi tipi ve LC tipi filtre kullanabilirdik. Biz pi tipi filtre kullanmayı seçtik. Bunun sebepleri:

- Pi tipi filtreler daha geniş bir frekans aralığında filtreleme yapabildiği için daha net bir parazit temizliği yaparlar.
- Power'dan sonraki ilk filtre olarak kullanacağımızdan dolayı maksimum netlikte güç almamız gerekiyor.
- LC filtre ile arasında yalnızca bir kapasitörlük maliyet farkı bulunuyor. Bu düşük maliyet farkı proje bütçesini etkilemiyor.

# Voltajı Regüle Etmek
Projemizde 12v bir akü tarafından güç alıyoruz ancak 5v ve 3.3v ile çalışan bileşenler mevcut. Bundan dolayı 12 voltu hem 3.3v hem de 5v olarak düşürmemiz gerekiyor. Bu işleme "regüle" adı veriliyor. Voltaj regülesini yapmanın birden fazla yolu var. Şimdi bunlara kısaca değinelim ve projede hangi yöntemi kullanacağımızı açıklayalım.

### Anahtarlamalı Regülatörler
Anahtarlamalı regülatörler, voltajı düşürmek için bir anahtarlama elemanı (genellikle MOSFET) kullanır. Giriş voltajı hızlı bir şekilde açılıp kapanarak enerji düzenlenir ve endüktörler ile kapasitörler kullanılarak çıkış voltajı istenilen seviyede tutulur. Bu yöntem yüksek verimlilik ve geniş giriş voltajı aralığı sağlar.

### Doğrusal Regülatörler
Doğrusal regülatörler, voltajı düşürmek için bir direnç kullanarak giriş voltajı ile çıkış voltajı arasındaki farkı kaybederler. Bu yöntem, çıkış voltajını oldukça stabil tutar, ancak verimliliği genellikle düşük olur çünkü fazla enerji ısı olarak yayılır.

### Zener Diyot Regülatörleri
Zener diyot regülatörleri, bir zener diyotu kullanarak voltajı sabitler. Giriş voltajı, zener diyotun ters yönde çalışmasını sağlayacak şekilde seçilir ve bu diyot, belirli bir voltajda sabitler. Bu yöntem genellikle düşük akım uygulamaları için uygundur.

Voltajı düşürmek veya yükseltmek için bunların haricinde de yöntemler bulunuyor ancak yaygın kullanılan ve bu projede kullanılması potansiyel olan seçenekler bunlar. Her birinin kendine göre kullanım alanları mevcut.

Projemizde anahtarlamalı regülatörler kullanacağız. Bunun birden fazla sebebi var:

- Akünün giriş voltajı sabit olarak 12v olmayacak. Akü tam şarjda iken 13 voltlara kadar çıkabilirken, akü deşarj olurken 9 voltlara kadar düşecektir. Bu nedenle bize geniş giriş aralığına sahip bir regülatör gerekiyor.
- Doğrusal regülatörler ve zener diyotlar sistemin verimliliğini oldukça düşürmektedir. Boşa giden güç ısıya dönüşerek aynı zamanda sistemin ısınmasını sağlamaktadır. Eğer küçük miktarlarda düşüş yapacak olsaydık tercih edilebilirdi ancak 5v ve 3.3v'a regüle etmek için projemize uygun değiller.
- Anahtarlamalı regülatörler güç kaybını minimuma indirerek akımın korunmasını sağlarlar. Bu sayede oldukça az ısınma yaparlar.

### Anahtarlı Regülatör Kullanımı
Anahtarlı regülatörler bir entegreden ve yan bileşenlerden oluşur. Entegre hazır olarak alınır, sonrasında ise çevre bileşenlerin devreleri çizilerek çalışır hale getirilirler. Kullanılacak entegrenin datasheet'inde yer alan çevre bileşenlere göre bir devre çizimi yapılabilir. Çevre bileşenlerde genellikle endüktör, kapasitör, diyot kullanılır. 

**Önemli Not:**Kullanılan diyotun sebep olduğu voltaj kaybını hesap ederek sistemi oluşturmak oldukça önemlidir. Diyot üzerinden yük geçişi olduğunda bir miktar voltaj kaybına sebep olur.

# Güvenlik Sistemleri

## Aşırı Gerilim Koruma Devresi

Aşırı gerilim koruma devresi oluşturmak ve kullanmak için öncelikle gerekli bileşenleri seçmeliyiz. Genellikle, bir voltaj referansı olarak Zener diyot veya voltaj referansı, bir komparatör ve bir anahtar elemanı (MOSFET veya röle) kullanıyoruz. Komparatörün pozitif girişine Zener diyotun katodunu bağlayıp, anotunu giriş voltajına bağlıyoruz. Komparatörün negatif girişine ise giriş voltajını bağlıyoruz. Komparatörün çıkışını anahtar elemanına bağlayarak, aşırı voltaj algılandığında devreyi açacak şekilde düzenliyoruz. Eğer MOSFET kullanıyorsak, gate pinini komparatör çıkışına, source pinini toprağa ve drain pinini yükünüzün toprak hattına bağlıyoruz. Röle kullanıyorsak, rölenin bobinini komparatör çıkışına bağlıyoruz. Devreyi test ederken, giriş voltajını yavaşça artırarak Zener diyot üzerindeki voltajı izliyoruz ve voltaj eşiğine ulaşıldığında komparatör çıkışının değişip değişmediğini, MOSFET'in açılıp açılmadığını veya rölenin çekilip çekilmediğini kontrol ediyoruz. Bu adımları izleyerek, aşırı gerilim durumlarında sisteminizi otomatik olarak koruyabiliyoruz.
## Aşırı Akım Koruma Devresi 

Aşırı akım koruma devresi oluşturmak ve kullanmak için öncelikle uygun bileşenleri seçmeliyiz. Genellikle, bir akım sensörü veya şönt direnç, bir komparatör ve bir anahtar elemanı (MOSFET veya röle) kullanıyoruz. Akım sensörü veya şönt direnci, akımı ölçmek için kullanılır ve bu ölçüm, komparatörün bir girişine bağlanır. Komparatörün diğer girişine, belirlenen akım eşiğini temsil eden bir referans voltajı bağlarız. Komparatörün çıkışını anahtar elemanına bağlayarak, aşırı akım algılandığında devreyi açacak şekilde düzenleriz. Eğer MOSFET kullanıyorsak, gate pinini komparatör çıkışına, source pinini toprağa ve drain pinini yükünüzün toprak hattına bağlıyoruz. Röle kullanıyorsak, rölenin bobinini komparatör çıkışına bağlıyoruz. Devreyi test ederken, akım seviyesini yavaşça artırarak şönt direncin üzerindeki voltajı izleriz ve akım eşiğine ulaşıldığında komparatör çıkışının değişip değişmediğini, MOSFET'in açılıp açılmadığını veya rölenin çekilip çekilmediğini kontrol ederiz. Bu adımları takip ederek, aşırı akım durumlarında sisteminizi otomatik olarak koruyabiliriz.

## Kısa Devre Koruması
Kısa devre durumunda sistem çok yüksek akım çekeceği için aşırı akım koruma devresi bağlantıyı kesecek ve sistemi koruyacaktır. Tepki süresi boyunca geçen sürede bazı ekipmanlar zarar görebilir. Zararı minimuma indirmek için aşırı akım koruma devresinde tepki süresini minimize edecek bileşenler kullanmalıyız.

