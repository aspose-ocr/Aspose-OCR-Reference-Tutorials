---
category: general
date: 2026-01-13
description: Aspose を使用して中国語テキストを認識し、画像からテキストを抽出する方法。ヒンディー語言語パックのダウンロード、ページをテキストに変換する方法などを学びましょう。
draft: false
keywords:
- how to use aspose
- recognize chinese text
- extract text from image
- convert page to text
- download hindi language pack
language: ja
og_description: Aspose OCR を使用して中国語テキストを認識し、画像からテキストを抽出し、ヒンディー語言語パックをダウンロードし、C# でページをテキストに変換する方法。
og_title: Aspose OCR の使い方 – 中国語テキストを認識し、画像テキストを抽出する
tags:
- Aspose
- OCR
- C#
- Image Processing
title: Aspose OCR を使用して中国語テキストを認識する方法 – 完全ガイド
url: /ja/net/text-recognition/how-to-use-aspose-ocr-to-recognize-chinese-text-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose OCR を使用して中国語テキストを認識する方法 – 完全ガイド

クラウドサービスと格闘せずに OCR タスクに **Aspose の使い方** を知りたくありませんか？ あなたは一人ではありません。多くの開発者が **中国語テキストを認識** し、スキャンしたページからデータを取得し、さらにはリアルタイムで言語を切り替える信頼できる方法を必要としています。このチュートリアルでは、画像からテキストを抽出し、**ヒンディー語言語パックをダウンロード**し、**ページをテキストに変換**する方法を示す、完全なエンドツーエンドの例を順に解説します—すべてオフラインで実行できます。

このガイドの最後までに、Chinese‑language TIFF を読み取り、認識された文字を出力できる実行可能な C# コンソール アプリが手に入り、必要に応じて他の言語を追加する方法が分かります。余計な装飾はなく、純粋で実用的な手順だけです。

## 前提条件

- .NET 6.0 SDK（または任意の最新 .NET バージョン）をインストール。
- Visual Studio 2022 または C# 拡張機能付き VS Code。
- Aspose.OCR NuGet パッケージ（`Aspose.OCR`）をプロジェクトに追加。
- サンプル画像（`chinese_page.tif`）を参照できるフォルダーに配置。
- デモを初めて実行する際にインターネット接続が必要（**ヒンディー語言語パックをダウンロード**するため）。

以上です—他に必要なものはありません。さあ、始めましょう。

![Aspose OCR の使用例](/images/how-to-use-aspose-ocr.png "Aspose OCR の使用例")

## 手順 1: Aspose.OCR NuGet パッケージをインストール

**Aspose を使用**するには、まずライブラリが必要です。プロジェクト フォルダーでターミナルを開き、次のコマンドを実行します：

```bash
dotnet add package Aspose.OCR
```

このコマンドは最新の安定版（2026年1月時点、バージョン 23.11）を取得します。パッケージを最新に保つことで、最新の言語パックやパフォーマンス向上が得られます。

## 手順 2: 必要な言語パックをダウンロード（オフライン使用）

Aspose は必要に応じて言語リソースを提供します。後でインターネット接続なしで **中国語テキストを認識** できるように、今回はパックをキャッシュします。また、マルチ言語サポートを示すために **ヒンディー語言語パックをダウンロード** します。

```csharp
using Aspose.OCR;
using Aspose.OCR.Resources;

// Cache Chinese Simplified resources
ResourceManager.Download(OcrLanguage.ChineseSimplified);

// Cache Hindi resources (optional but shown for completeness)
ResourceManager.Download(OcrLanguage.Hindi);
```

> **プロのコツ:** インターネットに接続されたマシンでこのブロックを一度だけ実行してください。その後の実行ではローカルキャッシュからパックが読み込まれ、OCR が完全にオフラインになります。

## 手順 3: OCR エンジンを初期化

`OcrEngine` インスタンスの作成は簡単です。このオブジェクトは設定を保持し、重い処理を実行します。

```csharp
// Step 3: Create the OCR engine
var ocrEngine = new OcrEngine();
```

ノイズの多いスキャンで精度を上げたい場合は、後で `ImagePreprocessingOptions` などの設定を調整できます。ほとんどのクリーンな TIFF ではデフォルト設定で十分です。

## 手順 4: 画像を読み込み、認識を実行

ここでエンジンにソースファイルを指定し、先ほどキャッシュした中国語を使用して **画像からテキストを抽出** するよう指示します。

```csharp
// Step 4: Load the image file
var imagePath = @"YOUR_DIRECTORY/chinese_page.tif";
var ocrImage = OcrImage.FromFile(imagePath);

// Step 5: Recognize the image using Chinese Simplified language
OcrResult ocrResult = ocrEngine.Recognize(ocrImage, OcrLanguage.ChineseSimplified);
```

