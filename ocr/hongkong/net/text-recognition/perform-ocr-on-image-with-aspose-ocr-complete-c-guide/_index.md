---
category: general
date: 2026-06-22
description: 使用 Aspose.OCR 於 C# 進行影像 OCR。學習從 PNG 提取文字、將影像轉換為文字，並辨識包括俄文在內的 PNG 文字。
draft: false
keywords:
- perform ocr on image
- extract text from png
- convert image to text
- recognize text from png
- read russian text
language: zh-hant
og_description: 在 C# 中使用 Aspose.OCR 進行影像 OCR。本指南說明如何從 PNG 提取文字、將影像轉換為文字，以及高效閱讀俄文文字。
og_title: 使用 Aspose.OCR 在圖像上執行 OCR – C# 教學
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Perform OCR on image using Aspose.OCR in C#. Learn to extract text
    from png, convert image to text, and recognize text from png including Russian
    language.
  headline: Perform OCR on Image with Aspose.OCR – Complete C# Guide
  type: TechArticle
tags:
- OCR
- C#
- Aspose
title: 使用 Aspose.OCR 於影像執行 OCR – 完整 C# 指南
url: /zh-hant/net/text-recognition/perform-ocr-on-image-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose.OCR 在圖像上執行 OCR – 完整 C# 指南

有沒有想過如何 **在圖像上執行 OCR** 而不需要花上數小時去尋找合適的函式庫？依我的經驗，Aspose.OCR 讓整個過程如同散步般輕鬆，特別是當你需要 **從 png 檔案中提取文字**（且文字為西里爾字母）時。

在本教學中，我們將逐步示範一個實務範例，不僅 **將圖像轉換為文字**，還會示範如何 **從 png 識別文字** 以及 **可靠地讀取俄文文字**。完成後，你將擁有一個可直接執行的主控台應用程式，能將 OCR 結果直接印在螢幕上。

---

![執行 OCR 圖像工作流程圖](image-placeholder.png "執行 OCR 圖像工作流程圖")

## 執行 OCR 圖像 – 步驟實作

以下是完整且可執行的程式碼。請隨意將它貼到新的主控台專案中，按下 F5，即可看到魔法發生。

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

