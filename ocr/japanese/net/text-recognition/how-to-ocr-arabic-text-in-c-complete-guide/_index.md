---
category: general
date: 2026-05-28
description: Aspose.OCR を使用した C# でのアラビア語 OCR の方法。PNG ファイルからアラビア語テキストを認識し、画像からテキストを抽出し、数分で
  OCR 用に画像を読み込む方法を学びましょう。
draft: false
keywords:
- how to OCR Arabic
- recognize Arabic text
- extract text from image
- recognize text from PNG
- load image for OCR
language: ja
og_description: Aspose.OCR を使用した C# でのアラビア語 OCR の方法。このチュートリアルでは、PNG 画像からアラビア語テキストを認識し、画像からテキストを抽出し、OCR
  用に画像を読み込む方法を示します。
og_title: C#でアラビア語テキストをOCRする方法 – ステップバイステップガイド
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: How to OCR Arabic in C# using Aspose.OCR. Learn to recognize Arabic
    text from PNG files, extract text from image and load image for OCR in minutes.
  headline: How to OCR Arabic Text in C# – Complete Guide
  type: TechArticle
- description: How to OCR Arabic in C# using Aspose.OCR. Learn to recognize Arabic
    text from PNG files, extract text from image and load image for OCR in minutes.
  name: How to OCR Arabic Text in C# – Complete Guide
  steps:
  - name: 1. *What if the Arabic language pack doesn’t download?*
    text: 'Aspose.OCR attempts to fetch the pack from its CDN. If the download fails
      (e.g., due to firewall restrictions), download the `Arabic.zip` manually from
      Aspose’s support portal and set:'
  - name: 2. *Can I OCR multiple images in a loop?*
    text: Absolutely. Just move the `engine.Image = …` line inside a `foreach` that
      iterates over your file list. Re‑using the same `OcrEngine` instance saves memory
      because the language model stays cached.
  - name: 3. *What about mixed‑language documents (Arabic + English)?*
    text: 'Set `engine.Configuration.Language = Language.Multilingual` or specify
      a list like:'
  - name: 4. *Do I need to pre‑process the image?*
    text: For best results, ensure the PNG is high‑contrast and not heavily compressed.
      Simple preprocessing—like converting to grayscale or applying a slight blur
      removal—can be done with `engine.Image = ImageProcessor.ApplyFilters(engine.Image,
      ...)` (Aspose provides a set of filters).
  type: HowTo
tags:
- OCR
- C#
- Aspose
title: C#でアラビア語テキストをOCRする方法 – 完全ガイド
url: /ja/net/text-recognition/how-to-ocr-arabic-text-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#でアラビア語テキストをOCRする方法 – 完全ガイド

C#で**アラビア語をOCRする方法**を、適切なライブラリを探すのに何日もかけずに知りたくありませんか？ あなたは一人ではありません。PNGファイルからアラビア語テキストを認識する必要があると、多くの開発者が壁にぶつかります。特に右から左へ書くスクリプトは少し余分な配慮が必要です。  

このチュートリアルでは、**アラビア語テキストを認識**し、**画像からテキストを抽出**し、Aspose.OCR を使用した **OCR 用の画像のロード** 手順を正確に示す、完全に動作する例を順に解説します。最後まで読むと、コンソールにアラビア語文字列を直接出力する、すぐに実行できるコンソールアプリが手に入ります。

> **得られるもの:** 完全なコードリスト、すべての構成フラグの明確な説明、そして言語パックが欠如している場合や混在方向の文書など、一般的な落とし穴への対処法のヒント。

## 前提条件

- .NET 6.0 SDK 以降（コードは .NET Core 3.1 でも動作します）
- Visual Studio 2022 または C# プロジェクトをビルドできる任意のエディタ
- Aspose.OCR NuGet パッケージ（`Aspose.OCR`） – `dotnet add package Aspose.OCR` でインストール
- アラビア文字が含まれるサンプル PNG 画像（ここでは `arabic_sign.png` と呼びます）

