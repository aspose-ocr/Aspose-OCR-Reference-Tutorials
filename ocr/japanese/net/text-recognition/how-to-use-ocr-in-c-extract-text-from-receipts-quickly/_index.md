---
category: general
date: 2026-03-05
description: C#でOCRを使用してレシート画像からテキストを抽出する方法。OCR用に画像をロードし、数分でレシート画像を認識する方法を学びましょう。
draft: false
keywords:
- how to use OCR
- extract text from receipt
- load image for OCR
- recognize receipt image
language: ja
og_description: C#でOCRを使用してレシートからテキストを抽出する方法。ステップバイステップのガイドに従って画像をOCRに読み込み、レシート画像を効率的に認識しましょう。
og_title: C#でOCRを使用する方法 – 高速レシートテキスト抽出
tags:
- OCR
- C#
- Aspose
- Receipt Processing
title: C#でOCRを使用する方法 – レシートからテキストを素早く抽出
url: /ja/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-receipts-quickly/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# で OCR を使用する方法 – レシートからテキストをすばやく抽出

食料品のレシートの写真から直接データを取得する方法として **OCR の使い方** を考えたことはありますか？ あなただけではありません。多くの小規模ビジネスアプリでは、ぼやけた PNG を実際に扱える構造化テキストに変換することがボトルネックになっています。  

良いニュースです。C# と Aspose.OCR の数行で **OCR 用画像の読み込み** を行い、エンジンを実行し、**レシート画像の認識** を1分未満で行えます。以下に、完全で実行可能なサンプルと、ほとんどのチュートリアルが省略しがちなコツをご紹介します。

## 本ガイドでカバーする内容

* Aspose.OCR NuGet パッケージのインストール。  
* OCR エンジンの設定 – 正しく **OCR の使い方** を行うためのコア。  
* レシートファイルの読み込み（これが **OCR 用画像の読み込み** 手順です）。  
* 認識プロセスを実行し、JSON と XML のレイアウトデータの両方を取得。  
* ライセンスがない、またはサポートされていない画像形式など、一般的な落とし穴への対処。  

最後まで読むと、フォルダーに入れた任意のレシートからテキストを抽出する自己完結型プログラムが手に入ります。外部サービスは不要、隠されたマジックもありません。

## 前提条件

* .NET 6 SDK 以降（コードは .NET Core でもコンパイル可能）。  
* 有効な Aspose.OCR ライセンスファイル（`Aspose.OCR.lic`）。まだ持っていない場合は Aspose から無料トライアルを取得できます。  
* サンプルのレシート画像 – `receipt.png` で問題ありませんが、一般的なラスタ形式であればどれでも構いません。  

これらが揃っているなら、素晴らしいです – さっそく始めましょう。

