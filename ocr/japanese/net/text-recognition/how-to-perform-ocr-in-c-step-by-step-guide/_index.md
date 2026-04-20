---
category: general
date: 2026-02-14
description: Aspose.OCR を使用した C# での OCR の実行方法 – 画像からテキストを抽出し、ファイルから画像を読み込み、画像上で OCR
  を迅速に実行する方法を学びます。
draft: false
keywords:
- how to perform OCR
- extract text from image
- load image from file
- recognize text from jpg
- run OCR on image
language: ja
og_description: Aspose.OCR を使用した C# での OCR の実行方法。このガイドでは、画像からテキストを抽出し、ファイルから画像を読み込み、画像上で効率的に
  OCR を実行する方法を示します。
og_title: C#でOCRを実行する方法 – 完全プログラミングチュートリアル
tags:
- OCR
- C#
- Aspose
- Image Processing
title: C#でOCRを実行する方法 – ステップバイステップガイド
url: /ja/net/text-recognition/how-to-perform-ocr-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#でOCRを実行する方法 – 完全プログラミングチュートリアル

スマートフォンで撮った写真で **how to perform OCR**（OCRの実行方法）を知りたくなったことはありませんか？ナビゲーションアプリ用に JPEG から道路標識のテキストを取得したり、スキャンした契約書のバッチを検索可能なテキストに変換したりしたいかもしれません。要するに、*extract text from image*（画像からテキストを抽出）をクラウドに送信せずに行いたいということです。

良いニュースは、Aspose.OCR for .NET を使えばすべてローカルで実行できることです。このチュートリアルでは、ファイルから画像を読み込む方法、JPG からテキストを認識する方法、そして最終的に **run OCR on image** ファイルを完全にオフラインで実行する方法を順に解説します。最後まで読むと、認識されたアラビア語テキストをコンソールに出力する、すぐに実行できるスニペットが手に入ります。

> **What you’ll get:** 自己完結型の実行可能な C# プログラム、各行が重要な理由の説明、そしてリソースが見つからない、またはサポートされていない言語といった一般的なエッジケースの対処法に関するヒント。

## 前提条件

本格的に始める前に、以下が揃っていることを確認してください。

