---
category: general
date: 2026-03-28
description: Aspose OCR を使用して Java で画像の OCR を実行し、画像をテキストに変換し、PNG からタイ語テキストを迅速かつ確実に抽出します。
draft: false
keywords:
- run OCR on image
- convert image to text
- extract text from PNG
- extract Thai text
- recognize Thai text
language: ja
og_description: Java と Aspose OCR を使用して画像の OCR を実行し、画像をテキストに変換する方法、PNG からタイ語テキストを抽出する方法、そして一般的な落とし穴への対処法を学びます。
og_title: Javaで画像のOCRを実行 – タイ語テキストを高速抽出
tags:
- OCR
- Java
- Aspose
- Image Processing
title: Javaで画像のOCRを実行 – PNGからタイ語テキストを抽出
url: /ja/java/ocr-operations/run-ocr-on-image-with-java-extract-thai-text-from-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Javaで画像のOCRを実行 – フル機能チュートリアル

Javaコードから直接 **run OCR on image** ファイルを実行したことがありますか？タイ語のレシート、スキャンした文書、スクリーンショットなどを多数持っていて、手動で入力せずにテキストが欲しいというケースはよくあります。特にソースが PNG で言語がラテン文字以外の場合、これは大きな痛点です。

このガイドでは、Aspose OCR ライブラリを使用して **run OCR on image** を実行し、画像をプレーンテキストに変換し、タイ文字を確実に抽出する方法をステップバイステップで示します。最後まで読めば、**convert image to text**、**extract text from PNG**、さらには数行のコードだけで **recognize Thai text** できるようになります。

## このチュートリアルでカバーする内容

* Maven/Gradle プロジェクトへの Aspose OCR 依存関係の設定。  
* `OcrEngine` の初期化とタイ語用の設定。  
* PNG ファイルに対して OCR を実行し、エラー処理を行う方法。  
* 結果をコンソールに出力し、出力内容を確認する手順。  

Aspose の事前知識は不要です。基本的な Java IDE と処理したい画像ファイルがあれば始められます。

## 前提条件

* Java 8 以上がインストールされていること（ライブラリは Java 11+ でも動作します）。  
* ビルドツール – Maven または Gradle（ここでは Maven の例を示します）。  
* Aspose OCR ライセンス（無料トライアルでもテストは可能ですが、ライセンスを取得すると評価制限が解除されます）。  
* タイ語テキストを含む PNG、例: `input.png` をプロジェクトの resources フォルダーに配置しておくこと。

---

## 手順 1: Aspose OCR をプロジェクトに追加

### Maven

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- Use the latest version -->
</dependency>
```

### Gradle (Kotlin DSL)

```kotlin
implementation("com.aspose:aspose-ocr:23.9")
```

> **プロのコツ:** ライブラリのバージョンは公式の Aspose リリースノートと同期させてください。新しいバージョンでは言語パックやパフォーマンス改善が追加されています。

依存関係が解決されると、IDE が必要なクラスを自動でインポートします。

## 手順 2: OCR エンジンの初期化

エンジンはプロセスの中心、すなわちピクセルパターンを解析する「脳」のようなものです。ここではタイ文字だけを対象にするよう設定します。

```java
import com.aspose.ocr.*;