![OCR の使用例](https://example.com/ocr-receipt.png "OCR の使用例")

## 手順 1: Aspose.OCR をインストールし新しいプロジェクトを作成

まず最初に、実際に重い処理を行うライブラリが必要です。プロジェクトフォルダーでターミナルを開き、次のコマンドを実行してください。

```bash
dotnet new console -n ReceiptOcrDemo
cd ReceiptOcrDemo
dotnet add package Aspose.OCR
```

このコマンドはコンソールアプリを作成し、最新の Aspose.OCR パッケージを取得します。私の経験では、プロジェクト名を短くしておくと、生成されたパスが読みやすくなり、特に複数のデモアプリを扱い始めたときに便利です。

## 手順 2: OCR エンジンの初期化 – **OCR の使い方** の核心

ここでは、C# で “**OCR の使い方**” という質問に答えるコードを書きます。`Program.cs` を開き、内容を以下のスニペットに置き換えてください。コメントに注目してください – 各行の *why*（なぜ）を説明しており、単なる *what*（何を）だけではありません。

```csharp
using System;
using System.IO;
using Aspose.OCR;          // Aspose OCR namespace
using Aspose.OCR.Image;   // For loading images

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Create and configure the OCR engine.
        // -------------------------------------------------
        var ocrEngine = new OcrEngine();

        // Why set a license? Without it the engine runs in evaluation mode,
        // which adds a watermark to the output and limits batch size.
        ocrEngine.SetLicense("Aspose.OCR.lic");

        // -------------------------------------------------
        // 2️⃣ Load the receipt image – this is the **load image for OCR** step.
        // -------------------------------------------------
        // Change the path to point at your own receipt file.
        string imagePath = Path.Combine(
            Environment.CurrentDirectory, "receipt.png");

        // The ImageStream class abstracts file I/O and supports many formats.
        ocrEngine.Image = ImageStream.FromFile(imagePath);

        // -------------------------------------------------
        // 3️⃣ Run the recognition process – this is where we **recognize receipt image**.
        // -------------------------------------------------
        var ocrResult = ocrEngine.Recognize();

        // -------------------------------------------------
        // 4️⃣ Export the layout information as JSON.
        // -------------------------------------------------
        string jsonResult = ocrResult.ToJson();
        File.WriteAllText("receipt.json", jsonResult);
        Console.WriteLine("✅ JSON saved to receipt.json");

        // -------------------------------------------------
        // 5️⃣ Export the same layout information as XML.
        // -------------------------------------------------
        string xmlResult = ocrResult.ToXml();
        File.WriteAllText("receipt.xml", xmlResult);
        Console.WriteLine("✅ XML saved to receipt.xml");

        // -------------------------------------------------
        // 6️⃣ Quick preview – print the plain text to console.
        // -------------------------------------------------
        Console.WriteLine("\n--- Extracted Text ---");
        Console.WriteLine(ocrResult.Text);
    }
}
```

### これが機能する理由

* **`OcrEngine`** はエントリーポイントで、後で調整できるすべての設定（言語、DPI など）を保持します。  
* **`SetLicense`** は評価版の透かしを除去します – コードを配布する際に重要なステップです。  
* **`ImageStream.FromFile`** は **OCR 用画像の読み込み** を行い、PNG、JPEG、BMP、TIFF などを処理します。  
* **`Recognize()`** は実際に **レシート画像の認識** を行うメソッドです。内部では二値化、セグメンテーション、文字分類が行われます。  
* JSON と XML へのエクスポートにより、人間が読めるダンプと、下流のパーサーに渡せる機械向け構造の両方が得られます。  

## 手順 3: デモを実行し出力を確認

コンパイルして実行します：

```bash
dotnet run
```

すべて正しく設定されていれば、以下のような出力が表示されます：

```
✅ JSON saved to receipt.json
✅ XML saved to receipt.xml

--- Extracted Text ---
Walmart Supercenter
Date: 03/04/2026
Item    Qty   Price
Milk    2     2.58
Bread   1     1.99
Total   4.57
```

コンソールにはプレーンテキストが表示され、`receipt.json` と `receipt.xml` には座標や信頼度スコアなどの詳細なレイアウト情報が含まれます。これらのファイルは、後で各行をデータベースのフィールドにマッピングする必要がある場合に便利です。

## エッジケースとプロのコツ

### 1️⃣ ライセンスがない、または無効な場合

`SetLicense` が失敗すると、エンジンはトライアルモードにフォールバックし、出力に透かしが入ります。呼び出しを try/catch でラップし、親切なメッセージをログに出しましょう：

```csharp
try { ocrEngine.SetLicense("Aspose.OCR.lic"); }
catch (Exception ex)
{
    Console.WriteLine("⚠️ License not found – running in trial mode.");
    Console.WriteLine(ex.Message);
}
```

### 2️⃣ サポートされていない画像形式

Aspose.OCR はほとんどのラスタ形式をサポートしていますが、PDF やマルチページ TIFF を渡す場合は、対象ページを画像に変換する必要があります。`Aspose.PDF` ライブラリでその変換が可能です。

### 3️⃣ 大きなレシートとパフォーマンス

10 MB の画像を処理すると遅くなることがあります。エンジンに渡す前に解像度を下げましょう：

```csharp
ocrEngine.Image = ImageStream.FromFile(imagePath).Resize(1024, 0);
```

`Resize` メソッドはアスペクト比を保ち（高さに `0` を指定）、典型的なレシートに対する OCR 精度を損なうことなくファイルサイズを大幅に削減します。

### 4️⃣ 言語とフォントの問題

レシートには特殊文字（€, ¥ など）が含まれることがあります。ロケールが分かっている場合は言語を明示的に設定してください：

```csharp
ocrEngine.Language = Language.English; // or Language.Spanish, etc.
```

混在言語のレシートの場合は、マルチリンガルモードを有効にできます：

```csharp
ocrEngine.Language = Language.English | Language.French;
```

### 5️⃣ 構造化データの抽出

生テキストも有用ですが、ほとんどのアプリは構造化されたフィールド（日付、合計、商品など）を必要とします。JSON レイアウトには各単語の `BoundingBox` 座標が含まれています。以下のように後処理できます：

```csharp
var layout = Newtonsoft.Json.Linq.JObject.Parse(jsonResult);
foreach (var word in layout["Words"])
{
    string text = (string)word["Text"];
    // Simple heuristics: look for "$" or "Total"
}
```

このスニペットは概念を示しています。実運用では正規表現や小さなルールエンジンを使用することが多いでしょう。

## よくある質問

**Q: これを Linux で実行できますか？**  
A: もちろんです。Aspose.OCR はクロスプラットフォーム対応で、Linux マシンに .NET ランタイムをインストールすれば同じコードが動作します。

**Q: 1 分間に数十枚のレシートを処理する必要がある場合は？**  
A: `Parallel.ForEach` ループを立ち上げ、単一の `OcrEngine` インスタンスを再利用します – 読み取り専用操作ではスレッドセーフです。ライセンスの同時実行制限に注意してください。

**Q: 角度がついたモバイル写真でも動作しますか？**  
A: エンジンには基本的なデスキュー機能が含まれていますが、画像が大きく傾いている場合は、画像処理ライブラリ（例: OpenCV）で事前に補正し、レシートを真っ直ぐにしてから処理すると良いでしょう。

## 完全な動作例（コピー＆ペースト）

以下は `Program.cs` に貼り付けられる *全体* のプログラムです。ライセンスファイルとレシート画像以外に必要なファイルはありません。

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Image;

class Program
{
    static void Main()
    {
        // Create and configure the OCR engine
        var ocrEngine = new OcrEngine();
        try
        {
            ocrEngine.SetLicense("Aspose.OCR.lic");
        }
        catch (Exception)
        {
            Console.WriteLine("⚠️ Running in trial mode – license not found.");
        }

        // Load the image to be processed (load image for OCR)
        string imagePath = Path.Combine(Environment.CurrentDirectory, "

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}