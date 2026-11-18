---
category: general
date: 2026-05-03
description: Aspose OCR for Java を使用して画像からテキストを認識し、画像をテキストに変換する方法を学びます。OCR の精度を向上させるヒントや
  PNG ファイルで OCR を実行する方法も含まれています。
draft: false
keywords:
- recognize text from image
- convert image to text
- improve ocr accuracy
- load image for ocr
- run ocr on png
language: ja
og_description: Aspose OCR for Java を使用して画像からテキストを認識するステップバイステップガイド。画像をテキストに変換し、OCR
  の精度を向上させ、PNG で OCR を実行する方法を学びます。
og_title: Aspose OCRで画像からテキストを認識する – Javaチュートリアル
tags:
- OCR
- Java
- Aspose
- Image Processing
title: Aspose OCRで画像からテキストを認識する – 完全なJavaガイド
url: /ja/python-java/general/recognize-text-from-image-with-aspose-ocr-complete-java-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 画像からテキストを認識する Aspose OCR – 完全な Java ガイド

画像からテキストを**認識する**必要があったことはありませんか？しかし、どのライブラリが信頼できる結果を提供するか分からなかった…という方は多いです。スキャンした PDF、レシート、検査報告書からデータを抽出しようとしたときに、壁にぶつかることがよくあります。朗報です。Aspose OCR for Java を使えば、全工程がとても簡単になり、数行のコードで**画像をテキストに変換する**ことさえ可能です。

このチュートリアルでは、OCR 用に画像をロードする方法、設定を調整して**OCR精度を向上させる**コツ、そして最終的に**PNGでOCRを実行する**ファイルでテキストを抽出して表示するまで、必要な手順をすべて解説します。余計な説明は省き、すぐにプロジェクトに組み込める実用的なサンプルを提供します。

---

## 必要なもの

始める前に、以下がマシンに揃っていることを確認してください：

| 前提条件 | 理由 |
|--------------|--------|
| Java 17（またはそれ以降） | Aspose OCR は Java 8+ を対象としていますが、最新の JDK の方がパフォーマンスが向上します。 |
| Aspose OCR for Java ライブラリ (`aspose-ocr.jar`) | 重い処理を実行するコアエンジンです。 |
| 有効な Aspose OCR ライセンス ファイル (`Aspose.OCR.Java.lic`) | フル機能が有効になります。ライセンスがないと試用版の透かしが表示されます。 |
| 明瞭なテキストを含む画像ファイル（PNG、JPEG、TIFF など） | 具体例として `lab_report.png` を使用します。 |
| カスタム辞書（オプション） | 「hemoglobin」など、ドメイン固有の用語認識を向上させます。 |

これらの項目に見覚えがなくても慌てないでください。JAR をインストールし、簡単なテキストファイルを作成するだけで済む作業ですので、後ほど手順を説明します。

---

## 手順 1 – プロジェクトの設定と依存関係のインポート

