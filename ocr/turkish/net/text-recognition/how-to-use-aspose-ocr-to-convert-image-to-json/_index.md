---
category: general
date: 2026-03-15
description: Aspose OCR'yi kullanarak görüntülerden metin çıkarmayı ve C#'ta görüntüyü
  JSON'a dönüştürmeyi öğrenin. PNG dosyalarından metin tanımayı ve hızlı bir şekilde
  yapılandırılmış çıktı almayı keşfedin.
draft: false
keywords:
- how to use aspose
- convert image to json
- extract text from image
- recognize text from png
- how to extract ocr
language: tr
og_description: Aspose OCR'yi kullanarak görüntülerden metin çıkarmak ve C#'ta görüntüyü
  JSON'a dönüştürmek nasıl yapılır. Bu rehber, PNG'den metin tanıma ve yapılandırılmış
  çıktı elde etme sürecinde size yol gösterir.
og_title: Aspose OCR'yi Kullanarak Görüntüyü JSON'a Dönüştürme
tags:
- Aspose
- OCR
- C#
- JSON
title: Aspose OCR'yi Kullanarak Görüntüyü JSON'a Dönüştürme
url: /tr/net/text-recognition/how-to-use-aspose-ocr-to-convert-image-to-json/
---

produce final content with all translations and unchanged parts.

Make sure to keep shortcodes exactly as given.

Let's assemble.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose OCR'yi Görüntüyü JSON'a Dönüştürmek İçin Nasıl Kullanılır

Aspose OCR'yi nasıl kullanılır sorusu, geliştiricilerin resimlerden metin çekmesi gerektiğinde sıkça sorulan bir sorudur. **Görüntüyü JSON'a dönüştürmek** veya **PNG'den metin tanımak** istiyorsanız, bu kılavuz size kapsamlı bir çözüm sunar—gereksiz ayrıntı yok, sadece pratik, uçtan uca bir çözüm.

Önümüzdeki birkaç dakikada ihtiyacınız olan her şeyi adım adım göstereceğiz: kütüphaneyi kurmak, motoru JSON çıktısı için yapılandırmak, bir fiş PNG'si yüklemek, OCR çalıştırmak ve sonunda sonucu bir `.json` dosyasına yazmak. Sonunda **görüntüden metin çıkarma** işlemini tek bir metod çağrısıyla yapabilecek ve her adımın neden önemli olduğunu anlayacaksınız.

> **Pro ipucu:** Aspose OCR, geniş bir görüntü formatı yelpazesiyle (PNG, JPEG, BMP, TIFF) çalışır. Aşağıdaki aynı kod tüm formatları ele alır, böylece format‑özel mantık yazmanıza gerek kalmaz.

## Gereksinimler

- .NET 6.0 veya üzeri (kod .NET Framework 4.6+ üzerinde de çalışır)  
- Geçerli bir Aspose.OCR NuGet paketi (ücretsiz deneme veya lisanslı)  
- İşlemek istediğiniz bir görüntü dosyası (ör. `receipt.png`)  
- Visual Studio, VS Code veya tercih ettiğiniz herhangi bir C# editörü  

Hepsi bu—ekstra bağımlılık yok, dış hizmet yok. Hazır mısınız? Hadi başlayalım.

![aspose OCR motorunu nasıl kullanılır](image-placeholder.png "aspose OCR motorunu nasıl kullanılır")

## Aspose OCR'yi Nasıl Kullanılır – JSON Çıktısını Yapılandırma

OCR için **aspose nasıl kullanılır** sorusunun ilk adımı, bir `OcrEngine` örneği oluşturup ona JSON üretmesini söylemektir. Bu küçük yapılandırma anahtarı, sonucu daha sonra manuel olarak serileştirmenizi engeller.

