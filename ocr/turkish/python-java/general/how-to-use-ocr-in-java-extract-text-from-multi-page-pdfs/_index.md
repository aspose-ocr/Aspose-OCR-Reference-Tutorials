---
category: general
date: 2026-05-03
description: Java'da PDF dosyalarından metin çıkarmak için OCR nasıl kullanılır. PDF'den
  metin tanımayı öğrenin, PDF'yi metne dönüştürün ve OCR çok sayfalı PDF'yi verimli
  bir şekilde işleyin.
draft: false
keywords:
- how to use ocr
- extract text from pdf
- recognize text from pdf
- convert pdf to text
- ocr multi page pdf
language: tr
og_description: Java’da PDF dosyalarından metin çıkarmak için OCR nasıl kullanılır.
  Bu kılavuz, PDF’den metin tanıma, PDF’yi metne dönüştürme ve çok sayfalı PDF’lerde
  OCR işlemini nasıl gerçekleştireceğinizi gösterir.
og_title: Java'da OCR Nasıl Kullanılır – Çok Sayfalı PDF'lerden Metin Çıkarma
tags:
- ocr
- java
- pdf
- aspose
title: Java'da OCR Nasıl Kullanılır – Çok Sayfalı PDF'lerden Metin Çıkarma
url: /tr/python-java/general/how-to-use-ocr-in-java-extract-text-from-multi-page-pdfs/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java’da OCR Kullanımı – Çok Sayfalı PDF’lerden Metin Çıkarma

**How to use OCR** bir Java projesinde? PDF dosyalarından PDF’nin iç metin katmanına güvenmeden metin çıkarmanız gerektiğinde, doğru yerdesiniz. Bu öğretici, **PDF’den metin tanıma**, PDF’yi metne dönüştürme ve hatta **OCR çok sayfalı PDF**'yi tek bir çağrı ile işleme gibi tam, çalıştırılabilir bir çözümü adım adım gösterir.

Bir taranmış sözleşme aldığınızı hayal edin — PDF içinde 12 sayfalık bir TIFF. Dizineleme için aranabilir metne ihtiyacınız var, ancak dosyada gömülü karakter yok. Sorun değil; bunu tam olarak nasıl yapacağınızı adım adım göstereceğiz.

> **What you’ll get:** Aspose.OCR kullanan, çalıştırılmaya hazır bir Java kod parçacığı, her satırın neden önemli olduğuna dair açıklamalar, yaygın tuzaklar için ipuçları ve anında doğrulayabileceğiniz örnek çıktı.

---

## Gereksinimler

* **Java 17** (veya herhangi bir yeni JDK) – kod eski sürümlerle de çalışır, ancak 17 en ideal sürümdür.
* **Aspose OCR for Java** kütüphanesi – JAR dosyasını Aspose sitesinden indirebilir veya Maven/Gradle üzerinden ekleyebilirsiniz.
* İşlemek istediğiniz bir **çok sayfalı PDF** (veya TIFF). Örneklerimizde `contract_multipage.pdf` dosyasını `YOUR_DIRECTORY` adlı klasöre koyacağız.
* Geçerli bir **Aspose OCR lisans dosyası** (`Aspose.OCR.Java.lic`). Lisans olmadan kütüphane değerlendirme modunda çalışır; bu hızlı bir test için uygundur ancak bir filigran ekler.

Hepsi bu—ek OCR motorları, yerel ikili dosyalar yok, sadece tek bir JAR ve bir lisans.

