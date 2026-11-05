---
category: general
date: 2026-01-13
description: c# ocr öğreticisi, görüntüden metin nasıl çıkarılacağını, ocr için görüntünün
  nasıl yükleneceğini ve Aspose OCR kullanarak json çıktısının nasıl biçimlendirileceğini
  gösterir. Nesneyi json'a nasıl serileştireceğinizi öğrenin.
draft: false
keywords:
- c# ocr tutorial
- extract text from image
- format json output
- serialize object to json
- load image for ocr
language: tr
og_description: c# ocr öğreticisi, görüntüden metin çıkarma, ocr için görüntü yükleme
  ve Aspose OCR ile JSON çıktısını biçimlendirme adımlarını size gösterir.
og_title: c# ocr öğretici – Metni Çıkar ve JSON'u Biçimlendir
tags:
- OCR
- C#
- JSON
title: c# ocr öğreticisi – Görüntüden Metin Çıkar ve Biçimlendirilmiş JSON Al
url: /tr/net/text-recognition/c-ocr-tutorial-extract-text-from-image-and-get-formatted-jso/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# ocr tutorial – Görüntüden Metin Çıkarma ve JSON Çıktısını Biçimlendirme

Hiç **görüntü dosyalarından metin çıkarma** işlemini düşük seviyeli piksel işleme ile uğraşmadan C# projenizde yapmayı düşündünüz mü? İşte bu *c# ocr tutorial* tam da bu sorunu çözüyor. Birkaç dakika içinde **ocr için görüntüyü yükleme**, Aspose OCR çalıştırma ve **json çıktısını biçimlendirme** adımlarını göreceksiniz; böylece veriyi doğrudan API’nize ya da veritabanınıza aktarabilirsiniz.

Kodun her satırını adım adım inceleyecek, her parçanın neden önemli olduğunu açıklayacak ve beklemeniz gereken tam JSON örneğini göstereceğiz. Sonunda, bir fatura PNG’sini temiz, girintili JSON’a dönüştüren, çalıştırmaya hazır bir konsol uygulamanız olacak. Gereksiz ayrıntı yok, sadece .NET 6+ projenize ekleyebileceğiniz pratik bir çözüm.

## Bu c# ocr tutorial’da Neler Ele Alınıyor

- Aspose.OCR NuGet paketinin kurulumu  
- OCR işleme için bir görüntü dosyasının yüklenmesi  
- İngilizce metin (veya desteklenen herhangi bir dil) tanıma  
- **OCR sonucunu JSON’a serileştirme** ve güzel bir biçimlendirme  
- JSON çıktısını konsolda gösterme ve isterseniz kaydetme  

Sadece temel C# bilgisi ve güncel bir .NET SDK’sına ihtiyacınız var. Başka bir şey gerekmiyor. Faturalar, makbuzlar ya da taranmış formlar için **görüntüden metin çıkarma** konusunda meraklıysanız, okumaya devam edin.

---

## Adım 1: c# ocr tutorial Ortamını Kurun

Kod yazmaya başlamadan önce doğru araçlara sahip olduğunuzdan emin olun:

1. **.NET 6 SDK veya daha yeni bir sürüm** – Microsoft sitesinden indirebilirsiniz.  
2. **Visual Studio 2022** (Community sürümü yeterli) ya da tercih ettiğiniz herhangi bir editör.  
3. **Aspose.OCR NuGet paketi** – proje klasörünüzde `dotnet add package Aspose.OCR` komutunu çalıştırın.

> **İpucu:** Bir CI pipeline’ı kullanıyorsanız, paket referansını `.csproj` dosyanıza ekleyin; böylece derleme sırasında otomatik olarak geri yüklenir.

---

## Adım 2: OCR İçin Görüntüyü Yükleyin

Tutorial’ımızın ilk gerçek adımı, işlemek istediğiniz görüntüyü almaktır. Aspose OCR, PNG, JPEG ve TIFF gibi yaygın formatları destekler.

```csharp
using Aspose.OCR;
using System.Text.Json;

// Replace this with the actual path to your invoice image
string imagePath = @"C:\Invoices\invoice.png";

// Create an OcrImage instance from the file system
OcrImage inputImage = OcrImage.FromFile(imagePath);
```

> **Neden önemli:** Görüntüyü bir `OcrImage` olarak yüklemek, motorun bitmap verisine ve DPI bilgisine erişmesini sağlar; bu da tanıma doğruluğunu artırır. Bu adımı atlamak ya da bozuk bir dosya vermek, çalışma zamanı hatasına yol açar.

---

## Adım 3: Görüntüden Metin Çıkarma

Şimdi OCR motorunu çalıştırıyoruz. `Recognize` metodu, ham metin, güven skorları ve düzen detaylarını içeren zengin bir `OcrResult` nesnesi döndürür.

```csharp
// Initialize the OCR engine – no license needed for a trial run
OcrEngine ocrEngine = new OcrEngine();

// Recognize English text (you can change the language enum if needed)
OcrResult ocrResult = ocrEngine.Recognize(inputImage, OcrLanguage.English);
```

> **Köşe durumu:** Çok‑dilli bir belge işlemek istiyorsanız, farklı `OcrLanguage` değerleriyle `Recognize` metodunu iki kez çağırıp sonuçları birleştirin. Motor thread‑safe olduğundan büyük partileri paralelleştirebilirsiniz.

---

## Adım 4: Nesneyi JSON’a Serileştir – JSON Çıktısını Biçimlendirme

`OcrResult` nesnesi sade bir C# sınıfıdır; bu yüzden `System.Text.Json` ile doğrudan kullanılabilir. `WriteIndented` özelliğini etkinleştirerek çıktıyı insan‑okunur hâle getiriyoruz.

