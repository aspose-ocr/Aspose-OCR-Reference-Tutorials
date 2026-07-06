---
category: general
date: 2026-03-05
description: C#'ta OCR kullanarak fiş görüntülerinden metin çıkarma. OCR için görüntüyü
  nasıl yükleyeceğinizi ve dakikalar içinde fiş görüntüsünü nasıl tanıyacağınızı öğrenin.
draft: false
keywords:
- how to use OCR
- extract text from receipt
- load image for OCR
- recognize receipt image
language: tr
og_description: Faturalardan metin çıkarmak için C#'de OCR nasıl kullanılır. OCR için
  bir görüntüyü yüklemek ve fatura görüntüsünü verimli bir şekilde tanımak için bu
  adım adım rehberi izleyin.
og_title: C#'da OCR nasıl kullanılır – Hızlı Makbuz Metni Çıkarma
tags:
- OCR
- C#
- Aspose
- Receipt Processing
title: C#'ta OCR nasıl kullanılır – Makbuzlardan Metni Hızlıca Çıkarın
url: /tr/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-receipts-quickly/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#'ta OCR Nasıl Kullanılır – Makbuzlardan Metni Hızlıca Çıkarın

Bir market makbuzunun fotoğrafından verileri doğrudan çekmek için **OCR nasıl kullanılır**ı merak ettiniz mi? Tek başınıza değilsiniz. Birçok küçük‑işletme uygulamasında darboğaz, bulanık bir PNG'yi gerçekten çalışabileceğiniz yapılandırılmış metne dönüştürmektir.  

İyi haber? Birkaç satır C# ve Aspose.OCR ile **OCR için görüntü yükle**, motoru çalıştır ve **makbuz görüntüsünü tanı** işlemini bir dakikadan kısa sürede yapabilirsiniz. Aşağıda tamamen çalıştırılabilir bir örnek ve çoğu öğreticide atlanan zorlu bölümler için ipuçları bulacaksınız.

## Bu Kılavuzda Neler Ele Alınıyor

İhtiyacınız olan her şeyi adım adım inceleyeceğiz:

* Aspose.OCR NuGet paketinin kurulumu.  
* OCR motorunun yapılandırılması – **OCR nasıl kullanılır** sorusunun çekirdeği.  
* Bir makbuz dosyasının yüklenmesi (bu **OCR için görüntü yükle** adımı).  
* Tanıma sürecinin çalıştırılması ve hem JSON hem de XML düzen verilerinin alınması.  
* Eksik lisanslar veya desteklenmeyen görüntü formatları gibi yaygın tuzakların ele alınması.  

Sonunda, bir klasöre bıraktığınız herhangi bir makbuzdan metni çıkaran, dış hizmetlere ihtiyaç duymayan, gizli bir sihir içermeyen bağımsız bir programınız olacak.

## Önkoşullar

* .NET 6 SDK veya daha yeni bir sürüm (kod .NET Core ile de derlenebilir).  
* Geçerli bir Aspose.OCR lisans dosyası (`Aspose.OCR.lic`). Henüz bir lisansınız yoksa Aspose'tan ücretsiz deneme alabilirsiniz.  
* Örnek bir makbuz görüntüsü – `receipt.png` işinizi görecektir, ancak herhangi bir yaygın raster formatı da kullanılabilir.  

Bu öğelere sahipseniz, harika – hemen başlayalım.

