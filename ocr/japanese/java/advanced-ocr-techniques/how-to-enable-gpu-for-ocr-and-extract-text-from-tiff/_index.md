---
category: general
date: 2026-09-23
description: Aspose OCR for Java で GPU アクセラレーションを有効にし、tiff ファイルからテキストを迅速に抽出する方法を学びます。ステップバイステップのガイドでは、TIFF
  の読み込み、GPU デバイス ID の設定、テキストの読み取りをカバーします。
draft: false
keywords:
- extract text from tiff file
- gpu acceleration java
- ocr tiff java
- aspose ocr gpu
lastmod: 2026-09-23
og_description: Aspose OCR for Java で GPU アクセラレーションを有効にし、tiff ファイルからテキストを迅速に抽出する方法を学びます。このガイドでは、TIFF
  の読み込み、GPU デバイスの選択、抽出されたテキストの読み取りを示します。
og_image_alt: 'Tutorial image: enabling GPU for OCR in Java'
og_title: OCR Java で GPU アクセラレーションを使用して tiff ファイルからテキストを抽出
schemas:
- author: Aspose
  dateModified: '2026-09-23'
  description: Learn how to extract text from tiff file quickly by enabling GPU acceleration
    in Aspose OCR for Java. Step‑by‑step guide covers loading TIFF, setting GPU device
    ID, and reading text.
  headline: How to extract text from tiff file using GPU in OCR Java
  type: TechArticle
- questions:
  - answer: Absolutely—Aspose OCR runs on Windows, Linux, and macOS as long as the
      CUDA toolkit and drivers are installed.
    question: Does this work on Linux?
  - answer: Omit the `setUseGpu(true)` call or explicitly call `setUseGpu(false)`;
      the engine will run on CPU.
    question: What if I don’t have a GPU?
  - answer: Yes. `setImage` accepts JPEG, PNG, BMP, PDF, and more.
    question: Can I extract text from other formats?
  - answer: Accuracy drops sharply below 300 dpi. Pre‑process the image (binarization,
      deskew) for better results.
    question: How accurate is OCR on low‑resolution TIFFs?
  - answer: The library handles 30+ raster and document formats, including TIFF, JPEG,
      PNG, BMP, PDF, and GIF.
    question: How many formats does Aspose OCR support?
  type: FAQPage
tags:
- OCR
- Java
- GPU acceleration
title: GPU を使用した OCR Java で tiff ファイルからテキストを抽出する方法
url: /ja/java/advanced-ocr-techniques/how-to-enable-gpu-for-ocr-and-extract-text-from-tiff/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# GPU を使用した OCR Java で TIFF ファイルからテキストを抽出する方法

## クイック回答
- **GPU OCR の主な利点は何ですか？** 大きなマルチページ TIFF の処理が最大 5 倍速くなります。  
- **必要な Java バージョンは？** Java 17 以上（Java 8+ でも動作します）。  
- **特別なライセンスが必要ですか？** 本番環境で使用するには有効な Aspose OCR for Java ライセンスが必要です。  
- **Linux でも実行できますか？** はい。Aspose OCR はクロスプラットフォームで、CUDA ツールキットをインストールすれば動作します。  
- **GPU はオプションですか？** `setUseGpu(false)` を呼び出すことで CPU にフォールバックできます。

## OcrEngine とは？
`OcrEngine` クラスは Aspose OCR for Java の中心コンポーネントです。すべての OCR 機能をカプセル化し、画像の読み込み、言語や GPU 使用などの処理オプションの設定、認識されたテキストと信頼度データの取得を便利なオブジェクトで行えます。

`OcrEngine` は Aspose OCR のコアクラスで、OCR 処理エンジンを表し、画像の読み込み、オプション設定、結果取得のメソッドを提供します。

