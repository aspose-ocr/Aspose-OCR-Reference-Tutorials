---
category: general
date: 2026-07-05
description: Java を使用して PNG を PDF に変換しながら PDF 画像を圧縮します。OCR 用の画像前処理を学び、JPG のテキストを認識し、1
  つのチュートリアルでバッチ OCR を PDF に変換します。
draft: false
keywords:
- compress pdf images
- convert png to pdf
- image preprocessing for ocr
- recognize text jpg
- batch ocr to pdf
language: ja
og_description: Javaを使用してPDF画像を圧縮し、PNGをPDFに変換します。このガイドでは、OCR用の画像前処理、JPGのテキスト認識、バッチOCRからPDFへの変換について説明します。
og_title: JavaでPDF画像を圧縮 – 完全バッチOCRチュートリアル
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Compress PDF images while converting PNG to PDF using Java. Learn image
    preprocessing for OCR, recognize text JPG, and batch OCR to PDF in one tutorial.
  headline: Compress PDF Images with Java – Full Batch OCR to PDF Guide
  type: TechArticle
- description: Compress PDF images while converting PNG to PDF using Java. Learn image
    preprocessing for OCR, recognize text JPG, and batch OCR to PDF in one tutorial.
  name: Compress PDF Images with Java – Full Batch OCR to PDF Guide
  steps:
  - name: Expected Output
    text: 'Running the program prints a line for each image, e.g.:'
  - name: What if my server has no GPU?
    text: Just set `gpuSettings.setEnabled(false)`. The rest of the pipeline remains
      unchanged, and you still get multithreaded CPU processing.
  - name: My PDFs are still too large—can I lower the quality further?
    text: Yes. Adjust `options.setImageQuality(70)` or even `50`. Lower values shrink
      size more aggressively but may blur fine glyphs. Test with a representative
      sample.
  - name: How do I handle other image formats (TIFF, BMP)?
    text: 'Add the extensions to the filter lambda:'
  - name: Can I keep the original color images instead of binarizing?
    text: Replace `.addBinarize()` with `.addGrayscale()` in the preprocessor builder
      if you need color retention for downstream analysis.
  type: HowTo
tags:
- ocr
- java
- pdf
- image-processing
title: JavaでPDF画像を圧縮 – バッチOCRでPDFに変換する完全ガイド
url: /ja/java/advanced-ocr-techniques/compress-pdf-images-with-java-full-batch-ocr-to-pdf-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java で PDF 画像を圧縮 – バッチ OCR から PDF への完全ガイド

フォルダ内の PNG を検索可能な PDF に変換しながら **PDF 画像を圧縮** したことがありますか？ あなただけではありません。多くの自動化パイプラインで最大の課題は、画像品質、OCR 精度、最終 PDF サイズを同時に調整することです。

このチュートリアルでは、**PNG から PDF への変換**、**OCR 用画像前処理**の適用、そして最終的に **PDF 画像を圧縮** して軽量な出力を得る実践的な解決策を順を追って解説します。最後まで読むと、**JPG ファイルのテキスト認識**、**バッチ OCR から PDF へのワークフロー**の設定方法、そして PDF をすっきり保つ方法が分かります。

## 学べること

- Aspose OCR for Java のセットアップとライセンス適用
- マルチスレッド、GPU 加速、スペル補正のエンジン設定
- 再利用可能な **OCR 用画像前処理** パイプライン（ノイズ除去、コントラスト調整、二値化）の構築
- **PdfSaveOptions** を使用して **PDF 画像を圧縮** し、可読性を損なわない方法
- ディレクトリを走査して **PNG から PDF への変換** と **JPG のテキスト認識** を一括処理
- 任意のプロジェクトにすぐ組み込める、完全な Java プログラム

> **前提条件**: Java 8 以上、Maven または Gradle、Aspose OCR for Java のライセンス、処理したい PNG/JPG 画像が入ったフォルダ

---

## 手順 1: Aspose OCR ライセンスを適用する（本番環境必須）

OCR API を呼び出す前に有効なライセンスをロードする必要があります。ライセンスが無いと、トライアル制限に縛られます。

```java
import com.aspose.ocr.*;

public class LicenseSetup {
    public static void loadLicense() throws Exception {
        License license = new License();
        // Point to your license file – keep it out of source control!
        license.setLicense("Aspose.OCR.Java.lic");
    }
}
```

*重要ポイント*: ライセンス認証されたエンジンは GPU サポートや高精度を解放し、PDF に付随する透かしも除去してファイルサイズの肥大化を防ぎます。

---

## 手順 2: OCR エンジンを設定 – スレッド数、GPU、スペル補正

