---
category: general
date: 2026-03-07
description: Java を使用して画像で OCR を実行する。PNG からテキストを認識する方法、レシートからテキストを抽出する方法、OCR 用に画像を読み込む方法を、完全な
  Java OCR の例とともに学びます。
draft: false
keywords:
- run OCR on image
- recognize text from png
- extract text from receipt
- java OCR example
- load image for OCR
language: ja
og_description: Javaで画像のOCRを実行する。このガイドでは、PNGからテキストを認識し、レシートからテキストを抽出し、完全なJava OCRサンプルを使用して画像をOCR用に読み込む方法を示します。
og_title: Javaで画像のOCRを実行 – GPUによるテキスト抽出
tags:
- OCR
- Java
- GPU
- Image Processing
title: Javaで画像のOCRを実行 – GPUによるテキスト抽出
url: /ja/java/advanced-ocr-techniques/run-ocr-on-image-with-java-gpu-powered-text-extraction/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Javaで画像のOCRを実行 – GPUによる高速テキスト抽出

Javaで **画像のOCRを実行** したいと思ったことはありますか？しかし、どこから始めればよいか分からないことも多いでしょう。スキャンしたレシートや PNG のスクリーンショットからテキストを抽出しようとしたとき、多くの開発者が同じ壁にぶつかります。  

このチュートリアルでは、**complete Java OCR example**（完全な Java OCR の例）を順を追って解説します。この例は **recognizes text from PNG**（PNG ファイルからテキストを認識）するだけでなく、**extract text from receipt**（レシート画像からテキストを抽出）する方法も示し、速度向上のために GPU 加速を活用します。最後まで読むと、OCR 用に画像を読み込み、処理し、プレーンテキスト結果を出力する、すぐに実行できるプログラムが手に入ります。

## 学べること

- `ImageInputStream` を使ったシンプルな方法で **load image for OCR**（OCR 用画像の読み込み）を行う方法。
- GPU サポートを有効にし、エンジンが最新ハードウェア上でより高速に動作するようにすること。
- **recognize text from PNG**（PNG からテキストを認識）し、レシートから有用な文字列を抽出する正確な手順。
- 一般的な落とし穴（例：GPU デバイス ID が間違っている）とベストプラクティスのヒント。
- IDE にコピー＆ペーストできる、完全で実行可能なコードスニペット。

**前提条件**

- Java 17 以上（コードは簡潔さのために `var` キーワードを使用していますが、Java 8 を使用している場合は明示的な型に置き換えることができます）。
- `OcrEngine`、`ImageInputStream`、`OcrResult` クラスを提供する OCR ライブラリ（例として架空の *FastOCR* SDK を挙げていますが、実際に使用しているものに置き換えてください）。
- パフォーマンス向上を望む場合は GPU 対応マシン（任意ですが推奨）。

---

## ステップ 1: 画像で OCR を実行 – GPU 加速を有効化

最初に行うべきことは OCR エンジンを作成し、GPU を使用するよう指示することです。このステップは重要で、GPU サポートがない場合、エンジンは CPU にフォールバックし、高解像度のレシートでは顕著に遅くなります。

```java
// Step 1: Create the OCR engine and enable GPU acceleration
OcrEngine ocrEngine = new OcrEngine();

// Turn on GPU usage – this makes the recognition much faster
ocrEngine.getConfig().setUseGpu(true);          // enable GPU usage

// Optional: select which GPU device to use (0 = first GPU)
ocrEngine.getConfig().setGpuDeviceId(0);
```

**Why this matters:**  
GPU 加速は OCR エンジンが行う重い行列計算をオフロードします。GPU が複数ある場合は、`setGpuDeviceId` の値を変更してメモリが最も多いものを選択できます。GPU を有効にし忘れることは「なぜ OCR が遅いのか？」という不満の一般的な原因です。

> **Pro tip:** マシンに対応する GPU がない場合、`setUseGpu(true)` の呼び出しは単に無視されます—クラッシュは起きず、処理が遅くなるだけです。

---

## ステップ 2: OCR 用に画像を読み込む

エンジンの準備ができたので、画像を供給する必要があります。以下の例は、ディスク上に保存された PNG のレシートを読み込む方法を示しています。パスは OCR ライブラリがサポートする任意の画像形式に置き換えることができます。

```java
// Step 2: Load the image you want to recognize
ImageInputStream imageStream = new ImageInputStream("YOUR_DIRECTORY/receipt.png");
```

**Edge case:**  
ファイルが存在しない、またはパスが間違っている場合、`ImageInputStream` は `IOException` をスローします。呼び出しを try‑catch ブロックで囲み、役立つメッセージをログに記録してください：

```java
try {
    ImageInputStream imageStream = new ImageInputStream("YOUR_DIRECTORY/receipt.png");
} catch (IOException e) {
    System.err.println("Failed to load image: " + e.getMessage());
    return;
}
```

---

## ステップ 3: PNG からテキストを認識する

