---
category: general
date: 2026-07-05
description: Java를 사용해 PNG를 PDF로 변환하면서 PDF 이미지 압축하기. OCR을 위한 이미지 전처리를 배우고, JPG 텍스트를
  인식하며, 한 번의 튜토리얼로 배치 OCR을 PDF로 변환합니다.
draft: false
keywords:
- compress pdf images
- convert png to pdf
- image preprocessing for ocr
- recognize text jpg
- batch ocr to pdf
language: ko
og_description: Java를 사용하여 PDF 이미지를 압축하고 PNG를 PDF로 변환합니다. 이 가이드는 OCR을 위한 이미지 전처리,
  JPG 텍스트 인식 및 배치 OCR을 PDF로 변환하는 방법을 다룹니다.
og_title: Java로 PDF 이미지 압축 – 완전한 배치 OCR 튜토리얼
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Compress PDF images while converting PNG to PDF using Java. Learn image
    preprocessing for OCR, recognize text JPG, and batch OCR to PDF in one tutorial.
  headline: Compress PDF Images with Java – Full Batch OCR to PDF Guide
  type: TechArticle
- description: Compress PDF images while converting PNG to PDF using Java. Learn image
    preprocessing for OCR, recognize text JPG, and batch OCR to PDF in one tutorial.
  name: Compress PDF Images with Java – Full Batch OCR to PDF Guide
  steps:
  - name: Expected Output
    text: 'Running the program prints a line for each image, e.g.:'
  - name: What if my server has no GPU?
    text: Just set `gpuSettings.setEnabled(false)`. The rest of the pipeline remains
      unchanged, and you still get multithreaded CPU processing.
  - name: My PDFs are still too large—can I lower the quality further?
    text: Yes. Adjust `options.setImageQuality(70)` or even `50`. Lower values shrink
      size more aggressively but may blur fine glyphs. Test with a representative
      sample.
  - name: How do I handle other image formats (TIFF, BMP)?
    text: 'Add the extensions to the filter lambda:'
  - name: Can I keep the original color images instead of binarizing?
    text: Replace `.addBinarize()` with `.addGrayscale()` in the preprocessor builder
      if you need color retention for downstream analysis.
  type: HowTo
tags:
- ocr
- java
- pdf
- image-processing
title: Java로 PDF 이미지 압축 – 전체 배치 OCR을 PDF로 변환하는 가이드
url: /ko/java/advanced-ocr-techniques/compress-pdf-images-with-java-full-batch-ocr-to-pdf-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java로 PDF 이미지 압축 – 전체 배치 OCR to PDF 가이드

Ever needed to **PDF 이미지 압축** while turning a folder of PNGs into searchable PDFs? You’re not the only one. In many automation pipelines the biggest pain point is juggling image quality, OCR accuracy, and final PDF size—all at once.  

In this tutorial we’ll walk through a practical solution that **PNG를 PDF로 변환**, applies **OCR용 이미지 전처리**, and finally **PDF 이미지 압축** so the output stays lightweight. By the end you’ll know how to **텍스트 JPG 인식** files, set up a **배치 OCR to PDF** workflow, and keep your PDFs tidy.

## 배워게 될 내용

- Aspose OCR for Java 설정 및 라이선스 적용.
- 멀티스레딩, GPU 가속 및 맞춤법 교정을 위한 엔진 구성.
- 재사용 가능한 **OCR용 이미지 전처리** pipeline (denoise, contrast, binarize).
- **PdfSaveOptions**를 사용하여 가독성을 손상시키지 않으면서 **PDF 이미지 압축**.
- 디렉터리를 순회하며 **PNG를 PDF로 변환** 및 **텍스트 JPG 인식**을 일괄 처리.
- 어떤 프로젝트에도 삽입할 수 있는 완전한, 바로 실행 가능한 Java 프로그램.

> **Prerequisites**: Java 8+, Maven 또는 Gradle, Aspose OCR for Java 라이선스, 그리고 처리하려는 PNG/JPG 이미지 폴더.

---

## Step 1: Aspose OCR 라이선스 적용 (프로덕션에 필수)

Before you can call any OCR APIs you must load a valid license; otherwise you’ll be stuck with trial limitations.

```java
import com.aspose.ocr.*;

public class LicenseSetup {
    public static void loadLicense() throws Exception {
        License license = new License();
        // Point to your license file – keep it out of source control!
        license.setLicense("Aspose.OCR.Java.lic");
    }
}
```

*Why this matters*: 라이선스가 적용된 엔진은 GPU 지원, 높은 정확도, 그리고 PDF 파일을 부풀게 하는 워터마크를 제거합니다.

