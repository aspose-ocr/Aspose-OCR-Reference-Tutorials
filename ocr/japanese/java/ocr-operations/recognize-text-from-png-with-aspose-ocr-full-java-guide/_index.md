---
category: general
date: 2026-03-28
description: JavaでAspose OCRを使用してPNGからテキストを認識する方法を学びます。画像からテキストを抽出し、混在する言語に対して自動言語検出を有効にします。
draft: false
keywords:
- recognize text from png
- extract text from image
- enable auto language detection
language: ja
og_description: PNGからテキストを即座に認識します。このガイドでは、画像からテキストを抽出し、混在言語のPDFで自動言語検出を有効にする方法を示します。
og_title: Aspose OCRでPNGからテキストを認識する – 完全なJavaチュートリアル
tags:
- Aspose OCR
- Java
- Image Processing
title: Aspose OCRでPNGからテキストを認識する – 完全Javaガイド
url: /ja/java/ocr-operations/recognize-text-from-png-with-aspose-ocr-full-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# png からテキストを認識する Aspose OCR – 完全な Java チュートリアル

png ファイルから **テキストを認識** したいけれど、混在言語をうまく処理できるライブラリが分からない…ということはありませんか？同じ壁にぶつかる開発者は多いです。レシートやパスポート、多言語の看板を読み取る必要があるアプリでは特に悩みます。

良いニュースは、Aspose OCR を使えばそれがとても簡単になることです。数行のコードで **画像からテキストを抽出** し、PNG を検索可能なデータに変換でき、さらに **自動言語検出** を有効にすればエンジンがその場で適切なスクリプトを選択してくれます。

このチュートリアルでは、前提条件、ステップバイステップのコード、各設定の意味、出力の検証方法をすべて解説します。最後まで読めば、英語・ロシア語・中国語が混在した PNG を手動で言語パックを切り替えることなく読み取れる、実行可能な Java プログラムが手に入ります。

---

## 必要なもの

- **Java Development Kit (JDK) 8+** – 任意の最新 JDK でコンパイル可能です。
- **Aspose.OCR for Java** ライブラリ（2026 年時点の最新バージョン）。Maven Central または Aspose の公式サイトから取得できます。
- 複数言語が含まれる画像ファイル（例: `mixed-lang.png`）。
- 好みの IDE（IntelliJ IDEA、Eclipse、VS Code など） – もちろんシンプルなテキストエディタでも構いません。

> **Pro tip:** Maven を使用している場合は以下の依存関係を追加してください。Maven を使わない場合は JAR をダウンロードし、クラスパスに追加します。

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- replace with the newest version -->
</dependency>
```

---

## Step 1: Initialize the OCR Engine to recognize text from png

エンジンが何かを行う前に、`OcrEngine` のインスタンスが必要です。このオブジェクトがすべての設定オプションを保持し、重い処理を実行します。

```java
import com.aspose.ocr.*;

