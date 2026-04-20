---
category: general
date: 2026-02-17
description: 圖像轉文字 Java 教學：學習如何使用 Aspose OCR 從圖像中提取烏爾都文字。附帶完整的 Java OCR 範例。
draft: false
keywords:
- image to text java
- how to extract text
- extract urdu text
- java ocr example
- load image ocr
language: zh-hant
og_description: 圖像轉文字 Java 教程展示如何使用 Aspose OCR 從圖像中提取烏爾都文。請按照完整的 Java OCR 範例逐步操作。
og_title: 圖像轉文字 Java：使用 Aspose OCR 提取烏爾都文
tags:
- OCR
- Java
- Aspose
title: 圖像轉文字 Java：使用 Aspose OCR 提取烏爾都文
url: /zh-hant/java/ocr-operations/image-to-text-java-extract-urdu-text-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# image to text java：使用 Aspose OCR 提取烏爾都文字

如果你需要將烏爾都文文件進行 **image to text java** 轉換，你來對地方了。是否曾好奇過 *如何從手寫筆記或掃描的報紙頁面圖片中提取文字*？本指南將帶你一步步完成一個 **java ocr example**，使用 Aspose OCR 從圖片中直接提取烏爾都字符。

我們將從授權庫到在主控台列印結果全部說明。完成後，你將能夠 **load image ocr** 檔案、將語言設定為 Urdu，並取得乾淨的 Unicode 輸出——不需要額外工具。

## 需要的條件

- **Java Development Kit (JDK) 8+** – 此程式碼可在任何較新的 JDK 上執行。  
- **Aspose.OCR for Java** JAR（從 Aspose 官方網站下載）。  
- 有效的 **Aspose OCR license** 檔案 (`Aspose.OCR.lic`)。  
- 包含烏爾都文字的圖片，例如 `urdu-sample.png`。  

具備以上基礎後，你就可以直接進入程式碼，無需再搜尋缺少的相依套件。

## image to text java – 設定 Aspose OCR

首先，我們需要告訴 Aspose 我們已有授權。若未設定授權，函式庫會以評估模式執行，並在輸出中加入浮水印。

```java
import com.aspose.ocr.*;

public class UrduDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Apply the Aspose OCR license
        License license = new License();
        license.setLicense("Aspose.OCR.lic");
```

**Why this matters:** 授權會移除 5 秒的處理限制，並解鎖 2025‑Q3 新增的完整 Urdu 語言套件。若跳過此步驟，OCR 引擎仍能運作，但結果中會出現微小的「Evaluation」標記。

## How to Extract Text – Initialize the OCR Engine

現在我們建立引擎，並明確告訴它我們要處理 Urdu。`OcrLanguage.URDU` 常數會啟用正確的字元集與分割規則。

```java
        // Step 2: Create the OCR engine and set the language to Urdu
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.getLanguage().setLanguage(OcrLanguage.URDU); // added in 2025‑Q3
```

**Pro tip:** 若需要在一次執行中處理多種語言，可傳入以逗號分隔的清單，例如 `OcrLanguage.ENGLISH, OcrLanguage.URDU`。引擎會自動偵測每個區域的語言。

## Load Image OCR – Preparing the Input

Aspose 使用 `OcrInput` 物件來保存一張或多張圖片。此處我們 **load image ocr** 資料自本機檔案。

```java
        // Step 3: Load the image that contains Urdu text
        OcrInput ocrInput = new OcrInput();
        ocrInput.add("YOUR_DIRECTORY/urdu-sample.png");
```

> **Note:** Replace `YOUR_DIRECTORY` with the absolute path or a relative path from your project root. If the file isn’t found, Aspose throws a `FileNotFoundException`. A quick check with `new File(path).exists()` can save you a lot of debugging time.

## Recognize the Text – Running the OCR Process

在引擎配置完成且圖片載入後，我們最終呼叫 `recognize`。此方法會回傳包含擷取字串的 `OcrResult`。

```java
        // Step 4: Recognize the text from the image
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);
```