後でヒンディー語に切り替える場合は、`OcrLanguage.ChineseSimplified` を `OcrLanguage.Hindi` に置き換えるだけです。同じ `ocrEngine` インスタンスを複数の言語で再利用でき、再作成する必要はありません。

## 手順 5: 認識結果の出力

最後に、結果をコンソールに表示するかファイルに書き込みます。ここで **ページをテキストに変換** し、人間が読める形にします。

```csharp
// Step 6: Print the OCR result
Console.WriteLine("=== Recognized Text ===");
Console.WriteLine(ocrResult.Text);
```

プログラムを実行すると、次のような出力が表示されます：

```
=== Recognized Text ===
中华人民共和国成立于1949年...
```

(正確な出力は元の画像に依存します。)

## 完全な動作例

すべての要素を組み合わせた、コピー＆ペーストで使用できる完全なプログラムは以下です：

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Resources;

class PreloadResourcesDemo
{
    static void Main()
    {
        // 1️⃣ Download language packs (offline usage)
        ResourceManager.Download(OcrLanguage.ChineseSimplified);
        ResourceManager.Download(OcrLanguage.Hindi);   // optional

        // 2️⃣ Create OCR engine
        var ocrEngine = new OcrEngine();

        // 3️⃣ Load the image you want to recognize
        var imagePath = @"YOUR_DIRECTORY/chinese_page.tif";
        var ocrImage = OcrImage.FromFile(imagePath);

        // 4️⃣ Perform recognition using Chinese Simplified
        var ocrResult = ocrEngine.Recognize(ocrImage, OcrLanguage.ChineseSimplified);

        // 5️⃣ Output the recognized text
        Console.WriteLine("=== Recognized Text ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

`Program.cs` として保存し、`YOUR_DIRECTORY` を実際のフォルダー パスに置き換えて実行します：

```bash
dotnet run
```

抽出された中国語文字がコンソールに表示されます。

## よくある質問とエッジケース

### 画像の解像度が低い場合は？

Aspose OCR は 300 dpi 以上で最適に動作します。300 dpi 未満のスキャンの場合は、画像のシャープ化を有効にしてください：

```csharp
ocrEngine.ImagePreprocessingOptions.Sharpen = true;
```

### PDF を直接処理できますか？

はい。各 PDF ページを画像に変換（例: `Aspose.PDF` を使用）し、生成されたビットマップを `OcrEngine` に渡します。ワークフローは同じなので、依然として **画像からテキストを抽出** しています。

### マルチページ TIFF をどう扱うか？

`OcrImage.FromFile(path).Frames` を反復処理します。各フレームは個別の画像で、`ocrEngine.Recognize` に渡すことができます。結果を結合して全文書を作成します。

### ヒンディー語パックは中国語 OCR に本当に必要ですか？

いいえ、必要ありませんが、チュートリアルではマルチ言語サポートを示すために **ヒンディー語言語パックをダウンロード** する方法を紹介しています。列挙子の値を変更すれば、サポートされている任意の言語に切り替えられます。

### キャッシュされた言語ファイルはどこに保存されますか？

Aspose はそれらをユーザーのローカル アプリ データ フォルダー（`%APPDATA%\Aspose\OCR\Resources`）に書き込みます。そのフォルダーを削除すると、再ダウンロードが強制されます。

## 精度向上のヒント

- **画像を前処理**: グレースケールに変換、コントラストを上げる、またはデスキュー（傾き補正）を行う。
- `ocrEngine.Language` を `AutoDetect` ではなく単一言語に設定して、結果を高速化する。
- 期待する文字セットが分かっている場合は `ocrEngine.CharactersWhitelist` を使用する（例: 英数字のみ）。

## 結論

ここでは **Aspose の使い方** を通じて **中国語テキストを認識**、**画像からテキストを抽出**、**ヒンディー語言語パックをダウンロード**、そして **ページをテキストに変換** する方法を、コンパクトでオフライン対応の C# コンソール アプリを使って解説しました。手順はシンプルです：NuGet パッケージをインストールし、言語リソースをキャッシュし、`OcrEngine` を作成し、画像を読み込み、認識を実行し、結果を出力します。

これで基本ができたので、フォルダーをバッチ処理したり、ASP.NET API と統合したり、翻訳サービスと組み合わせて多言語パイプラインを構築したりと、ソリューションを拡張できます。可能性は無限です—さまざまな言語を試し、前処理オプションを調整し、OCR 精度の向上を実感してください。

質問がある、または面白いユースケースを共有したい方は、下にコメントを残してください。ハッピーコーディング！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}