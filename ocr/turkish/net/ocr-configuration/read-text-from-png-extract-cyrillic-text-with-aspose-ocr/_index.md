---
category: general
date: 2026-03-07
description: Aspose OCR kullanarak PNG'den metin okuma ve Kiril metni çıkarma, görüntüyü
  metne dönüştürme ve Kiril dil paketini indirme konusunda bilgi edinin.
draft: false
keywords:
- read text from png
- extract cyrillic text
- convert image to text
- load image for ocr
- download cyrillic language pack
language: tr
og_description: Aspose OCR'i C#'ta kullanarak PNG'den metin okuma, Kiril alfabesi
  metnini çıkarma ve görüntüyü metne dönüştürmeyi öğrenin.
og_title: png'den metin oku – Aspose OCR ile Kiril metni çıkar
tags:
- Aspose OCR
- C#
- Image Processing
title: png'den metin oku – Aspose OCR ile Kiril metnini çıkar
url: /tr/net/ocr-configuration/read-text-from-png-extract-cyrillic-text-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# png'den metin oku – Aspose OCR ile Kiril alfabesi metnini çıkar

png dosyalarından **metin okumak** ve Kiril karakterlerini çıkarmak mı istiyorsunuz? Bu rehberde, Aspose OCR kullanarak png'den metin nasıl okunur, Kiril metni nasıl çıkarılır ve **görüntüyü metne dönüştürür** sadece birkaç C# satırıyla gösteriyoruz.  

Eğer bir Rus faturasının ekran görüntüsüne bakıp kelimeleri aranabilir bir dizeye nasıl dönüştüreceğinizi merak ettiyseniz, doğru yerdesiniz. Ayrıca **Kiril dil paketini** otomatik olarak **indirmenizi** de anlatacağız, böylece ekstra dosyalar aramanıza gerek kalmayacak.

## Ne elde edeceksiniz

Bu öğreticinin sonunda şunları yapabilecek durumdasınız:

* **OCR için bir görüntü yükleyin** doğrudan diskten ya da bir akıştan.  
* Motoru **Kiril dili** olarak ayarlayın, manuel indirme yapmadan.  
* Tanıma çalıştırın ve bir PNG dosyasından **Kiril metnini çıkarın**.  
* Tanınan metni konsola yazdırın – veritabanlarına, arama indekslerine veya başka herhangi bir iş akışına aktarabileceğiniz temiz, düz‑metin bir sonuç.

Harici hizmetler, bulut anahtarları yok, sadece Aspose OCR NuGet paketi ve birkaç C# satırı.

## Önkoşullar

* .NET 6.0 veya üzeri (kod .NET Core, .NET Framework ve .NET 5+ üzerinde çalışır).  
* Visual Studio 2022 veya tercih ettiğiniz herhangi bir editör.  
* Aspose.OCR NuGet paketi (`dotnet add package Aspose.OCR`).  
* Kiril karakterleri içeren bir PNG görüntüsü – örneğin `cyrillic_sample.png` adlı dosya `YOUR_DIRECTORY` klasöründe bulunmalı.

> **İpucu:** Visual Studio kullanıyorsanız, proje üzerine sağ‑tıklayın → **Manage NuGet Packages** → “Aspose.OCR” aratın ve en son stabil sürümü kurun.

---

## Adım 1 – Aspose OCR'ı kurun ve motoru oluşturun

İlk olarak OCR motoru örneğine ihtiyacımız var. `OcrEngine` sınıfı tüm işlemler için giriş noktasıdır.

```csharp
using Aspose.OCR;
using Aspose.OCR.Settings;

// Create an OCR engine – this object holds all settings and results
var ocrEngine = new OcrEngine();
```

> **Neden önemli:** Motor dil paketlerini, görüntü verisini ve tanıma seçeneklerini kapsüleler. Tek bir kez örnekleyip birden çok görüntüde yeniden kullanmak performansı artırabilir.

---

## Adım 2 – **ocr için görüntü yükle** ve dili ayarla

Şimdi motorun hangi görüntüyü işleyeceğini ve hangi dili arayacağını belirtiyoruz. `Language.Cyrillic` ayarı, ilk çalıştırmada gerekli dil paketini otomatik olarak indirir.

```csharp
// 1️⃣ Load the PNG that contains Cyrillic text
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/cyrillic_sample.png");

// 2️⃣ Tell Aspose we want to read Cyrillic characters
ocrEngine.Settings.Language = Language.Cyrillic;   // downloads pack if missing
```

> **Köşe durumu:** PNG dosyanız çok büyükse (5 MB üzeri) tanıma süresini hızlandırmak için önce yeniden boyutlandırmak isteyebilirsiniz. `Image` özelliği aynı zamanda bir `Stream` de kabul eder; böylece bellekte, bir web isteğinde ya da Azure Blob’da dosya sistemine dokunmadan yükleyebilirsiniz.

---

## Adım 3 – **görüntüyü metne dönüştür** tek bir çağrı ile

Tanıma, `Recognize()` metodunu çağırmak kadar basittir. Bu çağrıdan sonra `Text` özelliği çıkarılan dizeyi tutar.

```csharp
// Run the OCR engine – this does the heavy lifting
ocrEngine.Recognize();

// Grab the result; it’s plain Unicode text
string extractedText = ocrEngine.Text;
```