追加の OCR エンジンや外部ツールは不要です。Aspose.OCR はコードを初めて実行したときに、アラビア語の言語データを自動的にダウンロードします。

![How to OCR Arabic example](/images/how-to-ocr-arabic.png "how to OCR Arabic example")

*画像の代替テキスト: 認識されたアラビア語テキストのコンソール出力を示す how to OCR Arabic example.*

## ステップ 1: 新しいコンソールプロジェクトを作成する

まず、コードを単独でテストできるように、新しいコンソールプロジェクトを作成します。

```bash
dotnet new console -n ArabicOcrDemo
cd ArabicOcrDemo
dotnet add package Aspose.OCR
```

> **プロのコツ:** Windows で Visual Studio を好む場合は、*Console App* プロジェクトを作成し、GUI から NuGet パッケージを追加するだけです。

## ステップ 2: OCR エンジンを初期化する

このプロセスの中心は `OcrEngine` クラスです。インスタンス化すると内部の OCR パイプラインが設定されます。

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Enums;

// Step 2: Create an OCR engine instance
var engine = new OcrEngine();
```

*なぜ重要か:* エンジンは言語、テキスト方向、画像ソースなどの構成を保持します。適切に初期化されていないエンジンでは、認識器はどの言語モデルを適用すべきか分かりません。

## ステップ 3: アラビア語の言語とテキスト方向を設定する

アラビア語は右から左へ書く言語なので、エンジンに言語と方向の両方を指示する必要があります。Aspose.OCR は、キャッシュに存在しない場合は自動的にアラビア語言語パックをダウンロードします。

```csharp
// Step 3: Set language to Arabic (auto‑download if missing)
engine.Configuration.Language = Language.Arabic;

// Preserve right‑to‑left ordering for Arabic text
engine.Configuration.TextDirection = TextDirection.RightToLeft;
```

> **エッジケース:** 企業プロキシの背後でコードを実行すると、自動ダウンロードが失敗することがあります。その場合は、Aspose のサイトから言語パックを手動でダウンロードし、`engine.Configuration.LanguageDataPath` をそのフォルダに設定してください。

## ステップ 4: OCR 用に画像をロードする

ここで PNG ファイルをメモリに読み込みます。`ImageStream.FromFile` ヘルパーがファイルを読み取り、Aspose.OCR と互換性のある内部画像表現を作成します。

```csharp
// Step 4: Load the image you want to recognize
engine.Image = ImageStream.FromFile(@"./arabic_sign.png");
```

*なぜこのステップが重要か:* OCR エンジンはファイルパスではなく画像オブジェクトでのみ動作します。`ImageStream.FromFile` を使用するとフォーマット処理が抽象化され、後で JPEG や BMP に差し替えてもコードの他の部分を変更する必要がありません。

## ステップ 5: 認識を実行する

言語、方向、画像がすべて設定されたら、`Recognize()` を呼び出してアラビア語文字列を抽出します。

```csharp
// Step 5: Run the recognition
string recognizedText = engine.Recognize();
```

このメソッドはプレーンな `string` を返します。画像に複数行が含まれる場合、改行文字 (`\n`) で区切られます。

## ステップ 6: 認識されたアラビア語テキストを出力する

最後に、結果をコンソールに出力します。コンソールが Unicode をサポートしていれば、アラビア文字が正しく表示されます（Windows Terminal や VS Code の統合ターミナルで問題なく動作します）。

```csharp
// Step 6: Display the result
Console.WriteLine("Recognized Arabic text:");
Console.WriteLine(recognizedText);
```

**期待される出力（例）:**

```
Recognized Arabic text:
مطار
```

文字化けが見られる場合は、コンソールのコードページが UTF‑8 に設定されているか確認してください。

```cmd
chcp 65001
```

## 完全な動作例

以下はプロジェクトにコピー＆ペーストできる完全な `Program.cs` です。抜け落ちている部分はなく、すぐに実行できるスニペットです。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Enums;

namespace ArabicOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Create OCR engine
            var engine = new OcrEngine();

            // Configure for Arabic language and RTL direction
            engine.Configuration.Language = Language.Arabic;
            engine.Configuration.TextDirection = TextDirection.RightToLeft;

            // Load the PNG image (replace with your actual path)
            engine.Image = ImageStream.FromFile(@"./arabic_sign.png");

            // Run recognition
            string recognizedText = engine.Recognize();

            // Output result
            Console.WriteLine("Recognized Arabic text:");
            Console.WriteLine(recognizedText);
        }
    }
}
```

