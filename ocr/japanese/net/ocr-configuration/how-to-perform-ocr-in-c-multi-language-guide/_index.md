---
category: general
date: 2026-04-29
description: Aspose OCR を使用して C# で OCR を実行する方法 – ヒンディー語テキストを抽出し、PNG からテキストを認識し、OCR
  言語をリアルタイムで変更する
draft: false
keywords:
- how to perform OCR
- extract Hindi text
- multi language OCR
- recognize text from PNG
- change OCR language
language: ja
og_description: Aspose OCR を使用した C# での OCR の実行方法。ヒンディー語テキストの抽出、PNG ファイルからのテキスト認識、OCR
  言語の動的変更を学びましょう。
og_title: C#でOCRを実行する方法 – 完全マルチ言語チュートリアル
tags:
- OCR
- C#
- Aspose
title: C#でOCRを実行する方法 – 多言語ガイド
url: /ja/net/ocr-configuration/how-to-perform-ocr-in-c-multi-language-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#でOCRを実行する方法 – マルチランゲージ ガイド

複数の言語が含まれる画像で **OCR を実行する方法** を疑問に思ったことはありませんか？たとえば、ロシア語のレシートとヒンディー語のチラシが並んでいて、別々のツールを使い分けずに両方のテキストを取得したいとします。これは国際文書を扱う人にとって共通の悩みです。

このチュートリアルでは、Aspose OCR を使用して **OCR を実行** するクリーンでエンドツーエンドな方法、ヒンディー語テキストの抽出、PNG ファイルからのテキスト認識、さらには **OCR 言語の変更** をリアルタイムで行う方法を示します。最後まで読むと、サポートされている任意の言語の組み合わせで動作する再利用可能なコードスニペットが手に入ります。

## 学習内容

- .NET プロジェクトで Aspose OCR エンジンを設定する方法。
- 静的言語の設定と、実行時に言語を切り替える違い。
- 画像からヒンディー語テキストを抽出する方法と、ライブラリが言語パックを自動でダウンロードできる理由。
- PNG ファイルの取り扱い、欠落した言語モジュールへの対処、一般的な落とし穴のトラブルシューティングのヒント。

> **プロのコツ:** すでに単一言語で Aspose OCR を使用している場合は、数行変更するだけで **マルチランゲージ OCR** ソリューションに変換できます。

---

## 前提条件

| 前提条件 | 理由 |
|----------|------|
| .NET 6 以降（または .NET Framework 4.7+） | Aspose OCR は最新ランタイムを対象としており、古いバージョンでは言語パックの自動ダウンロードがサポートされない可能性があります。 |
| Aspose.OCR NuGet パッケージ (`Install-Package Aspose.OCR`) | `OcrEngine` クラスと語言語列挙体を提供します。 |
| 既知のフォルダーに配置したサンプル PNG 画像 2 枚（`russian.png` と `hindi.png`） | **recognize text from PNG** と **extract Hindi text** を単一実行でデモします。 |
| インターネット接続（新しい言語を初めて要求する際） | ライブラリは必要な言語モジュールをオンデマンドで取得します。 |

追加の OCR バイナリや外部ツールは不要です—Aspose がすべての重い処理を行います。

---

## 手順 1 – Aspose OCR をインストールしてエンジンを作成する

まず最初に、Aspose OCR パッケージをプロジェクトに追加します。Package Manager Console を開き、次のコマンドを実行してください。

```powershell
Install-Package Aspose.OCR
```

これで `OcrEngine` インスタンスを作成できます。エンジンは実行時に再構成可能なスマートスキャナーと考えてください。

```csharp
using Aspose.OCR;
using System;

class MultiLanguageOcrDemo
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        var ocrEngine = new OcrEngine();
```

なぜエンジンを一度だけ作成するのでしょうか？同じインスタンスを再利用することで、ネイティブ OCR ライブラリの読み込みオーバーヘッドを繰り返し回避でき、大量バッチで顕著になることがあります。

---

## 手順 2 – ロシア語テキストを認識する（最初の言語）

ヒンディー語に進む前に、エンジンが既知の言語で動作することを確認しましょう。言語をロシア語に設定し、PNG を入力して結果を出力します。

