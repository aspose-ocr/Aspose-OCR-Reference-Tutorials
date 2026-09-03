---
category: general
date: 2026-01-10
description: 画像からアラビア語テキストを素早くOCRで抽出する方法。画像をテキストに変換し、PNGからテキストを読み取り、Aspose OCRでテキストを抽出する手順を学びましょう。
draft: false
keywords:
- how to run OCR
- extract arabic text
- convert image to text
- read text from png
- how to extract text
language: ja
og_description: C#でOCRを実行し、PNG画像からアラビア語テキストを抽出する方法。このガイドでは、画像をテキストに変換し、PNGからテキストをステップバイステップで読み取る方法を示します。
og_title: C#でOCRを実行する方法 – PNGからアラビア語テキストを抽出
tags:
- OCR
- C#
- Aspose
title: C#でOCRを実行する方法 – PNGからアラビア語テキストを抽出
url: /ja/net/text-recognition/how-to-run-ocr-in-c-extract-arabic-text-from-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#でOCRを実行する方法 – PNGからアラビア語テキストを抽出する

アラビア文字が含まれる画像で **OCRを実行する方法** を考えたことはありますか？ あなたは一人ではありません。多くの開発者は、PNGから **アラビア語テキストを抽出** したいときに、右から左へのスクリプトを問題なく処理できるライブラリがどれか分からず壁にぶつかります。  

このチュートリアルでは、**画像をテキストに変換**し、**PNGからテキストを読み取り**、最後に Aspose.OCR を使用して **テキストを抽出する方法** をクリーンな C# コンソールアプリで実行するために必要なすべてを解説します。最後までに、ターミナルにアラビア語文字列を直接出力する実行可能なプログラムが手に入ります。

## 学習できること

- Aspose.OCR NuGet パッケージをインストールし、参照する。  
- アラビア語サポートのために OCR エンジンを構成する。  
- PNG 画像をロードし、認識プロセスを実行する。  
- 抽出されたテキストを取得して表示する。  
- 設定を調整して精度を向上させ、一般的な落とし穴に対処する。

OCR の事前経験は不要です。C# の基本的な理解と .NET 開発環境（Visual Studio、Rider、または `dotnet` CLI があれば十分）さえあれば始められます。

---

## OCR の実行方法 – Aspose OCR のセットアップ

### 手順 1: Aspose.OCR NuGet パッケージを追加する

最初に必要なのは OCR ライブラリそのものです。Aspose.OCR は商用製品ですが、学習目的で完全に機能する無料トライアルが提供されています。

```bash
# Using the .NET CLI
dotnet add package Aspose.OCR
```

あるいは、Visual Studio の **NuGet パッケージ マネージャー** を開き、**Aspose.OCR** を検索して **インストール** をクリックします。

> **プロのコツ:** ライブラリを CI パイプラインで使用する予定がある場合、バージョンを固定するために `-v` フラグを追加してください。例: `dotnet add package Aspose.OCR -v 23.10`.

### 手順 2: 新しいコンソールプロジェクトを作成する（まだ持っていない場合）

```bash
dotnet new console -n ArabicOcrDemo
cd ArabicOcrDemo
```

これで、コードを書き込むための新しい `Program.cs` ファイルが用意できました。

---

## アラビア語テキストの抽出 – OCR コードの作成

以下は完全な実行可能プログラムです。`Program.cs` として保存するか（または自動生成されたファイルを置き換えて）使用してください。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Config;

