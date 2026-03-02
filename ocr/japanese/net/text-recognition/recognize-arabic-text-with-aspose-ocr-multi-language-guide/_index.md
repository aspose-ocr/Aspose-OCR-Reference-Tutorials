---
category: general
date: 2026-03-02
description: C# で Aspose OCR を使用してアラビア文字を瞬時に認識します。ウルドゥー語テキストの抽出、OCR 言語の変更、画像からテキストへの変換を、1
  つの実行可能なサンプルで学びましょう。
draft: false
keywords:
- recognize arabic text
- extract urdu text
- multi language ocr
- convert image to text
- change OCR language
language: ja
og_description: アラビア文字を素早く認識します。このガイドでは、ウルドゥー文字を抽出し、OCR 言語をリアルタイムで変更し、Aspose OCR を使用して
  C# で画像をテキストに変換する方法を示します。
og_title: Aspose OCRでアラビア語テキストを認識する – 完全マルチ言語チュートリアル
tags:
- OCR
- C#
- Aspose
- Multilingual
- Image Processing
title: Aspose OCRでアラビア語テキストを認識する – 多言語ガイド
url: /ja/net/text-recognition/recognize-arabic-text-with-aspose-ocr-multi-language-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose OCR でアラビア文字を認識する – 完全マルチランゲージチュートリアル

写真から **アラビア文字を認識** したいと思ったことはありませんか？ しかし、手間のかかるセットアップなしで対応できるライブラリが分からない…そんな方は多いです。レシートスキャナや看板翻訳、マルチリンガルチャットボットなど、実際のアプリでは画像から正確なアラビア文字を取得することが最初で、しばしば最も難しいステップです。

ポイントはこれです：Aspose OCR を使えばこの問題は簡単に解決できます。**アラビア文字を認識** できるだけでなく、**ウルドゥー文字を抽出** したり、言語をリアルタイムで切り替えたり、**画像をテキストに変換** したりでき、エンジンを再作成する必要はありません。このチュートリアルでは、これらを実現する単一の C# コンソールプログラムを順に解説し、各行が何故重要かを説明します。

ガイドを終えると、以下のように実行可能なコードスニペットが手に入ります。

* OCR エンジンを一度だけインスタンス化する。
* 言語をアラビア語に変更し、次にウルドゥー語に変更する。
* 任意の下流プロセスに渡せるクリーンな文字列を取得する。

外部サービス不要、隠されたマジックもなし――純粋な .NET コードだけです。

---

## 必要なもの

以下を事前に用意してください。

* **.NET 6+**（最新の LTS バージョンで問題ありません）。
* **Aspose.OCR for .NET** NuGet パッケージ – `dotnet add package Aspose.OCR` でインストール。
* 2 つのサンプル画像：アラビア文字が含まれるもの（`arabic_sign.png`）とウルドゥー文字が含まれるもの（`urdu_note.jpg`）。例: `C:\OCRSamples\` に配置。
* 基本的な C# の知識 – `Console.WriteLine` が書ければ十分です。

以上です。重たい OCR エンジンや GPU は不要です。さっそく始めましょう。

---

## ## recognize arabic text – Step 1: Create the OCR engine

最初に `OcrEngine` インスタンスを作成します。Aspose は必要に応じて言語パックをダウンロードするため、巨大なデータファイルを同梱する必要はありません。

```csharp
using Aspose.OCR;
using System.Drawing;

// Step 1: Create the OCR engine (resources are fetched lazily)
OcrEngine ocrEngine = new OcrEngine();
```

**Why this matters:**  
エンジンを一度だけ作成すればメモリと CPU サイクルを節約できます。言語ごとに新しいエンジンをインスタンス化すると、同じコア DLL を何度もロードして時間が無駄になります。遅延ダウンロードのため、最初の実行時にアラビア語パックの取得で一瞬止まることがありますが、2 回目以降は即座に処理できます。

> **Pro tip:** 大規模アプリ（例: Web API）ではエンジンをシングルトンとして保持し、初期化オーバーヘッドの繰り返しを防ぎましょう。

---

## ## extract urdu text – Step 2: Load an Arabic image and set the language

次にアラビア語画像をエンジンに読み込ませ、期待する言語を指定します。

```csharp
// Step 2: Load the Arabic image
Bitmap arabicImage = new Bitmap(@"C:\OCRSamples\arabic_sign.png");

// Tell the engine to use Arabic
ocrEngine.Language = OcrLanguage.Arabic;
```

**Why this matters:**  
OCR の精度は言語モデルに依存します。`OcrLanguage.Arabic` を明示的に設定することで、エンジンは正しい文字セット、合字処理、右から左へのレイアウト規則を適用します。このステップを省くと、Aspose は汎用モデルにフォールバックし、アクセント記号を誤認識しやすくなります。

---

## ## convert image to text – Step 3: Recognize the Arabic text

画像がロードされ言語が設定されたら、実際の認識は単一メソッド呼び出しで完了します。

```csharp
// Step 3: Recognize Arabic text
string arabicText = ocrEngine.Recognize(arabicImage);
Console.WriteLine("Arabic text: " + arabicText);
```

**Expected output (example):**

```
Arabic text: مرحبا بكم في متجرنا
```

結果が文字化けしている場合は、画像が鮮明かつコントラストが十分であるか、正しい言語が選択されているかを再確認してください。Aspose OCR は 300 dpi 以上の画像で最良の結果を出します。

---

## ## change OCR language – Step 4: Switch to Urdu without recreating the engine

ここがポイントです：同じエンジンインスタンスで言語を切り替えられます。再生成や破棄は不要です。

```csharp
// Step 4: Change the language to Urdu
ocrEngine.Language = OcrLanguage.Urdu;
```

**Why this matters:**  
バッチ処理パイプラインでフォルダー内に混在したスクリプトの文書がある場合に最適です。エンジンは内部でモデルを入れ替え、メモリ使用量は変わりません。

---

## ## extract urdu text – Step 5: Load a Urdu image and recognize it

同じエンジンでウルドゥー語画像を処理します。

```csharp
// Step 5: Load the Urdu image
Bitmap urduImage = new Bitmap(@"C:\OCRSamples\urdu_note.jpg");

