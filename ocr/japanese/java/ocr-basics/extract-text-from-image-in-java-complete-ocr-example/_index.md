---
category: general
date: 2026-02-19
description: Java OCR を使用して画像からテキストを抽出します。画像を OCR に読み込み、請求書ファイルからテキストを抽出する Java OCR
  の例を、数ステップで学びましょう。
draft: false
keywords:
- extract text from image
- java ocr example
- load image for ocr
- extract text from invoice
language: ja
og_description: Java OCR を使用して画像からテキストを抽出します。このガイドでは、OCR 用に画像を読み込む方法と、シンプルな Java OCR
  の例で請求書からテキストを取得する方法を示します。
og_title: Javaで画像からテキストを抽出 – 完全なOCR例
tags:
- OCR
- Java
- Aspose
- Image Processing
title: Javaで画像からテキストを抽出 – 完全なOCR例
url: /ja/java/ocr-basics/extract-text-from-image-in-java-complete-ocr-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Javaで画像からテキストを抽出 – 完全OCR例

画像から **テキストを抽出** したいけど、どのライブラリを選べばいいか分からないことはありませんか？ あなたは一人ではありません。請求書処理の自動化や検索可能なアーカイブ構築で、多くの開発者が同じ壁にぶつかります。良いニュースは、数行の Java コードで OCR 用に画像を読み込み、関心領域（ROI）を定義し、必要なテキストを正確に取得できることです。

このチュートリアルでは、Aspose.OCR を使用して **java ocr example** を実演し、**load image for OCR** の方法、ROI の設定、そして **extract text from invoice** ファイルの手順を詳しく解説します。最後まで読めば、任意の Java プロジェクトに組み込める実行可能なプログラムが手に入ります。

## 学べること

- `OcrEngine` インスタンスの作成方法とその重要性
- Aspose の `ImageStream` を使った **load image for OCR** の正しい手順
- **region of interest (ROI)** を設定して、請求書の金額が含まれる画像部分だけを処理する方法
- 認識されたテキストを取得し、コンソールに出力する方法
- よくある落とし穴（例：矩形座標の誤り）とその迅速な対処法

**前提条件**

- Java 8 以上がインストールされていること
- Maven または Gradle で Aspose.OCR ライブラリ（`com.aspose:aspose-ocr`）を取得できること
- `invoice.png` というサンプル請求書画像が既知のディレクトリに配置されていること

すべて揃いましたか？ では、始めましょう。

![Extract text from image using Java OCR](/images/extract-text-from-image-java.png "extract text from image example")

## 画像からテキストを抽出 – ステップバイステップ Java OCR 例

以下に完全なソースコードを示します。`RoiOcrExample.java` にコピー＆ペーストしてそのまま実行してください。

```java
import com.aspose.ocr.*;

public class RoiOcrExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create an OCR engine instance.
        // The engine holds all configuration and performs the heavy lifting.
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the source image.
        // You can point to any PNG, JPG, or TIFF file. Here we use a sample invoice.
        String imagePath = "YOUR_DIRECTORY/invoice.png";
        ocrEngine.setImage(ImageStream.fromFile(imagePath));

        // Step 3: Define the region of interest (ROI) you want to recognize.
        // x = 120, y = 340, width = 500, height = 120 – tweak these values for your own layout.
        Rectangle regionOfInterest = new Rectangle(120, 340, 500, 120);
        ocrEngine.setRegionOfInterest(regionOfInterest);

        // Step 4: Perform OCR on the specified ROI and retrieve the text.
        // recognize() returns an OcrResult object; getText() extracts the plain string.
        String extractedText = ocrEngine.recognize().getText();

        // Step 5: Output the recognized text.
        System.out.println("ROI text: " + extractedText);
    }
}
```

### 各ステップが重要な理由

1. **OCR エンジンの作成** – エンジンがなければ画像処理のコンテキストがありません。オブジェクトは後で多言語サポートが必要な場合に言語パックを調整することも可能です。  
2. **画像の読み込み** – `ImageStream.fromFile` はファイル形式を抽象化し、エンジンがバイト列を正しく読み取れるようにします。これを省略すると `NullPointerException` が発生します。  
3. **ROI の設定** – ページ全体を処理すると無駄が大きくなります。矩形を請求書の合計金額エリアに絞ることで認識速度が向上し、ノイズも減ります。  
4. **`recognize()` の呼び出し** – ここで魔法が起きます。メソッドは ROI 上で OCR アルゴリズムを実行し、結果オブジェクトを生成します。  
5. **出力の表示** – 実際のプロジェクトではデータベースに保存することが多いですが、デモとしては `System.out.println` が最適です。

## Load Image for OCR

パスは絶対でも相対でも構いませんが、Java プロセスがファイルを読み取れることを確認してください。Windows ではバックスラッシュをエスケープする必要があります（`C:\\images\\invoice.png`）またはスラッシュ表記（`C:/images/invoice.png`）でも構いません。

**プロチップ:** 多数の請求書をループ処理する場合は、同じ `OcrEngine` インスタンスを再利用すると内部リソースがキャッシュされ、スループットが向上します。

## Define Region of Interest (ROI)

適切な矩形を決めるには試行錯誤が必要です。画像を GIMP や Paint.NET などのエディタで開き、対象領域上にカーソルを合わせるとステータスバーに X/Y 座標が表示されます。

エッジケース: 請求書のレイアウトが可変の場合、まず画像全体をざっくりスキャンし、正規表現で “Total:” などのキーワードを検出してから ROI を動的に調整する方法があります。

## Perform OCR and Get Text

`recognize()` 呼び出しは同期的に動作し、エンジンが処理を完了するまでスレッドがブロックされます。大量バッチを処理する場合はスレッドプールを使って並列処理すると良いでしょう。ただし、各スレッドは独自の `OcrEngine` インスタンスを持つ必要があり、エンジンはスレッドセーフではありません。

## Run and Verify Output

コンパイルして実行:

```bash
javac -cp "path/to/aspose-ocr.jar" RoiOcrExample.java
java -cp ".:path/to/aspose-ocr.jar" RoiOcrExample
```

以下のような出力が得られるはずです:

```
ROI text: $1,254.00
```

出力が文字化けしている場合は、ROI の座標を再確認し、画像品質（300 dpi 以上がベスト）を確保してください。

### よくある落とし穴と対処法

| 症状 | 考えられる原因 | 対策 |
|------|----------------|------|
| 空文字列 | ROI が画像範囲外 | 矩形の値を画像サイズと照らし合わせて確認 |
| 誤認識された単語 | 解像度が低い | 高解像度の画像を使用するか、二値化などの前処理を適用 |
| `java.lang.NoClassDefFoundError` | クラスパスに Aspose JAR が無い | `aspose-ocr.jar` を `-cp` に追加するか、Maven/Gradle で依存管理 |

## Conclusion

これで、Java で **extract text from image** を実現する簡潔な **java ocr example** が完成しました。画像を正しく読み込み、焦点を絞った ROI を定義し、`recognize()` を呼び出すだけで、請求書ファイルから確実に **extract text from invoice** でき、下流システムへデータを流し込むことができます。

次は何をしますか？ ROI を日付やベンダー名など別フィールドに変更したり、言語パックを導入して多言語請求書に対応したり、OCR 処理を Spring Boot のマイクロサービスに組み込んでみてください。同様のパターンはレシート、パスポート、その他テキスト抽出が必要なドキュメントでも有効です。

このソリューションのスケーリングやノイズが多いスキャンの扱いについて質問があれば、下のコメント欄にどうぞ。ハッピーコーディング！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}