---
category: general
date: 2026-02-19
description: OCR のために画像の傾きを補正し、ノイズを除去する方法を学びます。このチュートリアルでは、テキスト画像の認識、画像の回転補正、そして Aspose
  OCR を使用した画像の前処理方法を示します。
draft: false
keywords:
- how to deskew image
- recognize text image
- how to remove noise
- correct image rotation
- preprocess image ocr
language: ja
og_description: 画像の傾きを補正し、ノイズを除去してテキスト画像を高速に認識する方法。Aspose を使用して画像の回転を修正し、OCR 前処理を行うガイドです。
og_title: 画像の傾き補正方法 – 完全OCR前処理チュートリアル
tags:
- OCR
- Java
- Image Processing
title: 画像の傾き補正方法 — ステップバイステップ OCR 前処理ガイド
url: /ja/java/ocr-operations/how-to-deskew-image-step-by-step-ocr-pre-processing-guide/
---

. So fine.

Now produce final content.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 画像の傾き補正方法 — 完全OCR前処理チュートリアル

OCRエンジンに渡す前に、画像の傾き補正（**how to deskew image**）を行う方法を考えたことはありますか？ 例えば、領収書の束をスキャンしたときに、ページが少し傾いていたり、ランダムなドットが散らばっていたりするかもしれません。これは一般的な悩みで、傾いたりノイズの多い画像は文字認識を妨げます。

良いニュースです。Aspose.OCR を使えば、数行の Java コードで画像の回転補正（correct image rotation）とノイズ除去（how to remove noise）を行うことができます。このガイドでは、ノイズがあり回転した PNG を読み込み、deskew と median denoise を適用し、**recognize text image** して結果を出力するまでの全工程を解説します。最後まで読めば、任意の Java プロジェクトに組み込める再利用可能なスニペットが手に入ります。

## 必要なもの

- **Java 17** 以上（コードは古いバージョンでもコンパイルできますが、17 が最適です）。
- **Aspose.OCR for Java** – 最新の JAR は Maven Central（`com.aspose:aspose-ocr`）から取得できます。
- 回転とノイズが混在した画像ファイル（例：`noisy-rotated.png`）。
- 軽量な IDE（IntelliJ、Eclipse、あるいは VS Code でも可）。

特別なビルドツールは不要です。シンプルに `javac` + `java` で実行すれば問題ありません。

## ステップ 1 – OCR エンジンインスタンスの作成  

最初に行うのは `OcrEngine` のインスタンス化です。これは後で文字を読み取る脳のようなものと考えてください。

```java
import com.aspose.ocr.*;

public class PreprocessExample {
    public static void main(String[] args) throws Exception {

        // Initialize the OCR engine – this object holds all settings
        OcrEngine ocrEngine = new OcrEngine();
```

> **プロのコツ:** 多数の画像を処理する場合はエンジンをシングルトンとして保持すると、内部バッファが再利用され、処理が高速化します。

## ステップ 2 – Deskew と Median Denoise の有効化（How to Remove Noise）  

ここでエンジンに **correct image rotation** と **how to remove noise** を指示します。どちらのフィルタもオプションですが、組み合わせることで精度が大幅に向上します。

```java
        // Turn on preprocessing filters
        ocrEngine.getPreprocessing().setDeskew(true);          // fixes rotation
        ocrEngine.getPreprocessing().setMedianDenoise(true);   // smooths out speckles
```

なぜ median denoise かというと、文字を構成するエッジ（線）を保持しつつ、孤立したピクセルを除去するからです。これがクリーンな OCR に必要な要素です。

## ステップ 3 – 処理対象画像の読み込み  

ここでは、エンジンにクリーニング対象のファイルを指定します。`ImageStream.fromFile` は PNG をメモリに読み込みます。

```java
        // Load the noisy‑rotated image
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/noisy-rotated.png"));
```

画像がリモートサーバ上にある場合は、代わりに `InputStream` を渡すだけです—Aspose がスムーズに処理します。

## ステップ 4 – OCR を実行し、認識テキストを取得  

前処理が有効になっているので、エンジンは補正された画像を読み取ります。`recognize()` 呼び出しは抽出された文字列を含む `RecognitionResult` を返します。

```java
        // Perform OCR – the engine automatically applies deskew & denoise first
        String recognizedText = ocrEngine.recognize().getText();

        // Show the output
        System.out.println("=== Recognized Text ===");
        System.out.println(recognizedText);
    }
}
```

元の画像が傾いていたり粒状であっても、コンソールにクリーンで読みやすいテキストが表示されるはずです。

## ステップ 5 – 結果の検証（期待される出力）  

すべてが正常に動作すると、コンソールには次のような出力が表示されます。

```
=== Recognized Text ===
Invoice #12345
Date: 2026‑02‑15
Total: $1,234.56
```

出力にまだ文字化けがある場合は、以下を再確認してください。

- 画像の解像度（理想は ≥ 300 dpi）。
- ファイルパスが正しいか。
- 追加のフィルタ（例：`setContrastStretch`）が有効かどうか。

## オプション: 例画像で視覚的に確認  

以下は、傾いてノイズのある領収書の小さなプレビューです。傾きに注目してください—このコードが自動で補正します。

![画像の傾き補正方法の例](deskew-demo.png "画像の傾き補正方法")

*Alt text: 画像の傾き補正方法 – 前後の処理*

## よくある質問

### PDF でも動作しますか、それとも PNG/JPEG のみですか？

Aspose.OCR は PDF を直接読み取れます。`ImageStream.fromFile` を `ImageStream.fromPdf` に置き換えるだけです。同じ前処理フラグが適用されるので、**how to deskew image** と **how to remove noise** が引き続き利用できます。

### 後続の処理で元の向きを保持したい場合は？

前処理を行う前に画像をクローンすることができます。

```java
Image original = ocrEngine.getImage().clone();
ocrEngine.getPreprocessing().apply(); // modifies the internal copy
// Use original later if needed
```

### デスクュー角度を手動で変更できますか？

はい。`setDeskewAngle(double degrees)` を使用すれば、オートデテクトアルゴリズムを上書きして角度を手動で設定できます。極端な回転でオートデテクトが失敗する場合に便利です。

### Median Denoise は Gaussian Blur とどう違うのですか？

Median フィルタは各ピクセルを周囲の中央値に置き換えるため、エッジを保持します。Gaussian Blur はすべてを平滑化し、文字のストロークまでぼやけさせる可能性があるため、OCR では median の方が安全です。

## まとめ  

このチュートリアルでは **how to deskew image** ファイルの方法を解説し、**how to remove noise** を実演し、Aspose OCR の組み込み前処理を使って **recognize text image** を行う方法を示しました。`setDeskew(true)` と `setMedianDenoise(true)` を有効にするだけで、**correct image rotation** とノイズ除去が自動的に行われ、乱雑なスキャンがクリーンなテキスト文字列に変換されます。

自由に試してみてください。異なるノイズ除去手法を試したり、PDF を入力したり、ループで複数画像を連結したりできます。同じパターン（engine → preprocess → recognize）はすべてのシナリオで機能し、あらゆる OCR パイプラインの堅実な基盤となります。

**次のステップ** として以下を検討できます：

- **バッチ処理** – 画像フォルダを走査し、各結果を `.txt` ファイルに書き出す。
- **言語パック** – 特定の言語辞書をロードして、英語以外のテキストの精度を向上させる。
- **高度なフィルタ** – 低コントラストスキャン向けに `setContrastStretch` や `setBinarization` など。

他に質問がありますか？ コメントを残してください。コーディングを楽しんで！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}