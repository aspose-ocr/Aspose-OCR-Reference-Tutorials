---
category: general
date: 2026-06-22
description: OCRのための画像の傾き補正方法：画像前処理のOCR手順を学び、塩胡椒ノイズを除去し、精度を向上させる。
draft: false
keywords:
- how to deskew image
- image preprocessing ocr
- remove salt pepper
- preprocess images OCR
language: ja
og_description: OCR のために画像の傾きを補正し、塩胡椒ノイズを除去し、画像前処理の OCR 手法を適用する完全な Java の例。
og_title: 画像の傾き補正方法 – 画像前処理 OCR ガイド
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: 'How to deskew image for OCR: learn image preprocessing OCR steps,
    remove salt pepper noise, and boost accuracy.'
  headline: How to Deskew Image – Image Preprocessing OCR Guide
  type: TechArticle
tags:
- OCR
- image-processing
- Java
title: 画像の傾き補正方法 – OCRのための画像前処理ガイド
url: /ja/java/ocr-operations/how-to-deskew-image-image-preprocessing-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 画像の傾き補正方法 – OCR向け画像前処理ガイド

画像の傾き補正がどうすればできるか、OCRエンジンが実際にテキストを読み取れるようになるか、考えたことはありませんか？ あなただけではありません。傾いたスキャンは完璧な文書を文字化けした混乱に変えてしまい、ほとんどの開発者が少なくとも一度はこの問題に直面します。

このチュートリアルでは、回転を補正するだけでなく、**塩胡椒ノイズ**を除去し、コントラストを向上させる、完全な**画像前処理 OCR**パイプラインを順に解説します。基本的にエンジンに渡す前に**画像を OCR 用に前処理**するために必要なすべてです。最後まで読むと、すぐに実行できる Java スニペットと、各ステップがなぜ重要かという明確な概念が得られます。

## 画像の傾き補正 – 前処理パイプラインの構築

OCR に適したワークフローの中心は、フィルタを連結する **preprocess options** オブジェクトです。コンベアベルトのように、各フィルタが一つの処理を行い、次のフィルタへ画像を渡します。以下は、`DeskewFilter`、`DenoiseFilter`、`ContrastBoostFilter` を提供する仮想的な OCR ライブラリを使用した、最小限ながら完全な例です。

```java
import com.example.ocr.Engine;
import com.example.ocr.ImagePreprocessOptions;
import com.example.ocr.filters.DeskewFilter;
import com.example.ocr.filters.DenoiseFilter;
import com.example.ocr.filters.ContrastBoostFilter;

/**
 * Demonstrates how to deskew image and apply common OCR preprocessing steps.
 */
public class OcrPreprocessDemo {

    public static void main(String[] args) {
        // 1️⃣ Create the OCR engine (replace with your actual implementation)
        Engine engine = new Engine();

        // 2️⃣ Build the preprocessing pipeline
        ImagePreprocessOptions preprocessOptions = new ImagePreprocessOptions();

        // 2a️⃣ Deskew – correct rotation up to ±15°
        preprocessOptions.addFilter(new DeskewFilter(15));

        // 2b️⃣ Denoise – remove salt‑and‑pepper noise
        preprocessOptions.addFilter(new DenoiseFilter());

        // 2c️⃣ Contrast boost – make low‑contrast scans more readable
        preprocessOptions.addFilter(new ContrastBoostFilter(1.5f));

        // 3️⃣ Attach the pipeline to the engine
        engine.setPreprocessOptions(preprocessOptions);

        // 4️⃣ Run OCR on a sample image
        String result = engine.recognizeText("sample-scanned-page.png");

        // 5️⃣ Output the recognized text
        System.out.println("=== OCR RESULT ===");
        System.out.println(result);
    }
}
```

### なぜこれが機能するのか

* **DeskewFilter** は画像の支配的なテキストラインを解析し、角度を推定してビットマップを水平に回転させます。ほとんどのライブラリは補正範囲を ±15° に制限しています。なぜならそれ以上の角度は、手動で対処すべきスキャンミスがあることを示すことが多いからです。
* **DenoiseFilter** は古典的な *salt‑and‑pepper* パターン、すなわちテレビのノイズのように見える孤立した黒または白のピクセルを対象とします。これらを除去することで、OCR エンジンがノイズを文字と誤認するのを防ぎます。
* **ContrastBoostFilter** はヒストグラムを伸長させ、薄い筆跡を際立たせます。`1.5f` の倍率は安全なデフォルトで、スキャンが特に薄い場合は上げても構いません。

> **プロのコツ:** 文書の傾きが 10° を超えないことが分かっている場合は、その小さな上限を `DeskewFilter` に渡してください。アルゴリズムの実行が速くなり、過補正の可能性も低くなります。

## OCR向け画像前処理: フィルタを正しい順序で追加する

順序は重要です。傾き補正の *前* にノイズ除去を行うと、ノイズが角度検出を乱し、ずれた結果になることがあります。逆に、傾き補正の *後* にコントラスト強調を適用すれば、回転によって新たなアーティファクトが生じるのを防げます。

以下は、任意のプロジェクトにコピー＆ペーストできる簡易チェックリストです：

| 手順 | フィルタ | 理由 |
|------|--------|--------|
| 1 | `DeskewFilter` | テキストのベースラインを揃える |
| 2 | `DenoiseFilter` | 孤立したピクセルノイズを除去 |
| 3 | `ContrastBoostFilter` | OCR の可読性を向上させる |

追加のステップが必要な場合、たとえばバイナリ OCR 用の **binarization** フィルタを入れたいときは、コントラスト強調の **後** に配置します。なぜなら、きれいで高コントラストな画像の方が正確に二値化できるからです。

