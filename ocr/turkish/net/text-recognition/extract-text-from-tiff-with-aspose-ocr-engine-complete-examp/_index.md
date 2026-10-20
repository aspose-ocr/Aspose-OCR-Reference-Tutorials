---
category: general
date: 2026-04-04
description: C#'ta bir OCR motoru örneği kullanarak TIFF dosyalarından metin çıkarmayı
  öğrenin. JSON ve XML çıktılı adım adım rehber.
draft: false
keywords:
- extract text from tiff
- ocr engine example
- Aspose OCR C#
- multi‑page TIFF OCR
- JSON OCR result
language: tr
og_description: C#'ta bir OCR motoru kullanarak TIFF dosyalarından metin çıkarma örneği.
  Ayrıntılı adımlar, tam kod ve JSON/XML çıktısı için ipuçları.
og_title: Aspose OCR Motoru ile TIFF'ten Metin Çıkarma – Tam Kılavuz
tags:
- C#
- OCR
- Aspose
- Image Processing
title: Aspose OCR Motoru ile TIFF'ten Metin Çıkarma – Tam Örnek
url: /tr/net/text-recognition/extract-text-from-tiff-with-aspose-ocr-engine-complete-examp/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# TIFF'ten Metin Çıkarma – C#'ta Tam OCR Motoru Örneği

Hiç **TIFF** görüntülerinden metin çıkarmak istediniz ama çok sayfalı dosyaları işleyebilecek bir kütüphaneyi, bir dizi geçici çözümle bulmak zorunda kaldınız mı? Tek başınıza değilsiniz. Birçok eski sistemde belgeler çok sayfalı TIFF taramaları olarak gelir ve ham metni çıkarmak, arama, uyumluluk ya da veri girişi otomasyonu için vazgeçilmez bir özelliktir.

İyi haber? Aspose OCR ile bunu sadece birkaç satır kodla yapabilirsiniz—düşük seviyeli piksel tamponlarıyla uğraşmanıza gerek yok. Bu öğretici, çok sayfalı bir TIFF'i yükleyen, her sayfayı tanıyan ve hem güzel biçimlendirilmiş JSON hem de isteğe bağlı XML üreten **tam bir OCR motoru örneği** üzerinden sizi yönlendirecek. Sonunda, TIFF dosyalarından saniyeler içinde metin çıkaran, çalıştırmaya hazır bir C# konsol uygulamanız olacak.

## Öğrenecekleriniz

- .NET projesinde Aspose OCR motorunu nasıl kuracağınızı.  
- **TIFF** dosyalarından, çok sayfalı işleme dahil, **metin çıkarmak** için gereken tam kodu.  
- JSON ile XML çıktısı arasındaki farkları ve ikisini de nasıl üretebileceğinizi.  
- Yaygın sorunları (ör. görüntü DPI, bellek kullanımı) nasıl çözeceğinize dair ipuçları.  

### Ön Koşullar

- .NET 6.0 SDK veya daha yeni bir sürüm (kod .NET Core ve .NET Framework ile çalışır).  
- Geçerli bir Aspose OCR lisansı (veya ücretsiz deneme anahtarı).  
- Visual Studio 2022 veya tercih ettiğiniz herhangi bir C# editörü.  
- Örnek çok sayfalı TIFF dosyası (örnekte `multi-page.tiff` olarak adlandırılmıştır).  

> **Pro ipucu:** Sıkı bir bütçeniz varsa, ücretsiz deneme sürümü ayda 100 sayfaya kadar metin çıkarmanıza izin verir—test için mükemmel.

---

## 1. Adım – OCR Motorunu Başlatma (ocr engine example)

**TIFF**'ten **metin çıkarmak** için önce OCR motorunun bir örneğine ihtiyacımız var. Bu nesne, daha sonra (dil, çözünürlük vb.) ayarlayabileceğiniz tüm yapılandırmaları tutar.

```csharp
using Aspose.OCR;
using System.IO;

// Create a new OCR engine – this is the core of our ocr engine example
var ocrEngine = new OcrEngine();

// Optional: set language if you know the document’s language
// ocrEngine.Language = Language.English;
```

*Neden önemli:* `OcrEngine` sınıfı ağır işleri soyutlar. Tek bir örnek oluşturup birden çok görüntüde yeniden kullanmak, her sayfa için yeni bir motor yaratmaktan daha bellek‑verimli olur.

---

## 2. Adım – Çok Sayfalı TIFF'i Yükleme (extract text from TIFF)

