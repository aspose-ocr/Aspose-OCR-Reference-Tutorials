---
category: general
date: 2026-03-07
description: Aspose OCR örneği, yazım denetimini nasıl etkinleştireceğinizi, özel
  bir sözlük ekleyeceğinizi, görüntü OCR'sini yükleyeceğinizi ve OCR hatalarını hızlıca
  nasıl düzelteceğinizi gösterir.
draft: false
keywords:
- aspose ocr example
- how to enable spellcheck
- how to add dictionary
- load image ocr
- how to fix ocr errors
language: tr
og_description: Aspose OCR örneği, yazım denetimini etkinleştirme, özel bir sözlük
  ekleme, OCR için bir görüntü yükleme ve yaygın OCR hatalarını düzeltme konusunda
  size rehberlik eder.
og_title: Aspose OCR Örneği – Yazım Denetimini Etkinleştir ve Hataları Düzelt
tags:
- Aspose
- OCR
- C#
- SpellCheck
title: Aspose OCR Örneği – C#'ta Yazım Denetimini Etkinleştir ve Hataları Düzelt
url: /tr/net/ocr-optimization/aspose-ocr-example-enable-spellcheck-and-fix-errors-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose OCR Örneği – C#'ta Yazım Denetimini Etkinleştir ve Hataları Düzelt

Ever needed an **Aspose OCR örneği** that not only reads text from an image but also cleans up those pesky spelling mistakes? You're not the only one. In many real‑world projects the raw OCR output is riddled with typos, especially when the source image contains low‑contrast fonts or handwritten notes.  

The good news? With Aspose.OCR you can **enable spellcheck**, plug in your own dictionary, and get a polished string in just a few lines of code. Below you’ll see exactly **how to enable spellcheck**, **how to add a dictionary**, and **how to load image OCR** so you can finally **fix OCR errors** without pulling your hair out.

In this tutorial we’ll cover everything you need—from NuGet installation to a complete, runnable program that prints corrected text. By the end you’ll have a solid **Aspose OCR example** you can drop straight into any .NET project.

## Önkoşullar

- .NET 6.0 SDK veya daha yenisi (kod .NET Core ve .NET Framework ile de çalışır)
- Visual Studio 2022 veya herhangi bir C# uyumlu IDE
- Açık, yazılmış İngilizce metin içeren bir görüntü dosyası (`typed_text.png`)
- Aspose.OCR NuGet paketini indirmek için internet erişimi

Başka üçüncü‑taraf kütüphanelerine gerek yok.

---

## 1. Adım – Aspose.OCR NuGet Paketini Yükleyin (Load Image OCR)

Kod yazmadan önce, OCR motorunu çalıştıran kütüphaneye ihtiyacımız var.

```bash
dotnet add package Aspose.OCR
```

> **Pro tip:** Visual Studio kullanıyorsanız, projeye sağ‑tıklayın → *Manage NuGet Packages* → **Aspose.OCR** aratın ve *Install*'a tıklayın.  

Paketi kurmak, `OcrEngine`, `ImageStream` ve daha sonra kullanacağımız yerleşik yazım denetimi araçlarına erişmenizi sağlar. Paket yerinde olduğunda, **load image OCR**'ye hazırsınız.

## 2. Adım – OCR Motoru Örneğini Oluşturun

Motoru oluşturmak, herhangi bir **Aspose OCR example**'da ilk somut adımdır. `OcrEngine`'i, bitmap'i analiz edip metin üreten bir beyin olarak düşünün.

```csharp
using Aspose.OCR;
using Aspose.OCR.SpellCheck;

// Step 2: Initialize the OCR engine
var ocrEngine = new OcrEngine();
```

## 3. Adım – Spellcheck'i Nasıl Etkinleştirirsiniz (Ve Neden Önemlidir)