次のコマンドで実行します:

```bash
dotnet run
```

コンソールにアラビア語のフレーズが表示され、PNG 画像から **アラビア語テキストを正常に認識** したことが確認できます。

## よくある質問への対処

### 1. *アラビア語言語パックがダウンロードされない場合は？*  
Aspose.OCR は CDN からパックの取得を試みます。ダウンロードが失敗した場合（例: ファイアウォールの制限）、Aspose のサポートポータルから `Arabic.zip` を手動でダウンロードし、以下のように設定します：

```csharp
engine.Configuration.LanguageDataPath = @"C:\Aspose\OCR\Languages";
```

### 2. *複数の画像をループで OCR できますか？*  
もちろんです。`engine.Image = …` 行を、ファイルリストを走査する `foreach` の中に移動すれば OK です。同じ `OcrEngine` インスタンスを再利用すると、言語モデルがキャッシュされたままになるためメモリを節約できます。

### 3. *混在言語ドキュメント（アラビア語＋英語）はどうですか？*  
`engine.Configuration.Language = Language.Multilingual` を設定するか、次のようにリストで指定します：

```csharp
engine.Configuration.Language = Language.Arabic | Language.English;
```

### 4. *画像の前処理は必要ですか？*  
最高の結果を得るには、PNG が高コントラストで過度に圧縮されていないことを確認してください。グレースケール変換や軽度のブラー除去などの簡単な前処理は、`engine.Image = ImageProcessor.ApplyFilters(engine.Image, ...)` で実行できます（Aspose はフィルタのセットを提供しています）。

## プロのコツとベストプラクティス

- **エンジンをキャッシュ:** 各画像ごとに新しい `OcrEngine` を作成するとオーバーヘッドが増えます。バッチ処理では単一インスタンスを保持してください。
- **DPI を手動で設定:** ソース画像が低解像度でスキャンされている場合は DPI を手動で設定します。Aspose.OCR は 300 DPI 以上で最適に動作します。
- **生の信頼度スコアを記録:** 認識結果を受け入れるか否か判断する必要があるときは、`engine.Result.Confidence` をログに残します。
- **PDF 変換と組み合わせる:** スキャンした PDF がある場合、各ページを画像として抽出（Aspose.PDF 使用）し、同じ OCR パイプラインに流し込みます。

## 結論

C# と Aspose.OCR を使って **アラビア語を OCR する方法** を、PNG ファイルのロードからクリーンなアラビア文字の抽出まで習得しました。このガイドでは、**アラビア語テキストを認識**するために必要なすべての構成フラグ、**画像からテキストを抽出**する方法、そして **OCR 用に画像をロード**する正確な手順を網羅しました。

ここからは、エンジンに街頭標識の写真をバッチで渡したり、異なる画像フォーマットで実験したり、認識したアラビア語を別の言語に翻訳するための後処理を追加したりしてみてください。可能性は無限で、基本パターンは変わりません。

PNG ファイルからのテキスト認識、他の右から左への言語の取り扱い、OCR の速度最適化など、さらに質問があれば下にコメントを残してください。ハッピーコーディング！

## 関連チュートリアル

- [Aspose.OCR を使用した言語選択付き C# で画像テキストを抽出](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [複数言語対応の Aspose OCR で画像テキストを認識](/ocr/english/net/ocr-settings/working-with-different-languages/)
- [OCR で矩形を準備して画像からテキストを抽出する方法](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}