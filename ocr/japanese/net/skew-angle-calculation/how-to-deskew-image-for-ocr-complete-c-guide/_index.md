---
category: general
date: 2026-01-06
description: Aspose OCR を使用して画像の傾きを補正し、ノイズを除去し、テキストを抽出する方法を学びましょう。ステップバイステップのガイドでは、OCR
  用に画像を読み込む方法も示しています。
draft: false
keywords:
- how to deskew image
- how to extract text
- how to remove noise
- recognize text from image
- load image for ocr
language: ja
og_description: Aspose OCR を使用して画像の傾き補正、ノイズ除去、テキスト抽出を学びましょう。ステップバイステップのガイドでは、OCR 用に画像を読み込む方法も示しています。
og_title: OCR用画像のデスキュー方法 – 完全C#ガイド
tags:
- OCR
- C#
- Image Processing
title: OCR用画像の傾き補正方法 – 完全C#ガイド
url: /ja/net/skew-angle-calculation/how-to-deskew-image-for-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR 用画像のデスケー（傾き補正）方法 – 完全 C# ガイド

スキャンした画像を OCR エンジンに渡す前に **画像をデスケー（傾き補正）** する方法を疑問に思ったことはありませんか？ あなたは一人ではありません—スキャンした写真が少し傾いていたり、ノイズが多かったり、単に読みにくいと、多くの開発者が同じ壁にぶつかります。良いニュースは、Aspose OCR を使えば、画像をまっすぐにし、クリーンにし、数行の C# でテキストを抽出できることです。

このチュートリアルでは **テキストの抽出方法**、**ノイズ除去方法**、そしてもちろん **画像のデスケー方法** を順に解説し、OCR 結果を完璧にします。最後まで読むと **OCR 用画像のロード方法** も理解でき、アプリケーションで使用できるクリーンで検索可能な文字列が手に入ります。

---

## 必要なもの

- **Aspose.OCR for .NET** (v23.12 以上)。NuGet パッケージは `Aspose.OCR`。
- .NET 6+（最新のランタイムであれば問題ありません）。
- 傾いている、または斑点があるサンプル画像（例: `skewed_photo.jpg`）。
- Visual Studio、Rider、またはお好みのエディタ。

追加のネイティブライブラリは不要です—Aspose がプロセス内で全て処理します。

## ステップ 1 – OCR エンジンのセットアップ（画像からテキストを認識）

**OCR 用画像をロード** する前に、エンジンインスタンスと読み取りたい言語を用意します。

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

// Create the OCR engine and tell it we’re reading English text.
OcrEngine ocrEngine = new OcrEngine
{
    Language = OcrLanguage.English
};
```

**Why this matters:** `OcrEngine` はプロセスの中心です。`Language` を早期に設定すると、認識アルゴリズムが適切な文字セットを使用し、精度が劇的に向上します。

## ステップ 2 – 画像の読み込み（OCR 用画像のロード）

エンジンにディスク上のファイルを指し示します。この段階で多くのチュートリアルが止まりますが、一般的な落とし穴も解説します。

```csharp
// Load the image you want to process.
ocrEngine.Image = ImageStream.FromFile(@"C:\Images\skewed_photo.jpg");
```

> **Pro tip:** テスト時は絶対パスを使用し、実運用では相対パスまたは埋め込みリソースに切り替えます。また、画像がサポートされている形式（JPEG、PNG、BMP、TIFF）であることを確認してください。 “Unsupported format” エラーが出たら、拡張子と MIME タイプを再確認しましょう。

## ステップ 3 – 前処理: デスケーとデスぺックル（画像の傾き補正とノイズ除去）

傾いた文書は OCR の古典的な悪夢です。Aspose は回転角度を自動検出できる `DeskewFilter` を提供します。これを `DespeckleFilter` と組み合わせて塩胡椒ノイズを除去します。

```csharp
// 1️⃣ Deskew – correct rotation up to 15° (adjust as needed)
ocrEngine.Filters.Add(new DeskewFilter { MaxAngle = 15 });

// 2️⃣ Despeckle – reduce noise; Strength 1‑5 (3 is moderate)
ocrEngine.Filters.Add(new DespeckleFilter { Strength = 3 });
```

### デスケーフィルタの仕組み
フィルタは画像内の支配的なテキストベースラインをスキャンし、傾き角度を算出してビットマップを回転させます。画像がすでに水平であればフィルタは何もしません—どのパイプラインにも安全に追加できます。

### デスぺックルフィルタの効果
ノイズはしばしば孤立した暗いまたは明るいピクセルとして現れます。デスぺックルアルゴリズムはメディアンフィルタを適用し、エッジ（文字のストロークなど）を保持しつつ斑点を平滑化します。強度を上げすぎると細部がぼやけるため、まずは `Strength = 3` で開始し、素材に合わせて調整してください。

> **Side note:** 画像の回転が極端（>15°）な場合は `MaxAngle` を増やします。上下逆さまにスキャンされた文書は、デスケーフィルタの前にカスタム回転ステップが必要になることがあります。

## ステップ 4 – 認識の実行（画像からテキストを認識）

前処理が整ったら、エンジンにテキストの読み取りを指示します。

```csharp
if (ocrEngine.Recognize())
{
    // The recognized text is now stored in ocrEngine.Text
    Console.WriteLine("=== Extracted Text ===");
    Console.WriteLine(ocrEngine.Text);
}
else
{
    Console.WriteLine("Recognition failed – check the image quality.");
}
```

### 背後で何が起きているか
1. **Binarization:** 画像を白黒に変換し、コントラストを強調します。  
2. **Segmentation:** ビットマップを行、単語、文字に分割します。  
3. **Classification:** 各文字を学習済みモデル（英字、数字、句読点）と照合します。  
4. **Post‑processing:** 言語ルール（例: スペルチェック）を適用し、可読性を向上させます。

既に **画像をデスケー** し **ノイズを除去** しているため、各ステージがよりクリーンなデータを受け取り、誤認識が大幅に減少します。

## ステップ 5 – 出力の検証とクリーンアップ（テキスト抽出の効果的な方法）

生の文字列には余分な改行やスペースが含まれることがあります。簡単なクリーンアップで下流処理の準備が整います。

```csharp
string raw = ocrEngine.Text;

