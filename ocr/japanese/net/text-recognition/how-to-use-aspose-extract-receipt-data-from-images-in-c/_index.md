---
category: general
date: 2026-04-04
description: Aspose を使用してレシートデータを抽出し、レシート画像を読み込み、OCR でレシート画像を処理する方法を、完全な C# サンプルとともに学びましょう。開発者向けのステップバイステップガイドです。
draft: false
keywords:
- how to use aspose
- extract receipt data
- how to extract receipt
- load receipt image
- ocr receipt image
language: ja
og_description: スキャンした領収書画像から領収書データを抽出するためのAsposeの使用方法。完全なC#コード、解説、OCR領収書画像処理のヒント。
og_title: Asposeの使い方 – 画像から領収書データを抽出する
tags:
- Aspose
- OCR
- C#
- Receipt Processing
title: Aspose の使い方 – C# で画像から領収書データを抽出する
url: /ja/net/text-recognition/how-to-use-aspose-extract-receipt-data-from-images-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose の使い方 – C# で画像から領収書データを抽出する

領収書の写真から構造化された情報を取得する方法として **Aspose の使い方** を考えたことはありませんか？ あなただけではありません。経費管理アプリを作る場合でも、請求書入力を自動化する場合でも、同じ課題があります。PNG や JPEG があり、手入力せずに店舗名、日付、合計金額が欲しいということです。

実は、Aspose.OCR を使えばこの一連の流れがとても簡単になります。このチュートリアルでは、領収書画像の読み込み、OCR の実行、そして数行の C# で領収書データを抽出する手順を解説します。最後までやれば、コンソールに店舗名、日付、合計金額を直接出力する実行可能なコンソールプログラムが手に入ります。

> **クイックウィン:** コードだけが必要な場合は、下部の「完全動作例」セクションにジャンプしてコピー＆ペーストしてください。

## 必要なもの

- **.NET 6.0 以降** (API は .NET Core と .NET Framework でも動作します)
- **Aspose.OCR for .NET** NuGet パッケージ (`Install-Package Aspose.OCR`)
- ローカルに保存したサンプル領収書画像 (PNG、JPG、または BMP)
- Visual Studio 2022 または C# プロジェクトをサポートする任意のエディタ

他のサードパーティライブラリは不要です。唯一の前提条件は C# コンソールアプリケーションの基本的な理解です—「Hello World」を書いたことがあれば問題ありません。

## Step 1 – Aspose.OCR のインストールと参照

Aspose の使い方** を始めるには、まずプロジェクトにライブラリを追加する必要があります。Package Manager Console を開いて次のコマンドを実行してください：

```powershell
Install-Package Aspose.OCR
```

あるいは NuGet UI を使用して “Aspose.OCR” を検索してください。インストール後、ファイルの先頭に必要な名前空間を追加します：

```csharp
using Aspose.OCR;
using Aspose.OCR.Structured;
```

> **プロのコツ:** NuGet パッケージは常に最新に保ちましょう。2026年4月現在、最新の安定版は 23.11.0 で、高解像度の領収書に対する OCR のパフォーマンスが向上しています。

## Step 2 – 領収書画像の読み込み

領収書画像ファイルを **load receipt image** する際、一般的にはローカルパスまたは Web リクエストからのストリームの 2 つの方法があります。このチュートリアルではシンプルにディスクから読み込みます：

```csharp
// Step 2: Load the receipt image to be processed
var ocrEngine = new OcrEngine
{
    Language = Language.English // set language for better accuracy
};

ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/receipt.png");
```

`YOUR_DIRECTORY/receipt.png` を実際の領収書ファイルへのパスに置き換えてください。ユーザーアップロードを扱う場合は、`MemoryStream` を `ImageStream.FromStream` に渡すことができます。

> **なぜ重要か:** 言語 (English) を指定すると、OCR エンジンが期待すべき文字セットを認識し、誤認識が減ります—特に数字や記号を含む **ocr receipt image** の場合は重要です。

