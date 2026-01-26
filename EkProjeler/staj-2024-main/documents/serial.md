# Seri Haberleşme Protokolleri

Seri haberleşme, verilerin bir cihazdan diğerine belirli bir sırayla gönderildiği bir iletişim yöntemidir. Bu yöntem, özellikle mikrodenetleyiciler, sensörler ve diğer elektronik bileşenler arasında veri aktarımı için yaygın olarak kullanılır. En sık kullanılan seri haberleşme protokolleri arasında UART, SPI ve I2C bulunur.

## UART (Universal Asynchronous Receiver/Transmitter)

UART, iki cihaz arasında veri alışverişini sağlayan basit bir seri haberleşme protokolüdür. Bu protokol, veri iletimini senkronize etmek için saat sinyaline ihtiyaç duymaz. Veriler, belirli bir hızda (baud rate) gönderilir ve alıcı cihaz bu hıza göre verileri okur.

- **Avantajları:**
  - Basit ve yaygın bir haberleşme yöntemi.
  - Saat sinyali gerektirmez.
  - İki cihaz arasında doğrudan bağlantı sağlar.

- **Dezavantajları:**
  - Aynı anda sadece iki cihaz arasında iletişim kurulabilir.
  - Senkronizasyon hatalarına duyarlıdır.

## SPI (Serial Peripheral Interface)

SPI, genellikle yüksek hızda veri iletimi gerektiren uygulamalarda kullanılan bir seri haberleşme protokolüdür. Bu protokol, bir ana cihaz (master) ve bir veya daha fazla bağlı cihaz (slave) arasında veri iletişimini sağlar. SPI, dört temel hat kullanır: saat (SCLK), ana cihaz veri çıkışı (MOSI), bağlı cihaz veri çıkışı (MISO) ve bağlı cihaz seçimi (SS).

- **Avantajları:**
  - Yüksek veri iletim hızı sağlar.
  - Birden fazla bağlı cihazla iletişim kurulabilir.
  - Senkron veri iletimi sayesinde güvenilir iletişim.

- **Dezavantajları:**
  - Daha fazla kablo gerektirir (4 hat).
  - Bağlı cihaz sayısı sınırlıdır.

## I2C (Inter-Integrated Circuit)

I2C, düşük hızda veri iletimi gerektiren uygulamalar için tasarlanmış, iki hatlı bir seri haberleşme protokolüdür. I2C, bir ana cihaz (master) ve birçok bağlı cihaz (slave) arasında iletişim kurmayı mümkün kılar. Bu protokolde, veri iletimi ve saat sinyali için sadece iki hat kullanılır: veri hattı (SDA) ve saat hattı (SCL).

- **Avantajları:**
  - Az sayıda hat gerektirir (2 hat).
  - Birden fazla cihazı aynı veri hattında yönetebilir.
  - Basit bağlantı yapısı.

- **Dezavantajları:**
  - Veri iletim hızı SPI kadar yüksek değildir.
  - İletişimde çakışma (collision) riski vardır.



MCU ile seri haberleşme için örnek diyagram aşağıdadır:

![Serial Port Diagram](https://raw.githubusercontent.com/hidroel/staj-2024/main/documents/images/Staj-2024-Serial-Port-Diagram.png)
