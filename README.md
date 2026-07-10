# PowerElectronics\_Intern\_Tasks

Staj Görevleri, LTspice Simülasyonları ve KiCad Donanım Tasarımları.



Bu proje, Fırçasız DC (BLDC) motorları sürebilmek için tasarlanmış bir güç katı  devresidir. Temelinde, klasik "H-Köprüsü" mantığının 3 fazlı motorlar için genişletilmiş hali olan 3'lü Yarım Köprü  topolojisi yer alır.

&#x20;Mikrodenetleyiciden gelen zayıf kontrol sinyalleri (PWM),  kapı sürücü (gate driver) entegreleri tarafından güçlendirilir. Bu PWM sinyalleri, devrenin anahtarlama elemanı olan 6 adet güç MOSFET'inin gatelerine iletilerek onların nano saniyeler içinde açılıp kapanmasını sağlar.

&#x20;6 MOSFET kesinlikle rastgele veya hepsi aynı anda açılmaz. Motoru döndürmek için 6 Adımlı Komütasyon denilen kusursuz bir sıra izlenir. Her adımda sadece 2 faz aktiftir: Bir fazın üst MOSFET'i  ve diğer bir fazın alt MOSFET'i açılır,3.faz boştadır. 

&#x20;Aynı faza ait alt ve üst MOSFET'ler, kısa devreyi önlemek için asla aynı anda açılmaz. Araya her zaman mikrosaniyelik bir ölü zaman (dead-time) konur.

&#x20;Bu ardışık aç-kapa işlemleri sonucunda ortaya çıkan bu yüksek akımlı enerji, kartın U, V ve W faz çıkışlarından motorun içindeki bobinlere iletilerek dönen bir manyetik alan yaratır ve rotoru döndürür.

&#x20;Motorun kararlı dönebilmesi için mikrodenetleyicinin, motorun içindeki mıknatısın (rotorun) o an fiziksel olarak nerede olduğunu bilmesi gerekir.

Hall sensörü olmayan motorlarda, rotorun konumunu bulmak için Back-EMF (Zıt EMK) yöntemi kullanılır. 6 adımlı komütasyon mantığında her an 2 faza akım verilirken, 3. faz her zaman boşta bırakılır.

&#x20;Motor dönerken tıpkı bir jeneratör gibi kendi içinde bir elektrik üretir. İşte boşta bırakılan bu 3. fazdan, motorun dönüşünden kaynaklanan Zıt EMK voltajı okunur. Bu sayede fiziksel bir sensöre ihtiyaç duymadan motorun anlık konumu tespit edilir ve bir sonraki PWM sinyalinin MOSFET'lere ne zaman gönderileceği kusursuz bir şekilde hesaplanır.



![Proje Ekranı](https://github.com/nurdagulocal66-collab/PowerElectronics_Intern_Tasks/raw/main/resimler/ekran1.png)

!\[Proje Ekranı](resimler/ekran2.png)

Bu proje, ilerleyen aşamalarda  motor sürücü kartı (inverter) olarak geliştirilebilir bir donanım altyapısına sahiptir. Tasarım sürecinde, sistemin kontrol edeceği motorun(42BLF01) maksimum tepe akımı 5.7 Amper olarak baz alınmıştır. Kart üzerindeki tüm yol genişlikleri, katman yerleşimleri ve komponent seçimleri tamamen bu akım değeri göz önüne alınarak yapılmıştır.



&#x20;Motorumuzun anlık olarak çekeceği 5.7A tepe akımının yolları eritmemesi, kartı aşırı ısıtmaması ve voltaj düşümüne (voltage drop) sebep olmaması için standart PCB kalınlık hesaplamalarını kullandık. 1 oz standart bakır kalınlığı için güç hatlarını ve motor faz çıkışlarını (U, V, W) 3 mm genişliğinde tasarlayarak kartın yüksek yük altında bile güvenle çalışmasını sağladık.Mikrodenetleyiciden çıkan, kapı sürücüye (gate driver) giden sinyal yollarını ve diğer lojik hatları 0.3 mm genişliğinde tuttuk.Bu yollardan yüksek bir akım geçmiyor, sadece veri ve tetikleme sinyalleri taşınıyor. Yolları ince tutarak hem kart üzerinde yer kazandık hem de sinyal yollarının birbirini etkilemesini engellemiş olduk.

&#x20; Kartın alt katmanını  hiç bölmeden tamamen kesintisiz bir toprak düzlemi  yaptık.

MOSFET'ler çok hızlı açılıp kapandığı için devrede ciddi bir elektromanyetik gürültü (EMI) oluşur. Alt katmandaki bu koca toprak alanı, gürültüyü emen bir kalkan görevi görerek kontrol sinyallerimizin temiz kalmasını sağlıyor.



&#x20;Motor anlık olarak 5.7A tepe akımı çekmek istediğinde özellikle ani kalkışlarda, güç hattında ciddi voltaj çökmeleri olur. 470 µF gibi büyük kapasiteli bu kapasitör, içinde yüksek miktarda enerji depolar. Hat gerilimi düşmeye çalıştığı anda bir pil gibi devreye girerek voltajı regüle eder ve sistemi besler. Güç girişine yakın konumlandırılmıştır.MOSFET'lerin nano saniyeler içinde açılıp kapanması, devrede  çok yüksek frekanslı elektriksel gürültüler (parazitler) üretir. 470 µF'lık büyük kapasitör hantaldır, bu hızlı gürültülere tepki veremez. İşte burada 100 nF devreye girer. Çok hızlı tepki veren bu minik kapasitörleri mosfet bacaklarının tam dibine koyduk. Böylece yüksek frekanslı parazitleri anında toprağa akıtarak devrenin güvenli çalışmasını sağladık.



!\[Proje Ekranı](resimler/ekran3.png)

!\[Proje Ekranı](resimler/ekran4.png)

!\[Proje Ekranı](resimler/ekran5.png)

!\[Proje Ekranı](resimler/ekran6.png)

