// Trim leading/trailing whitespace and collapse multiple newlines.
string cleaned = System.Text.RegularExpressions.Regex
    .Replace(raw, @"\s+", " ")
    .Trim();

Console.WriteLine("\n=== Cleaned Text ===");
Console.WriteLine(cleaned);
```

**Why clean it?** 多くの OCR ライブラリは元のレイアウトを保持しますが、PDF には便利でもプレーンテキストパイプラインではノイズになります。空白を正規化すれば、データベースに保存したり検索インデックスに投入したりする際の余計な作業が省けます。

## 完全な動作例

以下はすべてを結びつけた、コピー＆ペースト可能な完全プログラムです。`Program.cs` として保存し、Aspose.OCR NuGet パッケージを追加して実行してください。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize OCR engine
        OcrEngine ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.English
        };

        // 2️⃣ Load the image you want to process
        //    (this demonstrates how to load image for OCR)
        ocrEngine.Image = ImageStream.FromFile(@"C:\Images\skewed_photo.jpg");

        // 3️⃣ Add preprocessing filters
        //    - Deskew up to 15° (how to deskew image)
        //    - Despeckle with moderate strength (how to remove noise)
        ocrEngine.Filters.Add(new DeskewFilter { MaxAngle = 15 });
        ocrEngine.Filters.Add(new DespeckleFilter { Strength = 3 });

        // 4️⃣ Perform recognition (recognize text from image)
        if (ocrEngine.Recognize())
        {
            // 5️⃣ Output raw and cleaned text (how to extract text)
            Console.WriteLine("=== Raw OCR Output ===");
            Console.WriteLine(ocrEngine.Text);

            string cleaned = System.Text.RegularExpressions.Regex
                .Replace(ocrEngine.Text, @"\s+", " ")
                .Trim();

            Console.WriteLine("\n=== Cleaned OCR Output ===");
            Console.WriteLine(cleaned);
        }
        else
        {
            Console.WriteLine("OCR failed – verify the image path and quality.");
        }
    }
}
```

**Expected output**（サンプル画像に “Hello World” が含まれていると仮定）:

```
=== Raw OCR Output ===
Hello World

=== Cleaned OCR Output ===
Hello World
```

画像が大きく傾いている場合、`DeskewFilter` を追加する前は文字化けした出力が見られます。フィルタ適用後はテキストが読みやすくなり、目指した結果が得られます。

## よくある質問とエッジケース

| Question | Answer |
|----------|--------|
| *画像が 15° 以上回転している場合はどうすればいいですか？* | `DeskewFilter` の `MaxAngle` を増やします。45° まで安全ですが、極端な角度は手動で回転（`Image.Rotate(angle)`）する方が良い場合があります。 |
| *デスぺックル後も文字が抜け落ちます。* | `Strength` を 4‑5 に上げるか、デスぺックル前に `ContrastFilter` を追加してみてください。 |
| *PDF を直接処理できますか？* | はい—`PdfDocument` を使って各ページを画像にレンダリングし、同じパイプラインに渡します。 |
| *エンジンはスレッドセーフですか？* | スレッドごとに別々の `OcrEngine` インスタンスを作成してください。クラス自体はスレッドセーフでは保証されていません。 |
| *多言語文書はどう扱いますか？* | `ocrEngine.Language = OcrLanguage.Multilingual` と設定するか、ページごとに言語を切り替えます。 |

## 本番向け OCR のヒント

1. **バッチ処理:** フォルダ内の画像をループし、同一 `OcrEngine` インスタンスを再利用してオーバーヘッドを削減します。  
2. **ロギング:** `ocrEngine.LastError` を取得して、`Recognize()` が false を返したときの原因（未対応フォーマットや破損ファイルなど）を記録します。  
3. **パフォーマンス:** デスケーは最も CPU 負荷が高いステップです。画像がすでに水平であることが分かっている場合はフィルタを省略できます。  
4. **メモリ管理:** `ImageStream` オブジェクトは使用後に必ず `Dispose()`（例: `ocrEngine.Image.Dispose()`）して、長時間稼働するサービスでのメモリリークを防ぎます。  

## 結論

**画像のデスケー方法**、**ノイズ除去方法**、**OCR 用画像のロード方法**、そして **テキスト抽出方法** を Aspose OCR と C# で網羅しました。`DeskewFilter` と `DespeckleFilter` による前処理で、`Recognize()` がクリーンで検索可能な文字列を返す確率が大幅に向上します。

コードの最初の行から最終的なクリーン出力まで、手順はシンプルでありながら実務シナリオに十分対応できるパワフルさがあります。文書アーカイブサービス、レシートスキャンモバイルアプリ、バッチ処理バックエンドなど、さまざまな用途に活用できます。

次のステップに挑戦したいですか？ **言語検出** ステップを追加したり、業界固有の語彙に合わせた **カスタム OCR 辞書** を試したりして、精度をさらに高めてみましょう。可能性は無限大です。しっかりとした基盤ができたので、次は自由に創造してください。

Happy coding, and may your images always be perfectly straight! 

![デスケー後の修正された文書のイラスト](deskewed_example.png "画像のデスケー方法")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}