// Recognize Urdu text
string urduText = ocrEngine.Recognize(urduImage);
Console.WriteLine("Urdu text: " + urduText);
```

**Sample output:**

```
Urdu text: یہ ایک مثال کا نوٹ ہے
```

やはりクリアな画像がクリーンなテキストを生みます。文字が抜けている場合は、解像度を上げるか、簡単な前処理（例: コントラスト伸張）を検討してください。

---

## ## multi language ocr – Full, runnable program

以下は新しいコンソールプロジェクトに貼り付けてすぐに実行できる完全版プログラムです。すべての手順が組み込まれており、コード内に非自明な部分へのコメントも付いています。

```csharp
using Aspose.OCR;
using System.Drawing;

class MultiLanguageOcrDemo
{
    static void Main()
    {
        // 1️⃣ Create the OCR engine – resources are pulled on demand
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Load Arabic image & set language
        Bitmap arabicImage = new Bitmap(@"C:\OCRSamples\arabic_sign.png");
        ocrEngine.Language = OcrLanguage.Arabic;

        // 3️⃣ Recognize Arabic text
        string arabicText = ocrEngine.Recognize(arabicImage);
        System.Console.WriteLine("Arabic text: " + arabicText);

        // 4️⃣ Switch engine to Urdu (no new instance needed)
        ocrEngine.Language = OcrLanguage.Urdu;

        // 5️⃣ Load Urdu image & recognize
        Bitmap urduImage = new Bitmap(@"C:\OCRSamples\urdu_note.jpg");
        string urduText = ocrEngine.Recognize(urduImage);
        System.Console.WriteLine("Urdu text: " + urduText);
    }
}
```

> **Expected console output** (実際の文字列は画像次第です):  
> ```
> Arabic text: مرحبا بكم في متجرنا
> Urdu text: یہ ایک مثال کا نوٹ ہے
> ```

---

## ## multi language ocr – Common pitfalls and how to avoid them

| Issue | Why it happens | Fix |
|-------|----------------|-----|
| **Blank result** | 画像の解像度が低すぎる、または言語パックのダウンロードが完了していない。 | 300 dpi 以上の画像を使用し、インターネット接続がある状態で一度プログラムを実行してパックを取得。 |
| **Garbage characters** | 言語が誤って設定されている（例: デフォルトの英語）。 | `ocrEngine.Language` を必ず `Recognize` 呼び出し前に設定。 |
| **Out‑of‑memory exception** | 巨大画像を `Bitmap` を破棄せずにロードしたままにしている。 | `using` ステートメントで `Bitmap` を囲むか、認識後に `Dispose()` を呼び出す。 |
| **Slow first run** | ネットワークが遅く言語パックのダウンロードに時間がかかる。 | 開発マシンで事前にパックをダウンロードするか、オフラインインストーラを利用してデプロイに同梱。 |

---

## ## convert image to text – Extending the demo

基本ができたら、次のような応用も考えられます。

* **フォルダー内の混在スクリプト画像を一括処理できるか？**  
  もちろん可能です。ファイルを列挙し、ファイル名や簡易言語検出ロジックで言語を判定し、`ocrEngine.Language` を設定してから `Recognize` を実行します。

* **PDF ファイルはどう扱う？**  
  Aspose OCR は `PdfDocument` のページをビットマップにレンダリングして受け取るか、Aspose.PDF を使って画像を抽出してから処理できます。

* **右から左への順序は手動で処理する必要があるか？**  
  必要ありません。エンジンは Unicode 文字列を正しい順序で返します（アラビア語・ウルドゥー語共に対応）。

---

## Conclusion

これで **アラビア文字を認識** し、**ウルドゥー文字を抽出** できるだけでなく、**OCR 言語をリアルタイムで切り替え**、**画像をテキストに変換** する単一の再利用可能エンジンの使い方を習得しました。完全なサンプルはそのまま実行可能で、Aspose がサポートする任意の言語に拡張できます。

次のステップは？ 認識した文字列を翻訳 API に渡す、検索インデックスに保存する、あるいはペルシャ語やクルド語など他言語を `OcrLanguage.Persian` や `OcrLanguage.Kurdish` に差し替えて試してみてください。

Happy coding, and may your OCR pipelines be ever accurate! 

--- 

*Image illustration (optional)*  
![アラビア文字認識例](https://example.com/arabic-ocr.png "アラビア OCR の実行例")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}