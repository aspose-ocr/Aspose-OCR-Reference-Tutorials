---
category: general
date: 2026-03-21
description: C# OCRチュートリアル：C#でOCRを使用してPNG画像からウルドゥー語テキストを抽出する方法を学びます。ステップバイステップのコード、言語設定、実用的なヒントが含まれています。
draft: false
keywords:
- c# ocr tutorial
- extract urdu text
- recognize text image
- how to extract urdu
- ocr from png file
language: ja
og_description: c# OCRチュートリアル：C#でOCRを使用してPNG画像からウルドゥー語テキストを抽出する方法を学びましょう。コードとヒント付きの完全ガイド。
og_title: C# OCRチュートリアル – PNG画像からウルドゥー語テキストを抽出
tags:
- OCR
- C#
- Urdu
- Image Processing
title: C# OCRチュートリアル – PNG画像からウルドゥー語テキストを抽出
url: /ja/net/text-recognition/c-ocr-tutorial-extract-urdu-text-from-png-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# ocr チュートリアル – PNG画像からウルドゥー語テキストを抽出する

実際にPNGファイルからウルドゥー語テキストを抽出する **c# ocr tutorial** が必要だったことはありませんか？ あなたは一人ではありません。多くのプロジェクト—請求書処理、文書アーカイブ、あるいは簡易翻訳ツール—で、テキスト画像データを認識しなければならず、言語が重要になる瞬間に直面します。  

このガイドでは、OCRエンジンを使用してPNGからウルドゥー語テキストを抽出する、完全で実行可能なソリューションを順を追って解説します。各行の意味、欠落した言語パックの扱い方、画像が完璧でない場合の対処法を確認できます。最後まで読めば、他の言語やファイルタイプにもコードを応用できる自信がつきます。

## 学べること

- C# OCR ライブラリのセットアップ方法（隠された魔法はありません）  
- PNG ファイルから **extract urdu text** する正確な手順  
- 言語をウルドゥー語に設定する重要性と、エンジンが自動で欠落データをダウンロードする仕組み  
- 出力を検証し、一般的な落とし穴をトラブルシュートする方法  

外部ドキュメントへのリンクは不要です—必要な情報はすべてここにあります。

## 前提条件 (開始前に必要なもの)

| 要件 | 重要な理由 |
|------|------------|
| .NET 6.0+（または .NET Core 3.1） | モダンなAPIと非同期サポート |
| Visual Studio 2022（または C# 拡張機能付き VS Code） | IntelliSense 搭載の IDE によりコードが分かりやすくなります |
| `OcrEngine` を提供する OCR ライブラリ（例: **Microsoft.Windows.SDK.Contracts** またはサードパーティの NuGet） | `Language.Urdu` と `Recognize` メソッドを提供します |
| ウルドゥー語テキストを含む PNG 画像（例: `urdu_invoice.png`） | **recognize text image** 操作のソース |

OCR パッケージがまだない場合は、Package Manager Console で次のワンライナーを実行してください：

```powershell
Install-Package Microsoft.Windows.SDK.Contracts
```

> **Pro tip:** SDK は初回使用時に自動で言語データを取得するため、ウルドゥー語パックを手動でダウンロードする必要はありません。

## 手順 1: OCR ライブラリのインストールと参照

エンジンを作成できるようにする前に、プロジェクトが OCR パッケージを参照している必要があります。ファイルの先頭に以下の `using` ディレクティブを追加してください：

```csharp
using System;
using Windows.Media.Ocr;          // Core OCR classes
using Windows.Graphics.Imaging;   // For loading PNG files
using Windows.Storage;            // File handling helpers
```

これらの名前空間により、`OcrEngine`、`Language`、画像読み込みユーティリティにアクセスできます。別のライブラリを使用している場合は、同等の名前空間を探してください。

## 手順 2: OCR エンジンインスタンスの作成  

実際にエンジンを起動します。エンジンはピクセルパターンを文字として解釈する「脳」のようなものです。

```csharp
// Step 2: Initialize the OCR engine
OcrEngine ocrEngine = OcrEngine.TryCreateFromLanguage(new Language("ur"));
if (ocrEngine == null)
{
    Console.WriteLine("Failed to create OCR engine for Urdu. Check your language pack.");
    return;
}
```

**なぜ重要か:** `TryCreateFromLanguage` は言語データが存在しない場合に `null` を返すため、後でクラッシュする代わりに早期に失敗を検出できます。

## 手順 3: PNG 画像の読み込み  

OCR エンジンは `SoftwareBitmap` オブジェクトを扱い、ファイルパスそのものは受け取りません。以下のヘルパーはディスク上の PNG を読み込み、必要な形式に変換します。

```csharp
// Step 3: Load the PNG image into a SoftwareBitmap
async Task<SoftwareBitmap> LoadImageAsync(string path)
{
    StorageFile file = await StorageFile.GetFileFromPathAsync(path);
    using var stream = await file.OpenReadAsync();
    var decoder = await BitmapDecoder.CreateAsync(stream);
    // Convert to Gray8 for best OCR accuracy
    return await decoder.GetSoftwareBitmapAsync(BitmapPixelFormat.Gray8, BitmapAlphaMode.Ignore);
}
```

**エッジケース:** PNG がカラーの場合、グレースケール（`Gray8`）に変換すると認識精度が向上することが多く、特にウルドゥー語のような繊細なディアクリティックを含むスクリプトで有効です。

## 手順 4: 画像からテキストを認識  

これが **c# ocr tutorial** の核心です—エンジンに画像を読ませます。