## Step 3 – OCR の実行とレイアウト情報の取得

OCR のステップは単に生テキストを出力するだけでなく、レイアウトも取得します。これは後で構造化抽出を行う際に重要です。

```csharp
// Step 3: Run OCR to generate text and layout information (required for structured extraction)
ocrEngine.Recognize();
```

`Recognize()` が完了すると、`ocrEngine` はプレーンテキストと各単語の位置データの両方を保持します。これは次のステップで Aspose に “**how to extract receipt**” フィールドを自動的に抽出させるための基礎となります。

## Step 4 – Layout Recognizer の初期化

Aspose は領収書が一般的にどのように構成されているか（上部に店舗名、日付行、下部に合計）を認識する `LayoutRecognizer` クラスを提供します。設定済みの OCR エンジンを渡すだけです：

```csharp
// Step 4: Initialize the layout recognizer with the OCR engine
var layoutRecognizer = new LayoutRecognizer(ocrEngine);
```

内部では、認識器は通貨記号や日付パターンなどのヒューリスティックを適用し、生テキストを意味的なフィールドにマッピングします。

## Step 5 – 構造化領収書データの抽出

いよいよ楽しい部分です：**extract receipt data**。1 回のメソッド呼び出しで重い処理を行います：

```csharp
// Step 5: Extract structured receipt data (merchant, date, total amount)
var receiptData = layoutRecognizer.ExtractReceiptData();
```

`receiptData` は `ReceiptData` 型のオブジェクトです（`Aspose.OCR.Structured` に定義）。以下の 3 つの主要プロパティを持ちます：

- `Merchant` – 店舗名
- `Date` – 購入日 (`DateTime` 型、検出できた場合)
- `TotalAmount` – 合計金額 (`decimal` 型)

エンジンが特定のフィールドを見つけられなかった場合、プロパティは `null` または `0` になります。必要に応じてフォールバックロジックを追加できます（例: ユーザーに確認を促す）。

## Step 6 – 抽出情報の表示

最後に、結果をコンソールに出力します。ここで作業の成果が確認できます：

```csharp
// Step 6: Display the extracted information
Console.WriteLine($"Merchant: {receiptData.Merchant}");
Console.WriteLine($"Date:     {receiptData.Date:d}");
Console.WriteLine($"Total:    {receiptData.TotalAmount:C}");
```

フォーマット文字列 (`:d` と `:C`) はそれぞれ短い日付と通貨表記を生成し、出力を人間が読みやすい形にします。

### 期待される出力

領収書が “Coffee Corner” に属し、日付が 2025‑12‑01、合計が $4.75 であると仮定すると、コンソールは次のように表示されます：

```
Merchant: Coffee Corner
Date:     12/1/2025
Total:    $4.75
```

いずれかのフィールドが欠けている場合は空行またはデフォルト値が表示されます—デバッグに最適です。

## エッジケースと一般的な落とし穴

### 1. 低解像度画像

領収書画像がぼやけている、または 150 dpi 未満の場合、OCR の精度が大幅に低下します。Aspose に渡す前にシンプルなバイリニアフィルタで画像を拡大すると結果が改善します。

```csharp
ocrEngine.Image = ImageStream.FromFile("receipt.png")
    .Resize(2.0, InterpolationMode.Bilinear);
```

### 2. 英語以外の領収書

基本例は `Language.English` を使用しています。多言語の領収書の場合は、適切な enum（例: `Language.French`）に `Language` を設定するか、分からない場合は `Language.AutoDetect` を使用してください。

### 3. 1 つの画像に複数の領収書がある場合

Aspose のレイアウト認識は画像あたり 1 枚の領収書を想定しています。複数の領収書が横に並んだ写真がある場合は、画像を前処理して各領収書を個別のファイルに切り出してから OCR を実行する必要があります。

### 4. 通貨記号がない場合

合計金額が `$` 記号なしで表示されることがあります。認識器は数値は取得しますが、正しい小数点位置を保証するために文字列を後処理する必要があるかもしれません。

