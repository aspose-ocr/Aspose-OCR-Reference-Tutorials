---
category: general
date: 2026-02-09
description: Aspose OCR を使用して OCR を迅速に実行し、画像からテキストを認識し、PNG からテキストを抽出しながらモードと GPU メモリ上限を設定する方法。
draft: false
keywords:
- how to use ocr
- recognize text from image
- extract text from png
- how to set mode
- set gpu memory limit
language: ja
og_description: OCRを効率的に使用する方法 – 画像からテキストを認識し、PNGからテキストを抽出し、モードを設定し、JavaでGPUメモリ上限を制御する方法を学びましょう。
og_title: JavaでGPUアクセラレーションを利用したOCRの使用方法
tags:
- OCR
- Java
- GPU
- Aspose
title: JavaでGPUアクセラレーションを使用したOCRの使い方 – ステップバイステップガイド
url: /ja/java/advanced-ocr-techniques/how-to-use-ocr-with-gpu-acceleration-in-java-step-by-step-gu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# JavaでGPUアクセラレーションを使用したOCRの使い方 – 完全プログラミングチュートリアル

画像からテキストを抽出する **OCR の使い方** を、何千行ものコードを書かずに実現したいと思ったことはありませんか？請求書のスキャン、レシート処理、古い文書のデジタル化など、さまざまなプロジェクトで開発者は **画像からテキストを認識** する信頼できる方法を必要としています。特に PNG はクリーンで高解像度のグラフィックを含むことが多いです。

朗報です。Aspose OCR を使えばこの作業はとても簡単になり、さらにいくつか設定を変更すれば重い処理を GPU にオフロードできます。このチュートリアルでは、PNG の読み込みから **GPU 用にモードを設定**、**GPU メモリ上限を設定**、そして抽出したテキストの出力までの全工程を順に解説します。最後まで読めば、必要な機能をすべて備えた実行可能な Java プログラムが手に入ります。

## 学べること

- Aspose OCR for Java のインストールとインポート方法
- ライブラリを使った **画像からテキストを認識** の手順
- **PNG からテキストを抽出** する効率的な方法
- **モードを GPU に設定** し、**GPU メモリ上限を設定** してメモリ使用量を制御する方法
- 実務で遭遇しやすい落とし穴と対策

### 前提条件

- Java 8 以上（コードは JDK 11 でもコンパイル可能）
- GPU アクセラレーションを利用する場合は CUDA 対応ドライバを搭載した NVIDIA GPU
- Aspose OCR for Java の JAR（Aspose のサイトからダウンロード、または Maven/Gradle で追加）
- サンプル PNG 画像（例: `sample1.png`）を参照できるフォルダーに配置

---

## How to Use OCR – Enable GPU Mode

最初に行うべきは、Aspose OCR に CPU ではなく GPU で実行させたい旨を伝えることです。ここで **モードを設定** するキーワードが登場します。

```java
// Step 1: Create the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Step 2: Grab the configuration object
OcrEngineConfiguration config = ocrEngine.getConfiguration();

// Step 3: Switch processing mode to GPU
config.setProcessingMode(ProcessingMode.GPU);   // requires a CUDA‑compatible driver

// (Optional) Step 4: Limit GPU memory usage to 1024 MB
config.setGpuMemoryLimit(1024);                 // set gpu memory limit (MB)
```

**なぜ重要か:**  
GPU 処理は大量のバッチや高解像度画像に対して劇的に高速ですが、ビデオメモリも消費します。`setGpuMemoryLimit` を呼び出すことで、アプリケーションが GPU 全体を占有するのを防げます。これは UI や機械学習モデルなど、同じデバイスで他のワークロードが走っている場合に特に重要です。

---

## Recognize Text from Image Using Aspose OCR

エンジンの設定が完了したら、次は読み取り対象のファイルを指定します。これが **画像からテキストを認識** の核心です。

```java
// Step 5: Define the image to be processed
ImageRecognitionResult imageInfo = new ImageRecognitionResult();
imageInfo.setImagePath("YOUR_DIRECTORY/sample1.png");

// Step 6: Run the OCR operation
RecognitionResult ocrResult = ocrEngine.recognize(imageInfo);
```

**内部で何が起きているか:**  
Aspose OCR は PNG を読み込み、前処理（二値化、デスキューなど）を行った後、GPU 上で OCR ニューラルネットワークを実行します。結果オブジェクトには生テキストと各行の信頼度スコアが含まれます。

---

## Extract Text from PNG with GPU Memory Limit

認識が終わったら、プレーンテキストの抽出は非常に簡単ですが、出力を確認し忘れる開発者が多いです。ここでは **PNG からテキストを抽出** し、安全に表示する方法を示します。