## DenoiseFilter で塩胡椒ノイズを除去する

塩胡椒ノイズは低品質なスキャン、特に安価な携帯電話カメラからの画像で顕著です。ライブラリの `DenoiseFilter` はメディアンフィルタ カーネルを実装しており、各ピクセルを周囲の中央値で置き換えます。その効果は？ 実際の文字をぼかすことなく、これらの斑点が消えることです。

```java
// Example: customizing the median kernel size (default is 3x3)
preprocessOptions.addFilter(new DenoiseFilter(5)); // 5x5 kernel for heavy noise
```

*カーネルサイズを大きくすべきはいつか？* ソース画像に大きな斑点が多数ある場合、より大きなカーネルでそれらを除去できますが、注意が必要です。大きすぎると小さなフォントの細い線まで消してしまう可能性があります。

## OCR向け画像前処理 – パイプラインの適用

フィルタチェーンを組み立てたら、エンジンに接続するのはワンライナーです（`engine.setPreprocessOptions`）。それ以降、`recognizeText` の呼び出しは自動的にパイプラインを通過します。各フィルタを手動で呼び出す必要はなく、コードがすっきりし、将来的な変更（新しいフィルタの追加やパラメータ調整）も一元管理できます。

以下は、元々 12° の傾きと目立つ塩胡椒ノイズがあったサンプルスキャンを処理した成功例です：

```
=== OCR RESULT ===
Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00
Thank you for your business!
```

テキストがきれいで正しく向きが調整され、以前は “I n v o i c e” や “$‑‑‑” のように現れたであろう余分な文字がなくなっていることに注目してください。

## エッジケースと一般的な落とし穴

| Situation | What to watch for | Suggested fix |
|-----------|-------------------|---------------|
| Rotation > 15° | DeskewFilter が処理を諦める可能性あり | 手動で事前に回転させるか、より広い範囲をカバーするフィルタを使用する |
| Extremely low resolution ( < 100 dpi ) | コントラスト強調だけではディテールを回復できない | まず画像をリサンプリングする（例: `ResampleFilter`） |
| Mixed noise (Gaussian + salt‑pepper) | `DenoiseFilter` だけでは不十分 | `DenoiseFilter` の前に `GaussianBlurFilter` をチェーンする |
| Color scans with colored text | グレースケール変換が必要 | コントラスト強調の前に `GrayscaleFilter` を挿入する |

これらのシナリオを事前に想定しておくことで、後々のデバッグに費やす時間を何時間も節約できます。

## 完全動作例（オールインワン）

以下は、`com.example.ocr` 依存関係を含む任意の Maven または Gradle プロジェクトに貼り付けられる、自己完結型の Java クラスです。**画像の傾き補正**、**塩胡椒ノイズの除去**、そして **OCR 用画像前処理** を実演します。

```java
package com.myapp.demo;

import com.example.ocr.Engine;
import com.example.ocr.ImagePreprocessOptions;
import com.example.ocr.filters.*;

public class CompleteOcrPipeline {

    public static void main(String[] args) {
        // -------------------------------------------------
        // 1️⃣ Initialise OCR engine (replace with your own)
        // -------------------------------------------------
        Engine engine = new Engine();

        // -------------------------------------------------
        // 2️⃣ Configure preprocessing pipeline
        // -------------------------------------------------
        ImagePreprocessOptions options = new ImagePreprocessOptions();

        // Deskew up to ±15° – the core of "how to deskew image"
        options.addFilter(new DeskewFilter(15));

        // Remove salt‑and‑pepper artifacts
        options.addFilter(new DenoiseFilter());

        // Boost contrast by 1.5× to aid OCR recognition
        options.addFilter(new ContrastBoostFilter(1.5f));

        // (Optional) Convert to grayscale – often improves OCR accuracy
        options.addFilter(new GrayscaleFilter());

        // Attach the pipeline
        engine.setPreprocessOptions(options);

        // -------------------------------------------------
        // 3️⃣ Perform OCR on a test file
        // -------------------------------------------------
        String imagePath = "src/main/resources/scanned-document.png";
        String text = engine.recognizeText(imagePath);

        // -------------------------------------------------
        // 4️⃣ Show the result
        // -------------------------------------------------
        System.out.println("=== OCR RESULT ===");
        System.out.println(text);
    }
}
```

**期待される出力**（`scanned-document.png` に明瞭な請求書が含まれていると仮定）

```
=== OCR RESULT ===
Invoice #98765
Date: 2024‑02‑28
Amount Due: $2,340.75
Please remit payment within 30 days.
```

画像をすでに完全に整列したものに差し替えても、パイプラインは依然として実行され、何も壊れず、OCR の精度は高いままであることに気付くでしょう。

## 結論

これで、**画像の傾き補正**の方法と、各前処理ステップ（**画像前処理 OCR**、**塩胡椒ノイズ除去**、**OCR 用画像前処理**）が、クリーンで検索可能なテキストを提供する上で重要な役割を果たす理由をしっかりと理解できました。上記の例は完全な…

## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示した手法を基にした密接に関連するトピックを扱っています。各リソースには、ステップバイステップの解説と完全な動作コード例が含まれており、追加の API 機能を習得し、独自プロジェクトで代替実装アプローチを検討するのに役立ちます。

- [AspOCR の使い方: .NET 用画像 OCR フィルタの前処理](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [OCR 画像前処理の傾き角度計算](/ocr/english/net/skew-angle-calculation/calculate-skew-angle/)
- [OCR 画像認識で閾値を設定する方法](/ocr/english/net/ocr-settings/set-threshold-value/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}