まず、Maven（または Gradle）で新しいプロジェクトを作成し、Aspose OCR の依存関係を追加します。Maven を使用している場合は、以下のスニペットを `pom.xml` に貼り付けてください：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- check the latest version on Maven Central -->
</dependency>
```

Gradle を好む場合は、同等の設定は次の通りです：

```groovy
implementation 'com.aspose:aspose-ocr:23.10'
```

> **Pro tip:** バージョン番号に注意してください。新しいリリースには、**OCR精度を向上させる** 直接的なバグ修正が含まれることが多いです。

次に、`OcrDemo.java` という名前の Java クラスを作成します。ファイルの先頭で必要なクラスをインポートします：

```java
import com.aspose.ocr.OcrEngine;
import com.aspose.ocr.License;
import com.aspose.ocr.Image;
import com.aspose.ocr.OcrResult;
```

---

## 手順 2 – OCR エンジンの初期化とライセンスの適用

**PNGでOCRを実行する**には、まずエンジンにライセンスが適用されていることを知らせる必要があります。以下のコードで設定します：

```java
public class OcrDemo {
    public static void main(String[] args) {
        // Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Apply your license – replace the path with your actual license location
        License lic = new License();
        lic.setLicense("YOUR_DIRECTORY/Aspose.OCR.Java.lic");
        ocrEngine.setLicense(lic);
```

なぜ `License` オブジェクトを別に用意するのか？Aspose はライセンス管理をエンジン本体から分離しているため、マルチテナント SaaS シナリオでライセンスを動的に切り替えることが容易になります。

---

## 手順 3 – カスタム辞書のロード（オプションだが強力）

医療用語や化学式、ブランド名など、特定のドメイン用語を扱う場合は、カスタム辞書を使用すると**OCR精度を向上させる**効果が劇的です。辞書は 1 行に 1 単語のプレーンテキストファイルです：

```java
        // Optional: improve accuracy with a custom dictionary
        // Create a file named custom_dictionary.txt in YOUR_DIRECTORY
        ocrEngine.getConfig().setCustomDictionary("YOUR_DIRECTORY/custom_dictionary.txt");
```

> **Why it works:** OCR エンジンは辞書を利用して言語モデルを優先させ、例えば “hemo­globin” → “hemoglobin” のような誤認識を減らします。

辞書がない場合はこの行をスキップしてください。Aspose は組み込みの言語パックでも十分に機能します。

---

## 手順 4 – 処理したい画像のロード

ここで実際に**画像を OCR 用にロードする**作業を行います。Aspose は多数のフォーマットに対応していますが、PNG はロスレスであるため、スキャン文書に最適です。

```java
        // Load the PNG image containing the text you want to extract
        Image inputImage = Image.fromFile("YOUR_DIRECTORY/lab_report.png");
```

> **Edge case:** 画像が巨大（5 MB 超）な場合は、先に縮小して処理速度を上げることを検討してください。`Image` クラスの `resize` メソッドを認識前に呼び出すことができます。

---

## 手順 5 – OCR プロセスの実行とテキストの取得

すべての準備が整ったら OCR エンジンを起動します。`recognize` メソッドは抽出された文字列や信頼度スコア、必要に応じてレイアウト情報を含む `OcrResult` オブジェクトを返します。

```java
        // Perform OCR on the loaded image
        OcrResult result = ocrEngine.recognize(inputImage);

        // Print the extracted text to the console
        System.out.println("=== Extracted Text ===");
        System.out.println(result.getText());
    }
}
```

プログラムを実行すると、次のような出力が得られるはずです：

```
=== Extracted Text ===
Patient Name: John Doe
Hemoglobin: 13.5 g/dL
...
```

これで、Aspose OCR を使って**画像からテキストを認識する**ことと、**画像をテキストに変換する**ことに成功しました。

---

## 手順 6 – よくある落とし穴と対処法

堅実なライブラリでも、いくつかの障害が作業を妨げることがあります：

| 症状 | 考えられる原因 | 対策 |
|---------|--------------|-----|
| 空の出力 | ライセンスが適用されていない、または期限切れ | `Aspose.OCR.Java.lic` のパスを確認し、バージョンと一致しているか確認してください。 |
| 文字化け | 画像の解像度が低い、または過度に圧縮されている | より高解像度のソースを使用するか、画像を前処理（二値化、デスキュー）してください。 |
| ドメイン固有の単語が欠落 | カスタム辞書がない | 欠落している用語を1行ずつ記載した辞書ファイルを追加してください。 |
| 大量バッチで処理が遅い | マルチスレッド化がされていない | `OcrEngine` インスタンスのプールを作成（スレッドセーフ）し、画像を並列処理してください。 |

---

## 手順 7 – 例の拡張：結果をファイルに保存

抽出したテキストを後で分析したい場合は、単にファイルに書き出すだけです：

```java
import java.nio.file.Files;
import java.nio.file.Paths;
import java.nio.charset.StandardCharsets;

// ...

        // Save the text to a .txt file
        Files.write(Paths.get("output.txt"),
                    result.getText().getBytes(StandardCharsets.UTF_8));
        System.out.println("Text saved to output.txt");
```

これで、**画像を OCR 用にロードする**パイプラインが完成し、抽出した内容を好きな場所に保存できるようになりました。

---

## ボーナス: フォルダー内の複数 PNG ファイルで OCR を実行する

実務では数十枚のスキャンを一括処理することがよくあります。以下のループはディレクトリ内のすべての `.png` を取得して処理します：

```java
import java.io.File;

// ...

        File folder = new File("YOUR_DIRECTORY/scans");
        File[] pngFiles = folder.listFiles((dir, name) -> name.toLowerCase().endsWith(".png"));

        for (File png : pngFiles) {
            Image img = Image.fromFile(png.getAbsolutePath());
            OcrResult res = ocrEngine.recognize(img);
            System.out.println("---- " + png.getName() + " ----");
            System.out.println(res.getText());
        }
```

同じ `ocrEngine` インスタンスを再利用することを忘れないでください。ファイルごとに新しいインスタンスを作成すると、不要なオーバーヘッドが発生します。

---

## 結論

これで、Aspose OCR for Java を使用して**画像からテキストを認識する**フル機能のエンドツーエンドソリューションが手に入りました。画像のロード、カスタム辞書で**OCR精度を向上させる**オプション、**PNGでOCRを実行する**までのすべての工程がコードだけで完結し、任意の Java プロジェクトにすぐ組み込めます。

次のステップは？抽出したテキストを自然言語処理パイプラインに流し込んだり、手書きノートに対する OCR（Aspose には手書きモードもあります）を試したりしてみてください。可能性は無限大です。まずはこの第一歩を踏み出したことを祝福します。

Happy coding! もし問題が発生したら遠慮なくコメントを残してください。一緒にトラブルシューティングしましょう。

![コンソールの OCR 結果のスクリーンショット – 画像からテキストを認識](/images/ocr_console_result.png "画像からテキストを認識する例")

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}