public class ThaiOcrDemo {
    public static void main(String[] args) throws Exception {
        // Step 2: Create the OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Tell the engine to look for Thai language patterns
        ocrEngine.getRecognitionSettings().setLanguage("th");
```

言語を明示的に設定する理由は何ですか？ `"th"` を指定すると文字セットが絞られ、認識速度が向上し、似た形の文字の誤認識が減少します。

## 手順 3: PNG ファイルに対して OCR を実行

ここでエンジンにデコードしたい画像を渡します。`recognizeImage` メソッドは抽出された文字列と信頼度スコアを保持する `OcrResult` オブジェクトを返します。

```java
        // Step 3: Perform OCR on the target image
        String imagePath = "src/main/resources/input.png";
        OcrResult ocrResult = ocrEngine.recognizeImage(imagePath);
```

ファイルが見つからない場合、Aspose は `FileNotFoundException` をスローします。実運用コードでは `try‑catch` でラップするのが推奨ですが、このチュートリアルではシンプルにしています。

## 手順 4: 認識結果の出力

最後に結果をコンソールに出力します。`getText()` メソッドはプレーンな Java `String` を返すので、保存したりネットワークで送信したり、ファイルに書き込んだりできます。

```java
        // Step 4: Display the extracted Thai text
        System.out.println("=== Recognized Thai Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

プログラムを実行すると、次のような出力が得られるはずです。

```
=== Recognized Thai Text ===
สวัสดีครับ นี่คือข้อความจากรูปภาพ
```

出力が文字化けしている場合は、元の PNG が高解像度（最低 300 dpi）であること、言語コード `"th"` が目的の言語と一致していることを再確認してください。

### 完全なコード一覧

以下はそのまま実行可能な Java ファイルです。IDE にコピペし、必要に応じて画像パスを置き換えて **Run** をクリックしてください。

```java
import com.aspose.ocr.*;

public class ThaiOcrDemo {
    public static void main(String[] args) throws Exception {
        // Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Select Thai language for recognition
        ocrEngine.getRecognitionSettings().setLanguage("th");

        // Run OCR on the PNG image
        String imagePath = "src/main/resources/input.png";
        OcrResult ocrResult = ocrEngine.recognizeImage(imagePath);

        // Output the recognized text
        System.out.println("=== Recognized Thai Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

![画像のOCR実行例](image.png "画像のOCR実行例 – PNG からタイ語テキストを抽出する Java コード")

## 手順 5: よくあるバリエーションとエッジケース

### 他フォーマットでの Image → Text 変換

JPEG や BMP でも **convert image to text** が必要な場合は、`imagePath` の拡張子を変更するだけです。Aspose OCR は PNG、JPEG、BMP、TIFF、さらには PDF ページもサポートしています。

### 複数言語を含む PNG からのテキスト抽出

エンジンに複数言語を同時に検出させることも可能です：

```java
ocrEngine.getRecognitionSettings().setLanguage("th,en");
```

結果にはタイ語と英語の文字が混在し、バイリンガルのレシートなどに便利です。

### 低品質画像の処理

ぼやけたスキャンの場合は前処理を有効にすると効果的です：

```java
ocrEngine.getRecognitionSettings().setPreprocessMode(PreprocessMode.Auto);
```

これにより組み込みのノイズ除去とコントラスト強化アルゴリズムが動作し、**extract text from PNG** のステップが改善されます。

### ライセンスの有効化

ライセンスがない場合、Aspose は 100 ページ以降の出力に透かし行を挿入します。早めにライセンスをアクティベートしましょう：

```java
License license = new License();
license.setLicense("Aspose.OCR.lic");
```

`.lic` ファイルを JAR と同じディレクトリに置くか、絶対パスで参照してください。

## FAQ（よくある質問）

**Q: Linux でも動作しますか？**  
A: はい。Aspose OCR は純粋な Java ライブラリなので、JVM が動作する OS であれば問題ありません。

**Q: PNG に手書きのタイ文字が含まれている場合は？**  
A: 手書き認識は限定的です。専用のニューラルネットワークモデルが必要になることがあります。Aspose OCR は印刷文字で高い精度を発揮します。

**Q: フォルダー内の画像をバッチ処理できますか？**  
A: `Files.list(Paths.get("folder"))` で取得したファイルリストに対して `recognizeImage` をループで呼び出すだけです。パフォーマンス向上のため、同じ `OcrEngine` インスタンスを再利用してください。

## まとめ

Java で **run OCR on image** ファイルを実行し、PNG から **extract Thai text** する完全なエンドツーエンド例を解説しました。`OcrEngine` の初期化、言語設定、`recognizeImage` の呼び出し、結果の出力という流れをマスターすれば、サードパーティサービスに頼らず **convert image to text** が可能になります。

次のような活用が考えられます：

* 大量の **extract text from PNG** ファイルをデータマイニングに利用。  
* OCR 結果を翻訳 API に渡して英語訳を取得。  
* 言語コードを変更して中国語やアラビア語など、Aspose がサポートする他言語を試す。

ぜひ自分の画像で試してみてください。前処理設定を調整したり、異なるファイル形式で実験したりして、実務フローでどれだけ頑健に動作するか確認してみましょう。

Happy coding, and may your OCR pipelines be ever accurate!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}