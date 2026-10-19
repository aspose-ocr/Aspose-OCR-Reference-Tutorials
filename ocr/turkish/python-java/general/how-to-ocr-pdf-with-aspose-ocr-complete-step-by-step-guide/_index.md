---
category: general
date: 2026-05-03
description: Aspose OCR Java kullanarak PDF'yi OCR'lamak nasıl yapılır. PDF üzerinde
  OCR çalıştırmayı, PDF'den metin tanımayı, PDF'yi JSON'a dönüştürmeyi ve OCR için
  PDF'yi sadece birkaç satır kodla yüklemeyi öğrenin.
draft: false
keywords:
- how to ocr pdf
- run ocr on pdf
- recognize text pdf
- convert pdf to json
- load pdf for ocr
language: tr
og_description: Aspose OCR Java kullanarak PDF'yi OCR nasıl yapılır. Bu rehber, PDF
  üzerinde OCR çalıştırmayı, PDF'deki metni tanımayı, PDF'yi JSON'a dönüştürmeyi ve
  PDF'yi hızlı bir şekilde OCR için yüklemeyi gösterir.
og_title: Aspose OCR ile PDF'yi OCR'lamak – Tam Programlama Öğreticisi
tags:
- Aspose OCR
- Java
- PDF processing
title: Aspose OCR ile PDF'yi OCR'lamak – Tam Adım Adım Kılavuz
url: /tr/python-java/general/how-to-ocr-pdf-with-aspose-ocr-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PDF'yi Aspose OCR ile Nasıl OCR Yapılır – Tam Adım‑Adım Kılavuz

Hiç **PDF'yi OCR yapmanın** komut satırı araçlarıyla uğraşmadan ya da pahalı SaaS hizmetlerine para ödeyerek nasıl yapılacağını merak ettiniz mi? Tek başınıza değilsiniz. Birçok projede—fatura otomasyonu, taranmış sözleşmelerin arşivlenmesi veya aranabilir bir bilgi tabanı oluşturma—PDF'lerden hızlı ve güvenilir bir şekilde metin çıkarmanız gerekir.  

İyi haber? Aspose OCR for Java ile **PDF üzerinde OCR çalıştırabilir**, PDF sayfalarındaki metni tanıyabilir, **PDF'yi JSON'a dönüştürebilir** ve hatta **PDF'yi OCR için yükleyebilirsiniz** sadece birkaç satır kodla. Bu öğreticide tüm iş akışını adım adım inceleyecek, her adımın neden önemli olduğunu açıklayacak ve kendi projenize ekleyebileceğiniz çalıştırmaya hazır bir kod örneği sunacağız.

## Öğrenecekleriniz

