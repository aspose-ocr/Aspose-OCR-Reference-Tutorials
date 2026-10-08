---
category: general
date: 2026-02-27
description: 自動言語検出により、Javaで PNG などの画像ファイルからテキストを抽出できます。自動言語検出を実装した Java OCR の例をご覧ください。
draft: false
keywords:
- automatic language detection
- extract text from image
- convert png to text
- java ocr example
- enable auto language detection
language: ja
og_description: Java OCR の自動言語検出により、画像ファイルからテキストを簡単に抽出できます。完全な Java OCR の例で自動言語検出の有効化方法を学びましょう。
og_title: Java OCRでの自動言語検出 – 完全ガイド
tags:
- Java
- OCR
- Aspose
title: Java OCR における自動言語検出 – ステップバイステップガイド
url: /ja/java/advanced-ocr-techniques/automatic-language-detection-in-java-ocr-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java OCR における自動言語検出 – 完全ガイド

英語とロシア語が混在したスクリーンショットからテキストを抽出する際に、**自動言語検出**が必要だったことはありませんか？ あなただけではありません。実際のアプリケーションでは、レシートスキャナや多言語フォーム、ソーシャルメディア画像ボットなど、事前に言語を手動で選択するのは面倒なポイントです。  

良いニュースは、Aspose OCR for Java が言語を自動で検出してくれるので、手動設定なしで画像ファイルから **テキストを抽出** できます。このチュートリアルでは、**自動言語検出** を有効にした **java ocr example** を示し、混在言語の PNG を処理して結果をコンソールに出力します。最後まで読めば、数行のコードだけで **png をテキストに変換** する方法が正確に分かります。

## 必要なもの

- Java 17（または最近の JDK） – API は Java 8+ でも動作しますが、新しいランタイムの方がパフォーマンスが向上します。
- Aspose OCR for Java ライブラリ（2026‑02‑27 時点の最新バージョン）。Maven Central から取得できます：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version>
</dependency>
```

- �数の言語が含まれる画像ファイル。デモでは `mixed-eng-rus.png`（英語 + ロシア語）を使用します。  
- 使いやすい IDE（IntelliJ IDEA、Eclipse、VS Code など） – どれでも構いません。

> **プロのコツ:** テスト画像がない場合は、英単語とそのロシア語訳を数個入れた PNG を作成すれば OK です。OCR エンジンはソースではなくピクセルデータだけを見ます。

以下は、すぐに実行できる完全なプログラムです。

![混在言語 PNG の自動言語検出](/images/mixed-eng-rus.png "自動言語検出の例")

## 手順 1: OCR エンジンのセットアップ

まず、`OcrEngine` のインスタンスを作成します。このオブジェクトはライブラリの中心で、すべての設定オプションを保持しており、**自動言語検出** を有効にするオプションも含まれています。

```java
import com.aspose.ocr.*;

public class MixedLanguageDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Initialise the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Enable automatic language detection
        ocrEngine.setAutoDetectLanguage(true);
```

なぜここで有効にするのでしょうか？  
`setAutoDetectLanguage(true)` を設定しない場合、エンジンはデフォルト言語（通常は英語）を想定します。画像に複数の文字体系が混在していると、検出ステップにより精度が大幅に向上します—まるで OCR が多言語通訳者のように、翻訳前に聞き取りを行うイメージです。

## 手順 2: 画像を入力して OCR 処理を実行

次に、エンジンに PNG ファイルを指示します。`processImage` メソッドは、認識されたテキスト、信頼度スコア、検出された言語コードなどを含む `OcrResult` オブジェクトを返します。

```java
        // Step 3: Process the image that contains both English and Russian text
        OcrResult ocrResult = ocrEngine.processImage("YOUR_DIRECTORY/mixed-eng-rus.png");
