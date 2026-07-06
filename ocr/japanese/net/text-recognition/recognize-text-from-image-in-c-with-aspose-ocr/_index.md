---
category: general
date: 2026-02-22
description: Aspose OCR を使用して C# で画像からテキストを認識する。PNG からテキストを抽出し、画像をテキストに変換し、ライセンス用に埋め込みリソースを読み取るステップバイステップガイド。
draft: false
keywords:
- recognize text from image
- extract text from png
- convert image to text
- read embedded resource c#
- perform ocr on image
language: ja
og_description: Aspose OCRで画像からテキストを瞬時に認識。pngからテキストを抽出し、画像をテキストに変換し、シームレスなライセンスのために埋め込みリソースをC#で読み取る方法を学びましょう。
og_title: C#で画像からテキストを認識する – 完全なAspose OCRチュートリアル
tags:
- OCR
- C#
- Aspose
- Image Processing
title: C# と Aspose OCR を使用して画像からテキストを認識する
url: /ja/net/text-recognition/recognize-text-from-image-in-c-with-aspose-ocr/
---

Now produce final translation.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# で Aspose OCR を使って画像からテキストを認識する

画像からテキストを **認識したい** が、C# で何から始めればいいか分からないことはありませんか？ 開発者の多くが OCR に初めて触れるときに同じ壁にぶつかります。このチュートリアルでは、**png からテキストを抽出する**、**画像をテキストに変換する**、さらには **C# の埋め込みリソースからライセンスを読み込む** 方法を、手間なく実装できるソリューションとして紹介します。

埋め込み Aspose OCR ライセンスの読み込みから、最終的にコンソールへ文字列を出力するまでをすべてカバーします。最後まで読めば、任意の .NET プロジェクトに貼り付けてすぐに動かせる、自己完結型のプログラムが手に入ります。

## 必要なもの

- **.NET 6 以上**（コードは .NET Framework でもコンパイル可能ですが、現在の LTS は .NET 6 です）
- **Aspose.OCR for .NET** NuGet パッケージ（バージョン 23.9 以降）
- 明瞭な英字テキストが印刷された **サンプル PNG** 画像
- **Aspose OCR ライセンスファイル**（`Aspose.OCR.lic`）を *Embedded Resource* としてプロジェクトに追加  

これらに心当たりがなくても大丈夫です。以下の手順で取得・設定方法を順に説明します。

## 手順 1: 埋め込みリソースの C# ライセンスを読み込む  

OCR エンジンが動作する前に、Aspose に有効なライセンスが必要です。`.lic` ファイルを埋め込みリソースとして保持すれば、ソースツリーから除外でき、デプロイも楽になります。

```csharp
using System;
using System.Reflection;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // ------------------------------------------------------------
        // 1️⃣ Load the embedded Aspose OCR license
        // ------------------------------------------------------------
        var assembly = Assembly.GetExecutingAssembly();

        // The resource name follows the folder hierarchy in the project.
        // Adjust "MyApp.Resources.Aspose.OCR.lic" if yours differs.
        using (var licenseStream = assembly.GetManifestResourceStream(
               "MyApp.Resources.Aspose.OCR.lic"))
        {
            if (licenseStream == null)
            {
                Console.Error.WriteLine(
                    "License file not found. Make sure it's marked as Embedded Resource.");
                return;
            }

            var license = new License();
            license.SetLicenseFromStream(licenseStream);
        }

        // Continue with OCR steps...
```

**重要ポイント:**  
ライセンスを埋め込むことで、ソース管理に誤って公開されるリスクを防げます。また、ストリームが `null` の場合はプログラムが早期に終了するようにしているのが、防御的チェックの第一歩です。

## 手順 2: OCR エンジンを初期化する（画像で OCR を実行）  

ライセンスがロードされたら、`OcrEngine` インスタンスを作成します。サンプル PNG が英語なので、言語は English に設定します。

```csharp
        // ------------------------------------------------------------
        // 2️⃣ Initialise the OCR engine – this is where we perform OCR on image
        // ------------------------------------------------------------
        var ocrEngine = new OcrEngine
        {
            Language = Language.English   // change to Language.French etc. if needed
        };
```

**Tip:** `Language` 列挙体は 30 以上の言語に対応しています。`Language.Spanish` のように変更するだけで切り替え可能です。マルチ言語検出が必要な場合は、エンジンを別々にインスタンス化するか、`ocrEngine.AutoDetectLanguage = true`（新しい Aspose バージョンで利用可）を使用してください。

## 手順 3: PNG 画像を読み込む（PNG からテキストを抽出）  

Aspose OCR は独自の `Image` クラスを使用します。`System.Drawing.Image` ではありません。ファイルパスを指定するか、`Stream` を渡すことができます。

