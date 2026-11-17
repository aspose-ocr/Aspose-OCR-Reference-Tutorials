---
category: general
date: 2026-03-28
description: Aspose OCR を使用して Java で画像テキストを認識し、テキストを PNG ファイルとして抽出し、大きな画像の高速 OCR のために
  GPU 加速を利用する方法を学びましょう。
draft: false
keywords:
- recognize image text
- extract text png
- use gpu acceleration
- ocr large image
- java ocr example
language: ja
og_description: Javaで画像テキストを認識し、テキストを含むPNGファイルを抽出し、大きな画像のOCRにGPUアクセラレーションを使用する方法を学びましょう。
og_title: Java OCRで画像テキストを認識 – GPUアクセラレート例
tags:
- OCR
- Java
- GPU
title: Java OCRで画像テキストを認識する – GPUアクセラレート例
url: /ja/java/advanced-ocr-techniques/recognize-image-text-with-java-ocr-gpu-accelerated-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java OCRで画像テキストを認識 – GPUアクセラレーション例

大量のPNGから **画像テキストを認識** したいのに、CPU版が遅すぎて困ったことはありませんか？ あなただけではありません。請求書のスキャンや歴史的文書のアーカイブなど、実際のパイプラインでは画像サイズが非常に大きくなり、デフォルトのOCRエンジンでは追いつけません。  

良いニュースです：Aspose OCR for Java を使えば **GPUアクセラレーション** が利用でき、処理が飛躍的に高速化します。しかもコードは驚くほどコンパクトです。このチュートリアルでは、**PNG画像からテキストを抽出** し、CUDA対応GPUを活用し、**OCR large image** を数行のコードで処理する完全な実行可能Javaサンプルを紹介します。最後まで読めば、独自のJavaプロジェクトに組み込む方法と各設定が持つ意味が分かります。

## 学べること

- Maven または Gradle プロジェクトへの Aspose OCR の導入方法。  
- GPU 上で **画像テキストを認識** する手順。  
- GPU ストリーム数を設定することでスループットが向上する理由。  
- 出力結果の検証方法と一般的な落とし穴のトラブルシューティング。  

> **前提条件** – Java 17（またはそれ以降）、最新ドライバがインストールされた CUDA 対応 GPU、そして有効な Aspose OCR for Java ライセンス（評価用の無料トライアルで可）。他の外部ライブラリは不要です。

---

## Step 1: Add Aspose OCR Dependency

まず、Aspose OCR ライブラリをビルドに組み込みます。**Maven** を使用している場合は、`pom.xml` に以下のスニペットを追加してください。

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- check Maven Central for the latest version -->
</dependency>
```

**Gradle** を使用している場合は、`build.gradle` に次を記述します。

```gradle
implementation 'com.aspose:aspose-ocr:23.9'
```

> **プロのコツ**：2026年3月時点の最新バージョンには GPU ワークロード向けのパフォーマンス改善が含まれているため、常に最新リリースを取得してください。

---

## Step 2: Initialize the OCR Engine and Enable GPU

OCR エンジンの作成はシンプルです。重要なのは GPU フラグを有効にすることです。これをしないとエンジンは CPU モードにフォールバックします。

```java
import com.aspose.ocr.*;

public class GpuExample {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Enable GPU acceleration (requires a CUDA‑enabled GPU and driver)
        ocrEngine.getRecognitionSettings().setUseGpu(true);

        // 3️⃣ (Optional) Set the number of GPU streams for parallel processing
        //    More streams can improve throughput on multi‑core GPUs.
        ocrEngine.getRecognitionSettings().setGpuStreams(2);
```

### なぜ GPU を有効にするのか？

`setUseGpu(true)` を呼び出すと、Aspose は重い畳み込みニューラルネットワーク計算をグラフィックカードにオフロードします。これにより、特に画像サイズが **4000 × 4000 px** を超える **ocr large image** の処理時間が数秒短縮されます。環境に対応 GPU が無い場合は、この呼び出しは単に無視され、エンジンは CPU で動作し続けます—クラッシュは起きませんが、処理は遅くなります。

---

## Step 3: Recognize a PNG Image and Extract Its Text

次に、処理したいファイルをエンジンに渡します。例では `sample-large.png` を使用していますが、任意の PNG または JPEG に置き換えて構いません。

```java
        // 4️⃣ Perform OCR on the input image
        OcrResult ocrResult = ocrEngine.recognizeImage("YOUR_DIRECTORY/sample-large.png");