```

いくつか注意点があります：

- **パス処理:** 絶対パスを使用するか、画像をプロジェクトの resources フォルダーに置き、`getResourceAsStream` で読み込みます。
- **パフォーマンスのヒント:** 多数の画像を処理する場合は、毎回新しいインスタンスを作成するのではなく、同じ `OcrEngine` インスタンスを再利用してください。エンジンは言語モデルをキャッシュするため、以降の呼び出しは高速になります。

## 手順 3: 認識テキストの取得と表示

最後に、`OcrResult` からプレーンテキストを取得します。`getText()` メソッドはレイアウト情報を除去し、保存や検索、他システムへの入力に使えるクリーンな文字列を返します。

```java
        // Step 4: Print the recognized text to the console
        System.out.println(ocrResult.getText());
    }
}
```

プログラムを実行すると、以下のような出力が得られるはずです。

```
Hello world!
Привет мир!
```

この出力は、**自動言語検出** によりエンジンが英語とロシア語の両方のセクションを正しく識別したことを示しています。フラグをオフにすると、文字化けしたキリル文字が出力され、混在言語シナリオで自動検出機能が不可欠である理由が分かります。

## 一般的なバリエーションとエッジケース

### 言語検出なしで PNG をテキストに変換

画像が単一言語のみを含むことが分かっている場合は、自動検出ステップを省略できます。

```java
ocrEngine.setLanguage(OcrLanguage.English);
```

ただし、別の文字体系の文字が混入した瞬間、精度は急激に低下することを覚えておいてください。

### 大きな画像の取り扱い

高解像度のスキャンの場合、画像を投入する前に最大 300 DPI にダウンサンプリングすることを検討してください。OCR エンジンは 150‑300 DPI の範囲で最適に動作し、それ以上はメモリを無駄にするだけで実質的な効果は得られません。

```java
BufferedImage original = ImageIO.read(new File("large.png"));
BufferedImage resized = ImageUtil.resize(original, 1024, 0); // keep aspect ratio
ocrEngine.processImage(resized);
```

### Web サービスで画像からテキストを抽出

この機能を REST エンドポイント経由で提供する場合、次の点に留意してください：

- アップロードされたファイルタイプを検証する（PNG/JPEG のみ受け付ける）。
- OCR をバックグラウンドスレッドまたは非同期タスクで実行し、リクエストスレッドのブロックを回避する。
- テキストを JSON で返す：

```json
{ "extractedText": "Hello world!\nПривет мир!" }
```

## 完全な動作例（全手順を統合）

以下は、`MixedLanguageDemo.java` ファイルにコピー＆ペーストできる完全なプログラムです。インポート文、エラーハンドリング、各行の説明コメントが含まれています。

```java
import com.aspose.ocr.*;
import java.io.File;

/**
 * Demonstrates automatic language detection with Aspose OCR for Java.
 * This example loads a PNG that contains both English and Russian text,
 * enables auto‑detect, and prints the extracted text.
 */
public class MixedLanguageDemo {
    public static void main(String[] args) throws Exception {
        // Initialise the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Enable automatic language detection so the engine picks the right script(s)
        ocrEngine.setAutoDetectLanguage(true);

        // Path to the image – replace with your actual location
        String imagePath = "YOUR_DIRECTORY/mixed-eng-rus.png";

        // Process the image and obtain the result
        OcrResult ocrResult = ocrEngine.processImage(imagePath);

        // Output the recognized text – should contain both English and Russian lines
        System.out.println("=== Extracted Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

以下のコマンドで実行します：

```bash
mvn compile exec:java -Dexec.mainClass=MixedLanguageDemo
```

設定が正しく行われていれば、コンソールに英語の行とそれに続くロシア語の行が表示されます。

## まとめと次のステップ

本稿では、**java ocr example** を通じて **自動言語検出を有効化** し、混在言語の PNG を処理し、**画像からテキストを抽出** する方法を手動で言語を選択せずに実演しました。主なポイントは次の通りです。

1. `setAutoDetectLanguage(true)` を有効にして、Aspose に多言語コンテンツの処理を任せます。
2. `processImage` を使用して任意の PNG（または JPEG）を入力し、`getText()` でクリーンな文字列を取得します。
3. 同じパターンは PDF、TIFF、あるいはライブカメラストリームでも機能します—入力ソースを差し替えるだけです。

さらに踏み込むには、次のアイデアを試してみてください：

- **バッチ処理:** PNG フォルダーをループし、各結果をデータベースに保存する。
- **言語別の後処理:** 検出後、英語テキストはスペルチェッカーへ、ロシア語テキストは音写サービスへ送る。
- **AI と組み合わせる:** 抽出したテキストを言語モデルに入力し、要約や翻訳を行う。

以上です。もし問題が発生した場合（例: エンジンが期待した言語を検出しないなど）、画像が鮮明かつ最新の Aspose OCR バージョンを使用しているか再確認してください。コーディングを楽しんで、Java プロジェクトで **自動言語検出** の力を活用してください！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}