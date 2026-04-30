---
category: general
date: 2026-04-29
description: Aspose OCR kullanarak çevrim dışı bir görüntüden metin tanımayı öğrenin.
  Tek bir C# uygulamasında PNG’den metin çıkarma ve OCR için görüntü yükleme adımlarını
  içerir.
draft: false
keywords:
- recognize text from image
- extract text from png
- load image for ocr
- Aspose OCR offline
- C# OCR example
language: tr
og_description: C#'ta Aspose OCR ile çevrim dışı görüntüden metin tanıma. PNG'den
  metin çıkarmak ve OCR için resmi yüklemek için adım adım kılavuz.
og_title: Görüntüden metin tanıma – Tam Offline OCR Rehberi
tags:
- OCR
- C#
- Aspose
- Image Processing
title: C#'te Görüntüden Metin Tanıma – Çevrimdışı OCR Öğreticisi
url: /tr/net/text-recognition/recognize-text-from-image-in-c-offline-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# görselden metin tanıma – Tam Çevrimdışı OCR Kılavuzu

Hiç **görselden metin tanıma** ihtiyacı duydunuz mu uygulamanız internet bağlantısı olmayan bir makinede çalışırken? Belki bir saha cihazı tarayıcısı, güvenli bir kiosk geliştiriyorsunuz ya da sadece bulut hizmetlerinin gecikmesinden kaçınmak istiyorsunuz. Bu öğreticide, Aspose OCR kullanarak **görselden metin tanıma** yapan bağımsız bir C# programını adım adım inceleyeceğiz ve ayrıca **png'den metin çıkarma** ve kaynaklar diskte bulunduğunda **ocr için görsel yükleme** nasıl yapılır göstereceğiz.

İhtiyacınız olan her şeyi ele alacağız: tam NuGet paketi, önceden indirilmiş OCR modülleri için klasör düzeni ve işler ters gittiğinde kodunuzun sağlam kalmasını sağlayacak birkaç ipucu. Sonunda, tanınan metni konsola yazdıran çalıştırılabilir bir konsol uygulamanız olacak—herhangi bir ağ çağrısına gerek kalmayacak.

## Önkoşullar

- .NET 6 (veya herhangi bir yeni .NET çalışma zamanı) yerel olarak yüklü.  
- Visual Studio 2022 veya VS Code—favori IDE’niz yeterli.  
- Aspose.OCR NuGet paketi (`dotnet add package Aspose.OCR`).  
- Aspose portalından indirilen çevrimdışı OCR kaynak dosyaları (sadece birkaç MB).  
- İşlemek istediğiniz bir PNG görüntüsü (`offline_test.png`).

> **Pro tip:** Kaynak klasörünü çalıştırılabilir dosyanızın yanına koyun; böylece göreli yol çözümü çok kolay olur.

## Adım 1 – OCR Motoru Örneğini Oluşturma

İlk yaptığımız şey `OcrEngine` örneğini oluşturmak. Bunu, daha sonra pikselleri analiz edecek beyin olarak düşünebilirsiniz.

```csharp
using Aspose.OCR;
using System;

class OfflineDemo
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();
```

Her çalıştırmada yeni bir örnek oluşturmanın nedeni nedir? Özellikle otomatik kaynak indirme gibi seçenekleri değiştirirken temiz bir durum garantiler. Uzun süren bir hizmette motoru yeniden kullanabilirsiniz, ancak basit bir demo için bu yaklaşım en güvenli olandır.

## Adım 2 – Motoru Çevrimdışı Kaynaklarınıza Yönlendirme

Aspose OCR genellikle dil paketlerini buluttan çeker. Çevrimdışı **görselden metin tanıma** istediğimiz için, motorun dosyaların nerede olduğunu bilmesi gerekir.

```csharp
        // Step 2: Point the engine to the folder containing the pre‑downloaded OCR modules
        ocrEngine.Config.ResourcesPath = @"YOUR_DIRECTORY";
```