画像が読み込まれたので、OCR エンジンはいよいよ処理を開始できます。このステップは実際に **recognizes text from PNG**（PNG（または他のサポート形式）からテキストを認識）し、`OcrResult` オブジェクトを返します。

```java
// Step 3: Run the OCR process on the image
OcrResult ocrResult = ocrEngine.recognize(imageStream);
```

**What’s happening under the hood?**  
エンジンは前処理（傾き補正、二値化）を行い、文字を検出するニューラルネットワークを実行し、結果をテキスト行に組み立てます。先ほど GPU を有効にしたため、これらのニューラルネットワーク計算はグラフィックカード上で行われ、全体の実行時間が数秒短縮されます。

---

## ステップ 4: レシートからテキストを抽出する

認識が完了したら、通常は生のテキストだけが欲しいでしょう。`OcrResult` クラスは通常 `getText()` メソッドを提供し、単一の `String` を返します。その後、後処理（例：合計金額や日付を抽出する正規表現）を行うことができます。

```java
// Step 4: Print the recognized plain‑text result
System.out.println("Recognized text:");
System.out.println(ocrResult.getText());
```

**典型的なレシート出力:**  

```
Store: Coffee Corner
Date: 2026-03-07
Item      Qty   Price
Latte      2    $5.80
Muffin     1    $2.50
TOTAL           $8.30
```

この文字列を自分のパーサーに渡すことで、合計金額や項目、税情報などを抽出できます。

---

## ステップ 5: 完全な Java OCR 例 – 実行可能

すべてをまとめると、`Main.java` ファイルに貼り付けられる **complete Java OCR example**（完全な Java OCR 例）があります。OCR ライブラリがクラスパスに含まれていることを確認してください。

```java
import com.fastocr.OcrEngine;
import com.fastocr.ImageInputStream;
import com.fastocr.OcrResult;

public class Main {
    public static void main(String[] args) {
        // 1️⃣ Create OCR engine and enable GPU
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.getConfig().setUseGpu(true);          // enable GPU usage
        ocrEngine.getConfig().setGpuDeviceId(0);        // optional: select GPU #0

        // 2️⃣ Load the image you want to recognize
        ImageInputStream imageStream;
        try {
            imageStream = new ImageInputStream("YOUR_DIRECTORY/receipt.png");
        } catch (Exception e) {
            System.err.println("Error loading image: " + e.getMessage());
            return;
        }

        // 3️⃣ Run OCR on the image
        OcrResult ocrResult = ocrEngine.recognize(imageStream);

        // 4️⃣ Output the plain‑text result
        System.out.println("Recognized text:");
        System.out.println(ocrResult.getText());
    }
}
```

**期待されるコンソール出力**（上記のサンプルレシートを想定）:

```
Recognized text:
Store: Coffee Corner
Date: 2026-03-07
Item      Qty   Price
Latte      2    $5.80
Muffin     1    $2.50
TOTAL           $8.30
```

出力が文字化けしている場合は、画像が鮮明（高 DPI）であること、OCR の言語パックがレシートの言語と一致していることを再確認してください。

---

## よくある質問と落とし穴

| Question | Answer |
|----------|--------|
| *GPU が検出されない場合は？* | エンジンは自動的に CPU にフォールバックします。ドライバを確認し、`setGpuDeviceId` が実在するデバイスに一致しているか確認してください（Linux では `nvidia-smi` が役立ちます）。 |
| *JPEG や TIFF ファイルを処理できますか？* | はい。`ImageInputStream` のファイル拡張子を変更するだけです。OCR ライブラリは通常、フォーマットを自動検出します。 |
| *多数のレシートをバッチ処理する方法はありますか？* | 認識コードをループで囲み、同じ `OcrEngine` インスタンスを再利用してください。画像ごとに再初期化すると GPU メモリが無駄になります。 |
| *低コントラストのレシートの精度を向上させるには？* | OCR エンジンに渡す前に画像を前処理（コントラストを上げ、グレースケールに変換）してください。一部のライブラリは `preprocess` API を提供しています。 |

---

## 結論

Java で画像ファイルに対して **run OCR on image**（画像の OCR を実行）する方法が分かりました。画像の読み込みからレシートのクリーンなテキスト抽出までカバーしています。このウォークスルーでは **recognize text from PNG**、**extract text from receipt** を取り上げ、任意のプロジェクトに適用できる **java OCR example** を示しました。  

次のステップは？GPU フラグをオフにしてパフォーマンス差を確認したり、画像解像度を変えて実験したり、正規表現ベースのパーサーを統合して合計金額を自動抽出したりしてみてください。より高度なトピックに興味がある場合は、**OCR post‑processing**、**language model correction**、**batch processing pipelines** を調べてみましょう。  

楽しいコーディングを、そしてレシートが常に読みやすいことを願っています！  

![画像で OCR を実行する例](/images/run-ocr-on-image.png "画像で OCR を実行 – Java の例")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}