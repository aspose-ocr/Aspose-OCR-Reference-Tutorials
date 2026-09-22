---
category: general
date: 2026-01-07
description: 使用 Aspose OCR Java 從圖像取得 OCR 文字。了解如何提取文字圖像、載入圖像 OCR，並在數分鐘內執行 Java OCR
  範例。
draft: false
keywords:
- get OCR text
- extract text image
- java OCR example
- aspose OCR Java
- load image OCR
language: zh-hant
og_description: 使用 Aspose OCR Java 從圖像獲取 OCR 文字。本指南展示 Java OCR 示例，說明如何提取圖像文字，以及如何高效載入圖像進行
  OCR。
og_title: 在 Java 中取得 OCR 文字 – 完整的 Aspose OCR 教學
tags:
- OCR
- Java
- Aspose
- Image Processing
title: 在 Java 中取得 OCR 文字 – 完整的 Aspose OCR 範例
url: /zh-hant/java/ocr-basics/get-ocr-text-in-java-complete-aspose-ocr-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Java 中獲取 OCR 文字 – 完整 Aspose OCR 範例

有沒有曾經需要從掃描文件中**獲取 OCR 文字**，卻不確定該選哪個函式庫？你並非唯一面臨此問題的人。在許多實務專案中——例如發票自動化、收據處理或多語言表單數位化——從影像中擷取文字是自動化的第一步。

在本教學中，我們將示範一個使用 Aspose OCR for Java 函式庫的**java OCR 範例**。完成後，你將了解如何**載入影像 OCR**、執行引擎，並以極少的程式碼**提取文字影像**資料。沒有冗餘，只提供可直接複製貼入專案的實用解決方案。

## 你將學到的內容

- 如何設定 Aspose OCR for Java（包括 Maven 坐標）。
- 逐步說明如何**載入影像 OCR**並指定語言。
- 如何將**獲取的 OCR 文字**作為純字串並印出到主控台。
- 處理多語言影像與自動偵測語言的技巧。

*先決條件*：Java 8 或更新版本、支援 Maven 的 IDE（IntelliJ IDEA、Eclipse 或 VS Code），以及有效的 Aspose OCR for Java 授權（免費試用版可用於評估）。

---

