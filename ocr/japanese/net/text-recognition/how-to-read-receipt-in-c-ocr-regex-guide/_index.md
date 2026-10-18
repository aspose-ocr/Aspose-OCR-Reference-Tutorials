---
category: general
date: 2026-02-13
description: Aspose OCRを使って領収書を素早く読み取り、正規表現で金額を抽出する方法。OCRで領収書をステップバイステップで処理する手順を学びましょう。
draft: false
keywords:
- how to read receipt
- extract amount using regex
- regex find total
- process receipt with ocr
language: ja
og_description: Aspose OCR と正規表現を使用して C# で領収書を読み取る方法。このガイドでは、OCR で領収書を処理し、合計金額を抽出する手順を示します。
og_title: C#で領収書を読み取る方法 – 完全OCR＆正規表現チュートリアル
tags:
- OCR
- C#
- Regex
- Aspose
title: C#で領収書を読み取る方法 – OCRと正規表現ガイド
url: /ja/net/text-recognition/how-to-read-receipt-in-c-ocr-regex-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# で領収書を読み取る方法 – OCR + 正規表現ガイド

領収書画像を **手入力せずに読み取る** 方法を考えたことはありませんか？ 多くの小規模ビジネスアプリでは、領収書の写真から合計金額を取得する必要がありますが、手作業で入力すると自動化の意味がなくなります。朗報です！ Aspose OCR を使えばエンジンに重い処理を任せ、シンプルな正規表現で合計金額を抽出できます。このチュートリアルでは **process receipt with OCR** の流れを解説し、正規表現で金額を抽出し、すぐに使える合計値を取得するまでを実演します。

完全に実行可能なサンプルを確認し、領収書言語モデルが重要な理由を学び、通貨記号の違いや “Total” ラベルがないケースなどのエッジケースへの対処法もご紹介します。外部ドキュメントは不要です—必要なものはすべてここにあります。

## 学べること

- 領収書専用の認識を行う Aspose OCR の設定方法（`Receipt` 言語モデルは画像の歪み除去とノイズ除去を自動で行います）。  
- **extract amount using regex** パターンで金額を抽出する正規表現の適用方法（米国スタイルの領収書の多くに対応）。  
- “TOTAL”, “Total:”, “Grand Total – $12.34” など、一般的なバリエーションへの対処法。  
- 結果を安全に出力する方法と、パターンが見つからなかったときの対処法。  

**前提条件**: .NET 6+（または .NET Framework 4.7+）、有効な Aspose OCR ライセンスまたはトライアル、ローカルに保存された領収書画像。これだけです—Aspose.OCR 以外の NuGet パッケージは不要です。

---

## Step 1 – Aspose OCR をインストールしてプロジェクトを準備する

### なぜ重要か

Aspose OCR は **process receipt with OCR** 用に特化したモデルを提供しており、しわくちゃの紙をまっすぐにし、背景ノイズを無視します。汎用テキストモデルを使うと、特に低解像度のスキャンでエラーが増えます。

### コード

```csharp
// Install the package via NuGet first:
//   dotnet add package Aspose.OCR
using Aspose.OCR;
using Aspose.OCR.Enums;
using System.Text.RegularExpressions;

// If you have a license file, load it now (optional but removes trial watermark)
var license = new Aspose.OCR.License();
license.SetLicense("Aspose.OCR.lic");
```

> **プロのコツ:** ライセンスファイルはソース管理フォルダーの外に置き、誤ってコミットしないようにしましょう。

---

## Step 2 – 領収書認識用に OCR エンジンを構成する

### なぜ重要か

`Receipt` 言語モデルには組み込みの歪み除去とノイズ除去があり、折れた紙やしわが多い実際の領収書でも精度が大幅に向上します。

### コード

```csharp
// Step 2: Create and configure the OCR engine for receipt processing
var ocrEngine = new OcrEngine
{
    // Receipt model is optimized for invoices, grocery receipts, etc.
    Language = OcrLanguage.Receipt
};
```

---

## Step 3 – 領収書画像からテキストを認識する