```csharp
        // Step 2: Configure the engine for Russian and recognize the image
        ocrEngine.Config.Language = OcrLanguage.Russian;
        var russianImagePath = @"YOUR_DIRECTORY/russian.png";
        var russianOcrResult = ocrEngine.Recognize(OcrEngine.LoadImage(russianImagePath));
        Console.WriteLine("Russian: " + russianOcrResult.Text);
```

**内部で何が起きているか？**

`OcrEngine.LoadImage` は PNG を Aspose の内部ビットマップ形式で読み込みます。`Config.Language` プロパティは OCR エンジンに使用する辞書と文字セットを指示します。`Recognize` を呼び出すと、エンジンはキリル文字用に調整されたニューラルネットワークモデルを実行し、プレーンテキスト出力を含む `OcrResult` オブジェクトを返します。

> **期待される出力（例）**  
> `Russian: Привет, мир! Это тестовое изображение.`

文字化けが発生した場合は、画像が破損していないか、ロシア語言語モジュールが存在するか（基本パッケージに同梱）を再確認してください。

---

## 手順 3 – ヒンディー語に切り替える – **OCR 言語の変更** を動的に

さあ、楽しい部分です：エンジンを再作成せずに言語を切り替えます。Aspose OCR は初回リクエスト時にヒンディー語モジュールをダウンロードするので、インターネット接続は一度だけ必要です。

```csharp
        // Step 3: Switch the engine to Hindi (the language module will be downloaded automatically) and recognize the image
        ocrEngine.Config.Language = OcrLanguage.Hindi;
        var hindiImagePath = @"YOUR_DIRECTORY/hindi.png";
        var hindiOcrResult = ocrEngine.Recognize(OcrEngine.LoadImage(hindiImagePath));
        Console.WriteLine("Hindi: " + hindiOcrResult.Text);
    }
}
```

**なぜこれが機能するのか？**

`Config.Language` のセッターが遅延ロードの手順をトリガーします。要求された言語パックがディスクに存在しない場合、Aspose は CDN にアクセスし、圧縮モジュールを取得してキャッシュし、その後認識を続行します。この設計により、実行時にコンテンツに合わせて適応する **マルチランゲージ OCR** パイプラインを構築できます。

> **サンプルヒンディー語出力**  
> `Hindi: नमस्ते दुनिया! यह एक परीक्षण छवि है।`

同じ `ocrEngine` オブジェクトがキリル文字とデーヴァナーガリー文字の両方をシームレスに処理できることに注目してください。これが **OCR 言語の変更** をリアルタイムで行う力です。

---

## 手順 4 – PNG ファイルを効率的に扱う

上記の例はどちらも PNG 画像を使用しています。PNG はスクリーンショットやスキャン文書で一般的なフォーマットです。PNG はロスレスで、ピクセルデータがそのまま保持されるため OCR に最適です。ただし、大きな PNG はメモリを多く消費します。以下に簡単なヒントをいくつか示します：

1. **必要に応じてリサイズ** – 画像の幅が 2000 px を超える場合、`System.Drawing.Image` で縮小してから Aspose に渡します。
2. **DPI を設定** – 一部の OCR エンジンは 300 DPI が有利です。カスタム解像度を持つ `Bitmap` を受け取る `OcrEngine.LoadImage` のオーバーロードで埋め込めます。

```csharp
using System.Drawing;

// Example of downscaling a huge PNG
Bitmap original = new Bitmap(@"YOUR_DIRECTORY/large.png");
int maxWidth = 2000;
if (original.Width > maxWidth)
{
    int newHeight = (int)((double)original.Height / original.Width * maxWidth);
    Bitmap resized = new Bitmap(original, new Size(maxWidth, newHeight));
    original.Dispose(); // free original memory
    original = resized;
}
var result = ocrEngine.Recognize(OcrEngine.LoadImage(original));
```

これらの調整によりメモリ使用量が抑えられ、OCR エンジンが扱いやすいピクセルグリッドで動作するため、精度が向上することが多いです。

---

## 手順 5 – すべてを統合する – 完全動作サンプル

