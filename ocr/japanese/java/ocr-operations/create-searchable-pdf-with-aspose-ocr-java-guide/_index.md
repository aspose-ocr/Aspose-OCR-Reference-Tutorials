---
category: general
date: 2026-03-26
description: Aspose.OCR Java を使用して検索可能な PDF を作成する – 画像の OCR を読み込み、主要言語を設定し、画像からテキストを抽出して
  OCR PDF を保存する方法を学ぶ。
draft: false
keywords:
- create searchable pdf
- set primary language
- extract text from image
- load image ocr
- save ocr pdf
language: ja
og_description: Aspose.OCR Javaで検索可能なPDFを作成する。画像のOCRをロードし、主要言語を設定し、画像からテキストを抽出し、OCR
  PDFとして保存するステップバイステップガイド。
og_title: Aspose.OCRで検索可能なPDFを作成する – Javaガイド
tags:
- Aspose.OCR
- Java
- PDF
- OCR
title: Aspose.OCR を使用して検索可能な PDF を作成する – Java ガイド
url: /ja/java/ocr-operations/create-searchable-pdf-with-aspose-ocr-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.OCR を使用した検索可能 PDF の作成 – Java ガイド

スキャンしたドキュメントから **create searchable pdf** を作成したいが、どこから始めればいいか分からないことはありませんか？ あなたは一人ではありません—Java で OCR に初めて取り組む多くの開発者が同じ壁にぶつかります。良いニュースは、Aspose.OCR が画像の読み込みから主要言語の設定、最終的に OCR 対応 PDF の保存まで、全工程を非常にシンプルにしてくれることです。このチュートリアルでは、**extracts text from image** の完全な実行可能サンプルを順に解説し、**set primary language** を行い、最後に **save OCR pdf** を作成して任意のリーダーで開く方法を示します。

GPU アクセラレーションを有効にして処理速度を向上させる方法や、混合言語ドキュメント（この例では Tamil + English）を扱う実用的なヒントもいくつか紹介します。最後まで読むと、プロジェクトにすぐ組み込める堅牢な本番対応スニペットが手に入ります。

## 必要なもの

- **Java 17**（または最近の JDK；Aspose.OCR は Java 8+ をサポート）
- **Aspose.OCR for Java** ライブラリ（公式サイトからダウンロード、または Maven で追加）
- **license file**（または 30 日間のトライアル）
- テキストを含む画像ファイル（デモでは `sample-mixed-tamil-eng.jpg` を使用）

余計なフレームワークやネイティブ依存関係は不要です—純粋な Java と Aspose.JAR だけです。

---

## ステップ 1: Create Searchable PDF – プロジェクトのセットアップ

コードに入る前に、プロジェクトが **create searchable pdf** ファイルを作成できる状態か確認しましょう。

```bash
# Maven dependency (add to pom.xml)
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- check the latest version -->
</dependency>
```

> **Pro tip:** バージョン番号は常に最新に保ちましょう。新しいリリースには GPU 使用時のパフォーマンス改善が含まれていることが多いです。

次に、`RecentFeaturesDemo` というシンプルな Java クラスを作成します。このクラスは **load image OCR**、言語設定の構成、そして最終的に **save OCR pdf** を行うすべてのロジックを保持します。

## ステップ 2: Load Image OCR とエンジンの初期化

パイプラインの最初の実際のステップは **load image OCR** です。これにより Aspose.OCR に解析対象のファイルを指示します。

```java
import com.aspose.ocr.*;

public class RecentFeaturesDemo {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Load your Aspose.OCR license (or use the 30‑day trial)
        License license = new License();
        license.setLicense("YOUR_DIRECTORY/Aspose.OCR.Java.lic");

        // 2️⃣ Create and configure the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Enable GPU acceleration – speeds up recognition dramatically
        ocrEngine.getEngineSettings().setUseGpu(true);
        // Use all available CPU cores for parallel processing
        ocrEngine.getEngineSettings().setUseParallelProcessing(true);
```