## Java で OCR の GPU を有効にする方法
画像を読み込み、GPU をオンにし、`recognize` を呼び出すだけです。`setUseGpu(true)` で GPU を有効にすると、エンジンはピクセル集中的な処理をグラフィックカードにオフロードし、特に高解像度やマルチページ TIFF の処理時間が大幅に短縮されます。

## 必要なもの
- Java 17 以上（コードは Java 8+ でも動作します）。  
- Aspose OCR for Java 23.10（または最新リリース）。  
- 最新ドライバーがインストールされた CUDA 対応 GPU。  
- サンプルのマルチページ TIFF ファイル（例: `sample_large.tif`）。  

Maven を使わないですか？ JAR をクラスパスに置くだけです。

![GPU を有効にするチュートリアル](gpu-ocr.png)

[GPU を有効にするチュートリアル](gpu-ocr.png)

*画像の代替テキスト: Java で OCR の GPU を有効にする方法*

## 手順 1: OCR 用に TIFF 画像を読み込む

`setImage` メソッドはファイルを `ImageStream` でラップし、エンジンが手動で分割することなくマルチページ TIFF を処理できるようにします。ファイルが見つからない場合は、明確な `FileNotFoundException` がスローされます。

```java
import com.aspose.ocr.*;

public class GpuOcrDemo {
    public static void main(String[] args) throws Exception {
        // Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Load the TIFF file – this is where we "read text from TIFF"
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample_large.tif"));
```

> **重要な理由:** `setImage` 呼び出しはページ処理を抽象化し、単一のエンジンインスタンスで文書全体を処理できます。

## 手順 2: GPU 加速を有効にする

GPU をオンにするのはブールフラグ 1 つです。ほとんどのシステムではデフォルト GPU がデバイス 0 ですが、Aspose に最適なデバイスを自動選択させることもできます。

```java
        // Enable GPU acceleration (requires a supported driver)
        ocrEngine.getEngineOptions().setUseGpu(true);
```

> **プロのコツ:** 複数の GPU を搭載したワークステーションでは、デバイス ID を指定することで遅い統合 GPU への予期せぬフォールバックを防げます。

## 手順 3: GPU デバイス ID を設定する（オプション）

OCR を処理すべき GPU が分かっている場合（例えば専用 AI カード）、`setGpuDeviceId` で明示的に設定できます。

```java
        // Optional: select the GPU device (0 = first device, 1 = second, etc.)
        ocrEngine.getEngineOptions().setGpuDeviceId(0);
```

> **エッジケース:** 無効な ID を渡すと `IllegalArgumentException` が発生します。`ocrEngine.getEngineOptions().getAvailableGpuDevices()` で有効な ID を一覧表示してください。

## 手順 4: 画像を処理し、画像からテキストを抽出する

OCR を実行すると、プレーン文字列とオプションの信頼度スコアを含む `OcrResult` が返されます。

```java
        // Perform OCR – this is where we "convert TIFF to text"
        OcrResult ocrResult = ocrEngine.process();

        // Output the recognized text
        System.out.println("Recognized text:");
        System.out.println(ocrResult.getText());
    }
}
```

### 期待される出力

TIFF に “Hello, World!” が含まれている場合、結果は次のようになります：

```
Recognized text:
Hello, World!
```

エンジンは改行、句読点、基本的なレイアウト検出を自動的に処理します。ページ単位で抽出したい場合は `ocrResult.getPages()` を参照してください。

## 手順 5: 出力を検証し、一般的な問題に対処する

GPU が使用されないことがある理由はいくつかあります。インストールされたドライバのバージョンが最低要件未満の場合、ライブラリは CUDA を初期化できません。ビデオメモリが不足するとエンジンは CPU にフォールバックし、一部の統合グラフィックスは OCR 加速に必要な計算能力を欠いています。

### GPU が使用されない理由
- **ドライバの不一致:** GPU ドライバは Aspose のリリースノートに記載された最低バージョンを満たす必要があります。  
- **メモリ不足:** 非常に大きな画像は VRAM を超える可能性があり、その場合エンジンは CPU にフォールバックし、警告をログに記録します。  
- **サポートされていないハードウェア:** 統合グラフィックスは必要な計算能力を欠いていることが多いです。

