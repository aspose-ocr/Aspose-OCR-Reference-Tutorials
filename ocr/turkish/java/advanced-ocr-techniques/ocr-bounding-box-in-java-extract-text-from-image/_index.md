---
category: general
date: 2026-06-16
description: Java'da OCR sınırlama kutusu öğreticisi, görüntüden metin nasıl çıkarılacağını,
  görüntüden metin nasıl okunacağını ve JPG dosyaları için OCR güven skorunun nasıl
  alınacağını gösterir.
draft: false
keywords:
- ocr bounding box
- extract text from image
- ocr confidence score
- recognize text from jpg
- read text from image
language: tr
og_description: Java'da OCR sınırlama kutusu, JPG dosyalarından metin tanımanıza,
  görüntüden metin çıkarmanıza ve OCR güven puanlarını görüntülemenize olanak tanır—hepsi
  basit bir kod örneğinde.
og_title: Java'da OCR Sınır Kutusu – Görüntüden Metin Çıkar
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: OCR bounding box tutorial in Java shows how to extract text from image,
    read text from image, and get OCR confidence score for JPG files.
  headline: OCR Bounding Box in Java – Extract Text from Image
  type: TechArticle
tags:
- OCR
- Java
- image-processing
- text-recognition
title: Java'da OCR Sınır Kutusu – Görüntüden Metin Çıkarma
url: /tr/java/advanced-ocr-techniques/ocr-bounding-box-in-java-extract-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java’da OCR Sınırlama Kutusu – Görüntüden Metin Çıkarma

Her zaman bir Java görüntüsündeki her metin parçası için **ocr bounding box** nasıl alınır merak ettiniz mi? Bu öğreticide **görüntüden metin çıkarma**, **görüntüden metin okuma** ve **jpg dosyalarından metin tanıma** sırasında **ocr confidence score** nasıl görüntülenir göstereceğiz. Kısa cevap? Modern bir OCR kütüphanesiyle birkaç satır kod ve her çağrının neden önemli olduğuna dair bir açıklama.

Aşağıda tamamen çalıştırılabilir bir örnek, adım adım açıklama ve doğrudan projenize kopyalayabileceğiniz birkaç pratik ipucu bulacaksınız. Sonunda şu şekilde bir çıktı elde edebileceksiniz:

```
Text: "Hello World"  Confidence: 0.97  Box: (x=12, y=45, width=210, height=30)
```

## Gerekenler