```csharp
// Serialize the OCR result with pretty printing
string json = JsonSerializer.Serialize(ocrResult, new JsonSerializerOptions
{
    WriteIndented = true
});
```

> **Elde edeceğiniz:** Tanınan metin, güven ve sayfa düzeni bilgilerini içeren güzel girintili bir JSON dizesi. Günlükleme, web servisine gönderme ya da NoSQL veritabanına kaydetme için idealdir.

---

## Adım 5: Biçimlendirilmiş JSON’ı Görüntüleme ve (İsteğe Bağlı) Kaydetme

Son olarak JSON’ı konsola yazdırıyoruz. İsterseniz `File.WriteAllText` ile bir dosyaya da kaydedebilirsiniz.

```csharp
// Show the JSON in the console
Console.WriteLine(json);

// Optional: Save to a .json file next to the image
string jsonPath = Path.ChangeExtension(imagePath, ".json");
File.WriteAllText(jsonPath, json);
Console.WriteLine($"\nJSON saved to: {jsonPath}");
```

**Beklenen konsol çıktısı (kısaltılmış):**

```json
{
  "Text": "Invoice #12345\nDate: 2025‑12‑01\nTotal: $250.00",
  "Confidence": 0.97,
  "Pages": [
    {
      "PageNumber": 1,
      "Blocks": [
        {
          "Text": "Invoice #12345",
          "Confidence": 0.99,
          "Rectangle": { "X": 50, "Y": 30, "Width": 200, "Height": 30 }
        }
        // …more blocks…
      ]
    }
  ]
}
```

OCR motoru herhangi bir metin bulamazsa, `Text` alanı boş bir string ve `Confidence` değeri `0` olur. Bu, görüntü kalitesini yeniden kontrol etmeniz gerektiğine işaret eder.

---

## Adım 6: Tam Çalışan Örnek

Her şeyi bir araya getirdiğimizde, yeni bir konsol uygulamasına kopyalayıp yapıştırabileceğiniz tam program aşağıdadır:

```csharp
using Aspose.OCR;
using System;
using System.IO;
using System.Text.Json;

class JsonResultDemo
{
    static void Main()
    {
        // 1️⃣ Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Load the source image (replace with your own path)
        string imagePath = @"C:\Invoices\invoice.png";
        OcrImage inputImage = OcrImage.FromFile(imagePath);

        // 3️⃣ Recognize text – this is the core of our c# ocr tutorial
        OcrResult ocrResult = ocrEngine.Recognize(inputImage, OcrLanguage.English);

        // 4️⃣ Serialize the result with pretty formatting
        string json = JsonSerializer.Serialize(ocrResult, new JsonSerializerOptions
        {
            WriteIndented = true
        });

        // 5️⃣ Output to console and optionally write to a file
        Console.WriteLine(json);
        string jsonPath = Path.ChangeExtension(imagePath, ".json");
        File.WriteAllText(jsonPath, json);
        Console.WriteLine($"\nJSON saved to: {jsonPath}");
    }
}
```

Programı çalıştırın (`dotnet run` komutunu proje klasöründen çalıştırın) ve konsolda taranmış faturanızın güzel biçimlendirilmiş JSON temsilini izleyin.

---

## Yaygın Tuzaklar ve İpuçları (c# ocr tutorial Ekstra)

| Sorun | Neden Oluşur | Çözüm |
|-------|--------------|-------|
| **Boş `Text` alanı** | Görüntü düşük kontrastlı ya da döndürülmüş. | Görüntüyü ön‑işleme (kontrast artırma, eğikliği düzeltme) yapın veya `OcrEngine.ImagePreprocess` kullanın. |
| **`System.DllNotFoundException`** | Aspose OCR yerel ikili dosyaları eksik. | NuGet paketinin doğru geri yüklendiğinden ve çalışma zamanı mimarisinin (x64/x86) OS’nizle eşleştiğinden emin olun. |
| **Büyük PDF’lerde performans yavaşlığı** | OCR her sayfayı sıralı işliyor. | Sayfa başına ayrı `OcrEngine` örnekleri oluşturarak paralelleştirin (motor thread‑safe). |
| **JSON çok büyük** | Tüm detayları, sınırlama kutularını da serileştiriyorsunuz. | Serileştirmeden önce sadece `Text` ve `Confidence` içeren bir DTO kullanın. |

> **Unutmayın:** Bu tutorial, temiz ve uçtan uca bir akış göstermeyi amaçlar. JSON’u daha sonra kısaltabilir ya da ekstra meta veri ekleyebilirsiniz.

---

## Sonuç

Bir **c# ocr tutorial** tamamladınız; görüntüyü yüklediniz, **görüntüden metin çıkarma** yaptınız ve **json çıktısını biçimlendirme** için **nesneyi json’a serileştirme** işlemini gerçekleştirdiniz. Adımlar basit, kod çalıştırılmaya hazır ve JSON, sonraki işlemler için mükemmel bir şekilde girintili.

Sırada ne var? `OcrLanguage.English` yerine `OcrLanguage.French` deneyin veya bir klasördeki makbuzları döngüyle işleyin. JSON’u doğrudan Azure Blob Storage’a kaydetmeyi ya da bir makine öğrenmesi modeline beslemeyi de keşfedebilirsiniz.

Herhangi bir sorunla karşılaşırsanız, görüntü yolunun doğru olduğundan ve Aspose OCR lisansınızın (varsa) `Recognize` çağrısından önce yüklendiğinden emin olun. İyi kodlamalar, ve OCR sonuçlarınız her zaman net olsun! 

--- 

*Image illustrating the OCR flow (alt text: "c# ocr tutorial diagram showing load image, recognize text, serialize to JSON")*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}