Ham OCR çıktısı genellikle “teh” gibi “the” yerine yanlış tanınan kelimeler içerir. Yerleşik yazım denetleyiciyi etkinleştirmek, Aspose'un bu hataları en muhtemel doğru yazımla otomatik olarak değiştirmesini sağlar.

```csharp
// Step 3: Turn on spell checking and set the language to English
ocrEngine.Settings.SpellCheck.Enabled = true;
ocrEngine.Settings.SpellCheck.Language = SpellCheckLanguage.English;
```

> **Neden spellcheck'i etkinleştirirsiniz?**  
> - **Doğruluk:** Bir son‑işlem yazım denetimi, basılı belgeler için genel metin doğruluğunu %10‑15 artırabilir.  
> - **Kullanıcı deneyimi:** Temiz metin, sonucu arama indekslerine veya analiz boru hatlarına beslediğinizde daha az temizlik anlamına gelir.

## 4. Adım – Sözlük Nasıl Eklenir (Özel Kelimeler)

Bazen varsayılan sözlük, marka adlarınızı, ürün kodlarınızı veya alan‑spesifik jargonunuzu bilmez. İşte **how to add dictionary** burada devreye girer.

```csharp
// Step 4: Add custom words that the spell checker should accept
ocrEngine.Settings.SpellCheck.CustomDictionary.AddWords(new[]
{
    "AsposeOCR",   // our library name
    "OCRify",      // a fictional product
    "CSharpify"    // another custom term
});
```

Bir dizi, bir liste ya da büyük bir özel kelime hazineniz varsa bir dosyadan okuyarak besleyebilirsiniz. Yazım denetleyici artık bu girdileri geçerli kabul edecek ve yanlış düzeltmeleri önleyecektir.

## 5. Adım – OCR İçin Görüntüyü Yükleyin (Load Image OCR)

Motor yapılandırıldıktan sonra, okumak istediğimiz resme işaret etmemiz gerekiyor. `ImageStream.FromFile` yardımcı işlevi dosya okuma detaylarını soyutlar.

```csharp
// Step 5: Load the image that contains the text to be recognized
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/typed_text.png");
```

> **İpucu:** Görüntünüz projenin bir alt klasöründe ise, *Copy to Output Directory* özelliğini *Copy always* olarak ayarlayın, böylece yol çalışma zamanında çözülür.

## 6. Adım – Tanıma Yapın ve OCR Hatalarını Düzeltin

Her şey ayarlandığında, `Recognize()`'a tek bir çağrı OCR boru hattını çalıştırır, yazım denetimini uygular ve temizlenmiş sonucu `ocrEngine.Text` içinde saklar.

```csharp
// Step 6: Run OCR and let the spell checker clean the output
ocrEngine.Recognize();

// Step 7: Output the corrected text to the console
Console.WriteLine("Corrected text:");
Console.WriteLine(ocrEngine.Text);
```

### Beklenen Çıktı

`typed_text.png` dosyasının `The quick brown fox jumps over teh lazy dog` cümlesini içerdiğini varsayarsak, konsol şu çıktıyı verir:

```
Corrected text:
The quick brown fox jumps over the lazy dog
```

“teh” kelimesinin otomatik olarak “the” olarak düzeltildiğine dikkat edin. Eğer özel sözlüğe “OCRify” eklemiş olsaydınız ve görüntü bu kelimeyi içeriyorsa, motor onu dokunulmamış bırakacaktı.

---

## Tam Çalışan Örnek (Kopyala‑Yapıştır Hazır)

Aşağıda, yeni bir konsol projesine ekleyebileceğiniz tam program bulunmaktadır. Yukarıdaki tüm adımları ve açıklık için birkaç yorum içerir.

