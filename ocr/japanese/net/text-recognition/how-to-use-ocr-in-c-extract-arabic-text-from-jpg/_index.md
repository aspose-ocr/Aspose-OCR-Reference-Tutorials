---
category: general
date: 2026-03-21
description: C#でOCRを使用して画像ファイルからテキストを認識する方法。JPGからアラビア語テキストを抽出し、プレーンテキストに変換する方法を学びます。
draft: false
keywords:
- how to use OCR
- extract arabic text
- recognize text from image
- image to text c#
- convert jpg to text
language: ja
og_description: C#でOCRを使用して画像ファイルからテキストを認識する方法。このガイドでは、JPGからアラビア語テキストを抽出し、編集可能なテキストに変換する方法を示します。
og_title: C#でOCRを使用する方法 – JPGからアラビア語テキストを抽出
tags:
- OCR
- C#
- Aspose
- Arabic
title: C#でOCRを使用する方法 – JPGからアラビア語テキストを抽出する
url: /ja/net/text-recognition/how-to-use-ocr-in-c-extract-arabic-text-from-jpg/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#でOCRを使用する方法 – JPGからアラビア語テキストを抽出する

ハードドライブに保存されたアラビア語テキストの画像があるとき、**how to use OCR** を考えたことはありませんか？ あなただけではありません。多くの開発者が同じ壁にぶつかります：JPEG があり、その中の文字が必要で、ゼロからニューラルネットを手書きしたくない。  

良いニュースは、数行の C# で **recognize text from image** ファイルからすべてのアラビア文字を抽出し、保存・検索・表示できるクリーンな文字列を得られることです。このチュートリアルでは、ライブラリのインストール、言語モデルの設定、スキャンの実行、結果の出力までの全工程を解説します。最後まで読めば、数秒で **convert JPG to text** ができるようになります。

## 学べること

- .NET 用 Aspose.OCR NuGet パッケージをインストールする。
- 小規模なジョブに最適な CPU モードで OCR エンジンを初期化する。
- アラビア語言語モデルを自動的にロードする。
- JPEG 画像で OCR を実行し、認識されたテキストを取得する。
- 大きなファイルや言語データが欠如している場合など、一般的な落とし穴に対処する。

OCR の事前経験は不要です。C# と Visual Studio の基本的な理解があれば十分です。準備はいいですか？さっそく始めましょう。

## .NET 用 Aspose OCR のインストール

コードを実行する前に Aspose.OCR ライブラリが必要です。NuGet パッケージとして提供されているので、インストールはワンコマンドです：

```bash
dotnet add package Aspose.OCR
```

あるいは Visual Studio の UI が好きな場合は、**Tools → NuGet Package Manager → Manage NuGet Packages for Solution** を開き、**Aspose.OCR** を検索して **Install** をクリックします。パッケージはエンジンが初回使用時にダウンロードする言語データファイルを含め、必要なものすべてを取得します。

> **Pro tip:** プロジェクトは .NET 6 以降をターゲットにしてください。古いフレームワークでも動作しますが、パフォーマンス向上の恩恵を受けられません。

## OCR エンジンの初期化

ライブラリが揃ったので、`OcrEngine` のインスタンスを作成できます。ほとんどの小規模タスクではデフォルトの CPU モードで十分です。CPU モードはホストのプロセッサを使用し、GPU 加速に必要な追加設定を回避します。

```csharp
using Aspose.OCR;
using Aspose.OCR.Settings;

// Initialise the OCR engine (CPU mode is sufficient for small jobs)
var ocrEngine = new OcrEngine();
```

なぜ毎回新しいエンジンを作るのか？ `OcrEngine` オブジェクトは言語、DPI、出力形式などの設定を保持します。単一の操作にスコープを限定することで、クリーンな状態を保証し、異なる言語モデル間での誤動作を防げます。

## アラビア語言語モデルのロード

Aspose はオンデマンドで言語パックを提供します。`Language.Arabic` を初めて設定すると、約 30 MB のデータがローカルのキャッシュフォルダーにダウンロードされます。この一度きりのダウンロードにより、以降の実行は超高速になります。

```csharp
// Choose the language model to load.
// The first assignment triggers an automatic download of the language data (~30 MB).
ocrEngine.Settings.Language = Language.Arabic;
```

追加のスクリプト（たとえば英語やヒンディー語）に対応したい場合は、列挙子の値を変更するだけで済みます。余分なコードは不要です。エンジンは各言語を個別にキャッシュします。

## JPG 画像で OCR を実行する

エンジンとアラビア語モデルの準備ができたら、処理したい画像を指定します。パスは絶対でも相対でも構いませんが、ファイルが存在し読み取り可能であることを確認してください。