> **Arka planda ne oluyor?** Aspose, milyonlarca Kiril glifi üzerinde eğitilmiş bir sinir‑ağ‑tabanlı sınıflandırıcı çalıştırır. Kütüphane tüm bu karmaşıklığı soyutlar, siz sadece temiz Unicode alırsınız.

---

## Adım 4 – Sonucu çıktı olarak ver (ya da başka bir yere yönlendir)

Demo amaçlı metni konsola yazdıracağız, ancak kolayca bir dosyaya, veritabanına ya da bir arama indeksine yazdırabilirsiniz.

```csharp
// Show the OCR result in the console
Console.WriteLine("=== Recognized Cyrillic Text ===");
Console.WriteLine(extractedText);
```

**Beklenen çıktı** (`cyrillic_sample.png` dosyası “Привет мир” ifadesini içeriyorsa):

```
=== Recognized Cyrillic Text ===
Привет мир
```

Eğer çıktı bozuk görünüyorsa, görüntünün net olduğundan ve `Language.Cyrillic` ayarını yaptığınızdan emin olun. Motor varsayılan olarak İngilizce’yi kullanır; bu durumda Kiril karakterleri bilinmeyen semboller olarak değerlendirilir.

---

## Adım 5 – Tam, çalıştırılabilir örnek

Hepsini bir araya getirdiğimizde, yeni bir konsol projesine kopyalayıp yapıştırabileceğiniz bağımsız bir program elde ederiz.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Create the OCR engine
        // -------------------------------------------------
        var ocrEngine = new OcrEngine();

        // -------------------------------------------------
        // 2️⃣ Load the PNG and select Cyrillic language
        // -------------------------------------------------
        // Replace the path with the location of your PNG
        ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/cyrillic_sample.png");
        ocrEngine.Settings.Language = Language.Cyrillic; // auto‑downloads pack

        // -------------------------------------------------
        // 3️⃣ Perform recognition
        // -------------------------------------------------
        ocrEngine.Recognize();

        // -------------------------------------------------
        // 4️⃣ Output the extracted text
        // -------------------------------------------------
        Console.WriteLine("=== Recognized Cyrillic Text ===");
        Console.WriteLine(ocrEngine.Text);
    }
}
```

Dosyayı `Program.cs` olarak kaydedin, `dotnet run` komutunu çalıştırın ve Kiril metninin konsola yazdırıldığını görmelisiniz.

---

## Sık sorulan sorular & sorun giderme

| Soru | Cevap |
|----------|--------|
| **Dil paketi indirilemezse ne yapmalı?** | Makinenin internet erişimi olduğundan emin olun. Paket `%USERPROFILE%\.Aspose\OCR\Languages` içinde önbelleğe alınır. Bu klasörü silmek yeni bir indirme başlatır. |
| **Kiril dışındaki dilleri de okuyabilir miyim?** | Tabii ki – `Language.Cyrillic` yerine `Language.English`, `Language.Arabic` vb. kullanın. Aynı otomatik indirme mantığı geçerli olur. |
| **PNG çok gürültülü – sonuçlar kötü. Ne yapabilirim?** | Görüntüyü ön‑işleme tabi tutun: kontrastı artırın, gri tonlamaya çevirin veya medyan filtresi uygulayın. Aspose OCR ayrıca `Settings.ImagePreprocess` seçenekleri sunar. |
| **Her kelime için sınırlayıcı kutular (bounding box) almak mümkün mü?** | Evet, `Recognize()` sonrası `ocrEngine.Regions` özelliğini inceleyerek tespit edilen her kelimenin dikdörtgenini alabilirsiniz. |
| **Üretim ortamında lisansa ihtiyacım var mı?** | Ücretsiz değerlendirme sürümü 100 sayfaya kadar çalışır. Ticari projeler için lisans satın alın – değerlendirme filigranını kaldırır ve yüksek‑hızlı toplu işleme özelliğini açar. |

---

## Sonraki adımlar – çözümü genişletmek

* **Toplu işleme:** Bir klasördeki PNG dosyalarını döngüye alıp tüm metinleri bir CSV dosyasına toplayın.  
* **Azure Cognitive Search entegrasyonu:** Çıkarılan Kiril dizelerini hızlı arama için indeksleyin.  
* **PDF dönüşümüyle birleştirme:** Aspose.PDF kullanarak taranmış PDF'leri önce PNG'ye dönüştürün, ardından aynı OCR akışını çalıştırın.  

Tüm bu senaryolar, az önce ele aldığımız temel deseni yeniden kullanır: **OCR için görüntü yükle → dili ayarla → tanı → metni kullan**.

---

## Sonuç

Artık **png'den metin okuma**, **Kiril metni çıkarma** ve **görüntüyü metne dönüştürme** işlemlerini Aspose OCR ile C# içinde nasıl yapacağınızı biliyorsunuz. Temel adımlar motoru oluşturmak, görüntüyü yüklemek, doğru dili seçmek (bu da otomatik olarak **Kiril dil paketini indirir**), ve son olarak `Recognize()` çağrısını yapmak.

Farklı görüntülerle deneyin, `Settings` seçenekleriyle oynayın ve uygulamalarınızın aranabilir, çok dilli ve çok daha akıllı hale geldiğini izleyin.  

İyi kodlamalar, herhangi bir sorunla karşılaşırsanız yorum bırakmaktan çekinmeyin!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}