| 要件 | 理由 |
|-------------|--------|
| .NET 6.0 or later (or .NET Framework 4.7+) | Aspose.OCR は .NET Standard 2.0 を対象としているため、最新のランタイムであればどれでも動作します。 |
| Visual Studio 2022 (or VS Code with C# extension) | IDE を使用すると、NuGet パッケージの管理やコンソール アプリの実行が容易になります。 |
| Aspose.OCR NuGet package (`Aspose.OCR`) | 実際に OCR 処理を行うライブラリです。 |
| A folder containing the offline OCR resources (download from Aspose) | オフライン OCR リソースが格納されたフォルダー（Aspose からダウンロード）。 |
| An image file (e.g., `arabic_sign.jpg`) | アラビア語テキストを含む JPEG を使用しますが、任意の言語でも動作します。 |

これらが揃っていない場合は、今すぐ入手してください。途中で依存関係が欠けていることに気付くのは無駄です。

## 手順 1: Aspose.OCR のインストールとリソースの準備

まず、プロジェクトに Aspose.OCR パッケージを追加します。

```bash
dotnet add package Aspose.OCR
```

パッケージをインストールしたら、Aspose のウェブサイトから **offline OCR resource bundle** をダウンロードします。例として、マシン上のフォルダーに展開してください。

```
C:\OCRResources\
```

> **Why this matters:** 起動時にリソースを一度だけロードすることで、ネットワーク遅延がなくなり、データが外部に送信されないため GDPR に配慮したソリューションとなります。

## 手順 2: OCR エンジンの作成とリソースフォルダーの指定

ここでは `Engine` クラスのインスタンスを作成し、リソースの場所を指定します。これがローカルで **how to perform OCR** を実行するための核心です。

```csharp
using Aspose.OCR;
using Aspose.OCR.Settings;

// Step 2: Initialize the OCR engine with the offline resource folder
Engine ocrEngine = new Engine
{
    // Replace with the path you used in the previous step
    ResourceFolder = @"C:\OCRResources"
};

// Load the resources into memory – this prevents any hidden HTTP calls
ocrEngine.LoadResources();
```

> **Pro tip:** フォルダー パスが間違っている可能性がある場合は、`LoadResources` 呼び出しを try‑catch ブロックでラップしてください。例外メッセージに欠落しているファイルが正確に示されます。

## 手順 3: 画像をファイルからロードする

次に、エンジンが解析できるように **load image from file** が必要です。Aspose.OCR は独自の `ImageStream` ラッパーを使用します。

```csharp
// Step 3: Load the JPEG you want to recognize
ImageStream image = ImageStream.FromFile(@"C:\OCRResources\arabic_sign.jpg");
```

画像が別の場所にある場合は、パスを変更するだけです。`ImageStream` クラスは基盤となるビットマップ処理を抽象化しているため、GDI+ の互換性を気にする必要はありません。

## 手順 4: 言語設定を使用して JPG からテキストを認識する

ここからが **how to perform OCR** の核心です—実際に文字を認識します。アラビア語認識を要求しますが、`Language.Arabic` を他のサポートされている言語に置き換えることもできます。

```csharp
// Step 4: Run OCR specifying the desired language (Arabic in this example)
OcrResult ocrResult = ocrEngine.Recognize(
    image,
    new OcrOptions { Language = Language.Arabic }
);
```

> **Why specify a language?** OCR エンジンは言語固有の辞書と文字モデルを使用します。正しい言語を指定することで、特にアラビア語のような形状が複雑なスクリプトの精度が大幅に向上します。

## 手順 5: 抽出したテキストを表示する

最後に、**extract text from image** を実行し、結果を出力しましょう。これが OCR が成功したかを確認する最も簡単な方法です。

```csharp
// Step 5: Output the recognized text to the console
Console.WriteLine("=== OCR Result ===");
Console.WriteLine(ocrResult.Text);
```

プログラムを実行すると、サインに記載されたアラビア語のフレーズがコンソールに表示されます。出力が文字化けしている場合は、正しい言語が選択されているか、リソースフォルダーにアラビア語のデータファイルが含まれているかを再確認してください。

## 完全な動作例

以下は、すべての手順を統合した、コンパイル可能な完全なプログラムです。新しいコンソール プロジェクト（`dotnet new console`）にコピー＆ペーストし、**F5** を押して実行してください。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 1: Configure the OCR engine with offline resources
            // -------------------------------------------------
            Engine ocrEngine = new Engine
            {
                ResourceFolder = @"C:\OCRResources" // <-- change to your folder
            };
            ocrEngine.LoadResources(); // Loads language packs, fonts, etc.

            // -------------------------------------------------
            // Step 2: Load the image you want to process
            // -------------------------------------------------
            ImageStream image = ImageStream.FromFile(@"C:\OCRResources\arabic_sign.jpg");

            // -------------------------------------------------
            // Step 3: Recognize text – specify language to improve accuracy
            // -------------------------------------------------
            OcrResult ocrResult = ocrEngine.Recognize(
                image,
                new OcrOptions { Language = Language.Arabic } // Change as needed
            );

            // -------------------------------------------------
            // Step 4: Output the result
            // -------------------------------------------------
            Console.WriteLine("=== OCR Result ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

**期待される出力（例）:**

```
=== OCR Result ===
مطار القاهره الدولي
```

画像を英語のサインに置き換え、`Language.English` を設定すれば、同じコードで英語テキストが出力されます。これにより **run OCR on image** の柔軟性が示されます。

## Extract Text from Image – 一般的なシナリオの処理

### 1. 複数ページまたはマルチフレーム画像

TIFF のような一部の画像形式は複数ページを含むことがあります。そのような場合に **extract text from image** を行うには、各フレームをループ処理します。

```csharp
for (int i = 0; i < image.FramesCount; i++)
{
    image.CurrentFrame = i;
    OcrResult pageResult = ocrEngine.Recognize(image, new OcrOptions { Language = Language.English });
    Console.WriteLine($"Page {i + 1}: {pageResult.Text}");
}
```

### 2. 低解像度画像

OCR の精度は 70 dpi 未満になると大幅に低下します。結果がぼやけている場合は、まず画像を拡大することを検討してください。

```csharp
using System.Drawing;
using System.Drawing.Drawing2D;

// Load as Bitmap, resize, then wrap back into ImageStream
Bitmap bmp = new Bitmap(@"C:\OCRResources\lowres.jpg");
Bitmap highRes = new Bitmap(bmp, new Size(bmp.Width * 2, bmp.Height * 2));
ImageStream highResStream = ImageStream.FromBitmap(highRes);
```

### 3. 言語パックが欠如している場合

例外 *“Language data not found”* が発生した場合は、対応する `.dat` ファイルが `ResourceFolder` に存在するか確認してください。Aspose は言語ごとに別々の zip を提供しています。

## Run OCR on Image – パフォーマンスのヒント

- **Cache the Engine:** 各画像ごとに新しい `Engine` を作成するとオーバーヘッドが増えます。バッチ処理では単一のインスタンスを維持してください。
- **Parallelize Safely:** `LoadResources` 後、`Engine` は読み取り専用操作に対してスレッドセーフです。異なる画像に対して `Recognize` を呼び出す複数のタスクを起動できます。
- **Dispose When Done:** `Engine` は `IDisposable` を実装していますが、.NET の GC が最終的にクリーンアップします。`using` ブロックで `ocrEngine.Dispose()` を明示的に呼び出すのが良い習慣です。

```csharp
using (Engine ocrEngine = new Engine { ResourceFolder = @"C:\OCRResources" })
{
    ocrEngine.LoadResources();
    // run recognitions here
}
```

## Recognize Text from JPG – 注意すべきエッジケース

| 状況 | 確認項目 | 対策 |
|-----------|---------------|-----|
| **Corrupted JPEG** | `ImageStream.FromFile` が `FileNotFoundException` または `ArgumentException` をスローします。 | ファイルの整合性を確認し、必要なら画像をグラフィックエディタで再保存してください。 |
| **Unsupported language** | `Language` 列挙体に対象言語が含まれていません。 | Aspose.OCR を最新バージョンに更新してください。新しい言語が定期的に追加されています。 |
| **Mixed‑script images** (e.g., English + Arabic) | 単一の言語オプションでは二次的なスクリプトが認識されない可能性があります。 | 異なる言語オプションで OCR を二回実行し、結果を結合してください。 |

## まとめ – C#でOCRを実行する方法が分かりました

このガイドでは、Aspose.OCR を使用した **how to perform OCR** の手順を、NuGet パッケージのインストールから認識テキストの出力までカバーしました。**load image from file**、**extract text from image**、**recognize text from jpg**、そして安全に **run OCR on image** を本番環境向けに実行する方法を学びました。

### 次のステップは？

- **Experiment with other file formats**（PNG や BMP など）を試してみましょう。ファイル拡張子を変更するだけです。
- **Integrate with a database** で OCR 結果を保存し、検索可能なアーカイブを作成します。
- **Combine with computer‑vision**（例：OCR 前にテキスト領域を検出）で速度向上を図ります。

言語設定を調整したり、フォルダーをバッチ処理したり、出力を Web API に接続したりして自由にカスタマイズしてください。OCR は基礎的なブロックであり、より大きなワークフローに組み込むことで本当の力が発揮されます。

コーディングを楽しんで、画像が常にクリアでありますように！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}