### プログラムで CPU にフォールバックする方法
CPU 処理を確実に行いたい場合は、エンジンのオプションセッターに `false` フラグを渡して呼び出してください。これにより GPU の試行がすべて無効化され、OCR パイプラインはホストプロセッサ上で完全に実行されます。互換性のないグラフィックカードがないマシンで有用です。

```java
if (!ocrEngine.getEngineOptions().isGpuAvailable()) {
    System.out.println("GPU not available – switching to CPU.");
    ocrEngine.getEngineOptions().setUseGpu(false);
}
```

### ループで TIFF からテキストを読み取る
多数のファイルを処理する際は、GPU 加速を有効にしたままディレクトリを反復処理します。

```java
File folder = new File("YOUR_DIRECTORY");
for (File file : folder.listFiles((dir, name) -> name.toLowerCase().endsWith(".tif"))) {
    ocrEngine.setImage(ImageStream.fromFile(file.getAbsolutePath()));
    OcrResult result = ocrEngine.process();
    System.out.println("File: " + file.getName());
    System.out.println(result.getText());
}
```

このスニペットは、パフォーマンス向上を失うことなく大量の TIFF ファイルから **テキストを読み取る** 方法を示しています。

## よくある質問 (FAQ)

**Q: Linux でも動作しますか？**  
A: はい。CUDA ツールキットとドライバがインストールされていれば、Aspose OCR は Windows、Linux、macOS で動作します。

**Q: GPU がない場合はどうすればよいですか？**  
A: `setUseGpu(true)` 呼び出しを省くか、`setUseGpu(false)` を明示的に呼び出してください。エンジンは CPU で実行されます。

**Q: 他のフォーマットからテキストを抽出できますか？**  
A: はい。`setImage` は JPEG、PNG、BMP、PDF などを受け付けます。

**Q: 低解像度の TIFF の OCR 精度はどの程度ですか？**  
A: 300 dpi 未満になると精度が大幅に低下します。画像を前処理（二値化、傾き補正）すると結果が向上します。

**Q: Aspose OCR がサポートするフォーマットは何種類ですか？**  
A: このライブラリは TIFF、JPEG、PNG、BMP、PDF、GIF など、30 種類以上のラスタ・ドキュメント形式を扱えます。

## 結論

あなたは今、Aspose OCR for Java で GPU 加速を利用して **TIFF ファイルからテキストを抽出する方法**、特定の GPU デバイス ID の設定方法、単一または複数の TIFF を効率的に処理する方法を理解しました。フラグを 1 つ切り替えるだけで、OCR ロジックを変更せずに大幅な速度向上が得られます。

次に試すべきステップ:
- 数百枚の TIFF を並列スレッドでバッチ処理する。  
- カスタム言語パックをロードして、専門用語の認識精度を向上させる。  
- 正規表現で抽出テキストを後処理し、フォーマットを整える。

問題が発生した場合は、下にコメントを残してください。コーディングを楽しんで！

---

**Last Updated:** 2026-09-23  
**Tested With:** Aspose OCR for Java 23.10  
**Author:** Aspose

## 関連チュートリアル

- [Java OCR の GPU 有効化ステップバイステップガイド](/ocr/java/advanced-ocr-techniques/how-to-enable-gpu-for-java-ocr-step-by-step-guide/)
- [Aspose OCR を使用した画像からのテキスト認識 完全 Java ガイド](/ocr/java/advanced-ocr-techniques/recognize-text-from-image-with-aspose-ocr-full-java-guide/)
- [Java で画像 OCR を前処理し、精度とテキスト抽出を向上させる](/ocr/java/advanced-ocr-techniques/preprocess-image-ocr-in-java-boost-accuracy-extract-text/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}