---
category: general
date: 2026-03-26
description: png'den metni tanıyın ve Aspose OCR'i C#'ta kullanarak makbuz verilerini
  çıkarın. Görüntüyü JSON‑L'ye dönüştürün ve tam bir örnekte OCR ile makbuzu işleyin.
draft: false
keywords:
- recognize text from png
- extract text from receipt
- convert image to jsonl
- process receipt with ocr
- aspose ocr example c#
language: tr
og_description: png'den metni tanıyın ve makbuzları Aspose OCR ile C#'ta JSON‑L'ye
  dönüştürün. Tam adım‑adım kod ve ipuçları.
og_title: png'den metin tanıma – Aspose OCR C# Rehberi
tags:
- Aspose OCR
- C#
- JSONL
- Receipt Processing
title: png'den metin tanıma – Aspose OCR C# JSON‑L öğreticisi
url: /tr/net/text-recognition/recognize-text-from-png-aspose-ocr-c-json-l-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# png'den metin tanıma – Tam Aspose OCR C# Kılavuzu

Hiç **png'den metin tanıma** ihtiyacı duydunuz ama hangi kütüphanenin temiz, satır‑satır sonuçlar vereceğinden emin değildiniz? Yalnız değilsiniz. Birçok küçük işletme uygulamasında makbuz bir PNG görüntüsü olarak bulunur ve tutarı, tarihi ya da satıcı adını çıkarmak günlük bir sorun olur.  

İyi haber? Birkaç C# satırı ve **Aspose OCR** kütüphanesi ile **makbuzdan metin çıkarabilir**, ardından **görüntüyü jsonl'ye dönüştürebilirsiniz** sonraki analizler için. Bu öğreticide tüm süreci—PNG yükleme, OCR çalıştırma ve her satırı bir JSON‑L dosyasına yazma—adım adım göstereceğiz; böylece **OCR ile makbuzu işleyebilirsiniz** hemen.

İhtiyacınız olan her şeyi ele alacağız: gerekli NuGet paketleri, tam çalışan bir program, her adımın neden önemli olduğuna dair açıklamalar ve makbuzlar karıştığında işinize yarayacak birkaç pratik ipucu. Harici belgeye gerek yok; sadece kopyala‑yapıştır, çalıştır ve uyarlayın.

---

## Öğrenecekleriniz

- `Aspose.OCR` kullanarak **png'den metin tanıma** nasıl yapılır.
- `Receipt` satır nesnelerinden **metin çıkarma** ve güven puanlarını yakalama.
- Her OCR satırının ayrı bir JSON nesnesi olmasını sağlayacak şekilde **görüntüyü jsonl'ye dönüştürme**.
- **OCR ile makbuzu işleme** uçtan uca, boş görüntüler veya düşük güven puanlı satırlar gibi uç durumları ele alma.
- Yaygın OCR sorunlarını giderme ve doğruluğu artırma ipuçları.

### Önkoşullar