高速な OCR エンジンは **バッチ OCR から PDF** ジョブの要です。ホスト CPU が処理できるだけのスレッドを立ち上げ、GPU 加速（対応カードがある場合）を有効にし、スペル補正で OCR エラーをクリーンアップします。

```java
import com.aspose.ocr.*;
import com.aspose.ocr.gpu.GPUSettings;
import com.aspose.ocr.spell.SpellCorrectionOptions;

public class EngineConfig {
    public static OcrEngine createEngine() {
        OcrEngine ocrEngine = new OcrEngine();

        // Use all available logical processors
        ocrEngine.setThreadCount(Runtime.getRuntime().availableProcessors());

        // Enable GPU – huge speedup for large batches
        GPUSettings gpu = new GPUSettings();
        gpu.setEnabled(true);
        ocrEngine.setGpuSettings(gpu);

        // Light spell correction: fix common typos without over‑correcting
        SpellCorrectionOptions spellOpts = new SpellCorrectionOptions();
        spellOpts.setMaxEditDistance(1);
        ocrEngine.getSpellCorrection().setOptions(spellOpts);

        return ocrEngine;
    }
}
```

*プロのコツ*: ヘッドレスサーバーで GPU が無い場合は `gpu.setEnabled(false)` と設定すれば、コードはそのまま動作します（ただし少し遅くなります）。

---

## 手順 3: 画像前処理パイプラインを構築

スキャン画像はノイズや低コントラスト、照明ムラがつきものです。**OCR 用画像前処理** を行うことで、特に **JPG のテキスト認識** シナリオで認識率が大幅に向上します。

```java
import com.aspose.ocr.*;

public class PreprocessorSetup {
    public static ImagePreprocessor createPreprocessor() {
        return new ImagePreprocessor.Builder()
                .addDenoise(0.7)      // Reduce grain while preserving edges
                .addContrast(1.15)    // Boost contrast for clearer glyphs
                .addBinarize()        // Convert to black‑and‑white for OCR
                .build();
    }
}
```

*チェーン化の理由*: まずノイズ除去を行うことで二値化時に斑点が増幅されるのを防ぎ、次にコントラストで文字を際立たせ、最後に二値化で OCR エンジンが扱いやすいクリーンなバイナリ画像にします。

---

## 手順 4: PDF 保存オプションを設定 – **PDF 画像を効率的に圧縮**

Aspose は PDF 出力を細かく調整できます。画像圧縮を有効にし、サイズと可読性のバランスを取る品質レベルを設定します。

```java
import com.aspose.ocr.pdf.PdfSaveOptions;

public class PdfOptions {
    public static PdfSaveOptions createOptions() {
        PdfSaveOptions options = new PdfSaveOptions();
        options.setCompressImages(true);   // This is the key to compress PDF images
        options.setImageQuality(90);       // 90% retains sharp text while shrinking file size
        return options;
    }
}
```

*結果*: 各検索可能 PDF のサイズが目に見えて小さくなり、アーカイブやメール送信に最適です。

---

## 手順 5: フォルダを処理 – **PNG から PDF への変換** と **JPG のテキスト認識** を一括ループで実行

ここまでの要素をすべて組み合わせます。ループは入力ディレクトリを走査し、各 PNG または JPG に OCR を実行し、検索可能 PDF を出力フォルダに書き出します。PDF の名前は元画像名と同じになります。

```java
import com.aspose.ocr.*;
import com.aspose.ocr.pdf.PdfSaveOptions;
import java.io.File;

public class BatchOcrTutorial {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load license
        LicenseSetup.loadLicense();

        // 2️⃣ Engine & preprocessing
        OcrEngine ocrEngine = EngineConfig.createEngine();
        ocrEngine.setPreprocessor(PreprocessorSetup.createPreprocessor());

        // 3️⃣ PDF options (compress PDF images)
        PdfSaveOptions pdfOptions = PdfOptions.createOptions();

        // 4️⃣ Define input / output folders
        File inputFolder = new File("YOUR_DIRECTORY/input");
        File outputFolder = new File("YOUR_DIRECTORY/output");
        if (!outputFolder.exists()) outputFolder.mkdirs();

        // 5️⃣ Filter PNG & JPG files
        File[] imageFiles = inputFolder.listFiles((dir, name) ->
                name.toLowerCase().endsWith(".png") || name.toLowerCase().endsWith(".jpg"));

        if (imageFiles == null || imageFiles.length == 0) {
            System.out.println("No PNG or JPG files found in the input folder.");
            return;
        }

        // 6️⃣ Process each file
        for (File image : imageFiles) {
            // Recognize text – works for both PNG and JPG
            ocrEngine.recognizeImage(image.getAbsolutePath());

            // Build output PDF path (same base name)
            String pdfPath = outputFolder.getAbsolutePath() + File.separator +
                    image.getName().replaceAll("\\.(png|jpg)$", ".pdf");

            // Save as searchable PDF – this step also compresses images
            ocrEngine.saveAsSearchablePdf(pdfPath, pdfOptions);

            System.out.println("✅ Processed: " + image.getName() + " → " + pdfPath);
        }

        System.out.println("🎉 All files have been converted and compressed!");
    }
}
```