public class MixedLangExample {
    public static void main(String[] args) throws Exception {

        // Create the OCR engine – this is the entry point for all operations
        OcrEngine ocrEngine = new OcrEngine();

        // --------------------------------------------------------------
        // Step 2 and 3 are configured here (see next sections)
        // --------------------------------------------------------------

        // Recognize the image and get the result object
        OcrResult ocrResult = ocrEngine.recognizeImage("YOUR_DIRECTORY/mixed-lang.png");

        // Print the extracted text to the console
        System.out.println("=== Recognized Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

> **Why this matters:** `OcrEngine` は内部の OCR アルゴリズムを抽象化します。エンジンを一度インスタンス化して複数画像で再利用する方が、ファイルごとに新しいエンジンを作成するよりも効率的です。

---

## Step 2: Enable auto language detection

このステップを省略すると、エンジンはデフォルトで単一言語（通常は英語）を想定し、キリル文字や漢字が文字化けします。自動検出を有効にすれば、Aspose が画像をスキャンして最適な言語モデルを自動的に選択します。

```java
// Enable automatic language detection – the engine will sniff the script
ocrEngine.getRecognitionSettings().setAutoDetectLanguage(true);
```

> **What’s happening under the hood?** Aspose OCR は文字頻度と Unicode 範囲をチェックする軽量な事前分析を行います。支配的な言語が検出されると、重い OCR 処理の前に該当言語モデルに切り替えられます。

---

## Step 3: (Optional) Limit detection to likely languages – improve speed

期待する言語が分かっている場合は、エンジンにヒントを与えることができます。これにより検索範囲が狭まり、CPU 使用率が下がり、結果的に処理速度が向上します。

```java
// Suggest candidate languages – only English, Russian, and Chinese will be considered
ocrEngine.getRecognitionSettings()
         .setCandidateLanguages(new String[] { "en", "ru", "zh" });
```

> **Tip:** このステップを省略してもエンジンは動作しますが、サポートされているすべての言語を評価するため、大量のバッチ処理では数秒の遅延が発生することがあります。

---

## Step 4: Recognize the PNG and extract text from image

エンジンの設定が完了したら、`recognizeImage` を呼び出します。このメソッドはファイルパス、`java.io.File`、あるいは `java.io.InputStream` を受け取れるので、Web アップロードやクラウドストレージからの入力にも柔軟に対応できます。

```java
// Perform OCR on the specified PNG file
OcrResult ocrResult = ocrEngine.recognizeImage("YOUR_DIRECTORY/mixed-lang.png");

// The result object holds the raw text, confidence scores, and layout info
String extractedText = ocrResult.getText();
```

> **Edge case:** 画像が回転している場合、Aspose OCR は自動回転が可能です。出力がずれていると感じたら `setDetectOrientation(true)` を手動で設定してください。

---

## Step 5: Display the result – verify the output

コンソールへの出力はデモとしては十分ですが、実際のアプリではテキストをデータベースに保存したり、検索インデックスに投入したり、REST API のレスポンスとして返したりすることが多いでしょう。以下は最小限の検証スニペットです。

```java
System.out.println("=== Recognized Text ===");
System.out.println(extractedText);
```

### Expected console output

`mixed-lang.png` に次の 3 行が含まれていると仮定します。

```
Hello world!
Привет мир!
你好，世界！
```

期待される出力例は以下の通りです。

```
=== Recognized Text ===
Hello world!
Привет мир!
你好，世界！
```

出力が文字化けしている場合は、`setAutoDetectLanguage(true)` が有効か、候補言語リストに必要なスクリプトが含まれているかを再確認してください。

---

## Full Working Example (All Steps Combined)

```java
import com.aspose.ocr.*;

public class MixedLangExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Enable automatic language detection
        ocrEngine.getRecognitionSettings().setAutoDetectLanguage(true);

        // Step 3: (Optional) Limit detection to likely languages
        ocrEngine.getRecognitionSettings()
                 .setCandidateLanguages(new String[] { "en", "ru", "zh" });

        // Step 4: Recognize the PNG image
        OcrResult ocrResult = ocrEngine.recognizeImage("YOUR_DIRECTORY/mixed-lang.png");

        // Step 5: Output the recognized text
        System.out.println("=== Recognized Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

> **Run it:** `javac MixedLangExample.java` でコンパイルし、`java MixedLangExample` で実行します。Aspose OCR の JAR がクラスパスに含まれていることを確認してください（例: Windows では `-cp aspose-ocr-23.12.jar;.`、Linux/macOS では `-cp aspose-ocr-23.12.jar:.`）。

---

## Common Questions & Gotchas

| 質問 | 回答 |
|----------|--------|
| **画像が PNG ではなく JPEG の場合は？** | 同じ `recognizeImage` メソッドで JPEG、BMP、TIFF なども処理できます。拡張子を変更するだけです。 |
| **HTTP リクエストからのストリームを処理できますか？** | もちろん可能です。`recognizeImage(InputStream)` を使用し、リクエストの入力ストリームを直接渡してください。 |
| **似たようなスクリプト（例: セルビア語キリル vs ロシア語）の自動言語検出はどれくらい正確ですか？** | 多くの場合十分に正確ですが、`candidateLanguages` に言語を追加して他を除外すれば、強制的に選択できます。 |
| **Aspose OCR のライセンスは必要ですか？** | 無料評価ライセンスでテストは可能ですが、本番環境では透かしを除去し全機能を解放する有料ライセンスが必要です。 |
| **大量バッチ処理のパフォーマンスは？** | `OcrEngine` インスタンスを1つだけ再利用し、画像を順次またはスレッドプールで処理してください。読み取り専用操作に関してはスレッドセーフです。 |

---

## Next Steps & Related Topics

- **PDF 内の画像からテキストを抽出** – Aspose PDF と OCR を組み合わせてスキャン文書を処理します。
- **バッチ処理** – Java の `ExecutorService` を使って数千枚の PNG を並列化します。
- **ポストプロセッシング** – 抽出後にスペルチェックや言語別トークナイズを適用します。
- **クラウドストレージとの統合** – AWS S3 や Azure Blob Storage から直接 PNG をストリームで読み取ります。

ぜひ試してみてください。回転したスキャン画像がある場合は `setDetectOrientation(true)` を追加したり、候補言語リストに日本語 (`"ja"`) やアラビア語 (`"ar"`) を加えてみたりしてください。API はほとんどの OCR 中心プロジェクトに対応できる柔軟性があります。

---

## Conclusion

これで **png からテキストを認識** する Aspose OCR の完全なサンプルが完成しました。**画像からテキストを抽出** し、**自動言語検出** を有効にして混在言語コンテンツを処理する方法を学びました。コードは完結しており、解説は「やり方」と「理由」の両方を網羅しています。期待通りの出力が得られたら、環境は正しく設定されています。

別のユースケースがありますか？ コメントでシェアしたり、上記の次のステップを試したりしてください。Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}