        // 5️⃣ Print the recognized text to the console
        System.out.println("=== Recognized Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

プログラムを実行すると、以下のような出力が得られるはずです。

```
=== Recognized Text ===
Invoice #12345
Date: 2026‑03‑27
Total: $1,234.56
...
```

この出力は **画像テキストの認識** が成功し、**PNG からテキストを抽出** できたことを示しています。

---

## Step 4: Verify GPU Utilization (Optional but Helpful)

GPU が実際に使用されているか確認したい場合は、システムの GPU 監視ツール（例：Linux の `nvidia-smi`）を開きます。Java プロセスが走っている間、メモリ使用量と計算利用率に適度なスパイクが見えるはずです。

```bash
$ nvidia-smi
+-----------------------------------------------------------------------------+
| Processes:                                                                  |
|  GPU   PID   Type   Process name                  GPU Memory               |
|  0    12345 C++    java                           1024MiB                  |
+-----------------------------------------------------------------------------+
```

何もアクティビティが見えない場合は、次を再確認してください：

1. CUDA ドライバが GPU モデルと一致しているか。  
2. `setUseGpu(true)` の呼び出しが後続のコードで上書きされていないか。  
3. ライセンスファイル（所有している場合）が GPU 使用を制限していないか。

---

## Step 5: Handling Common Edge Cases

### GPU メモリを超える大画像

画像が非常に大きい（例：8000 × 8000 px）場合、GPU のメモリが不足することがあります。簡単な回避策は、Aspose に渡す前に画像を縮小することです。

```java
import java.awt.image.BufferedImage;
import javax.imageio.ImageIO;
import java.io.File;

BufferedImage original = ImageIO.read(new File("sample-large.png"));
int maxDim = 4000; // target max dimension
int width = original.getWidth();
int height = original.getHeight();

float scale = Math.min((float)maxDim / width, (float)maxDim / height);
int newWidth = Math.round(width * scale);
int newHeight = Math.round(height * scale);

BufferedImage resized = new BufferedImage(newWidth, newHeight, original.getType());
// Simple scaling (for demo purposes)
resized.getGraphics().drawImage(original, 0, 0, newWidth, newHeight, null);
ImageIO.write(resized, "png", new File("sample-resized.png"));
```

その後、`recognizeImage` に `"sample-resized.png"` を渡します。これにより OCR の精度を保ちつつ、GPU のメモリ制限内で処理できます。

### マルチページ PDF

Aspose OCR は PDF もページ単位で処理できます。各ページを画像に変換し、エンジンに渡すループを組みます。**use gpu acceleration** フラグは同様に機能し、PDF‑to‑text パイプラインを高速化します。

---

## Full Working Example (Copy‑Paste Ready)

以下はコンパイル・実行可能な完全な Java クラスです。`YOUR_DIRECTORY` を PNG ファイルが置かれているパスに置き換えてください。

```java
import com.aspose.ocr.*;

public class GpuExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Enable GPU acceleration (requires a CUDA‑enabled GPU and driver)
        ocrEngine.getRecognitionSettings().setUseGpu(true);

        // Step 3: (Optional) Set the number of GPU streams for parallel processing
        // Using 2 streams works well on most modern GPUs.
        ocrEngine.getRecognitionSettings().setGpuStreams(2);

        // Step 4: Perform OCR on the input image
        // This will **recognize image text** from a PNG file.
        OcrResult ocrResult = ocrEngine.recognizeImage("YOUR_DIRECTORY/sample-large.png");

        // Step 5: Print the recognized text to the console
        System.out.println("=== Recognized Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

**期待される出力** – 画像からエンジンが読み取れたすべてのテキストをプレーンテキストで表したものです。画像に表が含まれている場合、セルの内容が改行で連結されます。Aspose はレイアウトを保持しませんが、必要に応じて文字列を後処理できます。

---

## Frequently Asked Questions

| Question | Answer |
|----------|--------|
| **Do I need a paid license?** | トライアルは最大200ページまで使用でき、OCR の透かしは無効です。製品版ライセンスを取得すれば制限が解除され、GPU スタックもフルに利用可能になります。 |
| **What if my GPU is older (e.g., GTX 750)?** | 古い GPU でも動作することがありますが速度は低下します。Compute Capability 3.0 以上が必要です。 |
| **Can I process JPG or BMP files?** | もちろん可能です。`recognizeImage` は Java ImageIO がサポートするすべての形式を受け付けます。 |
| **Is there a way to batch‑process many images?** | OCR 呼び出しをループで回し、必要に応じて `setGpuStreams` を増やして同時ストリーム数を調整してください。 |
| **What if I need to preserve layout?** | Aspose OCR の `LayoutOptions` を使用すればバウンディングボックスが取得できます。詳細は API ドキュメントをご参照ください（本ガイドの範囲外です）。 |

---

## Conclusion

これで **java ocr example** が完成し、**画像テキストを認識**、**PNG からテキストを抽出**、そして **GPUアクセラレーション** を活用して **ocr large image** の処理を高速化できるようになりました。GPU ストリーム数の調整や、必要に応じた画像の縮小を行うことで、ほぼすべてのハードウェア構成に合わせた最適化が可能です。

次のステップは？ 同じパイプラインでスキャンした領収書のフォルダを処理したり、Aspose の `TextRegion` API を試して元のレイアウトを保持したりしてみてください。問題が発生したら、Aspose フォーラムや Javadoc が有力な情報源です—本稿で解説した基本を忘れずに。

Happy coding, and may your OCR be lightning‑fast!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}