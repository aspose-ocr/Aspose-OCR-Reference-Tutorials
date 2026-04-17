---
category: general
date: 2026-03-29
description: C#でAspose OCRを使用して画像からテキストを抽出します。自動回転OCRと、完璧な結果を得るためのスキャン画像の傾き補正方法を学びましょう。
draft: false
keywords:
- extract text from image
- auto rotate ocr
- how to deskew scanned image
- Aspose OCR C#
- image preprocessing OCR
language: ja
og_description: Aspose OCR を使用して画像からテキストを抽出します。このガイドでは、OCR の自動回転と C# でスキャン画像の傾き補正方法を示します。
og_title: C#で画像からテキストを抽出 – 自動回転OCRと傾き補正
tags:
- C#
- OCR
- Aspose
- Image Processing
title: C#で画像からテキストを抽出 – 自動回転OCRと傾き補正ガイド
url: /ja/net/ocr-optimization/extract-text-from-image-in-c-auto-rotate-ocr-deskew-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# で画像からテキストを抽出 – Auto‑Rotate OCR と Deskew ガイド

画像から **extract text from image** したいのに、ファイルが奇妙な角度で入ってきたことはありませんか？　特にスキャンした請求書や撮影したレシート、歪んだ PDF を扱うときに頻繁に起こる頭痛の種です。良いニュースは、独自の回転アルゴリズムを自分で書く必要はないということです。Aspose OCR の組み込み *auto rotate OCR* 機能を使えば、エンジンが画像を自動で整列させ、**extract text from image** をスムーズに実行できます。

このチュートリアルでは、次のことを行う完全な実行可能 C# プログラムを順を追って解説します。

* 自動向き検出とデスクューを有効にした OCR エンジンの初期化
* 回転または歪んだ画像の認識
* 検出された回転角度と抽出されたテキストの両方を取得

外部サービスは不要、面倒な数式計算も不要――数行のコードと、必要に応じた *how to deskew scanned image* の明確な説明だけです。

## 必要なもの

| 前提条件 | 重要な理由 |
|--------------|----------------|
| .NET 6.0 以降（または .NET Framework 4.6+） | Aspose OCR はこれらのランタイム向けに NuGet パッケージとして提供されています。 |
| Visual Studio 2022（または任意の C# エディタ） | NuGet パッケージの追加やコンソール アプリの実行が簡単です。 |
| サンプル画像（`rotated_document.jpg`） | JPEG、PNG、BMP、または TIFF 形式で、完全に正立していない画像である必要があります。 |
| Aspose.OCR NuGet パッケージ（`Install-Package Aspose.OCR`） | `OcrEngine`、`PreprocessingFilters`、その他関連型を提供します。 |

上記がすべて揃っていればすぐに始められます。足りない場合は、NuGet から最新の Aspose OCR を取得してください――ワンクリックでインストールできます。

---

## Step 1 – OCR エンジンの初期化 (Primary Keyword in Action)

最初に `OcrEngine` インスタンスを作成し、**auto rotate OCR** と **deskew** を有効にします。この 2 つのフラグはビット単位の OR (`|`) で結合されます。`PreprocessingFilters` は `[Flags]` 属性が付与された列挙型です。

```csharp
using System;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // Initialise the OCR engine with English language and preprocessing options
        OcrEngine ocrEngine = new OcrEngine
        {
            Language = Language.English,
            // Enable both auto‑rotate and auto‑deskew
            Preprocessing = PreprocessingFilters.AutoRotate | PreprocessingFilters.AutoDeskew
        };
```

> **Why this matters:**  
> *Auto‑rotate OCR* は画像のテキストベースラインを解析し、正しい向きを推測して内部で回転させます。*Auto‑deskew* はスキャン文書にしばしば見られる微小な傾きを補正します。両方を有効にすることで、手動で画像を編集することなく最高の **extract text from image** 結果が得られます。

---

## Step 2 – 画像を認識し結果を取得

エンジンにファイル パスを渡します。`RecognizeImage` メソッドは `OcrResult` オブジェクトを返し、検出された回転角度、信頼度スコア、プレーンテキスト出力が含まれます。

```csharp
        // Recognise the image file and obtain the OCR result
        OcrResult ocrResult = ocrEngine.RecognizeImage("YOUR_DIRECTORY/rotated_document.jpg");
```

> **Tip:** ストリーム（例: アップロードされたファイル）で処理する場合は `ocrEngine.RecognizeImage(Stream)` を使用してください。前述の前処理フラグは同様に適用され、**auto rotate OCR** の恩恵を受けられます。

---

## Step 3 – 回転角度と抽出テキストの表示

最後にコンソールへ 2 つの情報を出力します。エンジンが判断した画像の回転角度と、実際に抽出されたテキストです。