---

## Step 2: OCR 엔진 구성 – Threads, GPU, and Spell Correction

A fast OCR engine is the backbone of any **배치 OCR to PDF** job. We’ll spin up as many threads as the host CPU can handle, enable GPU acceleration (if you have a compatible card), and tighten spell correction to clean up OCR errors.

```java
import com.aspose.ocr.*;
import com.aspose.ocr.gpu.GPUSettings;
import com.aspose.ocr.spell.SpellCorrectionOptions;

public class EngineConfig {
    public static OcrEngine createEngine() {
        OcrEngine ocrEngine = new OcrEngine();

        // Use all available logical processors
        ocrEngine.setThreadCount(Runtime.getRuntime().availableProcessors());

        // Enable GPU – huge speedup for large batches
        GPUSettings gpu = new GPUSettings();
        gpu.setEnabled(true);
        ocrEngine.setGpuSettings(gpu);

        // Light spell correction: fix common typos without over‑correcting
        SpellCorrectionOptions spellOpts = new SpellCorrectionOptions();
        spellOpts.setMaxEditDistance(1);
        ocrEngine.getSpellCorrection().setOptions(spellOpts);

        return ocrEngine;
    }
}
```

*Pro tip*: GPU가 없는 헤드리스 서버에서 실행 중이라면 `gpu.setEnabled(false)`만 설정하면 됩니다 – 코드는 여전히 동작하지만 약간 느려집니다.

---

## Step 3: 이미지 전처리 파이프라인 구축

Raw scans often suffer from noise, low contrast, or uneven lighting. **OCR용 이미지 전처리** dramatically improves recognition rates, especially for **텍스트 JPG 인식** scenarios.

```java
import com.aspose.ocr.*;

public class PreprocessorSetup {
    public static ImagePreprocessor createPreprocessor() {
        return new ImagePreprocessor.Builder()
                .addDenoise(0.7)      // Reduce grain while preserving edges
                .addContrast(1.15)    // Boost contrast for clearer glyphs
                .addBinarize()        // Convert to black‑and‑white for OCR
                .build();
    }
}
```

*Why we chain these*: 먼저 노이즈 제거를 하면 이진화 단계에서 잡음이 확대되는 것을 방지합니다; 그 다음 대비를 조정하여 문자들이 돋보이게 하고; 마지막으로 이진화를 통해 OCR 엔진이 깨끗한 이진 이미지를 사용하도록 합니다.

---

## Step 4: PDF 저장 옵션 준비 – **PDF 이미지 압축** Efficiently

Aspose lets you fine‑tune the PDF output. We’ll turn on image compression and set a quality level that balances size and legibility.

```java
import com.aspose.ocr.pdf.PdfSaveOptions;

public class PdfOptions {
    public static PdfSaveOptions createOptions() {
        PdfSaveOptions options = new PdfSaveOptions();
        options.setCompressImages(true);   // This is the key to compress PDF images
        options.setImageQuality(90);       // 90% retains sharp text while shrinking file size
        return options;
    }
}
```

*Result*: 각 검색 가능한 PDF는 눈에 띄게 작아집니다—아카이브하거나 이메일로 전송하기에 이상적입니다.

---

## Step 5: 폴더 처리 – **PNG를 PDF로 변환** 및 **텍스트 JPG 인식**을 한 루프에서 수행

Now we bring everything together. The loop walks through an input directory, runs OCR on each PNG or JPG, and writes a searchable PDF to an output folder. The PDF name mirrors the source image name.

```java
import com.aspose.ocr.*;
import com.aspose.ocr.pdf.PdfSaveOptions;
import java.io.File;

public class BatchOcrTutorial {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load license
        LicenseSetup.loadLicense();

        // 2️⃣ Engine & preprocessing
        OcrEngine ocrEngine = EngineConfig.createEngine();
        ocrEngine.setPreprocessor(PreprocessorSetup.createPreprocessor());

        // 3️⃣ PDF options (compress PDF images)
        PdfSaveOptions pdfOptions = PdfOptions.createOptions();

        // 4️⃣ Define input / output folders
        File inputFolder = new File("YOUR_DIRECTORY/input");
        File outputFolder = new File("YOUR_DIRECTORY/output");
        if (!outputFolder.exists()) outputFolder.mkdirs();

        // 5️⃣ Filter PNG & JPG files
        File[] imageFiles = inputFolder.listFiles((dir, name) ->
                name.toLowerCase().endsWith(".png") || name.toLowerCase().endsWith(".jpg"));

        if (imageFiles == null || imageFiles.length == 0) {
            System.out.println("No PNG or JPG files found in the input folder.");
            return;
        }

        // 6️⃣ Process each file
        for (File image : imageFiles) {
            // Recognize text – works for both PNG and JPG
            ocrEngine.recognizeImage(image.getAbsolutePath());

            // Build output PDF path (same base name)
            String pdfPath = outputFolder.getAbsolutePath() + File.separator +
                    image.getName().replaceAll("\\.(png|jpg)$", ".pdf");

            // Save as searchable PDF – this step also compresses images
            ocrEngine.saveAsSearchablePdf(pdfPath, pdfOptions);

            System.out.println("✅ Processed: " + image.getName() + " → " + pdfPath);
        }

        System.out.println("🎉 All files have been converted and compressed!");
    }
}
```

