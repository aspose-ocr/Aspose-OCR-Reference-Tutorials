---
category: general
date: 2026-02-14
description: 使用 Aspose OCR 在 Java 中從圖像提取文字。了解如何從表單欄位中提取文字，並使用感興趣區域以獲得精確結果。
draft: false
keywords:
- extract text from image
- extract text from form
language: zh-hant
og_description: 使用 Aspose OCR 在 Java 中從圖像提取文字。本教學示範如何透過感興趣區域從表單欄位提取文字。
og_title: 使用 Aspose OCR 從圖像中提取文字 – Java 指南
tags:
- OCR
- Java
- Aspose
- Image Processing
title: 使用 Aspose OCR 從圖像提取文字 – Java 指南
url: /zh-hant/java/advanced-ocr-techniques/extract-text-from-image-with-aspose-ocr-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose OCR 從影像擷取文字 – Java 教學

是否曾經需要 **從影像擷取文字**，卻因為必須解析整張圖片而浪費 CPU，且結果雜訊太多？你並不孤單。在許多實務應用——例如發票掃描器、護照讀取器或資料輸入表單——中，我們只關心少數欄位，而不是整個畫布。

好消息是 Aspose OCR 讓你 **從影像擷取文字**，同時也能透過定義多邊形只擷取特定表單區域。在本教學中，你將看到如何使用 Java **從表單擷取文字**，了解此方法的重要性，以及當出現問題時該如何調整。

以下內容將從設定函式庫到處理棘手的邊緣案例全部說明，最後你會得到一段可直接執行的程式碼，僅抓取你需要的資料。

## 需要的環境

- Java 17（或任何較新的 JDK）——較新版本對 Unicode 支援較佳。  
- Aspose.OCR for Java 23.10（或閱讀時的最新版本）。  
- 一張名為 `form.png`、具備明確欄位的範例影像。  
- IDE 或簡易文字編輯器——IntelliJ IDEA、VS Code，甚至 Notepad 都可。

核心示範不需要 Maven/Gradle，只要把 Aspose OCR JAR 加入 classpath 即可。

---

## 步驟 1 – 初始化 OCR 引擎並載入影像

引擎首先需要一張位圖來處理。我們會指向與原始檔案同一資料夾下的 `form.png`。

```java
import com.aspose.ocr.*;
import java.awt.Polygon;
import java.util.*;

public class MultiRoiDemo {
    public static void main(String[] args) throws Exception {

        // Create the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Load the source image – replace the path if your file lives elsewhere
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/form.png"));
```

*為什麼這很重要：*  
建立全新的 `OcrEngine` 可確保環境乾淨，避免舊設定影響本次執行。提前載入影像也會驗證檔案是否存在，讓你在後續步驟前就收到有用的例外訊息。

> **小技巧：** 若影像過大（超過 5 MB），建議先縮小。Aspose OCR 在任一維度低於 2000 px 時效能較佳。

---

## 步驟 2 – 為欲讀取的欄位定義多邊形

*感興趣區域*（ROI）就是告訴引擎要看哪裡的多邊形。以下範例建立兩個矩形——一個對應「First Name」，另一個對應「Date of Birth」。請自行調整座標以符合你的表單。

```java
        // Polygon for the first field (e.g., First Name)
        Polygon firstField = new Polygon(
                new int[]{50, 200, 200, 50},   // X‑coordinates
                new int[]{100, 100, 150, 150}, // Y‑coordinates
                4);

        // Polygon for the second field (e.g., Date of Birth)
        Polygon secondField = new Polygon(
                new int[]{300, 500, 500, 300},
                new int[]{200, 200, 250, 250},
                4);
```

*為什麼使用多邊形而非矩形？*  
多邊形能彈性處理傾斜或非矩形的框框——這在掃描未完全對齊的印刷表單時相當常見。

---

## 步驟 3 – 告訴 Aspose OCR 只聚焦於這些區域

現在把多邊形綁定到引擎。`setRegionsOfInterest` 方法接受一個列表，因而可以加入任意多的欄位。

```java
        // Limit OCR to the defined regions
        ocrEngine.getEngineOptions()
                 .setRegionsOfInterest(Arrays.asList(firstField, secondField));
```

*底層發生了什麼？*  
Aspose OCR 會將每個多邊形裁切成獨立的位圖，執行辨識演算法，最後再把結果合併。這大幅降低了來自周圍圖形的誤判。

---

## 步驟 4 – 執行 OCR 程序

所有設定完成後，我們呼叫 OCR。`process()` 會回傳一個 `OcrResult` 物件，內含擷取的文字與信心分數。

```java
        // Execute OCR on the selected ROIs
        OcrResult ocrResult = ocrEngine.process();
```

若需要每個欄位的信心分數，可檢查 `ocrResult.getRegions()`——每個區域都有自己的分數。對於大多數簡單表單，整體文字已足夠。

---

