---
category: general
date: 2026-06-22
description: C#でAspose.OCRを使用して画像のOCRを実行します。pngからテキストを抽出し、画像をテキストに変換し、ロシア語を含むpngのテキストを認識する方法を学びます。
draft: false
keywords:
- perform ocr on image
- extract text from png
- convert image to text
- recognize text from png
- read russian text
language: ja
og_description: C# と Aspose.OCR を使用して画像の OCR を実行します。このガイドでは、png からテキストを抽出し、画像をテキストに変換し、ロシア語テキストを効率的に読み取る方法を示します。
og_title: Aspose.OCRで画像のOCRを実行する – C#チュートリアル
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Perform OCR on image using Aspose.OCR in C#. Learn to extract text
    from png, convert image to text, and recognize text from png including Russian
    language.
  headline: Perform OCR on Image with Aspose.OCR – Complete C# Guide
  type: TechArticle
tags:
- OCR
- C#
- Aspose
title: Aspose.OCRで画像のOCRを実行する – 完全なC#ガイド
url: /ja/net/text-recognition/perform-ocr-on-image-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.OCR を使用した画像の OCR 実行 – 完全 C# ガイド

画像ファイルで **OCR を実行** したいのに、適切なライブラリを探すのに何時間も費やしたことはありませんか？ 私の経験では、Aspose.OCR を使えば、特にキリル文字で書かれた **png からテキストを抽出** する場合でも、まるで公園を散歩するかのように簡単です。  

このチュートリアルでは、実際の例を通して **画像をテキストに変換** するだけでなく、**png からテキストを認識** し、**ロシア語テキストを読み取る** 方法を示します。最後まで読めば、OCR 結果をコンソールに直接出力する実行可能なコンソール アプリが手に入ります。

---

![画像の OCR 実行ワークフロー図](image-placeholder.png "画像の OCR 実行ワークフロー図")

## 画像の OCR 実行 – 手順ごとの実装

以下は完全に実行可能なコードです。新しいコンソール プロジェクトにコピー＆ペーストして F5 を押すだけで、魔法が起きます。

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