`YOUR_DIRECTORY` ifadesini, Aspose indirmesinden çıkardığınız `ocrdata` klasörünü içeren mutlak ya da göreli yol ile değiştirin. Yol yanlış olursa motor `FileNotFoundException` hatası verir—bu yüzden yazımı iki kez kontrol edin.

## Adım 3 – Otomatik Kaynak İndirmeyi Kapatma

Varsayılan olarak Aspose eksik modülleri anında indirmeye çalışır. Çevrimdışı senaryo için bu özelliği açıkça devre dışı bırakıyoruz.

```csharp
        // Step 3: Disable automatic resource download to enforce offline operation
        ocrEngine.Config.AllowAutomaticResourceDownload = false;
```

Bu satırı unutursanız, motor bir ağ çağrısı yapmaya çalışır; bu birçok kurumsal güvenlik duvarında sessizce başarısız olur ve size boş bir sonuç verir. Kapatmak ayrıca ilk tanıma geçişini hızlandırır çünkü motor indirme kontrolünü atlar.

## Adım 4 – Görseli Yükleme ve OCR Çalıştırma

Şimdi nihayet **ocr için görsel yükleme** yapıyoruz. Statik `LoadImage` yardımcı metodu bir dosya yolu alır ve motorun tüketebileceği bir `Image` nesnesi döndürür.

```csharp
        // Step 4: Load the image to be processed and run OCR
        var ocrResult = ocrEngine.Recognize(
            OcrEngine.LoadImage(@"YOUR_DIRECTORY/offline_test.png"));
```

PNG dosyası kullandığımıza dikkat edin—kayıpsız metin çıkarımı için mükemmel. JPEG'ınız varsa aynı çağrı çalışır, ancak PNG genellikle sıkıştırma artefaktı olmadığı için daha temiz sonuçlar verir.

## Adım 5 – Tanınan Metni Görüntüleme

`Recognize` metodu, bir `Text` özelliği içeren `OcrResult` döndürür. Biz bunu basitçe konsola yazarız.

```csharp
        // Step 5: Display the recognized text
        Console.WriteLine(ocrResult.Text);
    }
}
```

Programı çalıştırdığınızda aşağıdakine benzer bir şey görmelisiniz:

```
Hello, Aspose OCR!
This is an offline test.
```

Eğer çıktı boşsa, `ResourcesPath`'i iki kez kontrol edin ve dil modülünün (ör. `English`) mevcut olduğundan emin olun.

![Aspose OCR kullanarak görselden metin tanıma](/images/offline_ocr_demo.png "görselden metin tanıma")

*Yukarıdaki ekran görüntüsü, png'den metin çıkarıldıktan sonra konsol çıktısını gösterir.*

## Yaygın Kenar Durumları ve Nasıl Ele Alınır

### 1. Görsel Çok Büyük

Çok yüksek çözünürlüklü PNG'ler bellek baskısına neden olabilir. Motorun önüne göndermeden önce görseli küçültün:

```csharp
using System.Drawing;

// Load, resize, then pass to OCR
var original = (Bitmap)Image.FromFile(@"YOUR_DIRECTORY/offline_test.png");
var resized = new Bitmap(original, new Size(original.Width / 2, original.Height / 2));
var tempPath = Path.Combine(Path.GetTempPath(), "temp_resized.png");
resized.Save(tempPath);
var ocrResult = ocrEngine.Recognize(OcrEngine.LoadImage(tempPath));
```

### 2. Dil Algılanmadı

Eğer **png'den metin çıkarma** yaparken İngilizce dışındaki bir dil içeriyorsa, dili açıkça ayarlayın:

```csharp
ocrEngine.Config.Language = Language.French; // or Language.Spanish, etc.
```

İlgili dil paketinin çevrimdışı kaynak klasörünüzde mevcut olduğundan emin olun.

### 3. Boş veya Düşük Kontrastlı Görseller

