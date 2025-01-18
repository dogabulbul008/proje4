# proje4

Hibernation Modu ile GPIO Kullanımı ve RTC Tabanlı Uyanma
Bu proje, bir mikrodenetleyicinin (örneğin, TI TM4C serisi bir mikrodenetleyici) Hibernation (Uyku) Modu özelliklerini kullanarak sistemin düşük güç tüketimini nasıl sağlayabileceğini gösterir. Bu proje aynı zamanda bir GPIO pini (kırmızı LED) ve RTC (Real-Time Clock) tabanlı uyandırma işlemini içermektedir.

Projenin Amacı

Bu projede:
Hibernation (Uyku) Modu kullanılarak cihazın enerji tasarrufu yapması sağlanır.
Real-Time Clock (RTC) kullanılarak cihazın belirli bir süre sonra otomatik olarak uyanması sağlanır.
Uyuma öncesi bir kırmızı LED yakılır, uyandıktan sonra bu LED söndürülür.

Donanım Gereksinimleri
TI Tiva C LaunchPad (TM4C123 veya benzeri bir model)
On-board kırmızı LED (GPIO_PIN_1, Port F) ya da harici bir LED.

Kodun Adım Adım Çalışma Mantığı
Sistem Saati Ayarı:
Sistem saati, ana osilatörü (16 MHz) kullanacak şekilde ayarlanır.
Bu, tüm modüllerin zamanlama işlemleri için temel oluşturur.
Hibernation Modülünün Etkinleştirilmesi:
Hibernation modülü aktif hale getirilir ve sistem saati bu modüle bağlanır.

RTC'nin Sıfırlanması ve Etkinleştirilmesi:
RTC, sıfırlanarak 0'dan başlatılır.
RTC modülü aktif hale getirilir ve zaman sayaçları çalışmaya başlar.

Uyandırma Kaynaklarının Ayarlanması:
Hibernation modu için iki uyandırma kaynağı belirlenmiştir:
RTC Match (RTC Eşleşme): RTC sayaç değeri belirlenen süreye ulaştığında cihaz uyanır.
Wake Pin (Harici Uyandırma Pin): Belirli bir harici tetikleyici ile cihaz uyandırılabilir.

Uyku Süresinin Ayarlanması:
RTC Match, mevcut zaman değeri ile 10 saniye sonrasını ayarlayacak şekilde yapılandırılmıştır.

GPIO ve LED Ayarları:
GPIO Port F etkinleştirilir.
Port F'deki kırmızı LED çıkış olarak ayarlanır.
Uyku moduna geçmeden önce LED yakılır.

Hibernation Moduna Geçiş:
HibernateRequest() fonksiyonu ile cihaz uyku moduna alınır.
Uyku sırasında cihaz minimum güç tüketimi yapar.

Uyandıktan Sonra Çalışma:
RTC Match veya uyandırma pini tetiklendiğinde cihaz uyanır.
Uyandıktan sonra LED söndürülür ve diğer işlemler gerçekleştirilir.

Fonksiyonlar ve Tanımlamalar
SysCtlClockSet(): Sistem saatini yapılandırır.
SysCtlPeripheralEnable(): Belirli bir çevresel birimi etkinleştirir.
SysCtlPeripheralReady(): Çevresel birimin kullanıma hazır olup olmadığını kontrol eder.
HibernateEnableExpClk(): Hibernation modülünü etkinleştirir ve saat kaynağını bağlar.
HibernateRTCSet(): RTC sayacını belirli bir değere sıfırlar.
HibernateRTCEnable(): RTC'yi etkinleştirir.
HibernateWakeSet(): Uyandırma kaynaklarını belirler.
HibernateRTCMatchSet(): RTC sayaç eşleşme değerini ayarlar.
HibernateRequest(): Cihazı uyku moduna alır.
GPIOPinTypeGPIOOutput(): Belirli bir GPIO pinini çıkış olarak ayarlar.
GPIOPinWrite(): GPIO pinine lojik 1 veya lojik 0 yazmak için kullanılır.

Projenin Çalıştırılması
Proje Hazırlığı:
Gerekli donanım (örneğin Tiva C LaunchPad) bağlanır.
Kod, Code Composer Studio (CCS) veya benzeri bir geliştirme ortamında derlenir ve mikrodenetleyiciye yüklenir.

Projenin Çalışma Aşamaları:
Cihaz açıldıktan sonra kırmızı LED yanar.
RTC 10 saniye geri sayım yapar.
10 saniye sonra cihaz uyku modundan çıkar ve kırmızı LED söner.

Dikkat Edilmesi Gerekenler
Enerji Tüketimi: Hibernation modu cihazın minimum enerji harcamasını sağlar. Ancak diğer çevresel birimlerin kapatıldığından emin olun.
Uyandırma Süresi: RTC veya harici pin üzerinden cihaz uyandırılabilir. Bu proje yalnızca RTC Match ile uyandırmayı kapsar.
GPIO Bağlantıları: Kırmızı LED'in doğru GPIO pinine bağlı olduğundan emin olun (GPIO_PIN_1, Port F).

Geliştirme İçin Öneriler
Daha Fazla Uyandırma Kaynağı Ekleyin:
Harici bir buton gibi başka bir uyandırma kaynağı eklenebilir.
Enerji Tüketim Ölçümü:
Multimetre veya osiloskop ile enerji tüketimi ölçülebilir ve optimize edilebilir.
RTC Match Süresini Dinamik Yapın:
Kullanıcıdan alınan bir giriş ile RTC match süresini dinamik olarak ayarlayabilirsiniz.

Desteklenen Araçlar
Donanım: Tiva C LaunchPad (TM4C123)
Geliştirme Ortamı: Code Composer Studio (CCS)
Dil: C