```csharp
// ---------------------------------------------------------------
// Aspose OCR Example – Enable Spellcheck and Fix Errors
// ---------------------------------------------------------------

using System;
using Aspose.OCR;
using Aspose.OCR.SpellCheck;

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Create the OCR engine
            var ocrEngine = new OcrEngine();

            // 2️⃣ Enable spell checking (how to enable spellcheck)
            ocrEngine.Settings.SpellCheck.Enabled = true;
            ocrEngine.Settings.SpellCheck.Language = SpellCheckLanguage.English;

            // 3️⃣ Add custom words (how to add dictionary)
            ocrEngine.Settings.SpellCheck.CustomDictionary.AddWords(new[]
            {
                "AsposeOCR",
                "OCRify",
                "CSharpify"
            });

            // 4️⃣ Load the image (load image OCR)
            // Replace the path with the actual location of your image file
            ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/typed_text.png");

            // 5️⃣ Run OCR – this also fixes common OCR errors (how to fix ocr errors)
            ocrEngine.Recognize();

            // 6️⃣ Show the corrected result
            Console.WriteLine("Corrected text:");
            Console.WriteLine(ocrEngine.Text);
        }
    }
}
```

Bunu `Program.cs` olarak kaydedin, `dotnet run` komutunu çalıştırın ve konsolda düzeltilmiş cümleyi görmelisiniz.

---

## Sık Sorulan Sorular & Kenar Durumları

| Question | Answer |
|----------|--------|
| **Görüntü çok sayfalı bir PDF ise ne olur?** | Aspose.OCR, PDF sayfalarını görüntü olarak işleyebilir. `ocrEngine.Image = ImageStream.FromPdf("file.pdf", pageNumber: 1);` kullanın ve sayfalar arasında döngü yapın. |
| **Dilini İngilizce dışındaki bir dile değiştirebilir miyim?** | Kesinlikle. `ocrEngine.Settings.SpellCheck.Language = SpellCheckLanguage.French;` (veya desteklenen herhangi bir dil) olarak ayarlayın. |
| **Özel sözlüğüm çok büyük—performansı etkiler mi?** | Binlerce kelime eklemek başlangıçta küçük bir maliyet getirir, ancak arama, alt yapıda bir hash‑set sayesinde O(1) zaman alır. Çok büyük sözlükler için, uygulama başlangıcında bir kez yüklemeyi düşünün. |
| **OCR motoru bozuk bir görüntüde istisna fırlatırsa ne olur?** | `Recognize()` çağrısını try‑catch bloğuna alın ve `ocrEngine.LastError`'ı inceleyin. Ayrıca `ocrEngine.Image.Width` ve `Height` ile görüntü boyutlarını önceden doğrulayabilirsiniz. |
| **Üretim kullanımında lisansa ihtiyacım var mı?** | Ücretsiz değerlendirme testi için çalışır, ancak ticari lisans değerlendirme filigranını kaldırır ve tam performansı açar. |

## Sonuç

Artık **tam bir Aspose OCR example**'a sahipsiniz; bu örnek **spellcheck'in nasıl etkinleştirileceğini**, **sözlüğün nasıl ekleneceğini**, **image OCR'nin nasıl yükleneceğini** ve **OCR hatalarının nasıl düzeltileceğini** temiz ve üretim‑hazır bir şekilde gösterir. Yazım denetleyiciyi yapılandırıp özel bir kelime listesi sağlayarak, çıkarılan metnin kalitesini post‑processing mantığı yazmadan büyük ölçüde artırırsınız.

Bir sonraki adıma hazır mısınız? Dili İspanyolcaya değiştirin, çok sayfalı bir PDF besleyin veya çıktıyı aranabilir bir Azure Cognitive Search indeksine entegre edin. Aynı desen geçerlidir—sadece dil bayrağını ayarlayın ve belki özel sözlüğü genişletin.

Bu rehberi faydalı bulduysanız, GitHub'da yıldız verin, ekip arkadaşlarınızla paylaşın veya aşağıya bir yorum bırakın. Kodlamanız keyifli olsun ve OCR sonuçlarınız her zaman hatasız olsun!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}