> **Why this matters:** GPU を有効化（`setUseGpu(true)`）すると、最新ハードウェアで処理時間が最大 70 % 短縮され、並列処理により GPU が稼働中でも CPU がアイドル状態にならないようになります。

## ステップ 3: 主言語の設定（および副言語）

このステップを省略すると、Aspose.OCR は言語を推測しようとしますが、処理が遅くなり精度も低下します。以下は **set primary language** を Tamil に設定し、英語をフォールバックとして追加する方法です。

```java
        // 3️⃣ Define languages – primary is Tamil, secondary is English
        ocrEngine.getLanguageSettings().setLanguage(Language.Tamil);
        ocrEngine.getLanguageSettings().setSecondaryLanguage(Language.English);
```

> **Explanation:** 主言語は認識時に使用される文字セットと辞書に影響します。副言語を追加することは、混合スクリプトのドキュメント（例：Tamil と English の両方が記載されたレシート）にとって重要です。  
> **Edge case:** ドキュメントに 2 つ以上の言語が含まれる場合、追加の言語ごとに `addAdditionalLanguage(...)` を呼び出すことができます。

## ステップ 4: 画像の前処理 – デスキューとノイズ除去

スキャン画像は回転や背景ノイズが発生しがちです。前処理を行うことで OCR エンジンが **extract text from image** をより確実に行えるようになります。

```java
        // 4️⃣ Pre‑processing options
        ocrEngine.getPreprocessingSettings()
                 .setDeskew(true)   // auto‑rotate tilted pages
                 .setDenoise(true); // suppress speckles and background patterns
```

> **Tip:** 画像がすでにクリアであることが分かっている場合、`setDenoise(true)` を省略して数ミリ秒の処理時間を削減できます。

## ステップ 5: 画像ファイルのロード

エンジンの準備が整ったので、解析したいファイルを指定します。

```java
        // 5️⃣ Load the image you want to recognize
        String imagePath = "YOUR_DIRECTORY/sample-mixed-tamil-eng.jpg";
        ocrEngine.setImage(ImageStream.fromFile(imagePath));
```

> **What if the path is wrong?** パスが間違っている場合、Aspose.OCR は明確な `FileNotFoundException` をスローします。エラーハンドリングを柔軟にしたい場合は、呼び出しを try‑catch でラップしてください。

## ステップ 6: OCR の実行と画像からのテキスト抽出

すべての設定が完了したので、実際に認識を実行する時です。このステップは **extracts text from image** を行い、PDF 作成に必要なデータを準備します。

```java
        // 6️⃣ Perform recognition
        if (ocrEngine.recognize()) {
            String recognizedText = ocrEngine.getText();

            // Print the raw OCR output – handy for debugging
            System.out.println("Recognized text:");
            System.out.println(recognizedText);
```

デモ画像の典型的なコンソール出力は次のようになります：

```
வணக்கம் World
This is a mixed language sample.
```

Tamil の行が正しく表示され、その後に English が続くことに気付くでしょう。これは **set primary language** を正しく設定した結果です。

## ステップ 7: OCR PDF の保存 – 最後のピース

パズルの最後のピースは **save OCR pdf** です。Aspose.OCR は元画像の上に見えないテキスト層を埋め込むことで、PDF を検索可能にします。

```java
            // 7️⃣ (Optional) Save a searchable PDF with an OCR layer
            String pdfPath = "YOUR_DIRECTORY/searchable.pdf";
            ocrEngine.save(pdfPath, SaveFormat.PdfSearchable);

            System.out.println("\nSearchable PDF saved to: " + pdfPath);
        } else {
            System.err.println("Recognition failed: " + ocrEngine.getErrorMessage());
        }
    }
}
```

`searchable.pdf` を Adobe Reader で開き、**Ctrl + F** を押すと、Tamil と English の両方の単語を検索できます—まさに **create searchable pdf** ワークフローが約束することです。

## 完全動作サンプル（コピー＆ペースト）

