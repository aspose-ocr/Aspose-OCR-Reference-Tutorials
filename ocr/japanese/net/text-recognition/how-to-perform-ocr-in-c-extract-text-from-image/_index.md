---
category: general
date: 2026-03-13
description: C#でOCRを実行し、OcrEngineを使用して画像からテキストを抽出する方法。ステップバイステップの完全ガイドで、画像をテキストに素早く変換する方法を学びましょう。
draft: false
keywords:
- how to perform OCR
- extract text from image
- convert image to text
- read text from picture
- how to extract text
language: ja
og_description: C#でOCRを実行する方法は？このガイドでは、画像からテキストを抽出し、画像をテキストに変換し、OcrEngineを使用して画像からテキストを読み取る方法を示します。
og_title: C#でOCRを実行する方法 – 画像からテキストを抽出
tags:
- OCR
- C#
- Image Processing
title: C#でOCRを行う方法 – 画像からテキストを抽出する
url: /ja/net/text-recognition/how-to-perform-ocr-in-c-extract-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#でOCRを実行する方法 – 画像からテキストを抽出する

C#でOCRを実行する方法は、画像ファイルから**テキストを読み取る**必要がある開発者にとって一般的な質問です。このガイドでは、`OcrEngine` ライブラリを使用して画像からテキストを抽出し、数行のコードだけで画像を検索可能な文字列に変換する方法を説明します。  

スキャンした請求書や手書きのメモ、スクリーンショットを見て「テキストをどうやって抽出すればいいんだろう？」と思ったことがあるなら、ここが適切な場所です。また、バッチ処理用に画像からテキストへの変換にも触れ、ワークフロー全体を自動化できるようにします。

---

## 必要なもの

Before we dive, make sure you have:

- **.NET 6.0 以上**（使用する API は .NET Standard 2.0+ でも動作します）
- **OcrEngine** NuGet パッケージ（または `Language`、`Image`、`Recognize`、`Text` プロパティを提供する互換性のある OCR ライブラリ）
- サンプル画像ファイル、例: `hindi_page.jpg` をコードから参照できるフォルダーに配置
- C# の基本的な構文の理解 – 高度なテクニックは不要

それだけです。外部サービスや API キーは不要で、ローカルのライブラリだけで重い処理を行います。

---

## ステップバイステップ実装

Below we break the process into logical chunks. Each section has a clear heading, a short code snippet, and an explanation of **why** the step matters—not just **what** it does.

### OCR を実行する方法 – 基本ステップ

The overall flow can be summarized in five actions:

1. OCR エンジンインスタンスを**作成**する
2. 認識したい言語を**選択**する
3. テキストを含む画像を**読み込む**
4. 認識アルゴリズムを**実行**する
5. 抽出されたテキストを**取得**する

これが骨組みです。以下のセクションで詳細を説明します。

---

### 画像からテキストを抽出 – エンジンの作成

First, we need an object that knows how to talk to the OCR engine.

```csharp
using System;
using OcrLibrary;   // Replace with the actual namespace of your OCR package

// Step 1: Create an OCR engine instance
OcrEngine ocrEngine = new OcrEngine();
```

*重要性:* `OcrEngine` をインスタンス化すると、内部バッファがすべて確保され、画像解析に必要なネイティブ DLL がロードされます。このステップを省略すると、後で呼び出す認識器が存在しなくなります。

> **プロのコツ:** 連続して多数の画像を処理する場合は、同じ `ocrEngine` インスタンスを維持してください。言語モデルを再利用し、以降の呼び出しを高速化します。

---

### 画像からテキストへ変換 – 言語の選択

OCR accuracy heavily depends on the language model you feed it. For Hindi, Tamil, or any other script, set the `Language` property accordingly.

```csharp
// Step 2: Select the language of the text to recognize (e.g., Hindi)
ocrEngine.Language = Language.Hindi;   // You can also use Language.Tamil, Language.English, etc.
```

*重要性:* エンジンは言語固有の文字セットと統計モデルを使用します。誤った言語を指定すると、特にラテン文字以外のスクリプトでは出力が乱れることが多いです。

> **エッジケース:** マルチ言語対応が必要な場合、いくつかのライブラリではフォールバックリストを設定でき、例として `ocrEngine.Language = Language.Multilingual;` があります。

---

### 画像からテキストを読む – ソース画像の読み込み

Now we point the engine at the file that holds the visual text.

```csharp
// Step 3: Load the image that contains the text
ocrEngine.Image = ImageStream.FromFile(@"C:\OCR\Samples\hindi_page.jpg");
```

*重要性:* `ImageStream.FromFile` は生のファイルを OCR コアが理解できるビットマップ形式に変換します。破損したファイルやサポートされていない形式（例: SVG）を指定すると例外が発生します。

> **注意:** 大きな画像は多くのメモリを消費します。高解像度のスキャンを処理する場合は、エンジンに渡す前に `Image.Resize` で縮小することを検討してください。

---

### 画像からテキストへ変換 – 認識の実行

With the engine ready and the image loaded, we finally invoke the OCR process.

```csharp
// Step 4: Perform the OCR operation
ocrEngine.Recognize();
```

*重要性:* `Recognize` は内部で前処理、セグメンテーション、文字分類、後処理といった一連のステップをトリガーします。この呼び出しはブロッキングで、スレッドはテキストが準備できるまで待機します。