class Program
{
    static void Main()
    {
        // Step 1: Load your Aspose.OCR license (if you have one)
        var license = new License();
        // license.SetLicense("Aspose.OCR.lic");   // uncomment and provide the path to your license file

        // Step 2: Create an OCR engine (CPU mode is the default)
        var ocrEngine = new OcrEngine();

        // Step 3: Specify the language to recognize – Russian (Cyrillic)
        ocrEngine.Language = OcrLanguage.Russian;

        // Step 4: (Optional) Set a download timeout for language resources, in seconds
        ocrEngine.ResourceDownloadTimeout = 120;

        // Step 5: Perform OCR on the image file
        var ocrResult = ocrEngine.RecognizeImage(@"YOUR_DIRECTORY/sample_russian.png");

        // Step 6: Output the recognized plain‑text
        System.Console.WriteLine(ocrResult.Text);
    }
}
```

執行程式後會輸出類似以下內容：

```
Привет, мир!
Это тестовое изображение.
```

此輸出證明我們已成功 **在圖像上執行 OCR** 並 **一次性讀取俄文文字**。

---

## 從 PNG 提取文字 – 載入檔案

在引擎執行工作之前，需要先取得可供處理的位圖。`RecognizeImage` 方法接受任何受支援的點陣圖格式路徑，而 PNG 是最常用於無損螢幕截圖的格式。

> **為什麼選擇 PNG？** 因為它保留每一個像素，這表示 OCR 引擎看到的正是你捕捉到的原始資料——沒有壓縮產生的雜訊會干擾辨識。

若你使用 JPEG 或 BMP，同樣的呼叫也能運作，只要把副檔名換掉即可。重要的是檔案必須存在，且你的應用程式具備讀取權限。

---

## 將圖像轉換為文字 – 內容辨識

本教學的核心在第 5 步，我們 **將圖像轉換為文字**。在底層，Aspose.OCR 會載入圖像，透過訓練過的西里爾字形神經網路進行辨識，最後回傳純文字字串。

* **提示：** 若發現字元亂碼，請增加 `ResourceDownloadTimeout` 或預先下載語言套件，以避免網路中斷。  
* **提示：** 若處理多頁 PDF，請對每一頁圖像迴圈呼叫，並將結果串接——每頁仍使用相同的 **在圖像上執行 OCR** 呼叫。

---

## 讀取俄文文字 – 設定語言

你可能會問：「我必須手動指定俄文嗎？」簡短的答案是：**是**，若想取得最佳準確度。透過設定 `ocrEngine.Language = OcrLanguage.Russian;`，我們告訴引擎載入西里爾字元集與語言模型。

若省略此步驟，引擎會預設使用英文，俄文字符將會變成問號或亂碼。因此，務必透過明確設定語言來 **讀取俄文文字**。

---

## 從 PNG 識別文字 – 處理逾時與資源

當 OCR 引擎首次需要下載語言資源時，網路延遲可能會造成問題。`ResourceDownloadTimeout` 屬性（第 4 步）提供了一個安全網。

* **何時調整：** 若使用緩慢的企業 VPN，請將逾時時間提升至 180 秒。  
* **何時不調整：** 若使用本機已安裝的語言套件，預設的 120 秒已足夠。

---

## 從 PNG 提取文字 – 授權管理（可選）

Aspose.OCR 在試用模式下即可直接使用，但授權可移除浮水印並解鎖完整 API。若要 **在圖像上執行 OCR** 且不受限制，請取消註解授權程式碼，並指向你的 `.lic` 檔案。

```csharp
var license = new License();
license.SetLicense(@"C:\Licenses\Aspose.OCR.lic");
```

---

## 將圖像轉換為文字 – 完整專案檢查清單

| ✅ | 項目 |
|---|------|
| 1 | 透過 NuGet 安裝 **Aspose.OCR** (`Install-Package Aspose.OCR`) |
| 2 | 加入 `using Aspose.OCR;` 與 `using Aspose.OCR.Models;` |
| 3 | （可選）套用授權 |
| 4 | 建立 `OcrEngine` 實例 |
| 5 | 設定 `Language = OcrLanguage.Russian` 以 **讀取俄文文字** |
| 6 | 視需要調整 `ResourceDownloadTimeout` |
| 7 | 呼叫 `RecognizeImage(@\"path\\to\\file.png\")` 以 **在圖像上執行 OCR** |
| 8 | 印出 `ocrResult.Text` —— 你剛剛已 **從 png 提取文字**！ |

---

## 常見問題與邊緣案例

**如果我的 PNG 同時包含英文與俄文怎麼辦？**  
你可以設定 `ocrEngine.Language = OcrLanguage.Multilingual;`，它會載入結合模型。引擎仍能準確 **從 png 識別文字**，但語言套件的檔案大小會稍微增加。

**我可以一次處理整個資料夾的圖像嗎？**  
當然可以。將 `RecognizeImage` 呼叫包在 `foreach (var file in Directory.GetFiles(folder, \"*.png\"))` 迴圈中。每次迭代都 **在圖像上執行 OCR**，且可將結果寫入 `.txt` 檔案。

**低解析度圖像該怎麼辦？**  
OCR 品質在低於 72 dpi 時會下降。若你的螢幕截圖模糊，建議先使用圖形函式庫將其放大，再交給 Aspose.OCR。函式庫本身不會神奇地提升像素品質。

---

## 生產環境 OCR 專業提示

* **快取結果：** 將純文字存入資料庫，以避免對未變更的檔案重複執行 OCR。  
* **驗證輸出：** 使用簡單的正規表達式檢查結果是否為空——若是，則以較長的逾時時間重新嘗試。  
* **平行化處理：** 大量處理時，可在不同執行緒上建立多個 `OcrEngine` 實例；只要每個執行緒使用自己的引擎，Aspose.OCR 即為執行緒安全。

---

## 結論

我們剛剛使用 Aspose.OCR **在圖像上執行 OCR**，示範了如何 **從 png 提取文字**、**將圖像轉換為文字**，以及 **從 png 識別文字**，同時 **無縫讀取俄文文字**。完整解決方案僅需一個 `Main` 方法即可實作，且只要稍作調整即可擴展至企業級情境。

準備好接受下一個挑戰了嗎？可嘗試使用 **ImageSharp** 等函式庫加入影像前處理（去斜、除噪），或將 OCR 結果匯出為 JSON 供後續分析。只要掌握 C# 中 OCR 的基礎，想像空間無限。

祝程式開發愉快，願你的圖像永遠清晰可讀！

## 接下來該學什麼？

以下教學涵蓋與本指南密切相關的主題，並以此為基礎。每篇資源皆提供完整可執行的程式碼範例與逐步說明，協助你精通更多 API 功能，並在自己的專案中探索其他實作方式。

- [使用 Aspose.OCR 以語言選擇提取圖像文字（C#）](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [使用 Aspose OCR 辨識多語言圖像文字](/ocr/english/net/ocr-settings/working-with-different-languages/)
- [將圖像轉換為文字 – 從 URL 執行 OCR](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}