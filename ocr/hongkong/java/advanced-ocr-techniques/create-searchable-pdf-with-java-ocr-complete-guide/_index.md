---
category: general
date: 2026-05-25
description: 使用 Aspose OCR 在 Java 中建立可搜尋的 PDF。了解如何將 PDF 轉換為可搜尋的 PDF、載入 PDF 進行 OCR，以及使用
  GPU 加速。
draft: false
keywords:
- create searchable pdf
- convert pdf to searchable pdf
- load pdf for ocr
- ocr pdf with gpu
language: zh-hant
og_description: 使用 Aspose OCR 在 Java 中建立可搜尋的 PDF。本教學示範如何將 PDF 轉換為可搜尋的 PDF、載入 PDF 進行
  OCR，以及使用 GPU 加速。
og_title: 使用 Java OCR 建立可搜尋 PDF – 完整指南
schemas:
- author: Aspose
  dateModified: '2026-05-25'
  description: Create searchable PDF in Java using Aspose OCR. Learn how to convert
    PDF to searchable PDF, load PDF for OCR, and accelerate with GPU.
  headline: Create Searchable PDF with Java OCR – Complete Guide
  type: TechArticle
- description: Create searchable PDF in Java using Aspose OCR. Learn how to convert
    PDF to searchable PDF, load PDF for OCR, and accelerate with GPU.
  name: Create Searchable PDF with Java OCR – Complete Guide
  steps:
  - name: Runs OCR on each page image.
    text: Runs OCR on each page image.
  - name: Generates an invisible text layer that matches the visual content.
    text: Generates an invisible text layer that matches the visual content.
  - name: Embeds that layer into a new PDF, preserving the original appearance.
    text: Embeds that layer into a new PDF, preserving the original appearance.
  type: HowTo
tags:
- OCR
- Java
- PDF
- Aspose
title: 使用 Java OCR 建立可搜尋 PDF – 完整指南
url: /zh-hant/java/advanced-ocr-techniques/create-searchable-pdf-with-java-ocr-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Java OCR 建立可搜尋 PDF – 完整指南

是否曾需要從掃描文件**建立可搜尋 PDF**檔案，但不知從何入手？您並不孤單。許多開發者在將僅含影像的 PDF 轉換為可文字搜尋的資產時，常會碰到相同的障礙，尤其在效能很重要的情況下。

在本教學中，我們將手把手示範如何使用 Aspose OCR for Java **建立可搜尋 PDF**檔案。還會示範如何**將 PDF 轉換為可搜尋 PDF**、**載入 PDF 進行 OCR**，甚至**使用 GPU 加速 OCR PDF**——全部寫在一個易讀的腳本裡。完成後，您將擁有可執行的程式，並清楚了解每一步的意義。

> **您將收穫**  
> * 一個完整的 Java 專案，能讀取混合語言的 PDF  
> * 支援 GPU 的 OCR，讓現代硬體的處理速度更快  
> * 可直接放入任何文件管理系統的可搜尋 PDF 輸出  

## 先決條件

在開始之前，請確保您已具備：

* 已安裝 Java 17（或更新版本）——舊版可能缺少必要的 API。  
* Maven 或 Gradle 來管理相依性——範例中使用 Maven。  
* Aspose OCR for Java 授權（免費試用版可用於測試）。  
* 一個包含掃描頁面的 PDF 檔案（示範使用 `mixed_lang.pdf`）。  

如果以上任一項您不熟悉，別擔心——以下步驟會提供完整指令，讓您快速上手。

