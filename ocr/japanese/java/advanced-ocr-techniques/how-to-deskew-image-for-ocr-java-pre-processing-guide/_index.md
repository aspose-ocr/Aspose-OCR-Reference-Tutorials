---
category: general
date: 2026-03-18
description: Aspose OCR Java を使用して画像を素早くデスキューする方法。OCR 用に画像を前処理し、スキャン画像をクリーンアップして、数ステップで
  OCR の精度を向上させる方法を学びましょう。
draft: false
keywords:
- how to deskew image
- preprocess image for ocr
- extract text from image
- clean scanned image
- improve ocr accuracy
language: ja
og_description: Aspose OCR Javaで画像の傾きを補正する方法、OCR用に画像を前処理する方法、スキャン画像をクリーンアップしてOCR精度を向上させる方法。
og_title: OCR用画像のデスキュー方法 – Javaガイド
tags:
- OCR
- Java
- Image Processing
title: OCR用画像の傾き補正方法 – Java 前処理ガイド
url: /ja/java/advanced-ocr-techniques/how-to-deskew-image-for-ocr-java-pre-processing-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR 用画像の傾き補正方法 – Java 前処理ガイド

スキャナーから奇妙な角度で出力される画像ファイルの**画像の傾き補正方法**を疑問に思ったことはありませんか？ あなただけではありません—画像が多い文書からテキストを抽出しようとすると、多くの開発者が同じ問題に直面します。 良いニュースは？ Java と Aspose OCR の数行で、画像を真っ直ぐにし、ノイズ除去し、スムーズにクリーンなテキストを取得できます。

このチュートリアルでは、全体のワークフローを順に解説します：ノイズが多く回転したスキャン画像の読み込み、DeskewFilter の適用、視覚的な雑音の除去、そして最終的に**画像からテキストを抽出**します。最後まで読むと、**OCR 用画像の前処理**、**スキャン画像のクリーニング**、そして**OCR 精度の向上**の方法が分かります。

## 必要なもの

- Java 17（または最近の JDK） – コードは標準の言語機能を使用します。  
- Aspose OCR for Java ライブラリ（無料トライアルで実験は十分可能です）。  
- ノイズが多く回転したサンプル画像（例：`noisy-rotated.png`）。  
- お好きな IDE（IntelliJ IDEA、Eclipse、VS Code…） – Java をコンパイルできる環境なら何でも可。

追加のフレームワークは不要です。Maven/Gradle の設定も不要で、インポート文は下記のものだけです。

---

## Aspose OCR を使用した画像の傾き補正方法

最初に取り組むべきは画像の傾きです。テキスト行が水平でないと、OCR エンジンは文字を誤認識します。`DeskewFilter` がその重い作業を担います。

```java
import com.aspose.ocr.OcrEngine;
import com.aspose.ocr.Image;
import com.aspose.ocr.preprocess.DeskewFilter;
import com.aspose.ocr.preprocess.DenoiseFilter;

public class PreprocessDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the raw scanned image
        Image scannedImage = Image.load("YOUR_DIRECTORY/noisy-rotated.png");

        // Step 3: Correct the image orientation (deskew)
        DeskewFilter deskewFilter = new DeskewFilter();
        scannedImage = deskewFilter.apply(scannedImage);

        // Step 4: Reduce visual noise (denoise)
        DenoiseFilter denoiseFilter = new DenoiseFilter();
        scannedImage = denoiseFilter.apply(scannedImage);

        // Step 5: Perform OCR on the cleaned image
        String recognizedText = ocrEngine.recognize(scannedImage);

        // Step 6: Output the extracted text
        System.out.println(recognizedText);
    }
}
```

> **Why this matters:** `DeskewFilter` は画像の幾何情報を解析し、回転角度を推定してビットマップを水平に戻します。このステップがなければ、ほとんどの OCR エンジンは斜めの文字を全く別のグリフとして扱い、**OCR 精度の向上** の取り組みが遠回りになります。  
> **Pro tip:** 逆さまになる可能性がある文書を扱う場合は、`DeskewFilter` の `setAutoRotate` フラグを有効にしてください（新しい Aspose リリースで利用可能）。必要に応じて自動で 180° 回転します。