```java
// Step 7: Output the recognized text
System.out.println("Recognized text:");
System.out.println(ocrResult.getText());
```

**期待される出力（例）:**

```
Recognized text:
Invoice #12345
Date: 2026-02-09
Total: $1,250.00
Thank you for your business!
```

画像にノイズや特殊フォントが含まれている場合、文字化けが起きることがあります。その際は前処理オプションを調整してください（例: `config.setLanguage(Language.ENGLISH)` や `config.setAutoSkewCorrection(true)`）。

---

## Full, Runnable Example

以下はすべてを組み合わせた完全な Java プログラムです。`GpuExample.java` という名前で保存し、画像パスを調整したうえで `javac`/`java` または IDE から実行してください。

```java
import com.aspose.ocr.*;
import com.aspose.ocr.configuration.*;

public class GpuExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Specify the image to be processed
        ImageRecognitionResult imageInfo = new ImageRecognitionResult();
        imageInfo.setImagePath("YOUR_DIRECTORY/sample1.png");

        // Step 2: Create the OCR engine and enable GPU processing
        OcrEngine ocrEngine = new OcrEngine();
        OcrEngineConfiguration config = ocrEngine.getConfiguration();

        // Step 3: Set processing mode to GPU (requires CUDA driver)
        config.setProcessingMode(ProcessingMode.GPU);

        // Step 4 (optional): Limit GPU memory usage to 1024 MB
        config.setGpuMemoryLimit(1024);

        // Step 5: Perform recognition
        RecognitionResult ocrResult = ocrEngine.recognize(imageInfo);

        // Step 6: Print the extracted text
        System.out.println("Recognized text:");
        System.out.println(ocrResult.getText());
    }
}
```

**プログラムの実行方法**

```bash
javac -cp "path/to/aspose-ocr.jar" GpuExample.java
java -cp ".:path/to/aspose-ocr.jar" GpuExample
```

JAR がクラスパスに含まれていないと `ClassNotFoundException` が発生しますので注意してください。

---

## Pro Tips & Common Pitfalls

- **GPU ドライバのバージョン:** `ProcessingMode.GPU` フラグは CUDA ドライバが未インストールまたは非互換の場合に例外を投げます。`nvidia-smi` で確認しましょう。
- **メモリ予算:** 同時に多数の画像を処理する場合は `setGpuMemoryLimit` の値を上げるか、ジョブを順次実行してメモリ不足を回避してください。
- **画像形式:** PNG は問題なく動作しますが、圧縮率の高い JPEG は認識エラーの原因になることがあります。OCR 前にロスレス PNG へ変換することを推奨します。
- **言語サポート:** デフォルトは英語です。他言語を使用する場合は `config.setLanguage(Language.SPANISH)`（または該当する enum）を `recognize` 前に呼び出してください。
- **パフォーマンステスト:** `System.nanoTime()` を使って GPU 有無でベンチマークを取り、速度向上がコストに見合うか確認しましょう。

---

## Frequently Asked Questions

**macOS や Linux でも動作しますか？**  
はい。Aspose OCR はクロスプラットフォームです。CUDA 対応 GPU と適切なドライバが OS にインストールされていれば問題なく動作します。

**GPU がない場合はどうすれば？**  
`setProcessingMode(ProcessingMode.GPU)` 行を削除すれば、エンジンは自動的に CPU モードにフォールバックします。

**PDF を直接処理できますか？**  
Aspose OCR はラスタ画像向けです。PDF を扱う場合は、まず各ページを画像（例: Aspose PDF を使用）に変換し、得られた PNG を OCR に渡してください。

---

## Conclusion

要点をまとめると、Aspose OCR を Java で **使用する方法** は次の 3 ステップです。エンジンの設定（**モードを設定** と **GPU メモリ上限を設定** を含む）、PNG へのパス指定、そして結果文字列の取得です。上記スニペットは完全に動作するエンドツーエンドのソリューションで、任意の Java プロジェクトに組み込めます。

**画像からテキストを認識** と **PNG からテキストを抽出** をマスターした今、フォルダー単位のバッチ処理やデータベース保存、さらには下流の NLP パイプラインへの入力など、活用の幅は無限です。GPU メモリとドライバ互換性だけは常に意識しておきましょう。

OCR、GPU アクセラレーション、または Aspose の機能についてさらに質問があれば、コメントを残すか公式ドキュメントで詳細なカスタマイズ方法を確認してください。Happy coding! 🚀

![how to use ocr diagram](https://example.com/images/ocr-gpu-diagram.png "how to use ocr diagram")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}