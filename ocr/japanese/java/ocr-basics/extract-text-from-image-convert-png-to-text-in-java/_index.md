---
category: general
date: 2026-02-19
description: Aspose OCR Java を使用して画像からテキストを抽出する – PNG をテキストに変換する方法、OCR 用に画像を読み込む方法、そして
  Java OCR チュートリアルに従う方法を学びましょう。
draft: false
keywords:
- extract text from image
- convert png to text
- load image for ocr
- java ocr tutorial
- Aspose OCR Java
- OCR language support
language: ja
og_description: Aspose OCR Javaで画像からテキストを抽出します。ステップバイステップのJava OCRチュートリアルに従って、PNGをテキストに変換し、OCR用に画像を読み込みます。
og_title: 画像からテキストを抽出 – Java OCRガイド
tags:
- OCR
- Java
- Aspose
- Image Processing
title: 画像からテキストを抽出 – JavaでPNGをテキストに変換
url: /ja/java/ocr-basics/extract-text-from-image-convert-png-to-text-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 画像からテキストを抽出 – Java OCR チュートリアル

画像からテキストを**抽出**したいと思ったことはありませんか、しかし手間のかかるライブラリ選びに悩んでいませんか？ あなただけではありません—開発者は常に「Java で PNG をテキストに変換するにはどうすればいいのか？」と質問します。 良いニュースは、Aspose OCR を使えば、全工程がまるで散歩のように簡単になることです。このガイドでは、完全な**java ocr tutorial**を順に解説し、**OCR 用に画像を読み込む**方法を示し、最終的にクリーンで検索可能なテキストを取得します。

エンジンの設定から多言語コンテンツの処理まで網羅しますので、最後にはサイズ・フォーマット・言語を問わず**画像からテキストを抽出**できるようになります。外部サービスや API キーは不要—JAR ファイル一つと数行のコードだけです。

## 必要なもの

始める前に、以下が揃っていることを確認してください。

- JDK 8 以上がインストール済み（コードは JDK 11+ でも動作します）。  
- Maven または Gradle で Aspose OCR ライブラリを取得するか、Aspose の公式サイトから JAR を手動でダウンロード。  
- 読み取り可能なテキストを含む PNG 画像（例として `khmer-sign.png` を使用）。  
- お好みの IDE またはテキストエディタ—IntelliJ IDEA、Eclipse、VS Code など、どれでも構いません。

以上です。重いフレームワークやクラウド認証情報は不要です。準備はできましたか？ 画像ファイルからテキストを抽出しましょう。

## 手順 1: Aspose OCR をプロジェクトに追加

まずは OCR エンジンをクラスパスに配置します。Maven を使う場合は `pom.xml` に次の依存関係を追加してください。

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- check the latest version on Maven Central -->
</dependency>
```

Gradle を使う場合は次のように記述します。

```groovy
implementation 'com.aspose:aspose-ocr:23.10'
```

手動で追加したい場合は、Aspose のダウンロードページから JAR を取得し、プロジェクトの `libs` フォルダに入れたうえでビルドパスに追加してください。

> **プロのコツ:** 常に最新の安定版を選びましょう。古いリリースは言語パックやバグ修正が欠けていることがあります。

## 手順 2: OCR エンジンのインスタンスを作成

ライブラリが利用可能になったら、`OcrEngine` を生成します。エンジンはピクセルを文字に変換する「脳」のようなものです。

```java
import com.aspose.ocr.*;