### 예상 출력

Running the program prints a line for each image, e.g.:

```
✅ Processed: invoice1.png → /output/invoice1.pdf
✅ Processed: receipt23.jpg → /output/receipt23.pdf
🎉 All files have been converted and compressed!
```

Open any resulting PDF in a viewer and you’ll see selectable, searchable text while the file size is typically **30‑50 % smaller** than a non‑compressed counterpart.

---

## 자주 묻는 질문 및 엣지 케이스

### 서버에 GPU가 없으면 어떻게 하나요?
Just set `gpuSettings.setEnabled(false)`. The rest of the pipeline remains unchanged, and you still get multithreaded CPU processing.

### PDF가 아직도 너무 크다면 품질을 더 낮출 수 있나요?
Yes. Adjust `options.setImageQuality(70)` or even `50`. Lower values shrink size more aggressively but may blur fine glyphs. Test with a representative sample.

### 다른 이미지 포맷(TIFF, BMP)은 어떻게 처리하나요?
Add the extensions to the filter lambda:

```java
name.toLowerCase().endsWith(".png") ||
name.toLowerCase().endsWith(".jpg") ||
name.toLowerCase().endsWith(".tif") ||
name.toLowerCase().endsWith(".bmp")
```

The same preprocessing pipeline works for most raster formats.

### 이진화 대신 원본 컬러 이미지를 유지할 수 있나요?
Replace `.addBinarize()` with `.addGrayscale()` in the preprocessor builder if you need color retention for downstream analysis.

---

## 프로덕션 수준 배치 OCR을 위한 팁

- **Memory management**: `OcrEngine` 인스턴스를 하나만 재사용(예시와 같이)하여 이미지당 객체 생성/소멸 오버헤드를 피합니다.
- **Error handling**: 파일당 블록을 `try/catch`로 감싸서 배치를 중단하지 않고 실패를 로그합니다.
- **Logging**: 확장 가능한 솔루션을 위해 `System.out.println` 대신 적절한 로깅 프레임워크(SLF4J, Log4j)를 사용합니다.
- **Parallelism**: 대용량 폴더의 경우 서브 디렉터리를 병렬 스트림으로 처리하는 것을 고려하되, GPU 경쟁 상황을 주시하세요.
- **Security**: 라이선스 파일을 저장소 외부에 보관하고 파일 시스템 권한으로 보호합니다.

---

## 결론

We’ve just demonstrated how to **PDF 이미지 압축** while performing a **배치 OCR to PDF** conversion that **PNG를 PDF로 변환**, **텍스트 JPG 인식**, and applies a robust **OCR용 이미지 전처리** pipeline. The full Java program is self‑contained, runs on any modern JDK, and produces lightweight searchable PDFs ready for archiving or downstream analysis.

Next steps? Experiment with different pre‑processing parameters, try out OCR languages other than English, or integrate the workflow into a Spring Boot microservice that watches a directory and processes files on the fly. The core concepts—license loading, engine configuration, preprocessing, and PDF compression—stay the same, giving you a solid foundation for any OCR‑driven project.

Got questions or want to share your own tweaks? Drop a comment below, and happy coding!

![배치 OCR 워크플로우 다이어그램: 입력 이미지, 전처리, OCR 엔진 및 압축된 PDF 출력](alt="Diagram of batch OCR workflow showing input images, preprocessing, OCR engine, and compressed PDF output")


## 다음에 배워야 할 내용은?

The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [PDF 텍스트 인식 – Aspose.OCR for Java OCR 작업](/ocr/english/java/ocr-operations/)
- [텍스트 이미지 인식 with Aspose OCR – 전체 Java OCR 튜토리얼](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [Java에서 Aspose.OCR BufferedImage를 사용해 이미지 텍스트 변환](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}