OCR düşük kontrastta zorlanır. Görseli basit bir eşik değeriyle ön işleme tabi tutun:

```csharp
using System.Drawing.Imaging;

var bitmap = new Bitmap(@"YOUR_DIRECTORY/offline_test.png");
for (int y = 0; y < bitmap.Height; y++)
{
    for (int x = 0; x < bitmap.Width; x++)
    {
        var pixel = bitmap.GetPixel(x, y);
        var gray = (pixel.R + pixel.G + pixel.B) / 3;
        var bw = gray > 128 ? Color.White : Color.Black;
        bitmap.SetPixel(x, y, bw);
    }
}
bitmap.Save(@"YOUR_DIRECTORY/processed.png");
```

Ardından OCR motorunu `processed.png` dosyasına yönlendirin. Bu küçük ayar genellikle %30 başarı oranını neredeyse mükemmel bir çıkarıma dönüştürür.

## Tam Çalışan Örnek

Aşağıda `Program.cs` dosyasına kopyalayıp yapıştırabileceğiniz *tam* program yer alıyor. `YOUR_DIRECTORY` ifadesini makinenizdeki gerçek yol ile değiştirmeyi unutmayın.

```csharp
using Aspose.OCR;
using System;
using System.IO;

class OfflineDemo
{
    static void Main()
    {
        // 1️⃣ Create OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Set offline resources folder
        ocrEngine.Config.ResourcesPath = @"C:\OCRResources";

        // 3️⃣ Prevent any network calls
        ocrEngine.Config.AllowAutomaticResourceDownload = false;

        // 4️⃣ Load PNG and recognize
        string imagePath = @"C:\OCRResources\offline_test.png";
        if (!File.Exists(imagePath))
        {
            Console.WriteLine($"Image not found: {imagePath}");
            return;
        }

        var ocrResult = ocrEngine.Recognize(OcrEngine.LoadImage(imagePath));

        // 5️⃣ Output the extracted text
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**Beklenen çıktı** (PNG içinde “Hello World!” olduğunu varsayarsak):

```
=== OCR Output ===
Hello World!
```

Projeyi klasöründen `dotnet run` komutuyla çalıştırın ve konsolun çıkarılan dizeyi yazdırmasını izleyin.

## Özet – Ne Başardık

- **görselden metin tanıma** tamamen çevrimdışı Aspose OCR kullanarak.  
- **png'den metin çıkarma** nasıl yapılır, dış hizmet olmadan gösterildi.  
- **ocr için görsel yükleme** ve motoru çevrimdışı çalışacak şekilde yapılandırmanın doğru yolu gösterildi.

Bunların tümü tek bir, bağımsız C# konsol uygulamasına sığar.

## Sonraki Adımlar ve İlgili Konular

- **Batch processing** – PNG'lerin bulunduğu bir klasörü döngüye alıp her sonucu bir `.txt` dosyasına yazın.  
- **Different file formats** – Daha yüksek doğruluklu taramalar için `LoadImage`'ı TIFF veya BMP ile deneyin.  
- **Performance tuning** – Çok çekirdekli bir sisteminiz varsa çok iş parçacıklı tanımayı etkinleştirin.  
- **Integration with ASP.NET Core** – Yüklenen bir görseli kabul eden ve OCR sonucunu dönen bir API uç noktası sunun, hâlâ çevrimdışı kalın.

PDF'lerle çalışmakla ilgileniyorsanız, “Aspose PDF kullanarak PDF'den metin tanıma” kılavuzumuza göz atın. Daha gelişmiş görsel ön işleme için OpenCV'nin C# bağlamalarına bakın.

---

*Kodlamaktan keyif alın! Herhangi bir sorunla karşılaşırsanız, aşağıya yorum bırakın—her ne kadar inatçı olursa olsun, herhangi bir görselden metni çıkarmanıza yardımcı olmaya çalışacağım.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}