![使用 Aspose OCR Java 從影像獲取 OCR 文字的流程圖](https://example.com/ocr-flowchart.png "取得 OCR 文字流程圖")

## 步驟 1 – 新增 Aspose OCR 相依性（載入影像 OCR）

首先，告訴 Maven 下載 Aspose OCR 函式庫。開啟 `pom.xml`，在 `<dependencies>` 內插入以下 `<dependency>` 區塊：

```xml
<!-- Aspose OCR for Java -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- Use the latest version available -->
</dependency>
```

> **專業提示**：如果你使用 Gradle，等價的寫法是 `implementation 'com.aspose:aspose-ocr:23.9'`。加入相依性是將**載入影像 OCR**功能加入專案的最簡單方式。

## 步驟 2 – 建立 OCR 引擎並載入影像

接下來，我們會寫一個簡短的 Java 類別，建立 `OcrEngine` 實例、指向影像檔案，並告訴引擎要辨識的語言。語言以 ISO‑639‑2 代碼表示（例如 `"tam"` 代表 Tamil）。

```java
package com.example.ocr;

import com.aspose.ocr.*;

public class LanguageExample {

    public static void main(String[] args) throws Exception {
        // 2️⃣ Initialize the OCR engine
        OcrEngine engine = new OcrEngine();

        // 2️⃣ Load the image you want to process – this is the "load image OCR" step
        engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/multilingual.png"));

        // 2️⃣ Choose the language (ISO‑639‑2). Change "tam" to any supported code.
        engine.getEngineOptions().setLanguage("tam");
        // If you prefer automatic detection, uncomment the next line:
        // engine.getEngineOptions().setAutoDetectLanguage(true);
```

### 為何要明確設定語言？

明確指定語言可減少誤判並加快辨識速度。對於多語言 PDF，你可以遍歷語言代碼陣列，或啟用自動偵測以提升便利性。

## 步驟 3 – 執行 OCR 程序並**獲取 OCR 文字**

引擎設定完成後，下一行程式碼實際執行辨識。結果物件包含擷取出的字串及其他中繼資料。

```java
        // 3️⃣ Perform OCR – this is where we finally **get OCR text**
        OcrResult result = engine.recognize();

        // 3️⃣ Output the recognized text to the console
        System.out.println("=== Extracted Text ===");
        System.out.println(result.getText());
    }
}
```

執行 `LanguageExample` 時，你應該會看到類似以下的輸出：

```
=== Extracted Text ===
தமிழ் உரை இங்கு வருகிறது...
```

如果使用了 `setAutoDetectLanguage(true)`，引擎會嘗試自行判斷語言，對於未知文件相當方便。

## 步驟 4 – 處理常見邊緣情況（提取文字影像變體）

### 處理低解析度影像

OCR 準確度在低於 300 dpi 時會急劇下降。若來源影像解析度過低，建議先進行升頻處理：

```java
engine.getEngineOptions().setResolution(300); // forces 300 DPI
```

### 移除背景噪點

掃描表單有時會出現雜點，干擾引擎辨識。你可以啟用前處理功能：

```java
engine.getEngineOptions().setPreprocessMode(EngineOptions.PreprocessMode.Auto);
```

### 從特定區域提取文字

若只需要特定矩形區域（例如表格儲存格）的文字，請在呼叫 `recognize()` 前設定 `Rectangle`：

```java
engine.setRegion(new Rectangle(50, 100, 400, 200));
```

這些調整讓你的**java OCR 範例**足以應付正式環境的工作負載。

## 步驟 5 – 驗證輸出（預期結果為何？）

成功執行後，程式會在主控台印出影像的純文字版本。對於多語言影像，可能會看到混合文字：

```
Hello World
こんにちは世界
مرحبا بالعالم
```

如果輸出為空或亂碼，請再次確認：

1. `setImage` 中的檔案路徑（是否正確？）。
2. 語言代碼是否與影像中的文字相符。
3. 影像品質（對比度、DPI）是否足夠。

## 完整範例（可直接複製貼上）

以下為完整檔案，可直接編譯執行。將 `YOUR_DIRECTORY/multilingual.png` 替換為實際測試影像的路徑。

```java
package com.example.ocr;

import com.aspose.ocr.*;

public class LanguageExample {
    public static void main(String[] args) throws Exception {
        // Initialize OCR engine
        OcrEngine engine = new OcrEngine();

        // Load the image – this is the core "load image OCR" step
        engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/multilingual.png"));

        // Set language (ISO‑639‑2). For Tamil use "tam". Change as needed.
        engine.getEngineOptions().setLanguage("tam");
        // Uncomment for auto‑detect:
        // engine.getEngineOptions().setAutoDetectLanguage(true);

        // Optional: improve accuracy on low‑res images
        // engine.getEngineOptions().setResolution(300);
        // engine.getEngineOptions().setPreprocessMode(EngineOptions.PreprocessMode.Auto);

        // Perform OCR and retrieve text
        OcrResult result = engine.recognize();

        // Print the extracted text – this is how we **get OCR text**
        System.out.println("=== Extracted Text ===");
        System.out.println(result.getText());
    }
}
```

編譯並執行：

```bash
mvn compile exec:java -Dexec.mainClass="com.example.ocr.LanguageExample"
```

現在你應該會在主控台看到擷取出的內容。

---

## 結論

我們剛剛示範了如何使用 Aspose OCR for Java **從影像獲取 OCR 文字**。依循此**java OCR 範例**，你可以**提取文字影像**資料、**載入影像 OCR**，甚至針對多語言或噪點影像微調引擎設定。

接下來你可以：

- 將 OCR 步驟整合到更大的工作流程中（例如，將文字儲存至資料庫）。
- 結合翻譯 API，將多語言掃描轉換為單一語言。
- 嘗試其他 Aspose OCR 功能，如 PDF 轉換或條碼偵測。

試一試、找出問題、再微調設定，直到輸出完美為止。祝程式開發愉快，願你的 OCR 永遠清晰無誤！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}