![Create searchable PDF using Aspose OCR Java](https://example.com/images/create-searchable-pdf.png "Create searchable PDF using Aspose OCR Java")

## 步驟 1：設定專案與 **建立可搜尋 PDF** – 專案初始化

首先，建立一個 Maven 專案。打開終端機並執行：

```bash
mvn archetype:generate -DgroupId=com.example.ocr \
    -DartifactId=SearchablePdfDemo -DarchetypeArtifactId=maven-archetype-quickstart \
    -DinteractiveMode=false
```

進入資料夾：

```bash
cd SearchablePdfDemo
```

在 `pom.xml` 中加入 Aspose OCR 相依性：

```xml
<dependencies>
    <dependency>
        <groupId>com.aspose</groupId>
        <artifactId>aspose-ocr</artifactId>
        <version>23.9</version> <!-- check Maven Central for the latest -->
    </dependency>
</dependencies>
```

> **為什麼這很重要：** **建立可搜尋 pdf** 的流程依賴於 `OcrEngine` 類別，該類別位於 Aspose OCR 函式庫內。若使用錯誤版本，會出現編譯錯誤或缺少功能。

現在在 `src/main/java/com/example/ocr/` 目錄下建立主 Java 類別 `QuickDemo.java`。

## 步驟 2：啟用 GPU 加速 – **OCR PDF with GPU**

GPU 加速可以為多頁 OCR 工作節省數分鐘。Aspose OCR 只需一行程式碼即可切換：

```java
// Enable GPU processing
engine.getEngineOptions().setUseGpu(true);
```

如果您的機器配備相容的 NVIDIA 或 AMD GPU 且已安裝正確的驅動程式，OCR 引擎會將繁重的運算交給顯示卡處理。否則，呼叫會安全地回退至 CPU 處理——不會當機，只是執行較慢。

> **專業提示：** 在 Linux 上，啟動 JVM 前可能需要設定 `LD_LIBRARY_PATH`，指向 CUDA 函式庫所在路徑。

## 步驟 3：**Load PDF for OCR** 與語言支援設定

現在我們真的要**load pdf for ocr**。Aspose OCR 會在內部將 PDF 頁面視為影像，只要把檔案指給引擎即可：

```java
// Load the source PDF document (image‑only PDF)
engine.getImage().loadFromFile("YOUR_DIRECTORY/mixed_lang.pdf");
```

接著告訴引擎您預期的語言。示範中我們以泰文為例，但若文件混合多種文字，可傳入語言陣列：

```java
engine.getEngineOptions().setLanguage(OcrLanguage.THAI);
```

如果您有自訂字典（例如領域專用詞彙），也可以把它插入：

```java
engine.getEngineOptions().getSpellCorrectorOptions()
      .setUserDictionaryPath("YOUR_DIRECTORY/thai_custom.txt");
```

> **為什麼要設定語言？** OCR 的準確度取決於語言模型。提供正確的 `OcrLanguage` 能大幅降低誤辨識，尤其是非拉丁字系時。

## 步驟 4：**Convert PDF to Searchable PDF** 一次呼叫完成

Aspose OCR 的亮點在於它能透過單一方法呼叫**convert PDF to searchable PDF**，不必手動拼接影像與文字層。

```java
// Export a searchable PDF in a single operation
engine.saveToSearchablePdf("YOUR_DIRECTORY/mixed_lang_searchable.pdf");
```

在背後，引擎會：

1. 對每一頁影像執行 OCR。  
2. 產生與視覺內容相符的隱形文字層。  
3. 將該文字層嵌入新 PDF，保留原始外觀。

最終產生的檔案外觀與輸入檔相同，但任何 PDF 閱讀器都能對其進行索引。

## 步驟 5：取得辨識文字並驗證輸出

即使已儲存可搜尋 PDF，您仍可能需要原始文字作為日誌或後續處理：

```java
// Output the recognized text to the console
System.out.println(engine.recognize().getText());
```

執行程式後，您應該會在主控台看到抽取出的泰文文字，並在目錄中產生 `mixed_lang_searchable.pdf`。

### 預期的主控台輸出（截斷版）

```
สวัสดีครับ นี่คือเอกสารตัวอย่าง...
...
```

在 Adobe Reader 或任何閱讀器中開啟產生的 PDF，按 **Ctrl + F**，即可搜尋剛才在主控台看到的詞彙。這證明我們成功**建立可搜尋 pdf**檔案。

## 步驟 6：常見陷阱與 **Pro Tips** 以提升 OCR 效能

| 問題 | 症狀 | 解決方案 |
|-------|----------|-----|
| **GPU 未偵測到** | 沒有速度提升，引擎回退至 CPU | 確認已安裝 CUDA 驅動，且 `java.library.path` 包含 GPU 函式庫。 |
| **缺少字型** | 文字層出現亂碼 | 在作業系統上安裝相應語言字型，或透過 `engine.getEngineOptions().setEmbedFonts(true)` 內嵌字型。 |
| **大型 PDF（> 500 頁）** | 記憶體不足錯誤 | 增加 JVM 堆疊大小（`-Xmx4g`），並設定 `engine.getEngineOptions().setThreadCount(Runtime.getRuntime().availableProcessors())` 以利用多核心。 |
| **自訂字典未套用** | 拼寫校正似乎被忽略 | 確認路徑為絕對路徑且檔案使用 UTF-8 編碼。 |

> **記得：** 當您想要 **ocr pdf with gpu** 並充分利用多核心 CPU 時，以下程式碼至關重要：`engine.getEngineOptions().setThreadCount(Runtime.getRuntime().availableProcessors());`。它會讓引擎為每個核心產生工作執行緒，讓 GPU 持續忙碌，同時 CPU 處理前後處理工作。

## 完整範例程式

以下是結合所有步驟的完整、可直接執行的 Java 程式。請將佔位路徑替換為您自己的目錄。

```java
import com.aspose.ocr.*;

public class QuickDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create an OCR engine instance
        OcrEngine engine = new OcrEngine();

        // Step 2: Enable GPU acceleration and use all available CPU cores
        engine.getEngineOptions().setUseGpu(true);
        engine.getEngineOptions().setThreadCount(Runtime.getRuntime().availableProcessors());

        // Step 3: Configure language support and a custom spell‑corrector dictionary
        engine.getEngineOptions().setLanguage(OcrLanguage.THAI);
        engine.getEngineOptions().getSpellCorrectorOptions()
              .setUserDictionaryPath("YOUR_DIRECTORY/thai_custom.txt");

        // Step 4: Load the source PDF document (this is where we **load pdf for ocr**)
        engine.getImage().loadFromFile("YOUR_DIRECTORY/mixed_lang.pdf");

        // Step 5: Export a searchable PDF in a single operation (**convert pdf to searchable pdf**)
        engine.saveToSearchablePdf("YOUR_DIRECTORY/mixed_lang_searchable.pdf");

        // Step 6: Output the recognized text to the console
        System.out.println(engine.recognize().getText());
    }
}
```

編譯並執行：

```bash
mvn compile exec:java -Dexec.mainClass="com.example.ocr.QuickDemo"
```

若一切配置正確，您將看到抽取的文字被印出，且在原始檔旁產生新的可搜尋 PDF。

## 結論

我們剛剛示範了如何使用 Aspose OCR 在 Java 中**建立可搜尋 pdf**檔案，涵蓋從專案設定到 GPU 加速處理的全部流程。透過**load pdf for OCR**、語言支援設定，並呼叫單行的**convert pdf to searchable pdf** 方法，即可得到可供搜尋引擎或內部檢索系統使用的完整索引文件。

接下來可以嘗試將 `OcrLanguage.THAI` 換成 `OcrLanguage.ENGLISH`，或結合多種語言以處理多語言 PDF。也可實驗 `engine.getEngineOptions().setResolution(300)` 參數，觀察 DPI 對準確度的影響，或嵌入自訂字型以提升舊版閱讀器的顯示效果。

對效能調校、授權或將此工作流程整合至 Spring Boot 服務有任何疑問，歡迎在下方留言，或參考 Aspose OCR Java 文件進一步探索。祝開發順利，將靜態掃描檔轉變為可搜尋的寶藏！

## 相關教學

- [使用 Aspose.OCR for Java 進行 PDF 文字辨識 – OCR 操作](/ocr/english/java/ocr-operations/)
- [在 Aspose.OCR for Java 中 OCR 辨識 PDF 文件](/ocr/english/java/ocr-operations/recognize-pdf/)
- [如何在 .NET 使用 Aspose.OCR 進行 PDF OCR](/ocr/english/net/text-recognition/recognize-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}