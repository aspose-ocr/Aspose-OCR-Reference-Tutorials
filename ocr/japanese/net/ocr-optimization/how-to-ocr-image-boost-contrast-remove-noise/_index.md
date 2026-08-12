---
category: general
date: 2026-02-22
description: Aspose OCRで画像をOCRする方法 – 画像ノイズを除去し、コントラストを高め、C#でテキスト画像を素早く抽出する。
draft: false
keywords:
- how to ocr image
- remove image noise
- boost image contrast
- extract text image
- recognize image text
language: ja
og_description: Aspose OCR を使用して画像を OCR し、ノイズを除去し、コントラストを強化し、C# でテキスト画像を抽出する方法を、完全な実行可能サンプルとともに学びましょう。
og_title: 画像のOCR方法 – コントラストを上げてノイズを除去
tags:
- OCR
- C#
- Image Processing
title: 画像のOCR方法：コントラストを強化し、ノイズを除去
url: /ja/net/ocr-optimization/how-to-ocr-image-boost-contrast-remove-noise/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 画像の OCR 方法 – コントラストを上げてノイズを除去する C#

歪んでいたり、粒状だったり、読みにくい **画像の OCR** を行う方法を考えたことはありませんか？ あなたは一人ではありません。 多くの実務プロジェクト—例えばレシートのスキャンや古い文書のデジタル化—では、生の画像が完璧であることはほとんどありません。 良いニュースは、C# と Aspose OCR の数行のコードで **画像ノイズの除去**、**画像コントラストの向上**、そして最終的に **画像からテキストを抽出** できることです。

このチュートリアルでは、完全なエンドツーエンド ソリューションを順を追って解説します。 最後まで読むと、OCR エンジンの設定方法、ノイズの多い画像のクリーンアップ方法、そして **画像テキストの認識** 方法が正確に分かり、結果を好きな場所へパイプできるようになります。 曖昧な参照は一切なく、実行可能なコードサンプルと各選択の根拠だけを提供します。

## 必要なもの

- .NET 6+（または .NET Core 3.1+ – API は同じです）
- Aspose.OCR NuGet パッケージ（`Install-Package Aspose.OCR`）
- 歪んでいてノイズが多いサンプル画像（例: `skewed_noisy.jpg`）
- お好みの IDE – Visual Studio、Rider、または VS Code で構いません

以上です。 これらが揃っていれば、すぐにコードに取り掛かれます。

![画像の OCR 例](/images/ocr-demo.png){alt="画像の OCR 例"}

## ステップ 1: OCR エンジンの初期化 – 正しく画像の OCR を行う方法  

最初に行うべきことは `OcrEngine` インスタンスを作成し、期待する言語を指定することです。 英語が最も一般的ですが、Aspose は多数の言語を標準でサポートしています。

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Filters;

class Program
{
    static void Main()
    {
        // Create the OCR engine and set the language to English.
        var ocrEngine = new OcrEngine { Language = Language.English };
```

**なぜ重要か:** エンジンは文字セットを把握している必要があります。 そうでなければ文字を推測するために余計なサイクルを消費し、精度が低下します。 言語を事前に設定しておくことで、必要な言語データだけをロードし、メモリ使用量も削減できます。

## ステップ 2: 画像を読み込み、画像ノイズの除去を開始  

次にディスクから画像を取得します。 多くの場合、ファイルは JPEG または PNG で、粒状ノイズが多く含まれています。 それを `Image` オブジェクトにロードすると、フィルタに渡せるハンドルが得られます。

```csharp
        // Load the input image (skewed and noisy)
        var inputImage = Image.Load(@"YOUR_DIRECTORY/skewed_noisy.jpg");
```

**プロのコツ:** 画像がクラウドバケットにある場合は、`Image.Load(Stream)` を使って直接ストリームから読み込めます。 これにより一時ファイルを書き出す手間が省けます。

## ステップ 3: フィルタチェーンを適用 – コントラストを上げノイズを除去  

Aspose OCR には便利なフィルタパイプラインが用意されています。 ここでは 3 つのフィルタをチェーンします。

1. **DeskewFilter** – 回転を補正し、テキストを水平にします。  
2. **DenoiseFilter** – 文字をぼかさずに粒状ノイズを除去します。  
3. **ContrastFilter** – 前景と背景の差を増幅し、薄い文字を際立たせます。

```csharp
        // Pre‑process the image with a chain of filters
        var processedImage = inputImage
            .Apply(new DeskewFilter())          // correct rotation
            .Apply(new DenoiseFilter())         // reduce grain
            .Apply(new ContrastFilter(1.5f));   // boost contrast
```

**なぜこれらのフィルタか？**  
- **Deskew** は正確な OCR に必須です。 数度のずれでも認識率が半減します。  
- **Denoise** はスマートフォンで撮影したスキャン画像に頻出する「画像ノイズ」問題を解決します。  
- **Contrast** は低コントラスト文書（色あせたレシートなど）の秘密の調味料です。  

`ContrastFilter` の factor（デフォルトは `1.0f`）は調整可能です。 `1.5f` 以上にすると画像が過度に露出することがあるので、数回試してみてください。

## ステップ 4: 画像テキストの認識 – 画像の OCR の核心  

画像がクリアになったら、OCR エンジンに渡します。

```csharp
        // Recognize text from the processed image
        var ocrResult = ocrEngine.Recognize(processedImage);
```

`Recognize` メソッドは抽出された文字列、信頼度スコア、必要に応じてハイライト用のバウンディングボックスを含む `OcrResult` オブジェクトを返します。

**エッジケース:** 画像に複数言語が混在している場合は `ocrEngine.Language = Language.English | Language.Spanish;` のように設定できます。 エンジンは両方の辞書を試します。

## ステップ 5: 結果の表示と検証 – アプリでテキスト画像を抽出  

最後にコンソールへテキストを出力します。 実際のアプリケーションでは、データベースやファイルに書き込んだり、下流の NLP パイプラインに渡したりすることが考えられます。

```csharp
        // Display the extracted text
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**期待される出力:**  

```
=== OCR Result ===
Invoice #12345
Date: 2024‑01‑15
Total: $256.78
Thank you for your business!
```

文字化けが見られる場合は、ステップ 3に戻ってフィルタパラメータを調整してください。 多くの場合、コントラスト factor を上げるか、追加で `SharpenFilter` を適用すれば解決します。

## よくある質問とヒント  

### 画像がすでに白黒の場合はどうすればいいですか？  
`ContrastFilter` を省略し、`DenoiseFilter` のみを使用してください。 バイナリ画像に過度のコントラストをかけるとアーティファクトが発生します。

### 10 MB 超の大容量ファイルはどう処理すればいいですか？  
フィルタ処理前に低解像度で読み込みます（例: `Image.Load(path, new LoadOptions { DesiredWidth = 2000 })`）。 テキストが判読可能であれば、縮小版でも OCR エンジンは問題なく動作します。

### Web API で実行できますか？  
もちろんです。 同じロジックを ASP.NET Core コントローラにラップし、`IFormFile` を受け取って OCR 結果を JSON で返すだけです。 `Image` オブジェクトは必ず Dispose してリソースを解放してください。

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}