**What’s happening under the hood?** OCR 引擎會先將圖片切割成行，再切割成字元，並套用 Urdu 專屬的形狀規則（如連字形）。因此提前設定語言相當重要，否則會得到亂碼的拉丁字元佔位符。

## Print the Recognized Urdu Text

最後一步只需要將結果印出。因為 Urdu 採用從右至左的書寫方向，請確保你的主控台支援 Unicode（大多數現代終端機皆支援）。

```java
        // Step 5: Print the recognized Urdu text
        System.out.println("Urdu text:\n" + ocrResult.getText());
    }
}
```

**Expected output (example):**

```
Urdu text:
یہ ایک مثال کا متن ہے جو تصویر سے نکالا گیا ہے۔
```

如果看到問號或空字串，請再次確認主控台編碼已設定為 UTF‑8（Windows 上使用 `chcp 65001`，或以 `-Dfile.encoding=UTF-8` 參數執行 Java）。

## Full Working Example – All Steps in One Place

以下是完整、可直接複製貼上的程式。沒有外部參考，只需單一 Java 檔案。

```java
import com.aspose.ocr.*;

public class UrduDemo {
    public static void main(String[] args) throws Exception {
        // Apply the Aspose OCR license
        License license = new License();
        license.setLicense("Aspose.OCR.lic");

        // Create the OCR engine and set the language to Urdu
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.getLanguage().setLanguage(OcrLanguage.URDU); // added in 2025‑Q3

        // Load the image that contains Urdu text
        OcrInput ocrInput = new OcrInput();
        ocrInput.add("YOUR_DIRECTORY/urdu-sample.png");

        // Recognize the text from the image
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);

        // Print the recognized Urdu text
        System.out.println("Urdu text:\n" + ocrResult.getText());
    }
}
```

Run it with:

```bash
javac -cp "aspose-ocr-23.10.jar" UrduDemo.java
java -cp ".:aspose-ocr-23.10.jar" UrduDemo
```

將 JAR 版本（`23.10`）換成你下載的版本即可。執行後，主控台應顯示從 PNG 中擷取出的 Urdu 句子。

## Common Pitfalls & Edge Cases

| 問題 | 發生原因 | 解決方法 |
|------|----------|----------|
| **Empty output** | 圖片過暗或解析度太低。 | 在送入 Aspose 前使用 `BufferedImage` 進行前處理（提升對比、二值化）。 |
| **Garbage characters** | 語言設定錯誤（預設為 English）。 | 確保在 `recognize` 之前呼叫 `ocrEngine.getLanguage().setLanguage(OcrLanguage.URDU);`。 |
| **License not found** | 路徑拼寫錯誤或檔案遺失。 | 使用絕對路徑，或將 `.lic` 檔放入 classpath，並呼叫 `license.setLicense("Aspose.OCR.lic");`。 |
| **Out‑of‑memory on large images** | 大型 PNG 佔用過多記憶體。 | 呼叫 `ocrEngine.setMaxImageSize(2000);` 讓引擎內部縮小，或自行調整圖片大小。 |

## Extending the Demo

- **Batch processing:** 迴圈遍歷資料夾，將每個檔案加入同一個 `OcrInput`，並將結果匯出為 CSV。  
- **Different languages:** 將 `OcrLanguage.URDU` 換成 `OcrLanguage.ARABIC`，或同時加入多種語言。  
- **Saving to file:** 使用 `Files.write(Paths.get("output.txt"), ocrResult.getText().getBytes(StandardCharsets.UTF_8));` 將結果寫入檔案。  

所有這些想法皆基於我們剛完成的 **java ocr example**，讓你能依實際專案需求客製化解決方案。

## Conclusion

你現在已擁有一套完整的 **image to text java** 工作流程，能使用 Aspose OCR 從圖片中提取 Urdu 字元。本文從授權、語言選擇、載入圖片到列印結果逐步說明，讓你可以直接把程式碼貼入任何 Java 專案並看到效果。

接下來，試著對較大的 PDF、不同的文字系統，或將 OCR 步驟整合到 Spring Boot REST 端點中進行實驗。相同的原則——**how to extract text**、**load image o

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}