Şimdi motoru kaynak dosyamıza yönlendiriyoruz. `ImageStream.FromFile` TIFF, JPEG, PNG ve daha birçok formatı destekler, ancak bu öğreticide sadece TIFF'e odaklanıyoruz.

```csharp
// Load the multi‑page TIFF you want to process
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/multi-page.tiff");
```

> **Not:** `YOUR_DIRECTORY` ifadesini makinenizdeki gerçek klasör yolu ile değiştirin.  
> **İpucu:** TIFF'iniz düşük DPI'ye (150'nin altında) sahipse, OCR doğruluğunu artırmak için ön işleme yapmayı düşünün.

---

## 3. Adım – Tüm Sayfaları Tanıma

`Recognize()` metodunu çağırmak, OCR algoritmasını **her sayfa** için çalıştırır. Sonuç nesnesi ham metni, güven skorlarını ve sayfa bazlı segmentasyonu içerir.

```csharp
// Run OCR on the loaded image – this extracts text from all pages
var ocrResult = ocrEngine.Recognize();
```

*Ne elde edersiniz:* `ocrResult` bir `PageResult` koleksiyonu tutar. Her sayfanın metnine `ocrResult.Pages[i].Text` ile erişebilirsiniz. Motor ayrıca kalite kontrolü için faydalı olabilecek güven seviyeleri sağlar.

---

## 4. Adım – Sonuçları JSON (ve isteğe bağlı XML) Olarak Kaydetme

Modern akışların çoğu JSON tercih eder, ancak eski sistemler hâlâ XML kullanır. İşte her iki formatı da güzel biçimlendirilmiş şekilde üretmenin yolu.

```csharp
// Convert the recognition result to pretty‑printed JSON
string jsonResult = ocrResult.ToJson(prettyPrint: true);
File.WriteAllText(@"YOUR_DIRECTORY/result.json", jsonResult);

// Optional: also output XML for older workflows
string xmlResult = ocrResult.ToXml();
File.WriteAllText(@"YOUR_DIRECTORY/result.xml", xmlResult);
```

### Örnek JSON Çıktısı (kısaltılmış)

```json
{
  "Pages": [
    {
      "PageNumber": 1,
      "Text": "Invoice #12345\nDate: 2024‑03‑15\nTotal: $1,250.00",
      "Confidence": 0.97
    },
    {
      "PageNumber": 2,
      "Text": "Itemized List\n1. Widget A – $500.00\n2. Widget B – $750.00",
      "Confidence": 0.95
    }
  ]
}
```

JSON insan tarafından okunabilir olduğundan hata ayıklama çok kolaydır. İhtiyacınız olursa XML aynı yapıyı yansıtır.

---

## 5. Adım – Çıkarma İşlemini Doğrulama (extract text from TIFF)

Dosyalar yazıldıktan sonra, bir hızlı kontrol hiçbir şeyin ters gitmediğinden emin olmanızı sağlar.

```csharp
// Load the JSON back just to confirm it was saved correctly
string loadedJson = File.ReadAllText(@"YOUR_DIRECTORY/result.json");
Console.WriteLine("First 200 characters of JSON output:");
Console.WriteLine(loadedJson.Substring(0, Math.Min(200, loadedJson.Length)));
```

Eğer snippet ekrana basıldıysa, **TIFF'ten metin çıkarmayı** başarıyla tamamlamış ve sonuçları kalıcı hale getirmişsiniz demektir. Bundan sonra JSON'u bir arama indeksine, veritabanına ya da herhangi bir downstream servise gönderebilirsiniz.

---

## Aspose OCR ile TIFF'ten Metin Çıkarma Neden Tercih Edilmeli?

- **Çok sayfalı destek kutudan çıktığı gibi** – TIFF'i manuel olarak bölmeye gerek yok.  
- **Yüksek doğruluk** – özel sinir ağı modelleri sayesinde.  
- **Çapraz platform** – Windows, Linux ve macOS .NET çalışma zamanlarında çalışır.  
- **Zengin çıktı formatları** (JSON, XML, düz metin) modern ve eski yığınlara uyum sağlar.  

Hala kararsızsanız, bir örnek belge üzerinde ücretsiz denemeyi deneyin. Açık kaynak alternatiflerine kıyasla hız ve sadeliği hemen fark edeceksiniz; çoğu ek görüntü ön işleme gerektirir.

---

## Yaygın Sorunlar ve Çözüm Önerileri

| Sorun | Belirti | Çözüm |
|-------|---------|-----|
| Düşük çözünürlüklü TIFF | Karakter eksikliği, düşük güven | OCR'den önce görüntüyü ≥150 DPI'ye yükseltin (`ocrEngine.Image = ImageStream.FromFile(...).Resize(150)` ) |
| Yanlış dil | Özellikle İngilizce dışı metinlerde bozuk kelimeler | `ocrEngine.Language = Language.Spanish` (veya uygun dili) `Recognize()`'den önce ayarlayın |
| Büyük dosyalarda bellek tükenmesi | `OutOfMemoryException` | Sayfaları partiler halinde işleyin: `ocrEngine.Image.Pages` üzerinden döngü kurup `RecognizePage(i)` çağırın |
| Lisans uygulanmadı | Çıktıda “Evaluation” filigranı | Lisansınızı kaydedin: `License license = new License(); license.SetLicense("Aspose.OCR.lic");` |

---

## Tam Çalışan Örnek (Kopyala‑Yapıştır Hazır)

Aşağıda yeni bir konsol projesine yapıştırabileceğiniz tam program yer alıyor. Tartıştığımız tüm parçalar—başlatma, yükleme, tanıma ve kaydetme—burada bulunuyor.

```csharp
using Aspose.OCR;
using System;
using System.IO;

namespace TiffOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣  Initialize the OCR engine (ocr engine example)
            // -------------------------------------------------
            var ocrEngine = new OcrEngine();

            // Optional: set license if you have one
            // var license = new License();
            // license.SetLicense("Aspose.OCR.lic");

            // -------------------------------------------------
            // 2️⃣  Load the multi‑page TIFF (extract text from TIFF)
            // -------------------------------------------------
            string tiffPath = @"YOUR_DIRECTORY/multi-page.tiff";
            if (!File.Exists(tiffPath))
            {
                Console.WriteLine($"File not found: {tiffPath}");
                return;
            }

            ocrEngine.Image = ImageStream.FromFile(tiffPath);

            // -------------------------------------------------
            // 3️⃣  Recognize every page
            // -------------------------------------------------
            var ocrResult = ocrEngine.Recognize();

            // -------------------------------------------------
            // 4️⃣  Save JSON (pretty) and optional XML
            // -------------------------------------------------
            string jsonPath = @"YOUR_DIRECTORY/result.json";
            string jsonResult = ocrResult.ToJson(prettyPrint: true);
            File.WriteAllText(jsonPath, jsonResult);
            Console.WriteLine($"JSON saved to {jsonPath}");

            // Optional XML output
            string xmlPath = @"YOUR_DIRECTORY/result.xml";
            string xmlResult = ocrResult.ToXml();
            File.WriteAllText(xmlPath, xmlResult);
            Console.WriteLine($"XML saved to {xmlPath}");

            // -------------------------------------------------
            // 5️⃣  Quick verification (extract text from TIFF)
            // -------------------------------------------------
            string preview = jsonResult.Length > 200 ? jsonResult.Substring(0, 200) + "..." : jsonResult;
            Console.WriteLine("\nPreview of JSON output:");
            Console.WriteLine(preview);
        }
    }
}
```

Dosyayı `Program.cs` olarak kaydedin, `dotnet run` komutunu çalıştırın ve konsolun JSON ve XML dosyalarının nereye kaydedildiğini bildirmesini izleyin. İşte bu kadar—**OCR motoru örneği** ile TIFF'ten metin çıkarmayı tamamladınız.

---

## Sonraki Adımlar ve İlgili Konular

- **Toplu işleme:** Yukarıdaki mantığı bir `foreach` döngüsü içinde sararak onlarca TIFF dosyasını otomatik olarak işleyin.  
- **Arama entegrasyonu:** JSON'u Elasticsearch ya da Azure Cognitive Search'e göndererek taranmış belgeler üzerinde tam metin arama sağlayın.  
- **Görüntü ön işleme:** Aspose’un `ImageProcessing` API'sını keşfederek OCR'den önce eğme, lekeleri temizleme veya kontrast ayarlama yapın.  
- **Alternatif çıktı:** Yalnızca ham stringlere ihtiyacınız varsa `ocrResult.ToPlainText()` kullanın.  

Diğer görüntü formatlarıyla da aynı desen çalışır; sadece kaynak dosyayı PDF ya da PNG olarak değiştirmeniz yeterlidir. Temel çıkarım, motor bir kez kurulduğunda geri kalanın tekrarlanabilir bir pipeline olmasıdır.

---

## Sonuç

Aspose OCR ile **TIFF'ten metin çıkarma** işlemini gerçekleştiren, temiz JSON ve isteğe bağlı XML üreten **tam bir OCR motoru örneği** üzerinden ilerledik. Kod kendi içinde bütünleşik, açıklamalar her adımın “neden”ini kapsıyor.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}