### 期待される出力

プログラム実行時に各画像ごとに以下のような行が表示されます。

```
✅ Processed: invoice1.png → /output/invoice1.pdf
✅ Processed: receipt23.jpg → /output/receipt23.pdf
🎉 All files have been converted and compressed!
```

生成された PDF をビューアで開くと、テキストが選択・検索可能でありながら、サイズは非圧縮版に比べ **30‑50 %** 程度小さくなっています。

---

## よくある質問とエッジケース

### サーバーに GPU が無い場合は？
`gpuSettings.setEnabled(false)` と設定すれば、残りのパイプラインはそのまま動作し、マルチスレッド CPU 処理が続きます。

### PDF がまだ大きい – さらに品質を下げられるか？
`options.setImageQuality(70)` や `50` に下げることでサイズをさらに削減できます。ただし数値が低すぎると細かな字形がぼやける可能性があるので、代表的なサンプルでテストしてください。

### 他の画像形式（TIFF、BMP）はどう扱う？
フィルタラムダに拡張子を追加します。

```java
name.toLowerCase().endsWith(".png") ||
name.toLowerCase().endsWith(".jpg") ||
name.toLowerCase().endsWith(".tif") ||
name.toLowerCase().endsWith(".bmp")
```

同じ前処理パイプラインがほとんどのラスタ形式で利用可能です。

### 二値化せずに元のカラー画像を保持したい場合は？
プリプロセッサービルダーの `.addBinarize()` を `.addGrayscale()` に置き換えれば、下流解析用にカラーを保持できます。

---

## 本番環境向けバッチ OCR のプロ Tips

- **メモリ管理**: 本稿のように単一の `OcrEngine` インスタンスを再利用し、画像ごとにオブジェクトを生成・破棄するオーバーヘッドを回避します。
- **エラーハンドリング**: ファイル単位の処理を `try/catch` で囲み、失敗をログに残しつつバッチ全体の中断を防ぎます。
- **ロギング**: `System.out.println` ではなく、SLF4J や Log4j といった本格的なロギングフレームワークを使用してスケーラビリティを確保します。
- **並列処理**: 大規模フォルダの場合はサブディレクトリを Parallel Stream で並列処理すると効果的ですが、GPU の競合には注意が必要です。
- **セキュリティ**: ライセンスファイルはリポジトリ外に配置し、ファイルシステム権限で保護してください。

---

## 結論

本稿では **PDF 画像を圧縮** しながら **バッチ OCR から PDF** への変換を実現し、**PNG から PDF への変換**、**JPG のテキスト認識**、そして堅牢な **OCR 用画像前処理** パイプラインを組み合わせました。完全な Java プログラムは自己完結型で、最新の JDK 上で動作し、軽量な検索可能 PDF を生成してアーカイブや downstream 分析にすぐ利用できます。

次のステップは？ 前処理パラメータをいろいろ試す、英語以外の OCR 言語を試す、あるいはディレクトリを監視してリアルタイムに処理する Spring Boot マイクロサービスに組み込むなどです。ライセンス読み込み、エンジン設定、前処理、PDF 圧縮というコア概念は変わらないので、OCR 主導プロジェクトの堅実な土台となります。

質問や独自のチューニング方法があればコメントで共有してください。Happy coding!

![バッチ OCR ワークフローの図（入力画像、前処理、OCR エンジン、圧縮 PDF 出力）](alt="バッチ OCR ワークフローの図（入力画像、前処理、OCR エンジン、圧縮 PDF 出力）")


## 次に学ぶべきこと


以下のチュートリアルは、本ガイドで示した手法を応用した関連トピックを扱っています。各リソースには完全なコード例とステップバイステップの解説が含まれており、API の追加機能を習得したり、別の実装アプローチを自分のプロジェクトで試したりするのに役立ちます。

- [PDF テキスト認識 – Aspose.OCR for Java の OCR 操作](/ocr/english/java/ocr-operations/)
- [Aspose OCR で画像テキストを認識 – 完全 Java OCR チュートリアル](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [Aspose.OCR BufferedImage を使用した Java での画像からテキストへの変換](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}