## 步驟 5 – 顯示（或儲存）擷取的文字

最後，我們把結果印到主控台。實務上你可能會寫入資料庫、JSON 檔，或透過 API 送出。

```java
        // Output the extracted text
        System.out.println("=== Extracted Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

**預期輸出（範例）：**

```
=== Extracted Text ===
John Doe
12/04/1990
```

這兩行分別對應我們先前定義的兩個多邊形。若出現多餘空白，可使用 `String.trim()` 進行去除。

---

## 大量欄位時的表單文字擷取方式

當表單包含數十個輸入欄位時，手動輸入座標相當繁瑣。以下是一個快速的模式：

1. **建立 CSV**，每列包含 `fieldName, x1, y1, x2, y2, x3, y3, x4, y4`。  
2. **在執行時載入 CSV**，逐行迴圈建立 `Polygon`，並加入 ROI 清單。  

```java
List<Polygon> rois = new ArrayList<>();
try (BufferedReader br = new BufferedReader(new FileReader("fields.csv"))) {
    String line;
    while ((line = br.readLine()) != null) {
        String[] parts = line.split(",");
        int[] xs = { Integer.parseInt(parts[1]), Integer.parseInt(parts[3]),
                    Integer.parseInt(parts[5]), Integer.parseInt(parts[7]) };
        int[] ys = { Integer.parseInt(parts[2]), Integer.parseInt(parts[4]),
                    Integer.parseInt(parts[6]), Integer.parseInt(parts[8]) };
        rois.add(new Polygon(xs, ys, 4));
    }
}
ocrEngine.getEngineOptions().setRegionsOfInterest(rois);
```

*為什麼要這樣做？*  
自動產生 ROI 讓同一段 Java 程式碼可重複使用於多種表單版型，保持專案 DRY（Don’t Repeat Yourself）。

---

## 邊緣案例與小技巧

- **旋轉的掃描檔：** 若整張影像被旋轉，可呼叫 `ocrEngine.getEngineOptions().setRotateAngle(degrees)`。  
- **低對比度：** 設定 `ocrEngine.getEngineOptions().setContrast(1.5f)` 以提升可讀性。  
- **非拉丁文字：** 使用 `ocrEngine.getEngineOptions().setLanguage(OcrLanguage.Spanish)`（或任何支援的語言）切換語言。  
- **部分 OCR 失敗：** 必須檢查 `ocrResult.getConfidence()`；若低於 80 %，建議提示使用者手動驗證。  

---

## 完整可執行範例（直接複製貼上）

以下程式碼即為完整範例，可直接編譯執行。將 `YOUR_DIRECTORY` 替換為放置 `form.png` 的資料夾路徑。

```java
import com.aspose.ocr.*;
import java.awt.Polygon;
import java.util.*;

public class MultiRoiDemo {
    public static void main(String[] args) throws Exception {

        // Step 1 – Initialize engine and load image
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/form.png"));

        // Step 2 – Define polygons for each form field
        Polygon firstField = new Polygon(
                new int[]{50, 200, 200, 50},
                new int[]{100, 100, 150, 150},
                4);
        Polygon secondField = new Polygon(
                new int[]{300, 500, 500, 300},
                new int[]{200, 200, 250, 250},
                4);

        // Step 3 – Limit OCR to those regions
        ocrEngine.getEngineOptions()
                 .setRegionsOfInterest(Arrays.asList(firstField, secondField));

        // Step 4 – Run OCR
        OcrResult ocrResult = ocrEngine.process();

        // Step 5 – Show the result
        System.out.println("=== Extracted Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

編譯指令：

```bash
javac -cp "aspose-ocr-23.10.jar" MultiRoiDemo.java
java -cp ".:aspose-ocr-23.10.jar" MultiRoiDemo
```

執行後，你應該會看到屬於定義 ROI 的兩行文字。

---

## 常見問題

**Q: 這能直接處理 PDF 嗎？**  
A: 不能直接。請先將每頁 PDF 轉成影像（例如使用 Aspose PDF），再交給 OCR 引擎。

**Q: 表單裡有核取方塊怎麼辦？**  
A: OCR 無法直接讀取布林值，但你可以把核取方塊區域當作 ROI，檢查像素密度以推斷是否被勾選。

**Q: 能一次擷取多頁表單的文字嗎？**  
A: 可以，對每頁影像迴圈使用相同的 ROI 清單，然後把結果串接起來。

---

## 結論

我們已完整示範如何使用 Aspose OCR **從影像擷取文字**，並說明同樣的技巧如何 **從表單擷取文字**，達到精準定位。透過定義多邊形、限制引擎焦點、以及處理常見陷阱，你可以快速取得乾淨的資料，且不必處理整張圖片的負擔。

準備好進一步了嗎？試著把 OCR 結果串成 JSON，或送入機器學習模型做驗證。只要你想得到，天空才是極限，而現在你已經掌握了關鍵。

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}