![OCR kullanımı örneği](https://example.com/ocr-demo.png "Java’da OCR Kullanımı – sürecin görsel özeti")

*Görsel alt metin: Java’da OCR kullanımı – yükleme, tanıma ve metin çıktısı sürecinin görsel özeti.*

---

## Adım 1: OCR Motorunu Kurun – **How to Use OCR** Doğru Şekilde

İlk yapmanız gereken, OCR motorunun bir örneğini oluşturmak ve lisansınızı uygulamaktır. Lisans olmadan motor yine çalışır, ancak çıktıda bir deneme filigranı görürsünüz.

```java
// Import the Aspose OCR package
import com.aspose.ocr.*;

public class OcrPdfDemo {
    public static void main(String[] args) {
        // 1️⃣ Create the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Apply your license – replace the path with your actual .lic file
        ocrEngine.setLicense(new License().setLicense("Aspose.OCR.Java.lic"));
```

**Neden Önemli:**  
`OcrEngine` görüntü analizini, dil algılamasını ve metin çıkarımını yöneten temel nesnedir. Lisansı erken ayarlamak, motorun daha sonra deneme moduna geçmesini önler ve doğruluğu etkileyebilir.

---

## Adım 2: Belgeyi Yükleyin – **Extract Text from PDF** Verimli Şekilde

Aspose OCR, PDF ve TIFF konteynerlerini doğrudan okuyabilir. Burada taranmış görüntüler içeren çok sayfalı bir PDF yüklüyoruz.

```java
        // 3️⃣ Load a multi‑page PDF (or TIFF) from disk
        PdfDocument pdfDoc = PdfDocument.fromFile("YOUR_DIRECTORY/contract_multipage.pdf");
```

**Neden Önemli:**  
`PdfDocument.fromFile` konteyneri ayrıştırır ve her sayfaya bir görüntü olarak erişim sağlar. Bu soyutlama, OCR motorunun orijinal format ne olursa olsun her sayfayı aynı şekilde işlemesine olanak tanır.

**Tip:** Kaynak dosyanız bir TIFF ise aynı çağrı çalışır—Aspose formatı otomatik algılar. Ek kod gerekmez.

---

## Adım 3: Tüm Sayfaları Tek Seferde Tanıyın – **Recognize Text from PDF** Sorunsuz Şekilde

Sayfaları kendiniz döngüye almanız yerine, motoru tüm belgeyi tek bir çağrıyla işleyebilirsiniz. Bu, **OCR çok sayfalı PDF** ile uğraşırken **PDF’yi metne dönüştürme** için en verimli yoldur.

```java
        // 4️⃣ Recognize text on all pages with a single method call
        List<OcrPageResult> recognizedPages = ocrEngine.recognizeDocument(pdfDoc);
```

**Neden Önemli:**  
`recognizeDocument` metodunu bir kez çağırmak, motorun tekrar tekrar başlatılmasından kaynaklanan yükü azaltır. Ayrıca sayfalar arasında tutarlı dil ayarlarını garantiler; bu, sık sık farklı fontlar kullanan yasal belgeler için kritiktir.

---

## Adım 4: Tanınan Metni Çıktılayın – **Convert PDF to Text** Dizineleme İçin

Şimdi her sayfa işlendiğine göre, sonuçları döngüyle gezip çıkarılan dizeleri yazdırıyoruz. Ayrıca bunları bir dosyaya, veritabanına yazabilir veya bir arama indeksine besleyebilirsiniz.

```java
        // 5️⃣ Loop through each page's result and print the text
        for (int i = 0; i < recognizedPages.size(); i++) {
            OcrPageResult pageResult = recognizedPages.get(i);
            System.out.println("--- Page " + (i + 1) + " ---");
            System.out.println(pageResult.getText());
        }
    }
}
```

**Beklenen çıktı (kısaltılmış):**

```
--- Page 1 ---
THIS AGREEMENT is made on the 1st day of January 2024...
--- Page 2 ---
WHEREAS, the Parties desire to...
...
```

PDF 12 sayfa içeriyorsa, on iki `--- Page X ---` bölümü ve her birinin ardından OCR‑çıkarılmış metin göreceksiniz.

---

## **OCR Multi Page PDF** için İleri Düzey İpuçları

### 1. Dil Ayarlarını Düzenleyin

Varsayılan olarak Aspose dili otomatik algılar, ancak belirterek işlemi hızlandırabilirsiniz:

```java
ocrEngine.getLanguage().setLanguage(Language.ENGLISH);
```

### 2. Görüntü Ön‑İşlemeyi Kontrol Edin

Taranmış sözleşmeler genellikle gürültülüdür. Eğikliği düzeltme ve ikilileştirme özelliklerini etkinleştirebilirsiniz:

```java
ocrEngine.getImageProcessingOptions()
        .setDeskew(true)
        .setBinarization(true);
```

### 3. Büyük Dosyaları Zarifçe İşleyin

100 MB’den büyük PDF’ler işliyorsanız, belgeyi bir kerede yüklemek yerine sayfaları akış (stream) olarak okuyun:

```java
for (int pageNum = 1; pageNum <= pdfDoc.getPageCount(); pageNum++) {
    OcrPageResult result = ocrEngine.recognizePage(pdfDoc.getPage(pageNum));
    // process result...
}
```

Bu desen bellek kullanımını azaltır ve toplu işler için kullanışlıdır.

### 4. Yapılandırılmış Formatlara Dışa Aktarın

Düz metnin ötesinde, JSON veya XML gibi formatlara dışa aktararak sonraki işlemler için kullanabilirsiniz:

```java
String json = pageResult.toJson();
System.out.println(json);
```

---

## Yaygın Tuzaklar ve Nasıl Kaçınılır

| Pitfall | Why It Happens | Fix |
|---------|----------------|-----|
| **Boş çıktı** | Lisans uygulanmadı veya dosya yolu hatalı. | `setLicense` yolunu doğrulayın ve dosyanın mevcut olduğunu onaylayın. |
| **Bozuk karakterler** | Yanlış dil ayarı veya düşük çözünürlüklü kaynak. | Doğru `Language` ayarını yapın ve kaynak görüntülerin ≥300 dpi olduğundan emin olun. |
| **Bellek dışı hatalar** | Büyük bir PDF’yi bir kerede yüklemek. | Yukarıda gösterilen akış (streaming) yaklaşımını kullanın. |
| **Kısmi sayfa tanıma** | PDF, karışık raster/vektör katmanları içeriyor. | OCR’dan önce PDF’yi düzleştirin: `pdfDoc.flatten();` |

---

## Özet – Neler Kapsandı

* **How to use OCR** Aspose ile Java’da.
* **Extract text from PDF** (veya TIFF) tek bir çağrıyla.
* **Recognize text from PDF** tüm sayfalarda manuel döngü olmadan.
* **Convert PDF to Text** ve temiz bir çıktı.
* **OCR multi page PDF** işlemek için ipuçları, dil ayarları ve bellek‑dostu akış dahil.

Artık herhangi bir Java projesine ekleyebileceğiniz tam, üretim‑hazır bir kod parçacığınız var. Görüntü‑işleme seçeneklerini istediğiniz gibi ayarlayabilir, çıktı hedefini değiştirebilir veya sonucu bir arama indeksine entegre edebilirsiniz.

---

## Sonraki Adımlar

* **Aspose OCR’un ileri özelliklerini keşfedin** – el yazısı tanıma veya PDF/A uyumluluğu gibi.
* **OCR’u PDF manipülasyonu ile birleştirin** (ör. PDF’ye aranabilir bir metin katmanı ekleyerek arama yapılabilir PDF’ler oluşturun).
* **Toplu işleme otomasyonu** – bir klasördeki PDF’leri okuyup her birinin sonucunu karşılık gelen `.txt` dosyasına yazın.

Herhangi bir sorunla karşılaşırsanız, Aspose forumları yardım almak için harika bir yerdir ve API referansı burada kullanılan her metodun ayrıntılı açıklamasını sunar.

Kodlamanın tadını çıkarın ve inatçı taramaları aranabilir metne dönüştürmenin keyfini yaşayın!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}