以下は、**OCR の実行方法**、**ヒンディー語テキストの抽出**、**PNG からのテキスト認識**、そしてエンジンを再起動せずに **OCR 言語の変更** をデモする、完全に実行可能なプログラムです。

```csharp
using Aspose.OCR;
using System;
using System.Drawing;

class MultiLanguageOcrDemo
{
    static void Main()
    {
        // Create a single OCR engine instance (re‑use it for all languages)
        var ocrEngine = new OcrEngine();

        // ----------- Russian ----------
        ocrEngine.Config.Language = OcrLanguage.Russian;
        var russianPath = @"YOUR_DIRECTORY/russian.png";
        var russianResult = ocrEngine.Recognize(OcrEngine.LoadImage(russianPath));
        Console.WriteLine("Russian: " + russianResult.Text);

        // ----------- Hindi ------------
        // The first time this runs, the Hindi language pack will be downloaded automatically.
        ocrEngine.Config.Language = OcrLanguage.Hindi;
        var hindiPath = @"YOUR_DIRECTORY/hindi.png";
        var hindiResult = ocrEngine.Recognize(OcrEngine.LoadImage(hindiPath));
        Console.WriteLine("Hindi: " + hindiResult.Text);

        // ----------- Optional PNG optimization ----------
        // If you have very large PNGs, resize them before recognition (example shown earlier).
        // This block is optional and can be removed if your images are already sized appropriately.
    }
}
```

**コードを実行**すると、次のような出力が得られます。

```
Russian: Привет, мир! Это тестовое изображение.
Hindi: नमस्ते दुनिया! यह एक परीक्षण छवि है।
```

これらの行が表示されたら、成功です—単一エンジンで **ヒンディー語テキストの抽出** と **PNG ファイルからのテキスト認識** ができる **マルチランゲージ OCR** ソリューションを構築できました。

---

## よくある質問 (FAQ)

| 質問 | 回答 |
|------|------|
| *Aspose OCR のライセンスは必要ですか？* | 無料の評価キーでテストは可能ですが、本番環境での使用には商用ライセンスが必要です。 |
| *1 つの画像で 2 つ以上の言語を認識できますか？* | はい。`Config.Language` を `OcrLanguage.Multiple` に設定し、カンマ区切りのリスト（例: `Russian, Hindi`）を渡します。 |
| *言語モジュールのダウンロードに失敗した場合は？* | ファイアウォールやプロキシ設定を確認してください。また、Aspose ポータルからモジュールを事前にダウンロードし、`Data` フォルダーに配置することもできます。 |
| *PNG が唯一のサポート形式ですか？* | いいえ。Aspose OCR は JPEG、BMP、TIFF、PDF（画像として）も扱えます。PNG はロスレス品質の一般的な選択肢に過ぎません。 |

---

## 次のステップと関連トピック

- **バッチ処理** – PNG ディレクトリをループし、結果を CSV ファイルに保存する。  
- **PDF 抽出** – `OcrEngine.RecognizePdf` を使用してスキャン PDF からテキストを取得する。  
- **カスタム辞書** – ユーザー提供の単語リストで組み込み言語パックを拡張し、ドメイン固有の語彙に対応する。  
- **パフォーマンスチューニング** – 大量画像セットを扱う際に `Parallel.ForEach` で呼び出しを並列化する。

これらの領域を探求することで、さまざまなシナリオで **OCR を実行する方法** の習熟度が高まります。

---

## 結論

これで、Aspose OCR を使用した C# での **OCR の実行方法**、リアルタイムでの言語切替、そして PNG 画像からの **ヒンディー語テキストの抽出** を習得しました。重要なポイントは、単一の `OcrEngine` インスタンスが多用途な **マルチランゲージ OCR** の仕事馬として機能することです—`Config.Language` を設定すれば、残りはライブラリが処理します。

コードを実行し、サンプル画像を自分の画像に置き換えて、追加の言語で実験してみてください。Aspose OCR の柔軟性により、簡単なプロトタイプから本番レベルの文書処理パイプラインへ、最小限の変更でスケールできます。

コーディングを楽しんで、テキスト抽出の冒険がエラーなく進むことを願っています！

![how to perform OCR example](/images/ocr-demo.png "how to perform OCR example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}