- .NET 6.0 veya daha yenisi (kod .NET Core ve .NET Framework ile de çalışır).
- Visual Studio 2022 veya tercih ettiğiniz herhangi bir IDE.
- Geçerli bir Aspose OCR lisansı (Aspose.com'dan ücretsiz geçici bir lisansla başlayabilirsiniz).
- Kontrol ettiğiniz bir klasörde `receipt.png` olarak kaydedilmiş örnek bir makbuz.

---

## Adım 1: Aspose OCR ile png'den metin tanıma

İlk olarak ihtiyacımız olan, başlatılmış bir `OcrEngine` nesnesidir. Bu nesne OCR motoru ayarlarını (dil, algılama modu vb.) tutar. Varsayılan olarak İngilizce kullanır ve sayfa düzenini otomatik algılar; bu çoğu makbuz için yeterlidir.

```csharp
using Aspose.OCR;
using Aspose.OCR.Export;
using System;
using System.IO;

class JsonLExample
{
    static void Main()
    {
        // Initialize the OCR engine – this is where Aspose loads its models.
        OcrEngine ocrEngine = new OcrEngine();

        // Load the PNG image that contains the receipt.
        string imagePath = @"YOUR_DIRECTORY\receipt.png";
        OcrImage receiptImage = OcrImage.FromFile(imagePath);

        // Run OCR and get the result object.
        OcrResult ocrResult = ocrEngine.Recognize(receiptImage);
```

**Neden önemli:**  
`OcrEngine` ağır iş yükünü üstlenen bileşendir; bir kez oluşturup birçok görüntüde yeniden kullanmak bellek tüketimini azaltır. Farklı bir dile (ör. İspanyolca makbuzlar) ihtiyacınız varsa, `Recognize` çağırmadan önce `ocrEngine.Language = OcrLanguage.Spanish;` ayarlayabilirsiniz.

## Adım 2: Makbuz satırlarından metin çıkarma

`OcrResult` içinde `Lines` adlı bir koleksiyon bulunur. Her satır ham metni ve bir güven puanı (0‑100) içerir. Bunları çıkarmak size ayrıntılı kontrol sağlar—düşük güven puanlı satırları atabilir veya manuel inceleme için işaretleyebilirsiniz.

```csharp
        // Prepare to write each line as a JSON‑L record.
        string jsonlPath = @"YOUR_DIRECTORY\receipt.jsonl";

        using (StreamWriter jsonLineWriter = new StreamWriter(jsonlPath))
        {
            foreach (var line in ocrResult.Lines)
            {
                // Build a simple JSON object for the line.
                string json = $"{{\"text\":\"{EscapeJson(line.Text)}\",\"confidence\":{line.Confidence}}}";
                jsonLineWriter.WriteLine(json);
            }
        }

        Console.WriteLine("JSON‑L file written to " + jsonlPath);
    }

    // Helper to escape quotes and backslashes in JSON strings.
    private static string EscapeJson(string s) => s.Replace("\\", "\\\\").Replace("\"", "\\\"");
}
```

**Neden JSON kaçışını yapıyoruz:**  
Makbuz metni, basit bir JSON dizesini bozabilecek tırnak işaretleri (`"`) veya ters eğik çizgiler (`\`) içerebilir. `EscapeJson` yöntemi geçerli bir JSON satırı sağlar.

**Çıktının görünümü:**  

```
{"text":"Store XYZ","confidence":98.5}
{"text":"Date: 2024-07-15","confidence":97.2}
{"text":"Total $23.45","confidence":99.1}
```

Her satır ayrı bir kayıt olup, veri gölüne akıtmak veya bir makine‑öğrenme modeline beslemek için mükemmeldir.

## Adım 3: Görüntüyü JSONL'ye Dönüştürme – uç durumları ele alma

Bir grup makbuzu işlerken, birkaç görüntü boş, bozuk veya çok düşük güven puanına sahip olabilir. Boru hattını biraz daha sağlam hâle getirelim.

```csharp
        // After OCR, check if any lines were detected.
        if (ocrResult.Lines.Count == 0)
        {
            Console.WriteLine("Warning: No text detected. Verify the image path and quality.");
            return;
        }

        // Optional: filter out lines with confidence below a threshold.
        const double minConfidence = 80.0;
        foreach (var line in ocrResult.Lines)
        {
            if (line.Confidence < minConfidence)
                continue; // skip noisy line
            // write as before...
        }
```

**Neden filtreleme:**  
Soluk kağıda basılmış makbuzlar düşük güvenli rastgele karakterler üretebilir. %80'in altındaki her şeyi atmak genellikle gürültüyü temizler ve faydalı veriyi korur.

## Adım 4: OCR ile Makbuzu İşleme – uçtan uca örnek

Her şeyi bir araya getirerek, işte **tam, çalıştırmaya hazır** program. `YOUR_DIRECTORY` ifadesini PNG dosyanızın bulunduğu klasörle değiştirin.

```csharp
using Aspose.OCR;
using Aspose.OCR.Export;
using System;
using System.IO;

class JsonLExample
{
    static void Main()
    {
        // 1️⃣ Initialize OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Load receipt PNG
        string imagePath = @"YOUR_DIRECTORY\receipt.png";
        OcrImage receiptImage = OcrImage.FromFile(imagePath);

        // 3️⃣ Perform OCR
        OcrResult ocrResult = ocrEngine.Recognize(receiptImage);

        // 4️⃣ Verify we got something back
        if (ocrResult.Lines.Count == 0)
        {
            Console.WriteLine("❗ No text found – check the image quality.");
            return;
        }

        // 5️⃣ Write each line to a JSON‑L file
        string jsonlPath = @"YOUR_DIRECTORY\receipt.jsonl";
        using (StreamWriter writer = new StreamWriter(jsonlPath))
        {
            const double minConfidence = 80.0;
            foreach (var line in ocrResult.Lines)
            {
                if (line.Confidence < minConfidence) continue; // skip low‑confidence

                string json = $"{{\"text\":\"{EscapeJson(line.Text)}\",\"confidence\":{line.Confidence}}}";
                writer.WriteLine(json);
            }
        }

        Console.WriteLine($"✅ JSON‑L written to: {jsonlPath}");
    }

    // Helper to make JSON safe
    private static string EscapeJson(string s) => s.Replace("\\", "\\\\").Replace("\"", "\\\"");
}
```

**Kodu çalıştırma:**  
1. Proje klasöründe bir terminal açın.  
2. `dotnet add package Aspose.OCR` – kütüphaneyi kurar.  
3. `dotnet run` – başarı mesajını ve bir `receipt.jsonl` dosyasının oluştuğunu görmelisiniz.

**Beklenen sonuç:**  
Her satır bir makbuz satırını yansıtan, güven puanlarıyla birlikte satır‑sınırlı bir JSON dosyası. Artık bu dosyayı Power BI, Elastic veya JSON‑L'yi anlayan herhangi bir analiz aracına aktarabilirsiniz.

## Yaygın Tuzaklar & Pro İpuçları

| Sorun | Neden Oluşur | Hızlı Çözüm |
|-------|--------------|-------------|
| **Boş çıktı** | Görüntü yolu yanlış veya dosya PNG değil. | Yolu tekrar kontrol edin, `File.Exists(imagePath)` kullanın. |
| **Bozuk karakterler** | Düşük DPI veya aşırı sıkıştırılmış PNG. | En az 300 dpi tarama kullanın; agresif JPEG sıkıştırmasından kaçının. |
| **Çok fazla düşük‑güven satırı** | Solmuş termal kağıda basılmış makbuz. | `minConfidence` eşiğini artırın veya görüntüyü ön‑işleyin (kontrast/eşik). |
| **JSON ayrıştırma hataları** | Makbuz metnindeki kaçış yapılmamış tırnaklar. | `EscapeJson` yardımcı metodunu tutun veya sağlam serileştirme için `System.Text.Json`'a geçin. |

Pro ipucu: Belirli alanları (ör. toplam tutar) çıkarmanız gerekiyorsa, JSON‑L dosyasına sahip olduktan sonra her `line.Text` üzerinde basit bir regex çalıştırın. Bu, OCR'ı iş mantığından ayırır ve hata ayıklamayı kolaylaştırır.

## Çözümü Genişletme

- **Toplu işleme:** `Main` mantığını bir dizindeki tüm PNG dosyaları üzerinde `foreach` ile döndürün.
- **Çok‑dilli destek:** `Recognize`'den önce `ocrEngine.Language = OcrLanguage.Spanish;` (veya desteklenen herhangi bir dil) ayarlayın.
- **Yapılandırılmış çıktı:** Satır‑satır JSON yerine `Date`, `Merchant`, `Total` özelliklerine sahip bir `Receipt` nesnesi oluşturup tek seferde serileştirin.

Bu varyasyonların tümü hâlâ temel olarak **görüntüyü jsonl'ye dönüştürür**, böylece OCR kısmına dokunmadan alt akış tüketicisini değiştirebilirsiniz.

## Sonuç

Aspose OCR kullanarak **png dosyalarından metin tanıma**, **makbuzdan metin çıkarma** ve **görüntüyü jsonl'ye dönüştürme** yoluyla kolay bir sonraki işlem için nasıl yapılacağını gösterdik. Tam, bağımsız C# programı tüm iş akışını gösteriyor—PNG yüklemeden, uç durumları ele almaya, temiz bir JSON‑L dosyası yazmaya—böylece kendi projelerinizde hemen **OCR ile makbuzu işleyebilirsiniz**.

Birkaç örnek makbuzla deneyin, güven eşiğini ayarlayın ve gürültülü bir görüntü yığınına nasıl hızlıca analiz için hazır yapılandırılmış veri dönüştüğünü görün. Rahat hissettiğinizde, toplu işleme keşfedin ya da harcama kategorilerini otomatik sınıflandırmak için küçük bir ML modeli ekleyin.

Sorularınız mı var, ya da akıllı bir düzenleme mi buldunuz? Aşağıya yorum bırakın—mutlu kodlamalar!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}