![回転前後の図 – 画像の傾き補正](https://example.com/deskew-diagram.png "画像の傾き補正例")

*画像の代替テキスト: 画像の傾き補正例*

---

## OCR 用画像の前処理 – ノイズ除去とクリーニング

画像が真っ直ぐになったら、次の障壁は視覚的ノイズです—小さな斑点、圧縮アーティファクト、薄い背景パターンなどが OCR エンジンを混乱させます。`DenoiseFilter` はエッジ（文字）を保持しつつ粒子を除去する微妙な平滑化アルゴリズムを適用します。

```java
// Step 4 (continued): Reduce visual noise (denoise)
DenoiseFilter denoiseFilter = new DenoiseFilter();
scannedImage = denoiseFilter.apply(scannedImage);
```

### ノイズ除去設定を調整するタイミング

- **Very dark scans:** 背景の影を除去するためにフィルタの強度を上げます（`denoiseFilter.setStrength(2)`）。  
- **Fine‑print fonts:** 細かいセリフがぼやけないように強度を下げます。  
- **Colored documents:** まずグレースケールに変換します（`scannedImage = scannedImage.toGrayscale();`）— OCR エンジンは単一チャンネル画像で最も効果的に動作します。

これらの調整は **スキャン画像のクリーニング** のベストプラクティスの一部です。クリアなビットマップは OCR エンジンからの信頼度スコアを直接高めます。

---

## 画像からテキストを抽出 – OCR エンジンの実行

画像が真っ直ぐで静かになったので、いよいよ**画像からテキストを抽出**です。`OcrEngine` クラスが裏で全てを処理します：セグメンテーション、文字分類、言語モデリング。

```java
// Step 5: Perform OCR on the cleaned image
String recognizedText = ocrEngine.recognize(scannedImage);
System.out.println(recognizedText);
```

#### 期待される出力

ソースファイルに “**Invoice # 12345**” という行が含まれている場合、コンソールには次のように表示されます：

```
Invoice # 12345
Date: 2026-03-18
Total: $1,250.00
```

出力が文字化けしている場合は、特に傾き補正の手順を再確認してください。たった 1 度の傾きでも数字や記号が崩れることがあります。

---

## よくある落とし穴と **OCR 精度の向上** のヒント

| 問題 | 精度に影響する理由 | 簡単な対策 |
|------|-------------------|------------|
| **Residual rotation** | OCR は水平ベースラインを前提とします。 | `deskewFilter.getAngle()` で角度を確認し、値をログに出力します。 |
| **Over‑denoising** | 細いストロークがぼやけ、“i” が “l” に変わります。 | デリケートなフォントには `setStrength(0.5)` を使用します。 |
| **Wrong image format** | JPEG の圧縮がアーティファクトを生成します。 | ロスレス保存の PNG または TIFF を推奨します。 |
| **Incorrect language** | エンジンはデフォルトで英語です。他の文字体系は明示的に設定が必要です。 | `ocrEngine.setLanguage(OcrEngine.Language.Spanish);` |
| **Low DPI (≤150)** | セグメンテーションに十分なピクセル情報がありません。 | 処理前に 300 DPI にリサンプリングします（`scannedImage = scannedImage.resample(300);`）。 |

### ボーナス: バッチ処理

スキャン画像が入ったフォルダーがある場合は、デモをループでラップします：

```java
File folder = new File("YOUR_DIRECTORY");
for (File file : folder.listFiles((dir, name) -> name.endsWith(".png"))) {
    Image img = Image.load(file.getAbsolutePath());
    img = new DeskewFilter().apply(img);
    img = new DenoiseFilter().apply(img);
    String text = ocrEngine.recognize(img);
    System.out.println("=== " + file.getName() + " ===");
    System.out.println(text);
}
```

このパターンにより、**OCR 用画像の前処理** を大規模に実行でき、コードベースをすっきり保ちつつパフォーマンスも予測可能です。

---

## まとめと次のステップ

本稿では **画像の傾き補正方法**、**OCR 用画像の前処理**、そして **画像からテキストを抽出** を Aspose OCR Java で実装する手順を解説しました。スキャンを真っ直ぐにし、ノイズを除去し、きれいなビットマップをエンジンに渡すことで、**OCR 精度の向上** が顕著に実感できるはずです。

次は以下の拡張を検討してください：

- **Language detection** – `ocrEngine.setLanguage` を検出されたスクリプトに基づいて切り替える。  
- **PDF output** – 認識したテキストを PDF ジェネレータに渡し、検索可能な文書を作成する。  
- **Machine‑learning post‑processing** – OCR 結果に対してスペルチェックやカスタム辞書を適用する。

これらのアイデアを試し、フィルタ強度をいろいろ変えてみれば、どんな文書デジタル化プロジェクトでも堅牢なパイプラインが構築できるでしょう。

*ハッピーコーディング！ 問題が発生したら下のコメント欄に書き込んでください—傾き補正やノイズ除去のパラメータ調整をお手伝いします。*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}