public class ExtractTextExample {
    public static void main(String[] args) throws Exception {
        // Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();
        // ... further steps will follow
    }
}
```

なぜ毎回新しいエンジンを作成するのか？ エンジンは内部バッファや言語データを保持しているため、クリーンな状態から開始することで、特に後で言語を切り替える場合に決定的な結果が得られます。

## 手順 3: 必要な言語を有効化（任意だが推奨）

Aspose OCR には多数の言語パックが同梱されています。画像の言語が分かっている場合は明示的に有効化しましょう。これにより認識速度と精度が向上します。サンプルではクメール語 (`khm`) を有効化しますが、英語なら `ENG`、中国語なら `CHN` などに置き換えてください。

```java
// Enable Khmer language support (ISO 639‑2 code "khm")
ocrEngine.getLanguages().add(OcrLanguage.KHM);
```

> **なぜ重要か:** **OCR 用に画像を読み込む**際、エンジンは有効化された言語辞書だけを検索します。すべての言語をオンにしたままにすると処理が遅くなり、誤認識が増える可能性があります。

## 手順 4: OCR 用に画像を読み込む – PNG をテキストに変換

ここで**OCR 用に画像を読み込む**処理が行われます。Aspose は低レベルの I/O を抽象化した便利な `ImageStream.fromFile` ヘルパーを提供しています。

```java
// Load the PNG that contains the text you want to extract
ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/khmer-sign.png"));
```

画像が JPEG、BMP、TIFF など別のフォーマットでも同じメソッドが機能します—Aspose が自動で形式を検出します。ファイルパスが正しいことを確認してください。間違っていると `FileNotFoundException` が発生します。

## 手順 5: OCR 処理を実行し PNG をテキストに変換

エンジンが準備でき、画像が読み込まれたら、認識は単一メソッド呼び出しで完了します。結果オブジェクトは生の文字列と信頼度スコアを提供します。

```java
// Run OCR and fetch the recognized text
String recognizedText = ocrEngine.recognize().getText();
```

これで**PNG をテキストに変換**しました。返された文字列はエンジンが見た通りの改行や空白を含んでいます。`trim()`、`replaceAll("\\s+", " ")`、または必要なクリーンアップ処理を施してください。

## 手順 6: 結果を出力（または保存）

簡単な動作確認として、コンソールに結果を出力します。実際のアプリケーションではファイルやデータベースに書き込んだり、別サービスに渡したりすることが多いでしょう。

```java
System.out.println("Recognized text:");
System.out.println(recognizedText);
```

**期待される出力**（サンプルのクメール文字列）は次のようになります:

```
សួស្តី
Welcome
```

出力が文字化けしている場合は、手順 3 で正しい言語を有効化したか、画像がぼやけていないか確認してください。解像度を 300 dpi 以上に上げると改善することが多いです。

## 完全動作サンプル

すべてを組み合わせた、`ExtractTextExample.java` に貼り付けて実行できる自己完結型プログラムは以下の通りです。

```java
import com.aspose.ocr.*;

public class ExtractTextExample {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Enable the language you need (Khmer in this case)
        ocrEngine.getLanguages().add(OcrLanguage.KHM);

        // 3️⃣ Load the PNG image you want to extract text from
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/khmer-sign.png"));

        // 4️⃣ Run OCR – this step actually converts PNG to text
        String recognizedText = ocrEngine.recognize().getText();

        // 5️⃣ Show the result
        System.out.println("=== OCR Result ===");
        System.out.println(recognizedText);
    }
}
```

プログラムの実行は次のコマンドで行います。

```bash
mvn compile exec:java -Dexec.mainClass=ExtractTextExample
```

Gradle を使用する場合は次のように実行してください。

```bash
./gradlew run --args='ExtractTextExample'
```

コンソールに抽出されたテキストが表示されれば、Aspose OCR を使って**画像からテキストを抽出**できたことになります。

## よくある落とし穴と対処法

| 症状 | 想定原因 | 対処 |
|------|----------|------|
| 空文字列が返る | 言語が有効化されていない、または誤った言語コード | 適切な `OcrLanguage`（例: 英語なら `ENG`）を追加 |
| 文字化け | 画像解像度が低すぎる、または背景がノイズ | 高解像度の画像を使用、またはシャープフィルタで前処理 |
| `OutOfMemoryError` | 非常に大きな画像をフルサイズで読み込んでいる | エンジンに渡す前に `ImageStream.fromFile(...).scale(0.5)` で縮小 |
| `FileNotFoundException` | パスが間違っている | 絶対パスまたは相対パスを確認し、`Paths.get(...).toAbsolutePath()` を使用 |

> **覚えておくべきこと:** OCR は確率的プロセスです。完璧な設定でも、特に手書きや筆記体のスクリプトでは手動で数文字修正する必要がある場合があります。

## チュートリアルの拡張 – 次のステップ

- **バッチ処理:** ディレクトリ内の PNG ファイルをループし、同じロジックを各画像に適用。  
- **PDF 出力:** Aspose PDF を使って抽出テキストを検索可能な PDF に埋め込む。  
- **言語検出:** `ocrEngine.detectLanguage()` を呼び出して、エンジンに自動で言語を推測させる。  
- **クラウド統合:** スケールが必要な場合はコードを REST エンドポイントでラップし、マイクロサービスから呼び出す。

これらすべては、今回完了した**java ocr tutorial**を基礎に構築でき、Aspose OCR API の汎用性の高さを実感できるでしょう。

## 結論

本稿では、Aspose OCR を利用して**画像からテキストを抽出**し、**PNG をテキストに変換**し、正しく**OCR 用に画像を読み込む**手順を一通り解説しました。手順はシンプルです：ライブラリを追加、エンジンを作成、適切な言語を有効化、PNG を読み込み、`recognize()` を実行し、出力を処理する。これを基にデータ入力の自動化や検索可能アーカイブの構築、画像から機械可読テキストが必要なあらゆるアプリケーションを実装できます。

ぜひ自分の画像で試してみてください—領収書のスクリーンショットやスキャンした契約書など。言語設定や解像度を調整すれば、ソリューションの柔軟性をすぐに実感できるはずです。問題が発生したら、上記の落とし穴表や Aspose の公式ドキュメント（常に最新）を参照してください。

Happy coding, and may your next project be full of clean, searchable text!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}