```csharp
        // Show the detected rotation and the recognised text
        Console.WriteLine($"Detected rotation: {ocrResult.RotationAngle}°");
        Console.WriteLine("----- Extracted Text -----");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**期待される出力**（入力画像により数値は変わります）:

```
Detected rotation: 12.3°
----- Extracted Text -----
Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00
Thank you for your business!
```

画像がすでに正立している場合、回転角度は `0°` となり、*auto‑deskew* アルゴリズムのおかげでクリーンなテキストが得られます。

---

## Step 4 – Scanned Image のデスクュー方法の理解 (Secondary Keyword Deep‑Dive)

OCR エンジンが非ゼロの回転を報告したとき、*how to deskew scanned image* が気になるかもしれません。内部では Aspose OCR が **Hough transform** を使って支配的なテキスト行の向きを検出し、その角度の逆方向にビットマップを回転させてテキストを真っ直ぐにします。

**いつ重要になるか？**  
* 紙をわずかな角度で給紙するスキャナ（オフィス環境で一般的）。  
* 手持ちのスマートフォンで撮影した写真――水平が完璧でないことが多い。  

**エッジケースの対処:**  
結果の `RotationAngle` が異常に大きい（例: > 45°）場合、エンジンが画像を誤認識した可能性があります（ロゴやテキスト以外のグラフィックなど）。その場合は次のいずれかを実行してください。

1. `System.Drawing` を使って画像を手動で回転させてからエンジンに渡す。  
2. 文書がすでに正立していることが分かっている場合は `AutoRotate` を無効にし、`AutoDeskew` のみを有効にする。

```csharp
// Example: manually rotate 90° clockwise before OCR
using (var img = Aspose.OCR.Image.Load("rotated_document.jpg"))
{
    img.Rotate(90);
    OcrResult result = ocrEngine.RecognizeImage(img);
    Console.WriteLine(result.Text);
}
```

---

## Step 5 – よくある落とし穴とプロのコツ (E‑E‑A‑T in Action)

| 落とし穴 | 発生理由 | 対策 |
|---------|----------------|-----|
| **ぼやけた低解像度画像** | OCR の精度が大幅に低下し、回転検出が失敗することがあります。 | 300 dpi 以上のスキャンを使用し、OCR 前にシャープ化フィルタを適用します。 |
| **混在言語** | エンジンはデフォルトで英語を使用するため、外国文字が文字化けします。 | `Language = Language.English | Language.Spanish`（または適切な組み合わせ）を設定します。 |
| **大容量ファイル（> 10 MB）** | メモリ圧迫により `OutOfMemoryException` が発生する可能性があります。 | 事前に画像を縮小するか、`OcrEngine.RecognizeRegion` を使ってタイル単位で処理します。 |
| **ファイルパスが間違っている** | `FileNotFoundException` でプログラムが停止します。 | `Path.Combine(Environment.CurrentDirectory, "rotated_document.jpg")` のようにパスを組み立てて堅牢性を高めます。 |

> **Pro tip:** 常に `ocrResult.RotationAngle` と `ocrResult.Confidence`（利用可能な場合）をログに残しましょう。これらの指標で、前処理設定を変えて再試行すべきか判断できます。

---

## Step 6 – サンプルの拡張 (What’s Next?)

自動回転とデスクューで **extract text from image** ができるようになったら、次のステップを検討してください。

* **バッチ処理** – フォルダ内の画像をループし、各結果をデータベースに保存。`RotationAngle > 5°` のものは手動レビュー対象としてフラグを付けます。  
* **PDF 変換** – 抽出したテキストと元画像を組み合わせ、Aspose.PDF を使って検索可能な PDF を作成します。  
* **言語自動検出** – Aspose.OCR の `AutoDetectLanguage` フラグを有効にし、エンジンに最適な言語を自動選択させます。  

これらはすべて同じコア原則に基づきます：ライブラリに向き検出を任せ、ビジネスロジックに集中することです。

---

## 完全動作サンプル (Copy‑Paste Ready)

```csharp
using System;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialise the OCR engine with auto‑rotate and auto‑deskew
        OcrEngine ocrEngine = new OcrEngine
        {
            Language = Language.English,
            Preprocessing = PreprocessingFilters.AutoRotate | PreprocessingFilters.AutoDeskew
        };

        // 2️⃣ Recognise the image – replace the path with your own file
        string imagePath = "YOUR_DIRECTORY/rotated_document.jpg";
        OcrResult ocrResult = ocrEngine.RecognizeImage(imagePath);

        // 3️⃣ Output the rotation angle and the recognised text
        Console.WriteLine($"Detected rotation: {ocrResult.RotationAngle}°");
        Console.WriteLine("----- Extracted Text -----");
        Console.WriteLine(ocrResult.Text);
    }
}
```

ファイル名を `Program.cs` として保存し、`dotnet add package Aspose.OCR` を実行後、`dotnet run` を実行してください。コンソールに回転角度とクリーンなテキストが表示されます。

---

## 結論

本稿では、C# で **extract text from image** を実行しつつ、Aspose OCR に *auto rotate OCR* と難しい *how to deskew scanned image* の処理を任せる方法を示しました。2 つの前処理フラグを有効にするだけで、エンジンは自動で歪んだ画像を整列させ、正しい向きを検出し、正確なテキストを提供します――手動で画像を編集する必要はありません。

バッチ処理や多言語対応、検索可能 PDF への統合など、さまざまな拡張に挑戦してみてください。OCR エンジンが重い作業を引き受けてくれるので、可能性は無限に広がります。

**ドキュメント パイプラインを次のレベルへ引き上げる準備はできましたか？** コードを取得し、独自のスキャンに適用して回転角度が消える様子をご確認ください。問題があれば下のコメント欄で教えてください――ハッピーコーディング！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}