```csharp
if (receiptData.TotalAmount == 0 && rawText.Contains("Total"))
{
    // fallback parsing logic here
}
```

## プロ向けの本番環境でのヒント

- **OCR エンジンをキャッシュ** してください。大量の領収書をバッチ処理する場合、同じインスタンスを再利用することで割り当てオーバーヘッドが減ります。
- **生の OCR テキストをログ** (`ocrEngine.Text`) に残して監査トレイルを確保します。フィールド抽出に失敗したときに役立ちます。
- **全体のフローを try/catch でラップ** し、ユーザーフレンドリーなエラーメッセージを表示します（例: “領収書を読み取れませんでした。より鮮明な画像をアップロードしてください”。）

## 完全動作例

以下は単体で動作するコンソールアプリケーションです。そのままコンパイルして実行できます。画像パスを置き換えるだけで準備完了です。

```csharp
// ------------------------------------------------------------
// How to Use Aspose – Extract Receipt Data from Images (C#)
// ------------------------------------------------------------
using System;
using Aspose.OCR;
using Aspose.OCR.Structured;

namespace ReceiptExtractor
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Create and configure the OCR engine for English language
            var ocrEngine = new OcrEngine
            {
                Language = Language.English
            };

            // 2️⃣ Load the receipt image you want to process
            // 👉 Make sure the file exists; otherwise an exception will be thrown.
            const string imagePath = "YOUR_DIRECTORY/receipt.png";
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // 3️⃣ Run OCR – this also captures layout information
            ocrEngine.Recognize();

            // 4️⃣ Initialize the layout recognizer with the OCR engine
            var layoutRecognizer = new LayoutRecognizer(ocrEngine);

            // 5️⃣ Extract structured receipt data (merchant, date, total amount)
            var receiptData = layoutRecognizer.ExtractReceiptData();

            // 6️⃣ Display the extracted information
            Console.WriteLine($"Merchant: {receiptData.Merchant ?? "Not detected"}");
            Console.WriteLine($"Date:     {(receiptData.Date == DateTime.MinValue ? "Not detected" : receiptData.Date.ToShortDateString())}");
            Console.WriteLine($"Total:    {(receiptData.TotalAmount == 0 ? "Not detected" : receiptData.TotalAmount.ToString("C"))}");

            // Keep the console window open when debugging
            Console.WriteLine("\nPress any key to exit...");
            Console.ReadKey();
        }
    }
}
```

**コードの実行**

1. 新しい .NET コンソールプロジェクトを作成します (`dotnet new console -n ReceiptExtractor`)。
2. Aspose.OCR パッケージを追加します (`dotnet add package Aspose.OCR`)。
3. 生成された `Program.cs` を上記のスニペットに置き換えます。
4. 指定したパスに領収書画像を配置します。
5. ビルドして実行します (`dotnet run`)。

先ほど示した通り、店舗名、日付、合計がコンソールに正確に表示されるはずです。

## まとめ

このガイドでは **Aspose の使い方** を通じて **領収書画像の読み込み**、**ocr receipt image** の実行、そして最終的に **領収書データの抽出** を数行のコードで行う方法を紹介しました。重要なポイントは、Aspose.OCR が重い処理を担ってくれることです—OCR エンジンを設定すれば、`LayoutRecognizer` が生テキストを信頼できる構造化オブジェクトに変換します。

次のステップは？ 抽出した値をデータベースに保存したり、PDF の領収書サマリーを生成したり、さらには機械学習モデルに渡して経費分類に利用したりしてみてください。請求書や出荷ラベルなど他の構造化ドキュメントタイプでも試すことができます—Aspose の `ExtractInvoiceData` も非常に似た方法で動作します。

エッジケースに関する質問や、マルチページ PDF の扱い方を知りたい場合はコメントを残すか、公式の Aspose.OCR ドキュメントで高度なシナリオを確認してください。コーディングを楽しんで、領収書自動化の **Aspose の使い方** のシンプルさを体感してください！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}