class Program
{
    static void Main()
    {
        // Step 1: Load your Aspose.OCR license (if you have one)
        var license = new License();
        // license.SetLicense("Aspose.OCR.lic");   // uncomment and provide the path to your license file

        // Step 2: Create an OCR engine (CPU mode is the default)
        var ocrEngine = new OcrEngine();

        // Step 3: Specify the language to recognize – Russian (Cyrillic)
        ocrEngine.Language = OcrLanguage.Russian;

        // Step 4: (Optional) Set a download timeout for language resources, in seconds
        ocrEngine.ResourceDownloadTimeout = 120;

        // Step 5: Perform OCR on the image file
        var ocrResult = ocrEngine.RecognizeImage(@"YOUR_DIRECTORY/sample_russian.png");

        // Step 6: Output the recognized plain‑text
        System.Console.WriteLine(ocrResult.Text);
    }
}
```

プログラムを実行すると、次のような出力が得られます。

```
Привет, мир!
Это тестовое изображение.
```

この出力は、**画像の OCR を実行** し、**ロシア語テキストを読み取る**ことに成功したことを示しています。

---

## PNG からテキストを抽出 – ファイルの読み込み

エンジンが作業を開始する前に、ビットマップが必要です。`RecognizeImage` メソッドは、サポートされている任意のラスタ形式へのパスを受け取りますが、PNG はロスレスなスクリーンショットに最も一般的です。  

> **なぜ PNG？** ピクセルがすべて保持されるため、OCR エンジンはキャプチャしたデータと全く同じ情報を見ます。圧縮アーティファクトが認識を妨げることはありません。

JPEG や BMP を扱う場合も、拡張子を変更すれば同じ呼び出しが機能します。重要なのは、ファイルが存在し、アプリに読み取り権限があることです。

---

## 画像をテキストに変換 – コンテンツの認識

チュートリアルの核心はステップ 5 の **画像をテキストに変換** です。内部では、Aspose.OCR が画像を読み込み、キリル文字用に訓練されたニューラル ネットワークを通して処理し、プレーンテキスト文字列を返します。  

実用的なヒントをいくつか:

* **Tip:** 文字化けが発生したら、`ResourceDownloadTimeout` を伸ばすか、言語パックを事前にダウンロードしてネットワークの遅延を回避してください。
* **Tip:** 複数ページの PDF の場合は、各ページ画像に対してループし、結果を連結します。ページごとに同じ **画像の OCR を実行** 呼び出しを行うだけです。

---

## ロシア語テキストを読む – 言語の設定

「ロシア語を手動で指定しなければならないの？」と疑問に思うかもしれません。簡潔に言えば **はい**、最適な精度を得るには必要です。`ocrEngine.Language = OcrLanguage.Russian;` と設定することで、エンジンはキリル文字セットとロシア語モデルをロードします。  

このステップを省略すると、エンジンはデフォルトで英語を使用し、ロシア語文字は疑問符や意味不明な文字に変換されます。したがって、必ず **ロシア語テキストを読む** ために言語を明示的に設定してください。

---

## PNG からテキストを認識 – タイムアウトとリソースの扱い

OCR エンジンが初回に言語リソースを取得する際、ネットワーク遅延が問題になることがあります。`ResourceDownloadTimeout` プロパティ（ステップ 4）は安全策として機能します。  

* **調整が必要なとき:** 低速な社内 VPN を使用している場合は、タイムアウトを 180 秒に伸ばしてください。
* **調整しなくて良いとき:** ローカルに事前インストールされた言語パックを使用している場合、デフォルトの 120 秒で十分です。

---

## PNG からテキストを抽出 – ライセンス管理（任意）

Aspose.OCR はトライアル モードでそのまま使用できますが、ライセンスを適用すると透かしが除去され、フル API が解放されます。制限なく **画像の OCR を実行** したい場合は、ライセンス行のコメントを外し、`.lic` ファイルへのパスを指定してください。  

```csharp
var license = new License();
license.SetLicense(@"C:\Licenses\Aspose.OCR.lic");
```

---

## 画像をテキストに変換 – プロジェクト全体チェックリスト

| ✅ | 項目 |
|---|------|
| 1 | NuGet で **Aspose.OCR** をインストール (`Install-Package Aspose.OCR`) |
| 2 | `using Aspose.OCR;` と `using Aspose.OCR.Models;` を追加 |
| 3 | （任意）ライセンスを適用 |
| 4 | `OcrEngine` インスタンスを作成 |
| 5 | `Language = OcrLanguage.Russian` を設定して **ロシア語テキストを読む** |
| 6 | 必要に応じて `ResourceDownloadTimeout` を調整 |
| 7 | `RecognizeImage(@"path\to\file.png")` を呼び出して **画像の OCR を実行** |
| 8 | `ocrResult.Text` を出力 – これで **png からテキストを抽出** 完了！ |

---

## よくある質問とエッジケース

**PNG に英語とロシア語の両方が含まれている場合は？**  
`ocrEngine.Language = OcrLanguage.Multilingual;` と設定すれば、複合モデルがロードされます。エンジンは依然として **png からテキストを認識** できますが、言語パックのサイズがやや大きくなります。

**画像フォルダー全体を処理したい場合は？**  
もちろん可能です。`foreach (var file in Directory.GetFiles(folder, "*.png"))` ループで `RecognizeImage` 呼び出しをラップすれば、各イテレーションで **画像の OCR を実行** し、結果を `.txt` ファイルに書き出すことができます。

**低解像度画像はどうですか？**  
解像度が 72 dpi 未満になると OCR の品質が低下します。ぼやけたスクリーンショットの場合は、Aspose.OCR に渡す前に画像処理ライブラリで拡大することを検討してください。ライブラリ自体がピクセル品質を自動的に向上させることはありません。

---

## 本番環境向け OCR のプロ・ティップ

* **結果をキャッシュ:** プレーンテキストをデータベースに保存し、変更のないファイルに対して OCR を再実行しないようにします。
* **出力を検証:** 正規表現で結果が空かどうかをチェックし、空の場合はタイムアウトを伸ばして再試行します。
* **並列処理:** 大量処理では、スレッドごとに独立した `OcrEngine` インスタンスを作成して並列実行します。各スレッドが自分のエンジンを持てば、Aspose.OCR はスレッドセーフです。

---

## 結論

Aspose.OCR を使って **画像の OCR を実行** し、**png からテキストを抽出**、**画像をテキストに変換**、**png からテキストを認識**、そして **ロシア語テキストを読む** 方法を実証しました。完全なソリューションは単一の `Main` メソッドに収まりますが、数点の調整でエンタープライズ規模のシナリオにも拡張可能です。

次のステップに挑戦してみませんか？ **ImageSharp** のようなライブラリで画像前処理（デスキュー、ノイズ除去）を追加したり、OCR 結果を JSON にエクスポートして下流の分析に活用したりしてみましょう。C# で OCR の基礎をマスターすれば、可能性は無限です。

Happy coding, and may your images always be legible!

## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示したテクニックを基に、さらに関連するトピックを深掘りします。各リソースには、ステップバイステップの解説と完全動作コード例が含まれており、API の追加機能や代替実装アプローチを自分のプロジェクトで試すのに役立ちます。

- [Aspose.OCR を使用した言語選択付き C# で画像テキストを抽出](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [複数言語対応の Aspose OCR で画像テキストを認識](/ocr/english/net/ocr-settings/working-with-different-languages/)
- [画像 URL から OCR を実行 – 画像をテキストに変換](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}