![OCR nasıl kullanılır örneği](https://example.com/ocr-receipt.png "how to use OCR example")

## Adım 1: Aspose.OCR'ı Kurun ve Yeni Bir Proje Oluşturun

İlk iş: gerçekten ağır işi yapan kütüphaneye ihtiyacınız var. Proje klasörünüzde bir terminal açın ve şu komutu çalıştırın:

```bash
dotnet new console -n ReceiptOcrDemo
cd ReceiptOcrDemo
dotnet add package Aspose.OCR
```

Bu komut bir konsol uygulaması iskeleti oluşturur ve en yeni Aspose.OCR paketini projeye ekler. Deneyimlerime göre, proje adını kısa tutmak, özellikle birden fazla demo uygulamasıyla uğraşmaya başladığınızda, oluşturulan yolları okumayı kolaylaştırır.

## Adım 2: OCR Motorunu Başlatın – **OCR nasıl kullanılır**ın Kalbi

Şimdi “**OCR nasıl kullanılır**” sorusuna yanıt veren kodu yazacağız. `Program.cs` dosyasını açın ve içeriğini aşağıdaki snippet ile değiştirin. Yorumlara dikkat edin – her satırın *neden*ini, sadece *ne* yaptığını açıklıyor.

```csharp
using System;
using System.IO;
using Aspose.OCR;          // Aspose OCR namespace
using Aspose.OCR.Image;   // For loading images

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Create and configure the OCR engine.
        // -------------------------------------------------
        var ocrEngine = new OcrEngine();

        // Why set a license? Without it the engine runs in evaluation mode,
        // which adds a watermark to the output and limits batch size.
        ocrEngine.SetLicense("Aspose.OCR.lic");

        // -------------------------------------------------
        // 2️⃣ Load the receipt image – this is the **load image for OCR** step.
        // -------------------------------------------------
        // Change the path to point at your own receipt file.
        string imagePath = Path.Combine(
            Environment.CurrentDirectory, "receipt.png");

        // The ImageStream class abstracts file I/O and supports many formats.
        ocrEngine.Image = ImageStream.FromFile(imagePath);

        // -------------------------------------------------
        // 3️⃣ Run the recognition process – this is where we **recognize receipt image**.
        // -------------------------------------------------
        var ocrResult = ocrEngine.Recognize();

        // -------------------------------------------------
        // 4️⃣ Export the layout information as JSON.
        // -------------------------------------------------
        string jsonResult = ocrResult.ToJson();
        File.WriteAllText("receipt.json", jsonResult);
        Console.WriteLine("✅ JSON saved to receipt.json");

        // -------------------------------------------------
        // 5️⃣ Export the same layout information as XML.
        // -------------------------------------------------
        string xmlResult = ocrResult.ToXml();
        File.WriteAllText("receipt.xml", xmlResult);
        Console.WriteLine("✅ XML saved to receipt.xml");

        // -------------------------------------------------
        // 6️⃣ Quick preview – print the plain text to console.
        // -------------------------------------------------
        Console.WriteLine("\n--- Extracted Text ---");
        Console.WriteLine(ocrResult.Text);
    }
}
```

### Neden Bu Şekilde Çalışır

* **`OcrEngine`** giriş noktasıdır; daha sonra (dil, DPI vb.) ayarlayabileceğiniz tüm yapılandırmaları tutar.  
* **`SetLicense`** değerlendirme filigranını kaldırır – kodu dağıtmayı planlıyorsanız kritik bir adımdır.  
* **`ImageStream.FromFile`** **OCR için görüntü yükle** işini yapar, PNG, JPEG, BMP, TIFF ve daha fazlasını destekler.  
* **`Recognize()`** aslında **makbuz görüntüsünü tanı** metodudur. İçeride ikilileştirme, segmentasyon ve karakter sınıflandırması gerçekleştirir.  
* JSON ve XML olarak dışa aktarmak, hem insan tarafından okunabilir bir döküm hem de sonraki ayrıştırıcılar için makine dostu bir yapı sağlar.

## Adım 3: Demo'yu Çalıştırın ve Çıktıyı Doğrulayın

Derleyin ve çalıştırın:

```bash
dotnet run
```

Her şey doğru bağlandıysa aşağıdakine benzer bir çıktı göreceksiniz:

```
✅ JSON saved to receipt.json
✅ XML saved to receipt.xml

--- Extracted Text ---
Walmart Supercenter
Date: 03/04/2026
Item    Qty   Price
Milk    2     2.58
Bread   1     1.99
Total   4.57
```

Konsol düz metni yazdırırken, `receipt.json` ve `receipt.xml` dosyaları ayrıntılı düzen bilgilerini (koordinatlar, güven skorları vb.) içerir. Bu dosyalar, daha sonra her satırı bir veritabanı alanına eşlemeniz gerektiğinde çok işe yarar.

## Kenar Durumları ve Uzman İpuçları

### 1️⃣ Eksik veya Geçersiz Lisans
`SetLicense` başarısız olursa motor deneme moduna geçer ve çıktıda bir filigran görürsünüz. Çağrıyı try/catch bloğuna alın ve dostça bir mesaj kaydedin:

```csharp
try { ocrEngine.SetLicense("Aspose.OCR.lic"); }
catch (Exception ex)
{
    Console.WriteLine("⚠️ License not found – running in trial mode.");
    Console.WriteLine(ex.Message);
}
```

### 2️⃣ Desteklenmeyen Görüntü Formatları
Aspose.OCR çoğu raster formatını destekler, ancak bir PDF ya da çok‑sayfalı TIFF verirseniz ilgilendiğiniz sayfayı önce bir görüntüye dönüştürmeniz gerekir. `Aspose.PDF` kütüphanesi bu dönüşümü yapabilir.

### 3️⃣ Büyük Makbuzlar ve Performans
10 MB bir görüntünün işlenmesi yavaş olabilir. Motorun önüne beslemeden çözünürlüğü düşürün:

```csharp
ocrEngine.Image = ImageStream.FromFile(imagePath).Resize(1024, 0);
```

`Resize` metodu en boy oranını korur (`0` yükseklik için) ve dosya boyutunu büyük ölçüde azaltır, tipik makbuzlar için OCR doğruluğundan ödün vermez.

### 4️⃣ Dil ve Yazı Tipi Sorunları
Makbuzlar özel karakterler (€, ¥, vb.) içerebilir. Yerel ayarı biliyorsanız dili açıkça ayarlayın:

```csharp
ocrEngine.Language = Language.English; // or Language.Spanish, etc.
```

Karışık‑dilli makbuzlar için çok‑dilli modu etkinleştirebilirsiniz:

```csharp
ocrEngine.Language = Language.English | Language.French;
```

### 5️⃣ Yapılandırılmış Veri Çıkarma
Ham metin faydalı olsa da, çoğu uygulama yapılandırılmış alanlara (tarih, toplam, ürünler) ihtiyaç duyar. JSON düzeni her kelime için `BoundingBox` koordinatlarını içerir. Aşağıdaki gibi bir post‑process uygulayabilirsiniz:

```csharp
var layout = Newtonsoft.Json.Linq.JObject.Parse(jsonResult);
foreach (var word in layout["Words"])
{
    string text = (string)word["Text"];
    // Simple heuristics: look for "$" or "Total"
}
```

Bu snippet fikri gösterir; üretimde muhtemelen bir düzenli ifade ya da küçük bir kural motoru kullanırsınız.

## Sıkça Sorulan Sorular

**S: Bunu Linux'ta çalıştırabilir miyim?**  
C: Kesinlikle. Aspose.OCR çapraz‑platformdur; Linux makinenize .NET runtime'ı kurmanız yeterli, aynı kod çalışır.

**S: Dakikada onlarca makbuzu işlemem gerekirse ne yapmalıyım?**  
C: Bir `Parallel.ForEach` döngüsü başlatın ve tek bir `OcrEngine` örneğini yeniden kullanın – okuma‑only işlemler için thread‑safe'dir. Lisans eşzamanlılık limitlerini de göz önünde bulundurun.

**S: Açılı bir açıyla çekilmiş mobil fotoğraflarla çalışır mı?**  
C: Motor temel deskew (eğri düzeltme) içerir, ancak çok eğik görüntüler için önce bir görüntü işleme kütüphanesi (ör. OpenCV) ile düzeltme yapmanız önerilir.

## Tam Çalışan Örnek (Kopyala‑Yapıştır)

Aşağıda `Program.cs` içine bırakabileceğiniz *tam* program yer alıyor. Lisans dosyası ve bir makbuz görüntüsü dışında başka bir dosyaya ihtiyacınız yok.

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Image;

class Program
{
    static void Main()
    {
        // Create and configure the OCR engine
        var ocrEngine = new OcrEngine();
        try
        {
            ocrEngine.SetLicense("Aspose.OCR.lic");
        }
        catch (Exception)
        {
            Console.WriteLine("⚠️ Running in trial mode – license not found.");
        }

        // Load the image to be processed (load image for OCR)
        string imagePath = Path.Combine(Environment.CurrentDirectory, "

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}