- Aspose OCR motorunu nasıl kurup lisansınızı uygulayacağınızı.
- **PDF'yi OCR için yüklemenin** tam yolunu ve tanıyıcıya nasıl besleyeceğinizi.
- **PDF metnini tanımanın** tüm sayfalarda tek bir çağrıyla nasıl yapılacağını.
- Tam OCR sonucunu **JSON** dosyasına (alt sistem API'leri için mükemmel) ve tek bir sayfayı **XML**'e dışa aktarmayı.
- Çok sayfalı PDF'lerle veya özel dil paketleriyle çalışırken ihtiyaç duyabileceğiniz ipuçları, tuzaklar ve varyasyonlar.

> **Önkoşullar** – Java 8 veya daha yeni bir sürüm, geçerli bir Aspose OCR for Java lisans dosyası (`Aspose.OCR.Java.lic`) ve sınıf yolunuzda Aspose OCR JAR dosyası gerekir. Başka harici kütüphane gerekmez.

---

## PDF'yi OCR – Aspose OCR Motorunu Başlatma

İlk olarak `OcrEngine` örneği oluşturmalı ve lisansınızı eklemelisiniz. Bu adım tüm özellik setini açar ve değerlendirme filigranını kaldırır.

```java
// Step 1: Initialize the OCR engine and apply the license
import com.aspose.ocr.*;

public class PdfOcrDemo {
    public static void main(String[] args) throws Exception {
        // Create the engine
        OcrEngine ocrEngine = new OcrEngine();

        // Apply the license – replace the path with your actual .lic file location
        License lic = new License();
        lic.setLicense("Aspose.OCR.Java.lic");

        // From here on the engine runs in licensed mode
```

**Neden önemli:**  
Lisans olmadan Aspose OCR, sayfa sayısını sınırlayan ve çıktıya filigran ekleyen sınırlı bir “deneme” modunda çalışır. Lisansı önceden uygulamak, sonraki adımların beklenmedik kısıtlamalar olmadan çalışmasını sağlar.

---

## PDF'yi OCR – Belgeyi Yükleme ve Metni Tanıma

Şimdi **PDF'yi OCR için yüklüyoruz**. Aspose OCR, PDF'leri özel bir `PdfDocument` türü olarak ele alır; bu tür içsel olarak her sayfayı bir görüntüye dönüştürür ve tanıyıcıya besler.

```java
        // Step 2: Load the PDF document you want to process
        PdfDocument pdfDoc = PdfDocument.fromFile("YOUR_DIRECTORY/input.pdf");

        // Step 3: Run OCR on the whole document
        // recognizeDocument returns an array of OcrPage objects, one per PDF page
        OcrPage[] ocrPages = ocrEngine.recognizeDocument(pdfDoc);
```

**Arka planda neler oluyor?**  
`recognizeDocument` her sayfayı dolaşır, optimal DPI'da rasterleştirir ve ardından OCR motorunu çalıştırır. Sonuç, her öğenin algılanan metni, güven skorlarını ve düzen bilgilerini içeren bir `OcrPage` dizisidir. Bu yaklaşım, ham PDF baytlarını genel bir OCR kütüphanesine vermekten çok daha güvenilirdir.

---

## OCR Sonucunu JSON'a Dönüştür – Tam Raporu Dışa Aktarma

Çoğu alt sistem JSON tercih eder çünkü Java, JavaScript, Python veya hatta PowerShell'de kolayca serileştirilebilir. Aspose OCR, tüm `OcrPage[]` dizisini serileştiren bir `JsonExport` yardımcı sınıfı ile birlikte gelir.

```java
        // Step 4: Export the complete OCR result to a JSON file
        String jsonPath = "YOUR_DIRECTORY/report_ocr.json";
        JsonExport.save(ocrPages, jsonPath);
        System.out.println("JSON saved to " + jsonPath);
```

**Ne zaman kullanılır?**  
OCR çıktısını bir arama indeksine (Elasticsearch, Solr) veya bir veri hattına beslemeniz gerektiğinde, JSON formatı her sayfa, satır ve kelime için güven değerleriyle birlikte yapılandırılmış bir temsil sunar.

---

## İlk Sayfayı XML'e Dışa Aktar – Tek Sayfayı Kaydet

Bazen sadece tek bir sayfa ilginizi çeker—belki ilk sayfa bir başlık ya da fatura numarası içerir. `XmlExport` sınıfı, tek bir `OcrPage`'i düzenli bir XML dosyasına dökmenizi sağlar.

```java
        // Step 5: Export the OCR result of the first page to an XML file
        String xmlPath = "YOUR_DIRECTORY/page1_ocr.xml";
        XmlExport.save(ocrPages[0], xmlPath);
        System.out.println("XML saved to " + xmlPath);
    }
}
```

**Neden XML?**  
Eski sistemler veya bazı kurumsal iş akışları hâlâ veri alımı için XML şemalarına dayanır. Oluşturulan dosya Aspose’un kendi şemasını izler, bu da doğrulamayı kolaylaştırır.

---

## Çıktıyı Doğrulama – JSON ve XML Dosyalarını Kontrol Etme

Program tamamlandığında `YOUR_DIRECTORY` içinde iki dosya görmelisiniz:

- `report_ocr.json` – Sayfa nesnelerinin bir dizisini içerir. Hızlı bir örnek şöyle görünebilir:

```json
[
  {
    "pageNumber": 1,
    "text": "Invoice #12345\nDate: 2026‑04‑30\n...",
    "confidence": 98.7,
    "words": [...]
  },
  {
    "pageNumber": 2,
    "text": "...",
    "confidence": 97.4,
    "words": [...]
  }
]
```

- `page1_ocr.xml` – Sayfa 1 için aynı bilgileri `<OcrPage>` etiketleri içinde tutar.

Herhangi bir editörde açın; ham OCR dizelerini, güven skorlarını ve sınırlayıcı kutu koordinatlarını göreceksiniz. JSON boş görünüyorsa, giriş PDF'inin gerçekten rasterleştirilmiş içerik (taranmış görüntüler) içerdiğini ve seçilebilir metin olmadığını iki kez kontrol edin—Aspose OCR yalnızca görüntüler üzerinde çalışır.

---

## Yaygın Tuzaklar & Profesyonel İpuçları

| Sorun | Neden Oluşur | Çözüm |
|-------|--------------|-------|
| **Boş JSON** | PDF yerel metin içeriyor, görüntü değil. | Görüntüleme zorlamak için `PdfDocument.fromFile(..., true)` kullanın veya sayfaları önceden görüntülere dönüştürün. |
| **Düşük güven** | Kaynak PDF düşük çözünürlüklü veya aşırı sıkıştırılmış. | `recognizeDocument` çağrısından önce `ocrEngine.getImageProcessingOptions().setDpi(300)` ile DPI'yi artırın. |
| **Lisans bulunamadı** | Yanlış yol veya eksik dosya. | Mutlak bir yol kullanın veya `.lic` dosyasını sınıf yoluna koyup `lic.setLicense("Aspose.OCR.Java.lic")` çağırın. |
| **Büyük PDF'lerde bellek tükenmesi** | Tüm sayfalar aynı anda belleğe yükleniyor. | Sayfaları partiler halinde işleyin: `recognizeDocument(pdfDoc, startPage, endPage)`. |

---

## Örneği Genişletme

- **Belirli bir dil ile PDF üzerinde OCR çalıştırma** – `ocrEngine.getLanguage().setLanguage(Language.English)` ayarlayın veya özel bir dil paketi yükleyin.  
- **Her sayfayı ayrı JSON dosyalarına dışa aktarma** – `ocrPages` üzerinde döngü kurup `JsonExport.save(page, "page" + page.getPageNumber() + ".json")` çağırın.  
- **Bir arama motoru ile bütünleştirme** – JSON'u Elasticsearch’ün `attachment` işlemcisine tam metin arama için besleyin.

---

## Sonuç

Artık Aspose OCR for Java kullanarak **PDF'yi OCR yapmanın** tam, üretim‑hazır bir çözümüne sahipsiniz. Motoru başlatıp PDF'yi yükleyerek, OCR çalıştırıp hem **JSON** hem de **XML** dışa aktararak OCR'ı herhangi bir arka uç iş akışına entegre edebilirsiniz—ister **PDF üzerinde OCR çalıştırın**, ister **PDF metnini tanıyın**, ister **PDF'yi JSON'a dönüştürün**, ister sadece **PDF'yi OCR için yükleyin**.

Biraz deneyin, DPI veya dil ayarlarını değiştirin ve önceki opak PDF'lerinizin aranabilir varlıklara dönüşümünü izleyin. Daha ileri gitmek mi istiyorsunuz? JSON'u Elasticsearch'e indeksleyin ya da XML'i XSLT ile işleyerek özel raporlar oluşturun.

İyi kodlamalar, PDF'leriniz her zaman okunabilir olsun! 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}