```csharp
// Run OCR on the input image.
var recognitionResult = ocrEngine.Recognize(@"YOUR_DIRECTORY/arabic_doc.jpg");
```

**Edge case:** JPEG が非常に大きい（5 MB 超）場合は、先に縮小した方が良いでしょう。大きな画像はメモリ使用量を増やし、認識速度を低下させます。`System.Drawing` や `ImageSharp` を使った事前リサイズで処理時間を大幅に短縮できます。

## 認識されたテキストの取得と表示

`Recognize` メソッドは `OcrResult` オブジェクトを返します。その `Text` プロパティに、エンジンが読み取れたすべてのプレーンテキストが格納されています。

```csharp
// Retrieve the recognised text and output it.
string extractedText = recognitionResult.Text;
Console.WriteLine(extractedText);
```

プログラムを実行すると、コンソールにアラビア文字が元の順序と改行を保ったまま表示されます。テキストをファイルに保存したい場合は、`File.WriteAllText` で書き出すだけです。

### 完全な動作例

すべてを組み合わせた、すぐに実行できるコンソールアプリの例です：

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialise the OCR engine (CPU mode works fine for most cases)
        var ocrEngine = new OcrEngine();

        // 2️⃣ Load the Arabic language pack – triggers a one‑time download (~30 MB)
        ocrEngine.Settings.Language = Language.Arabic;

        // 3️⃣ Specify the image path – replace with your actual file location
        string imagePath = @"YOUR_DIRECTORY/arabic_doc.jpg";

        // 4️⃣ Run OCR and capture the result
        var result = ocrEngine.Recognize(imagePath);

        // 5️⃣ Extract the text and display it
        string extractedText = result.Text;
        Console.WriteLine("=== Extracted Arabic Text ===");
        Console.WriteLine(extractedText);
    }
}
```

**Expected output (example):**

```
=== Extracted Arabic Text ===
هذا نص تجريبي باللغة العربية
تم استخراج هذا النص بنجاح
```

出力が文字化けしている場合は、画像が鮮明かつ言語が `Arabic` に設定されているかを再確認してください。ぼやけたスキャンや回転したページは OCR が失敗しやすい典型的な原因です。

## よくある質問とヒント

- **画像にアラビア語と英語の両方が含まれている場合は？**  
  `ocrEngine.Settings.Language = Language.Multilingual;` と設定すれば、Aspose が自動的に複数スクリプトを検出します。

- **GPU で処理を高速化できるか？**  
  はい。互換性のあるグラフィックカードと CUDA ランタイムがインストールされていれば、デフォルトエンジンを `new OcrEngine(OcrEngineMode.Gpu)` に置き換えてください。

- **UI で右から左への描画をどう扱うか？**  
  生の文字列は Unicode です。WinForms、WPF、ASP.NET などの最新 UI フレームワークは、適切な `FlowDirection` を設定すれば RTL レイアウトを自動的にサポートします。

- **画像サイズに制限はあるか？**  
  技術的にはありませんが、解像度が上がるとメモリ消費も増えます。大量のスキャン（例：書籍全体）を処理する場合は、ページ単位で処理することを検討してください。

## ビジュアル概要

以下は画像ファイルから抽出テキストへのフローを示すシンプルな図です。  

![OCR の使用方法フローダイアグラム – 画像からテキストへの変換](/images/ocr-flow.png)

*Alt text:* *C# で画像からテキストへの変換を示す OCR の使用方法フローダイアグラム。*

## 次のステップ

アラビア語 JPEG に対する **how to use OCR** をマスターしたので、ソリューションを拡張できます：

- **バッチ処理:** フォルダー内の画像をループし、各結果を個別の `.txt` ファイルに書き出す。
- **ポストプロセッシング:** 正規表現を使って余分な句読点や改行を除去する。
- **統合:** 抽出した文字列を検索インデックス（例: Azure Cognitive Search）に投入し、スキャン文書全体の全文検索を実現する。

他の言語に興味がある場合は、`Language` 列挙子の値を入れ替えるだけです。表や手書きメモを抽出したいですか？ Aspose.OCR には認識前にブロックを分割できる `LayoutAnalysis` 機能もあります。

---

### TL;DR

今や **how to use OCR** を C# で使い、JPEG から **extract Arabic text** でき、**recognize text from image** ファイルを効果的に処理し、**convert JPG to text** が可能です。上記の完全な実行例は、NuGet パッケージのインストールから最終文字列の出力までのすべての手順を示しています。サンプル画像を用意し、コードを貼り付けて実行すれば、外部サービス不要で魔法のようにテキストが取得できます。コーディングを楽しんでください！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}