以下はそのままコンパイルして実行できる完全なプログラムです。プレースホルダーのパスはご自身のディレクトリに置き換えてください。

```java
import com.aspose.ocr.*;

public class RecentFeaturesDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Load your Aspose.OCR license (or use the 30‑day trial)
        License license = new License();
        license.setLicense("YOUR_DIRECTORY/Aspose.OCR.Java.lic");

        // Step 2: Create and configure the OCR engine
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.getEngineSettings().setUseGpu(true);                     // enable CUDA GPU acceleration
        ocrEngine.getEngineSettings().setUseParallelProcessing(true);     // use multiple CPU cores
        ocrEngine.getLanguageSettings().setLanguage(Language.Tamil);      // primary language
        ocrEngine.getLanguageSettings().setSecondaryLanguage(Language.English); // secondary language
        ocrEngine.getPreprocessingSettings()
                 .setDeskew(true)   // correct image rotation
                 .setDenoise(true); // reduce background noise

        // Step 3: Load the image you want to recognize
        String imagePath = "YOUR_DIRECTORY/sample-mixed-tamil-eng.jpg";
        ocrEngine.setImage(ImageStream.fromFile(imagePath));

        // Step 4: Run OCR and obtain the plain‑text result
        if (ocrEngine.recognize()) {
            String recognizedText = ocrEngine.getText();

            // Step 5: (Optional) Save a searchable PDF with an OCR layer
            String pdfPath = "YOUR_DIRECTORY/searchable.pdf";
            ocrEngine.save(pdfPath, SaveFormat.PdfSearchable);

            System.out.println("Recognized text:");
            System.out.println(recognizedText);
            System.out.println("\nSearchable PDF saved to: " + pdfPath);
        } else {
            System.err.println("Recognition failed: " + ocrEngine.getErrorMessage());
        }
    }
}
```

次のコマンドで実行します：

```bash
javac -cp "path/to/aspose-ocr.jar" RecentFeaturesDemo.java
java -cp ".:path/to/aspose-ocr.jar" RecentFeaturesDemo
```

コンソールに抽出されたテキストが表示され、続いて **searchable pdf** がディスクに書き込まれたことを示す確認メッセージが出るはずです。

## よくある質問とエッジケース

### バイト配列から **load image OCR** が必要な場合は？

`ImageStream.fromFile(imagePath)` を `ImageStream.fromBytes(byteArray)` に置き換えることができます。画像がデータベースやウェブサービスから取得される場合に便利です。

### 既に画像を含む PDF を処理するには？

Aspose.OCR は PDF ページに直接対処できます：`ocrEngine.setDocument(PdfDocument.fromFile("input.pdf"))`。エンジンは認識前に各ページを内部でラスタライズします。

### GPU が検出されない場合、`setUseGpu(true)` を残すべきですか？

`setUseGpu(true)` が失敗した場合、Aspose.OCR は自動的に CPU にフォールバックします。有効化する前に `ocrEngine.getEngineSettings().isGpuAvailable()` で GPU の利用可否を確認できます。

### カスタムメタデータ付きで **save OCR pdf** できますか？

はい。認識後に `ocrEngine.getPdfSaveOptions().setTitle("My Document")` や `setAuthor("John Doe")` を呼び出し、`save` の前に設定します。

## 大量バッチ処理のパフォーマンスチップ

- **Batch processing:** �数の画像で同じ `OcrEngine` インスタンスを再利用します。実行間は `ocrEngine.clear()` を呼び出すだけです。
- **Thread pool:** 各画像タスクを `Callable` でラップし、`ExecutorService` に送信します。並列処理を有効にしているため、各スレッドがマルチコアの恩恵を受けます。
- **Memory management:** ギガピクセル画像の場合、`ocrEngine.getPreprocessingSettings().setResizeFactor(0.5)` でダウンサンプリングを検討し、RAM 使用量を抑えます。

## 結論

私たちは Aspose.OCR for Java を使用した完全な **create searchable pdf** ワークフローを一通り解説しました。**load image OCR** から始め、 

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}