### なぜ重要か

正規表現を適用する前に、生のテキストが必要です。`RecognizeImage` メソッドは `OcrResult` を返し、全文文字列や信頼度スコアなどを取得できます（必要に応じて後で利用可能）。

### コード

```csharp
// Step 3: Recognize text from the receipt image
// Replace the path with the actual location of your receipt file.
string receiptPath = @"C:\Receipts\sample-receipt.jpg";

OcrResult receiptResult = ocrEngine.RecognizeImage(receiptPath);

// Quick sanity check – print the whole OCR output (helps debugging)
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(receiptResult.Text);
Console.WriteLine("===================\n");
```

**期待される OCR 出力（例）**  
```
Walmart Supercenter
123 Main St.
Anytown, USA
Date: 02/12/2026
Item A   $3.45
Item B   $7.89
Subtotal $11.34
Tax      $0.91
Total:   $12.25
Thank you!
```

---

## Step 4 – **Extract Amount Using Regex** 用の正規表現を作成する

### なぜ重要か

領収書の形式は様々ですが、 “Total” という語（または類似語）に続く金額は信頼できるアンカーです。以下のパターンは任意の空白、コロン、ハイフン、そしてオプションの `$` 記号を許容します。

### コード

```csharp
// Step 4: Use a regular expression to locate the total amount in the recognized text
string pattern = @"Total\s*[:\-]?\s*\$?(\d+(\.\d{2})?)";
RegexOptions options = RegexOptions.IgnoreCase;

Match totalMatch = Regex.Match(receiptResult.Text, pattern, options);
```

**パターンの説明**

| 部分 | 意味 |
|------|---------|
| `Total` | “Total” という語を大文字小文字を区別せずに検索 |
| `\s*[:\-]?` | 任意の空白の後、オプションでコロンまたはハイフン |
| `\s*\$?` | 任意の空白とオプションのドル記号 |
| `(\d+(\.\d{2})?)` | 1 桁以上の数字、オプションで小数点と 2 桁のセント |

---

## Step 5 – 抽出した合計を出力するか、データ欠損時の処理を行う

### なぜ重要か

最高の OCR でも、ぼやけた領収書では単語が抜け落ちることがあります。優雅なフォールバックを用意すればクラッシュを防ぎ、カスタムロジック（例: ユーザーに確認を求める）を実装できます。

### コード

```csharp
// Step 5: Output the extracted total, or indicate it wasn't found
if (totalMatch.Success)
{
    string amount = totalMatch.Groups[1].Value;
    Console.WriteLine($"Total: ${amount}");
}
else
{
    Console.WriteLine("Total amount not found. Consider reviewing the OCR output manually.");
}
```

**コンソール出力例**

```
Total: $12.25
```

---

## 完全動作サンプル – すべての手順を 1 ファイルにまとめた例

以下はコンソールプロジェクトにそのまま貼り付け可能な、単一ファイルの自己完結型プログラムです。コメント、エラーハンドリング、オプションのライセンス読み込みを含んでいます。

```csharp
// ---------------------------------------------------------------
// How to Read Receipt in C# – OCR + Regex (Complete Example)
// ---------------------------------------------------------------
using Aspose.OCR;
using Aspose.OCR.Enums;
using System;
using System.Text.RegularExpressions;

class Program
{
    static void Main()
    {
        // 0️⃣ Optional: Load your Aspose OCR license (remove trial watermark)
        try
        {
            var license = new Aspose.OCR.License();
            license.SetLicense("Aspose.OCR.lic"); // path to .lic file
        }
        catch (Exception ex)
        {
            Console.WriteLine("License not found – running in trial mode.");
        }

        // 1️⃣ Configure the OCR engine for receipt processing
        var ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.Receipt // receipt model = de‑skew + de‑noise
        };

        // 2️⃣ Path to the receipt image (change to your file)
        string receiptPath = @"YOUR_DIRECTORY/receipt.jpg";

        // 3️⃣ Perform OCR
        OcrResult receiptResult = ocrEngine.RecognizeImage(receiptPath);

        // 4️⃣ Debug: show full OCR text (helps when regex fails)
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(receiptResult.Text);
        Console.WriteLine("===================\n");

        // 5️⃣ Regex to **extract amount using regex** (find the total)
        string pattern = @"Total\s*[:\-]?\s*\$?(\d+(\.\d{2})?)";
        Match totalMatch = Regex.Match(receiptResult.Text, pattern,
                                        RegexOptions.IgnoreCase);

        // 6️⃣ Output
        if (totalMatch.Success)
        {
            string amount = totalMatch.Groups[1].Value;
            Console.WriteLine($"Total: ${amount}");
        }
        else
        {
            Console.WriteLine("Total amount not found. You might need to adjust the regex or improve image quality.");
        }
    }
}
```