- **Java 11** veya daha yeni (aşağıdaki sözdizimi kısalık için `var` anahtar kelimesini kullanıyor, eski JDK’larda bunu kaldırabilirsiniz).  
- Java API sağlayan bir OCR kütüphanesi – bu rehberde popüler Tesseract motorunun ince bir sarmalayıcısı olan **[Tesseract4J](https://github.com/nguyenq/tess4j)** kullanacağız.  
- Açık, basılı metin içeren bir JPEG görüntüsü (`.jpg`).  
- Sevdiğiniz IDE (IntelliJ IDEA, Eclipse, VS Code…) – herhangi biri yeterli.

Kütüphaneyi eksik ise, şu Maven bağımlılığını ekleyin:

```xml
<dependency>
    <groupId>net.sourceforge.tess4j</groupId>
    <artifactId>tess4j</artifactId>
    <version>5.4.0</version>
</dependency>
```

Şimdi başlayalım.

![OCR sınırlama kutusu örneği](ocr-bounding-box.png "OCR sınırlama kutusu örneği")

## OCR Sınırlama Kutusu: Motoru Kurma

İlk yapmanız gereken bir OCR motoru örneği oluşturmak. Bunu, daha sonra pikselleri okuyacak tarayıcıyı açmak gibi düşünün.

```java
import net.sourceforge.tess4j.ITesseract;
import net.sourceforge.tess4j.Tesseract;
import net.sourceforge.tess4j.TesseractException;

ITesseract ocrEngine = new Tesseract();          // Step 1 – create the OCR engine
ocrEngine.setDatapath("tessdata");               // point to the language data files
ocrEngine.setLanguage("eng");                    // we’ll work with English for now
```

**Neden önemli:**  
`datapath` ayarlanmadan Tesseract dil paketlerinin nerede olduğunu bilemez ve “Failed loading language” gibi belirsiz bir hata alırsınız. `setLanguage` çağrısı yalnızca varsayılan İngilizce pakete ihtiyacınız varsa opsiyoneldir, ancak açık olmak gelecekteki okuyucular için kodu daha anlaşılır kılar.

## İşlemek İstediğiniz Görüntüyü Yükleyin

Sonra motoru analiz etmesini istediğiniz JPEG’i verin. Kütüphane bir `File` veya `BufferedImage` kabul eder; basitlik açısından `File` kullanacağız.

```java
import java.io.File;

File imageFile = new File("YOUR_DIRECTORY/text_page.jpg");   // Step 2 – load the image
```

**Pro ipucu:**  
Görseliniz kaynaklarda (ör. bir JAR içinde) bulunuyorsa, `getResourceAsStream` kullanıp `ImageIO.read` ile sarmalayın. Böylece öğretici hem yerel hem de paketlenmiş bir uygulamada çalışır.

## OCR Tanıma İşlemini Gerçekleştirin

Şimdi motoru resmi okumaya zorlayacağız. Sonuç düz metin dizgesi, ancak aynı zamanda **ocr confidence score** ve **ocr bounding box** da istiyoruz.

```java
try {
    // Step 3 – run OCR and get a result object with layout data
    var result = ocrEngine.doOCR(imageFile, null);
    // The simple doOCR call returns only text; to get boxes we need the
    // getWords method with a specific page iterator level.
    var words = ocrEngine.getWords(imageFile, ITesseract.PageIteratorLevel.RIL_WORD);
    
    // Step 4 – iterate over each detected word
    for (var word : words) {
        System.out.printf(
            "Text: \"%s\"  Confidence: %.2f  Box: %s%n",
            word.getText(),
            word.getConfidence(),
            word.getBoundingBox().toString()
        );
    }
} catch (TesseractException e) {
    System.err.println("OCR failed: " + e.getMessage());
}
```

**Neden `doOCR` yerine `getWords` kullanıyoruz:**  
`doOCR` ham dizgeyi verir ancak mekânsal bilgiyi atar. `RIL_WORD` (veya satır‑seviyesi kutular için `RIL_TEXTLINE`) ile `getWords` çağırarak her biri metin, güven skoru ve sınırlama dikdörtgeni taşıyan bir `Word` nesnesi listesi alırız. Bu, **ocr bounding box** özelliğinin kalbidir.

## Çıktıyı Anlamak

Yukarıdaki kodu temiz bir JPEG’e uyguladığınızda aşağıdaki gibi bir çıktı alırsınız:

```
Text: "Hello"  Confidence: 0.99  Box: java.awt.Rectangle[x=34,y=12,width=112,height=28]
Text: "World"  Confidence: 0.97  Box: java.awt.Rectangle[x=156,y=12,width=98,height=28]
```

- **Text** – tanınan karakterler.  
- **Confidence** – 0 ile 1 arasında bir kayan nokta değeri; yüksek olması motorun daha emin olduğunu gösterir.  
- **Box** – kelimeyi piksel koordinatları (x, y, genişlik, yükseklik) ile çevreleyen dikdörtgen.

Artık **görüntüden metin okuma** yapabilir ve her parçanın tuval üzerindeki tam konumunu bilebilirsiniz—vurgulama, kırpma veya sonraki NLP boru hatlarına besleme için mükemmel.

## Kenar Durumları & Yaygın Tuzaklar

| Durum | Dikkat Edilmesi Gereken | Çözüm / Çalışma Yöntemi |
|-----------|-------------------|-------------------|
| Görüntü bulanık veya düşük kontrastlı | Güven skorları dramatik şekilde düşer (çoğu zaman 0.6’nın altına). | OpenCV ile ön‑işleme: kontrastı artırın, eşikleme uygulayın. |
| JPEG döndürülmüş metin içeriyor | Sınırlama kutuları eğik veya eksik görünür. | `ocrEngine.setPageSegMode(ITesseract.PageSegMode.PSM_AUTO_OSD)` kullanarak Tesseract’in yönü otomatik algılamasını sağlayın. |
| Büyük görüntüler OutOfMemoryError’a neden oluyor | Java yığını büyük resimleri yüklerken dolar. | OCR’den önce görüntüyü küçültün (`ImageIO.read` → `BufferedImage.getScaledInstance`). |
| Kelime‑seviyesi yerine satır‑seviyesi kutulara ihtiyacınız var | `RIL_WORD` kelime bazlı kutular döndürür. | `ITesseract.PageIteratorLevel.RIL_TEXTLINE`’a geçin. |
| İngilizce dışı karakterler � olarak görünüyor | Dil verileri yüklenmemiş. | Uygun `.traineddata` dosyasını indirin ve `setDatapath`’i bu klasöre yönlendirin. |

Bu sorunları erken ele almak, ileride saatler süren hata ayıklamayı önler.

## Tam Çalışan Örnek (Tüm Adımlar Tek Dosyada)

Aşağıda `src/main/java` klasörüne kopyalayıp `mvn exec:java` ile çalıştırabileceğiniz, tüm tartıştıklarımızı bir araya getiren bağımsız bir Java sınıfı bulunuyor.

```java
package com.example.ocrdemo;

import net.sourceforge.tess4j.ITesseract;
import net.sourceforge.tess4j.ITesseract.RenderedFormat;
import net.sourceforge.tess4j.Tesseract;
import net.sourceforge.tess4j.TesseractException;
import net.sourceforge.tess4j.Word;

import java.io.File;
import java.util.List;

public class OcrBoundingBoxDemo {

    public static void main(String[] args) {
        // ==== Step 1: Initialize the OCR engine ====
        ITesseract ocrEngine = new Tesseract();
        ocrEngine.setDatapath("tessdata"); // folder containing .traineddata files
        ocrEngine.setLanguage("eng");      // English language pack

        // Optional: improve accuracy for printed text
        ocrEngine.setPageSegMode(ITesseract.PageSegMode.PSM_AUTO);
        ocrEngine.setOcrEngineMode(ITesseract.OEM_TESSERACT_ONLY);

        // ==== Step 2: Load the JPEG you want to read ====
        File imageFile = new File("YOUR_DIRECTORY


## Sonraki Öğrenmeniz Gerekenler


Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanarak yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini ustalaşmanız ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmeniz için adım adım açıklamalar içeren tam çalışan kod örnekleri sunar.

- [Extract Text from Image Java with Aspose.OCR Detect Areas Mode](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [Extract Text Images – OCR Basics with Aspose.OCR for Java](/ocr/english/java/ocr-basics/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}