namespace ArabicOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 1: Create an OCR engine instance
            // -------------------------------------------------
            var ocrEngine = new OcrEngine();

            // -------------------------------------------------
            // Step 2: Choose the language for recognition.
            // Here we use Arabic. You can swap this for
            // OcrLanguage.Korean, OcrLanguage.SerbianCyrillic, etc.
            // -------------------------------------------------
            ocrEngine.Language = OcrLanguage.Arabic;

            // -------------------------------------------------
            // Step 3: Load the image containing the text.
            // Replace the path with the location of your PNG.
            // -------------------------------------------------
            string imagePath = "YOUR_DIRECTORY/arabic_sample.png";
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // -------------------------------------------------
            // Step 4: Run the OCR process.
            // -------------------------------------------------
            ocrEngine.Recognize();

            // -------------------------------------------------
            // Step 5: Display the extracted text.
            // -------------------------------------------------
            Console.WriteLine("=== Extracted Arabic Text ===");
            Console.WriteLine(ocrEngine.Text);
        }
    }
}
```

#### 各行が重要な理由

- **`OcrEngine`**: 画像の読み込み、言語選択、認識を調整する中心クラスです。  
- **`Language = OcrLanguage.Arabic`**: アラビア語は右から左へのスクリプトと固有の字形を持つため、言語を設定することでエンジンは正しい文字モデルを適用します。  
- **`ImageStream.FromFile`**: PNG、JPEG、BMP など多数のフォーマットを処理します。`MemoryStream`（例: アップロードされたファイル）から読み込む必要がある場合は、この呼び出しを置き換えてください。  
- **`Recognize()`**: ピクセル解析、セグメンテーション、文字分類といった重い処理を実行します。  
- **`ocrEngine.Text`**: 最終的な Unicode 文字列で、さらに処理したり保存したり表示したりする準備ができています。

### 期待される出力

`arabic_sample.png` にフレーズ “مرحبا بالعالم”（Hello World）が含まれている場合、コンソールは次のように出力します：

```
=== Extracted Arabic Text ===
مرحبا بالعالم
```

出力が文字化けしている場合は、画像が鮮明か、言語がアラビア語に設定されているか、OCR エンジンのバージョンがドキュメントと一致しているかを再確認してください。

---

## 画像をテキストに変換 – 精度の調整

デフォルト設定はほとんどのクリーンなスキャンで機能しますが、実際の画像では追加の調整が必要になることが多いです。

| 設定 | 機能 | 使用タイミング |
|---------|--------------|-------------|
| `ocrEngine.Config.Preprocess = true` | 自動二値化とノイズ除去を有効にします。 | 影のあるスキャン文書。 |
| `ocrEngine.Config.Deskew = true` | 画像を回転させてわずかな傾きを補正します。 | 斜めに撮影された写真。 |
| `ocrEngine.Config.PageSegMode = PageSegMode.SingleBlock` | 画像全体を1つのテキストブロックとして扱います。 | シンプルなキャプションや1行ラベル。 |
| `ocrEngine.Config.CharWhitelist = "ءاأإآبتثجحخدذرزس شصضطظعغفقكلمنهوية"` | アラビア文字のみの認識に制限します。 | 混在言語ページでの誤認識を減らす。 |

エンジンを作成した直後に、これらの行を追加できます：

```csharp
ocrEngine.Config.Preprocess = true;
ocrEngine.Config.Deskew = true;
ocrEngine.Config.CharWhitelist = "ءاأإآبتثجحخدذرزسشصضطظعغفقكلمنهوية";
```

---

## PNG からテキストを読む – 異なる画像ソースの取り扱い

PNG がデータベースに保存されていたり、Web リクエストから来ることがあります。以下は `byte[]` から読み込む簡易バージョンです：

```csharp
byte[] pngBytes = File.ReadAllBytes("YOUR_DIRECTORY/arabic_sample.png");
using var ms = new MemoryStream(pngBytes);
ocrEngine.Image = ImageStream.FromStream(ms);
ocrEngine.Recognize();
Console.WriteLine(ocrEngine.Text);
```

残りのフローは同一なので、**テキストを抽出する方法** はソースに関係なく一貫しています。

---

## テキスト抽出方法 – 高度なオプションとエッジケース

### 1. マルチページ PDF または TIFF

マルチページ文書を OCR する必要がある場合、各ページをループ処理します：

```csharp
var pdfDoc = new Aspose.Pdf.Document("multi_page.pdf");
foreach (var page in pdfDoc.Pages)
{
    using var img = page.ConvertToImage();
    ocrEngine.Image = ImageStream.FromBitmap(img);
    ocrEngine.Recognize();
    Console.WriteLine($"Page {page.Number}: {ocrEngine.Text}");
}
```

> **注:** このスニペットには `Aspose.PDF` パッケージが必要です。

### 2. 言語の自動検出

Aspose.OCR は自動検出も提供していますが、処理は遅くなります。画像がアラビア語か他のスクリプトか不明な場合は、これを有効にしてください：

```csharp
ocrEngine.Language = OcrLanguage.AutoDetect;
```

エンジンは各言語モデルを試し、最適なものを選択します。

### 3. パフォーマンスのヒント

- **`OcrEngine`** オブジェクトを複数の画像で再利用する；毎回新しいインスタンスを作成するとオーバーヘッドが増えます。  
- **並列実行** は、スレッドごとに別々のエンジンインスタンスがある場合にのみ行ってください。1つのインスタンスを共有すると競合状態が発生します。

---

## 結論

C# で **OCR を実行する方法** を最初から最後までカバーし、**アラビア語テキストの抽出**、**画像をテキストに変換**、**PNG からテキストを読む**、そして様々なシナリオで **テキストを抽出する方法** を示しました。サンプルコードは完全で自己完結しており、任意の .NET コンソールプロジェクトに貼り付けてすぐに使用できます。

次のステップは？ `OcrLanguage.Arabic` を韓国語やセルビア語キリル文字に置き換えて、ライブラリの多言語対応力を体験してみてください。前処理フラグを試してノイズが多いスキャンの精度を向上させるか、OCR 処理を Web API に統合してユーザーが画像をアップロードし即座にテキスト結果を取得できるようにしましょう。

コーディングを楽しんで、OCR の結果が常にクリアでありますように！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}