**プログラムの実行手順**

1. 新しいコンソールプロジェクトを作成する（`dotnet new console -n ReceiptReader`）。  
2. Aspose.OCR NuGet パッケージを追加する（`dotnet add package Aspose.OCR`）。  
3. `YOUR_DIRECTORY/receipt.jpg` を実際の領収書画像パスに置き換える。  
4. ビルドして実行する（`dotnet run`）。  

すべてが正しく設定されていれば、OCR のダンプに続いて `Total: $xx.xx` が表示されます。

---

## エッジケースと一般的なバリエーションへの対処

### 1. 異なる通貨記号

ユーロ（€）やポンド（£）を扱う場合は、パターンを拡張します：

```csharp
string pattern = @"Total\s*[:\-]?\s*[$€£]?\s*(\d+(\.\d{2})?)";
```

### 2. “Total” ラベルがない場合

一部の領収書では “Grand Total” だけが表示されます。代替表現を追加します：

```csharp
string pattern = @"(?:Total|Grand\s*Total)\s*[:\-]?\s*[$]?\s*(\d+(\.\d{2})?)";
```

### 3. 複数の合計がある場合（例: “Subtotal” と “Total”）

正規表現が最初の一致を返す場合、**最後** の一致を取得したいことがあります：

```csharp
MatchCollection matches = Regex.Matches(receiptResult.Text, pattern,
                                         RegexOptions.IgnoreCase);
Match last = matches.Count > 0 ? matches[matches.Count - 1] : null;
```

### 4. 低解像度画像

- スキャン時に DPI を上げる（`300 DPI` が目安）。  
- Aspose に渡す前に簡易的なぼかし除去フィルタで前処理する（本ガイドの範囲外ですが、検討に値します）。

---

## 実務プロジェクト向けのプロティップ

- 複数フィールド（税額、項目など）を抽出する場合は **OCR 結果をキャッシュ** しておくと、OCR コストを一度だけに抑えられます。  
- **生の OCR テキストをデータベースにログ** しておくと、費用争議時の貴重な監査証跡になります。  
- Web API を構築する際は **バックグラウンドワーカーで OCR を実行** しましょう。数百ミリ秒かかりますが、非同期処理なら問題ありません。同期リクエストでは避けた方が無難です。  
- 永続化前に **抽出した金額をビジネスルールで検証**（例: 金額は 0 より大きい）してください。

---

## 結論

C# で Aspose OCR を使い **領収書画像を読み取る方法** と、**extract amount using regex** で合計行を確実に取得する手順を解説しました。`Receipt` 言語モデルを活用すれば、歪み除去・ノイズ除去されたテキストが得られ、シンプルな正規表現でほとんどの書式の違いに対応できます。上記のコードスニペットは任意の .NET コンソールまたはサービスプロジェクトにすぐ組み込め、エッジケースへの追加提案で本番環境でも安心して利用できます。

次のステップに進みませんか？ 個別の明細項目を抽出したり、税額を自動計算したり、経費管理 API と統合したりしてみましょう。パターンに合わない領収書に遭遇した場合は、**regex find total** アプローチは出発点に過ぎません—ロケールに合わせてパターンを調整すれば対応可能です。

Happy coding, and may your receipt‑processing be fast, accurate, and completely automated!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}