```csharp
// Step 4: Perform OCR on the loaded bitmap
async Task<string> RecognizeUrduAsync(string imagePath)
{
    SoftwareBitmap bitmap = await LoadImageAsync(imagePath);
    OcrResult result = await ocrEngine.RecognizeAsync(bitmap);
    return result.Text;
}
```

`OcrResult.Text` プロパティに生の Unicode 文字列が格納されます。事前に言語をウルドゥー語に設定しているため、エンジンは正しいスクリプト規則を適用します。

## 手順 5: 抽出テキストの出力と検証  

最後に結果をコンソールに出力します。実際のアプリではデータベースに保存したり、翻訳サービスに渡したりすることが考えられます。

```csharp
// Step 5: Run the OCR and display the result
static async Task Main(string[] args)
{
    string imageFile = @"C:\Images\urdu_invoice.png"; // adjust path as needed
    string extracted = await RecognizeUrduAsync(imageFile);
    Console.WriteLine("=== Extracted Urdu Text ===");
    Console.WriteLine(extracted);
}
```

**期待される結果:** 画像が鮮明であれば、次のように表示されます：

```
=== Extracted Urdu Text ===
بل نمبر: 12345
تاریخ: 21/03/2026
کل رقم: 5,000 روپے
```

出力が文字化けしている場合は、画像の品質（コントラスト、ノイズ）を確認し、二値化などの前処理を検討してください。

## PNG ファイルからウルドゥー語テキストを抽出する方法 – よくある落とし穴  

1. **低コントラスト** – 前景と背景の色が似ていると OCR が苦戦します。コード実行前に画像編集ツールでコントラストを上げてください。  
2. **不適切な DPI** – 300 dpi 以上でスキャンすると、エンジンがより多くのディテールを取得できます。  
3. **言語パックが欠落** – `TryCreateFromLanguage` の最初の呼び出しでダウンロードがトリガーされることがあります。インターネット接続があることを確認してください。  

これらの問題に対処すると、**recognize text image** の成功率が大幅に向上します。

## Recognize Text Image: 他のフォーマットへの拡張  

このチュートリアルは PNG に焦点を当てていますが、同じワークフローは JPEG、BMP、TIFF でも機能します—拡張子を変更し、デコーダが対応していることを確認すれば OK です。重要な行は変わらず `await ocrEngine.RecognizeAsync(bitmap);` です。

## PNG ファイルからの OCR のヒント – パフォーマンスとスケーリング  

- **バッチ処理:** 複数画像をリストに入れ、`Task.WhenAll` で認識を並列化します。  
- **エンジンのキャッシュ:** `OcrEngine` インスタンスを一度作成し、呼び出し間で再利用します。毎回構築するとオーバーヘッドが増えます。  
- **メモリ管理:** 使用後は `SoftwareBitmap` オブジェクトを必ず破棄します（`bitmap.Dispose()`）ことでプロセスを軽量に保ちます。

## 完全動作例（コピー＆ペースト可能）

以下はそのままコンパイルして実行できるプログラム全体です。すべての `using` 文、非同期処理、エラーチェックが含まれています。

```csharp
// Full C# OCR tutorial – Extract Urdu text from a PNG file
using System;
using System.Threading.Tasks;
using Windows.Media.Ocr;
using Windows.Graphics.Imaging;
using Windows.Storage;

class Program
{
    // Initialize the OCR engine for Urdu
    private static OcrEngine _ocrEngine = OcrEngine.TryCreateFromLanguage(new Language("ur"));

    static async Task Main(string[] args)
    {
        if (_ocrEngine == null)
        {
            Console.WriteLine("Urdu language pack not available. Ensure internet connectivity for automatic download.");
            return;
        }

        string imagePath = @"C:\Images\urdu_invoice.png"; // <-- change to your image location
        string text = await RecognizeUrduAsync(imagePath);
        Console.WriteLine("=== Extracted Urdu Text ===");
        Console.WriteLine(text);
    }

    // Load PNG and convert to grayscale bitmap
    private static async Task<SoftwareBitmap> LoadImageAsync(string path)
    {
        StorageFile file = await StorageFile.GetFileFromPathAsync(path);
        using var stream = await file.OpenReadAsync();
        var decoder = await BitmapDecoder.CreateAsync(stream);
        return await decoder.GetSoftwareBitmapAsync(BitmapPixelFormat.Gray8, BitmapAlphaMode.Ignore);
    }

    // Perform OCR and return the recognized text
    private static async Task<string> RecognizeUrduAsync(string imagePath)
    {
        SoftwareBitmap bitmap = await LoadImageAsync(imagePath);
        OcrResult result = await _ocrEngine.RecognizeAsync(bitmap);
        return result.Text;
    }
}
```

**期待される出力:** コンソールに画像内で検出されたウルドゥー語文字が右から左へ正しい順序で表示されます。

## 結論  

これで **c# ocr tutorial** は完了です。PNG から **extract urdu text** する方法、言語設定、結果の安全な取り扱いを実演しました。ライブラリのインストール、エンジン作成、画像読み込み、テキスト認識、出力の手順は、任意のスクリプトやファイルタイプに再利用できるパターンです。  

次のステップとして、**recognize text image** をマルチページ PDF（各ページを PNG に変換）に適用したり、翻訳 API と統合して抽出したウルドゥー語を自動で英語に変換したりしてみてください。このコアワークフローをマスターすれば、可能性は無限に広がります。

Happy coding, and may your OCR results be crystal‑clear!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}