```csharp
        // ------------------------------------------------------------
        // 3️⃣ Load the image – this is the step where we extract text from png
        // ------------------------------------------------------------
        const string imagePath = "YOUR_DIRECTORY/sample.png";

        if (!System.IO.File.Exists(imagePath))
        {
            Console.Error.WriteLine($"Image not found at {imagePath}");
            return;
        }

        var image = Image.Load(imagePath);
```

**エッジケース:** PNG にアルファチャンネル（透明背景）が含まれると、Aspose が空白を誤認識することがあります。その場合は `ImageProcessor` でフラット化すると改善しますが、ほとんどのスキャン文書ではデフォルトローダーで問題ありません。

## 手順 4: 認識を実行する（画像をテキストに変換）  

エンジンと画像が準備できたら、実際の OCR 呼び出しはワンライナーです。結果オブジェクトから生の文字列と信頼度スコアが取得できます。

```csharp
        // ------------------------------------------------------------
        // 4️⃣ Recognise the image – this is where we convert image to text
        // ------------------------------------------------------------
        var ocrResult = ocrEngine.Recognize(image);

        // Optional: check confidence (0‑100)
        Console.WriteLine($"Confidence: {ocrResult.Confidence}%");
```

**信頼度が重要な理由:**  
信頼度が低い（例: 70 % 未満）場合は、画像がぼやけているかフォントが未対応であることを示します。本番環境では別の OCR エンジンにフォールバックしたり、ユーザーに再スキャンを促したりすると良いでしょう。

## 手順 5: 認識結果を出力する  

最後に抽出した文字列をコンソールに出力します。実際のアプリではデータベースや JSON ファイルに保存したり、検索インデックスに流し込んだりすることも考えられます。

```csharp
        // ------------------------------------------------------------
        // 5️⃣ Output the recognised text – the final result of recognize text from image
        // ------------------------------------------------------------
        Console.WriteLine("\n--- Recognised Text ---");
        Console.WriteLine(ocrResult.Text);
    }
}
```

### 期待されるコンソール出力

```
Confidence: 96%
--- Recognised Text ---
Hello, world!
This is a sample PNG used for OCR testing.
```

上記（または類似）のテキストが表示されれば、**画像からテキストを認識する** に成功です！おめでとうございます。

## よくある落とし穴と回避策  

| 症状 | 考えられる原因 | 対策 |
|------|----------------|------|
| `License not set` 例外 | ライセンスファイルが埋め込まれていない、またはリソース名が間違っている | `Build Action = Embedded Resource` を確認し、完全修飾名を再チェック |
| 出力が空 | 画像の DPI が低すぎる（150 未満） | PNG を少なくとも 150 DPI にリサンプリングしてから Aspose に渡す |
| 文字化け | 言語設定が誤っている | `ocrEngine.Language` を正しい `Language` 列挙値に設定 |
| 大容量画像で `OutOfMemoryException` | 10 MB 以上の巨大 PNG を直接ロードしている | `Image.Load(stream, maxWidth: 2000, maxHeight: 2000)` でオンザフライに縮小 |

## プロのコツ: バッチ処理  

多数の **画像からテキストを認識する** 必要がある場合は、コアロジックを `foreach` ループで回し、同じ `OcrEngine` インスタンスを再利用します。エンジンを再利用することで、ネイティブライブラリのロード時間が削減され、ファイルごとに数ミリ秒の高速化が期待できます。

```csharp
var images = System.IO.Directory.GetFiles("YOUR_DIRECTORY", "*.png");
foreach (var path in images)
{
    var img = Image.Load(path);
    var result = ocrEngine.Recognize(img);
    Console.WriteLine($"{path} → {result.Text.Trim()}");
}
```

## 次のステップ  

- **前処理を微調整** – `ImageProcessor` でコントラスト向上やノイズ除去を試す  
- **他の出力形式を探索** – `ocrResult.GetWords()` でバウンディングボックスを取得し、UI 上でハイライト表示に活用  
- **Azure Cognitive Services と組み合わせ** – 手書き文字のクラウド認識が必要な場合に活用  

これらの拡張もすべて同じパターンです：ライセンスをロード → エンジンを作成 → 画像を供給 → テキストを取得。

![Screenshot of console showing recognized text from image](/images/ocr-result.png "recognize text from image result screenshot")

## まとめ  

本稿では、Aspose OCR を用いて C# で **画像からテキストを認識する** 完全なプロダクション向けサンプルをステップバイステップで解説しました。埋め込みリソースからのライセンス取得、PNG の読み込み、OCR の実行、結果の出力まで、すべて網羅しています。

これで **png からテキストを抽出する**、**画像をテキストに変換する**、さらには **C# の埋め込みリソースからライセンスを読み込む** が数十行のコードで実現できます。さまざまな言語や大規模バッチ、独自の文書処理パイプラインへの統合など、自由に試してみてください。Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}