> **パフォーマンスに関する注意:** 一般的なデスクトップでは、300 dpi のページを認識するのに < 1 秒です。サーバー上では UI のフリーズを防ぐため、バックグラウンドタスクで実行することを検討してください。

---

### テキスト抽出方法 – 結果の取得

Once recognition finishes, the engine stores the plain‑text output in the `Text` property.

```csharp
// Step 5: Output the recognized text
Console.WriteLine(ocrEngine.Text);
```

*重要性:* `Text` プロパティは、ファイルに書き出したりデータベースに保存したり、下流の NLP パイプラインに渡したりできる、クリーンな UTF‑8 文字列を提供します。

> **期待される出力:** サンプルのヒンディー語ページでは、次のような結果が得られるかもしれません  
> `यह एक उदाहरण पाठ है जो OCR द्वारा पहचाना गया है।`  
> （正確な出力は画像の品質と使用する言語モデルに依存します）

---

## 実務プロジェクトでの追加考慮事項

Below are some “what‑if” scenarios you’ll probably run into when you try to **extract text from image** in production.

以下は、実運用で**画像からテキストを抽出**しようとした際に遭遇しやすい「もしも」シナリオです。

### ループで複数画像を処理する場合

If you need to **convert image to text** for dozens of files, wrap the steps in a `foreach` loop and reuse the same `ocrEngine`:

```csharp
string[] files = Directory.GetFiles(@"C:\OCR\Batch\", "*.jpg");
foreach (var file in files)
{
    ocrEngine.Image = ImageStream.FromFile(file);
    ocrEngine.Recognize();
    File.WriteAllText(Path.ChangeExtension(file, ".txt"), ocrEngine.Text);
}
```

### 低品質スキャンへの対処

- **二値化**（`Image.Binarize()`）やノイズ除去、デスキュー処理で**前処理**する。
- スキャン時に**DPI を上げる**（300 dpi が安全な基準）。
- スクリプトのリガチャに対応した**言語モデル**を選択する（例: ヒンディー語ならデーヴァナーガリー）。

### Web 上の画像からテキストを読む

When the image comes from a URL, download it into a memory stream first:

```csharp
using (HttpClient client = new())
{
    byte[] data = await client.GetByteArrayAsync(imageUrl);
    using var ms = new MemoryStream(data);
    ocrEngine.Image = ImageStream.FromStream(ms);
    ocrEngine.Recognize();
    Console.WriteLine(ocrEngine.Text);
}
```

### スレッド安全性と並列処理

Most OCR libraries are **not** thread‑safe out of the box. If you plan to **read text from picture** concurrently, spin up separate `OcrEngine` instances per thread, or use a producer‑consumer queue to serialize access.

ほとんどの OCR ライブラリはデフォルトで**スレッド安全**ではありません。**画像からテキストを読む**処理を同時に行う予定がある場合、スレッドごとに別々の `OcrEngine` インスタンスを作成するか、プロデューサ‑コンシューマキューを使用してアクセスを直列化してください。

---

## 完全な動作例

Putting everything together, here’s a ready‑to‑run console app that demonstrates **how to perform OCR**, **extract text from image**, and **read text from picture** in one cohesive program.

```csharp
using System;
using OcrLibrary;               // Adjust to your OCR library's namespace
using System.IO;

class Program
{
    static void Main()
    {
        // Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Choose the language (Hindi in this case)
        ocrEngine.Language = Language.Hindi;

        // Load the image file
        string imagePath = @"C:\OCR\Samples\hindi_page.jpg";
        if (!File.Exists(imagePath))
        {
            Console.WriteLine($"Image not found: {imagePath}");
            return;
        }

        ocrEngine.Image = ImageStream.FromFile(imagePath);

        // Run the recognition process
        ocrEngine.Recognize();

        // Output the extracted text
        string result = ocrEngine.Text;
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(result);

        // Optional: Save to a .txt file
        string txtPath = Path.ChangeExtension(imagePath, ".txt");
        File.WriteAllText(txtPath, result);
        Console.WriteLine($"Text saved to {txtPath}");
    }
}
```

**期待される出力:** コンソールに `hindi_page.jpg` から抽出されたヒンディー語の文が表示され、続いてテキストファイルが作成されたことが確認されます。画像がきれいであれば、出力は元の印刷テキストとほぼ同一になります。

---

## 結論

You now know **how to perform OCR** in C# from start to finish, how to **extract text from image**, **convert image to text**, and **read text from picture** using a straightforward `OcrEngine` workflow. The five‑step pattern—create, set language, load, recognize, read—covers the majority of use cases, and the extra tips help you handle batch jobs, low‑quality scans, and web‑based sources.

これで、C# で **OCR を実行**する方法を最初から最後まで理解し、**画像からテキストを抽出**、**画像をテキストに変換**、**画像からテキストを読む**をシンプルな `OcrEngine` ワークフローで行えるようになりました。作成、言語設定、読み込み、認識、取得という5ステップのパターンはほとんどのユースケースをカバーし、追加のヒントはバッチジョブ、低品質スキャン、Web ソースの処理に役立ちます。

次の課題に挑戦したいですか？言語を英語に変えてみたり、画像としてレンダリングした PDF ページを入力したり、OCR の出力を検索インデックスパイプラインに連結したりしてみてください。C# の OCR 基礎をマスターすれば、可能性は無限です。

質問やうまくいかない画像があれば、下にコメントを残してください。一緒にトラブルシュートしましょう。ハッピーコーディング！  

![how to perform OCR example](images/ocr-example.png "how to perform OCR example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}