```csharp
using Aspose.OCR;
using Aspose.OCR.Config;
using System;
using System.IO;

class JsonOutputExample
{
    static void Main()
    {
        // 1️⃣ Create the OCR engine – this is the core object that does the heavy lifting.
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Tell Aspose to give us JSON instead of plain text.
        ocrEngine.Configuration.OutputFormat = OutputFormat.Json;

        // 3️⃣ Load the image you want to recognize.
        var inputImage = Image.FromFile(@"YOUR_DIRECTORY/receipt.png");

        // 4️⃣ Run the OCR process.
        var ocrResult = ocrEngine.Recognize(inputImage);

        // 5️⃣ Save the JSON payload to disk.
        File.WriteAllText(@"YOUR_DIRECTORY/receipt.json", ocrResult.Text);

        // 6️⃣ Let the developer know we’re done.
        Console.WriteLine("JSON saved.");
    }
}
```

**Neden önemli:** `OutputFormat`'u `Json` olarak ayarlamak, OCR motorunun metni zaten sayfalar, satırlar ve kelimeler hiyerarşisine düzenlediği anlamına gelir. Daha sonra ham dizeleri ayrıştırmanıza gerek kalmaz, bu da veri tabanına veri beslemek gibi sonraki işlemleri çok daha temiz hâle getirir.

## Aspose OCR ile Görüntüyü JSON'a Dönüştürme

Motor yapılandırıldıktan sonra, **görüntüyü JSON'a dönüştürme** kısmını daha ayrıntılı ele alalım.

1. **Görüntüyü yükle** – `Image.FromFile` desteklenen herhangi bir format için çalışır. Bir akış (ör. yüklenen dosya) ile çalışıyorsanız, bunun yerine `Image.FromStream` kullanabilirsiniz.  
2. **`Recognize` çalıştır** – bu metod bir `OcrResult` nesnesi döndürür. Çıktıyı JSON olarak ayarladığımız için `ocrResult.Text` zaten bir JSON dizesi içerir.  
3. **Dosyayı yaz** – `File.WriteAllText` JSON'ı kalıcı hale getirmenin en basit yoludur. Eğer bir bulut kovasına kaydetmeniz gerekiyorsa, bu satırı uygun SDK çağrısı ile değiştirin.

### Beklenen JSON Çıktısı

Tipik bir JSON yükü şu şekildedir (kısaltılmış):

```json
{
  "Pages": [
    {
      "PageNumber": 1,
      "Lines": [
        {
          "Words": [
            { "Text": "Total", "Confidence": 0.99 },
            { "Text": "$12.34", "Confidence": 0.98 }
          ]
        }
      ]
    }
  ]
}
```

Artık bu yapıyı herhangi bir sonraki sisteme besleyebilirsiniz—raporlama aracı, makine‑öğrenme modeli veya basit bir günlük dosyası olsun.

## Aspose OCR Kullanarak Görüntüden Metin Çıkarma

Yalnızca ham dizeye ihtiyacınız varsa (yani JSON ile ilgilenmiyorsanız), çıktı formatını basit metne geri döndürün:

```csharp
ocrEngine.Configuration.OutputFormat = OutputFormat.PlainText;
var plainResult = ocrEngine.Recognize(inputImage);
Console.WriteLine(plainResult.Text);
```

**Ne zaman düz metin seçilmeli?**  
- Hızlı hata ayıklama veya konsol çıktısı.  
- Özel sonrası‑işleme (ör. regex çıkarımı) uygulayacağınız senaryolar.

Ancak unutmayın, **görüntüden metin çıkarma** işlemini JSON ile yaptığınızda konumsal veri elde edersiniz—UI'da metni vurgulamak veya form alanlarıyla hizalamak için faydalıdır.

## PNG Dosyalarından Metin Tanıma

PNG, kayıpsız bir format olduğu için sıkıştırılmış JPEG'lere kıyasla genellikle daha iyi OCR doğruluğu sağlar. **PNG'den metin tanıma** sırasında en iyi sonuçları almanızı sağlamak için hızlı bir kontrol listesi:

| Kontrol Maddesi | Neden Yardımcı Olur |
|----------------|----------------------|
| 300+ DPI kullanın | Daha yüksek çözünürlük, motorun daha fazla pikselle çalışmasını sağlar. |
| Görüntüyü gri tonlamalı tutun | Gürültüyü azaltır; Aspose OCR otomatik olarak dönüştürür, ancak ön işleme hızlandırabilir. |
| Arka plan kalabalığını kaldırın | Temiz arka planlar güven skorlarını artırır. |

Düşük güven skorlarıyla karşılaşırsanız, DPI'yi artırmayı veya görüntüyü Aspose'a göndermeden önce basit bir eşik filtresi uygulamayı deneyin.

## OCR Sonuçlarını Programlı Olarak Nasıl Çıkarabilirsiniz

JSON'ı sadece kaydetmenin ötesinde, belirli alanları programlı olarak okumak isteyebilirsiniz—örneğin, bir fişteki toplam tutarı. JSON bir hiyerarşi içerdiği için, bunu bir C# nesnesine serileştirebilirsiniz:

```csharp
using System.Text.Json;

// Assuming ocrResult.Text contains the JSON string
var ocrData = JsonSerializer.Deserialize<OcrResponse>(ocrResult.Text);

// Example class definitions (simplified)
public class OcrResponse
{
    public Page[] Pages { get; set; }
}
public class Page
{
    public int PageNumber { get; set; }
    public Line[] Lines { get; set; }
}
public class Line
{
    public Word[] Words { get; set; }
}
public class Word
{
    public string Text { get; set; }
    public double Confidence { get; set; }
}
```

Artık `ocrData`'yı LINQ ile sorgulayabilirsiniz:

```csharp
var totalLine = ocrData.Pages
    .SelectMany(p => p.Lines)
    .FirstOrDefault(l => l.Words.Any(w => w.Text.Equals("Total", StringComparison.OrdinalIgnoreCase)));

if (totalLine != null)
{
    var amount = totalLine.Words
        .FirstOrDefault(w => w.Text.StartsWith("$"))
        ?.Text;
    Console.WriteLine($"Extracted amount: {amount}");
}
```

**Neden işe yarar:** JSON zaten her kelimenin sayfadaki konumunu bildirir, bu sayede düzen biraz değişse bile alanları güvenilir bir şekilde bulabilirsiniz.

## Kenar Durumları ve Yaygın Tuzaklar

- **Null Sonuç:** `ocrEngine.Recognize` `null` döndürürse, görüntü desteklenmiyor veya bozulmuş olabilir. Her zaman buna karşı önlem alın:

  ```csharp
  var ocrResult = ocrEngine.Recognize(inputImage);
  if (ocrResult == null) throw new InvalidOperationException("OCR failed – check the image path.");
  ```

- **Büyük Dosyalar:** Çok megabayt boyutundaki görüntüler için OCR'dan önce görüntüyü akış olarak işlemek veya yeniden boyutlandırmak, aşırı bellek kullanımını önleyebilir.

- **Lisans Sorunları:** Deneme sürümü çıktıya bir filigran ekler. Lisansınızı programın başında yüklediğinizden emin olun:

  ```csharp
  Aspose.OCR.License license = new Aspose.OCR.License();
  license.SetLicense("Aspose.OCR.lic");
  ```

- **Latin Olmayan Betikler:** Aspose OCR birçok dili destekler, ancak `Language` özelliğini uygun şekilde ayarlamanız gerekir (ör. `ocrEngine.Configuration.Language = Language.English;`).

## Tam Çalışan Örnek (Kopyala‑Yapıştır Hazır)

```csharp
using Aspose.OCR;
using Aspose.OCR.Config;
using System;
using System.IO;

class JsonOutputExample
{
    static void Main()
    {
        // Load your Aspose license (optional for trial)
        // var license = new Aspose.OCR.License();
        // license.SetLicense("Aspose.OCR.lic");

        // 1️⃣ Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Set output to JSON – this is the key step for convert image to JSON
        ocrEngine.Configuration.OutputFormat = OutputFormat.Json;

        // 3️⃣ Optional: improve accuracy for PNG files
        ocrEngine.Configuration.Dpi = 300; // higher DPI = better results

        // 4️⃣ Load the image you want to process
        var inputImagePath = @"YOUR_DIRECTORY/receipt.png";
        if (!File.Exists(inputImagePath))
            throw new FileNotFoundException($"Image not found: {inputImagePath}");

        var inputImage = Image.FromFile(inputImagePath);

        // 5️⃣ Run OCR – this is where we actually extract text from image
        var ocrResult = ocrEngine.Recognize(inputImage);
        if (ocrResult == null)
            throw new InvalidOperationException("OCR

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}