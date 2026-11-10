---
category: general
date: 2026-01-12
description: JavaでAspose OCRを使用して画像からテキストを抽出します。Java OCRの例で請求書画像からテキストを抽出する方法を学び、OCRテキストの出力を取得します。
draft: false
keywords:
- extract text from image
- how to extract text
- java ocr example
- process invoice image
- output ocr text
language: ja
og_description: JavaでAspose OCRを使用して画像からテキストを抽出します。このガイドでは、請求書画像からテキストを抽出する方法を示し、Java
  OCRの例を含み、OCRテキストを出力します。
og_title: Javaで画像からテキストを抽出 – 完全なOCR例
tags:
- OCR
- Java
- Aspose
title: Javaで画像からテキストを抽出 – 完全なOCR例
url: /ja/java/ocr-basics/extract-text-from-image-in-java-complete-ocr-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Javaで画像からテキストを抽出 – 完全OCR例

画像ファイルから **テキストを抽出** する方法で、髪の毛を抜かずに済む方法を考えたことはありませんか？たとえば、スキャンした請求書が山積みで、数字をすぐに取り出す必要がある場合です。私の経験では、専用のOCRライブラリに任せるのが最も簡単です。このチュートリアルでは、Aspose OCR for Java を使用して典型的な請求書画像から *テキストを抽出* する方法を示し、 **java ocr example** として OCR テキストを下流システムにパイプできるサンプルも紹介します。

プロジェクトのセットアップ、ヘッダーと合計金額にフォーカスした関心領域（ROI）の定義、そして抽出したテキストの出力まで、必要な手順をすべて解説します。最後まで読めば、**請求書画像** ファイルを自動で処理し、クリーンで検索可能なテキストを取得できるようになります。

> **得られるもの:** すぐに実行できる Java プログラム、各ステップの明確な説明、実務での請求書処理に役立つ実践的なヒント。

---

## 前提条件

作業を始める前に、以下が揃っていることを確認してください。

- Java Development Kit (JDK) 8 以上がインストールされていること。
- 依存関係管理のための Maven または Gradle（例は Maven）。
- Aspose OCR for Java のライセンス（無料トライアルでテスト可能）。
- 既知のディレクトリに配置した請求書画像（`invoice.png`）。

これらに見覚えがなくても心配はいりません。ほとんどはダウンロードだけで手に入りますし、コミュニティエディションでもコードはコンパイルできます。

---

## 手順 1: Maven プロジェクトのセットアップ

まず、Maven プロジェクトを新規作成（または既存プロジェクトに追加）します。`pom.xml` に Aspose OCR の依存関係を追加してください。

```xml
<!-- pom.xml -->
<dependencies>
    <dependency>
        <groupId>com.aspose</groupId>
        <artifactId>aspose-ocr</artifactId>
        <version>23.9</version> <!-- Use the latest version available -->
    </dependency>
</dependencies>
```

> **プロのコツ:** バージョン番号は常に最新に保ちましょう。新しいリリースは、請求書に見られる特殊フォントの認識精度が向上していることが多いです。

ファイルを保存したら、`mvn clean install` を実行してローカルリポジトリにライブラリを取得します。

---

## 手順 2: 請求書画像の読み込み

ライブラリの準備ができたら、簡単な Java クラスを書きます。最初に行うのは `OcrEngine` インスタンスの作成と、読み込む画像へのパス指定です。

```java
import com.aspose.ocr.*;

public class RoiExample {
    public static void main(String[] args) throws Exception {
        // Step 2: Load the source image
        OcrEngine engine = new OcrEngine();
        engine.setImage("YOUR_DIRECTORY/invoice.png"); // <-- replace with your path
```

なぜ画像の読み込み **前に** エンジンを作成するのか？エンジンは言語、DPI、ROI などの設定を保持します。画像を先に指定しておくことで、これらの設定が対象ファイルに正しく適用されます。

---

## 手順 3: 関心領域 (ROI) の定義

請求書にはテーブル、ロゴ、細字などノイズが多く含まれます。OCR をヘッダーと合計金額のみに絞ることで、速度と精度が大幅に向上します。Aspose では矩形で領域を指定できます。

```java
        // Step 3: Define the regions of interest (header and total amount)
        OcrRegion region = OcrRegion.builder()
                .addRectangle(0, 0, 800, 150)      // header area
                .addRectangle(0, 1200, 800, 200)   // total amount area
                .build();

        // Apply ROI to the engine
        engine.setRegion(region);
```

座標はピクセル単位（`x`, `y`, `width`, `height`）です。請求書のサイズがバラバラの場合は、画像サイズを取得して動的に計算すると良いでしょう。バッチ処理向けの **process invoice image** ソリューションを作る際の拡張ポイントです。

---

## 手順 4: 指定領域で OCR を実行

ROI を設定したら、OCR エンジンは重要な部分にだけ注目します。`recognize()` メソッドは抽出されたテキストを含む `OcrResult` を返します。

```java
        // Step 4: Run OCR on the specified regions
        OcrResult result = engine.recognize();
```

内部では Aspose が二値化、ノイズ除去、文字分割といった前処理を自動で行います。これらを手動で呼び出す必要はなく、`recognize()` に任せるだけです。

---

## 手順 5: 抽出テキストの出力

最後に、テキストをコンソールに出力します。実際のアプリケーションではデータベースに保存したり、下流の分析パイプラインに渡したり、検索可能な PDF を生成したりすることも考えられます。

```java
        // Step 5: Output the extracted text
        System.out.println("ROI text:");
        System.out.println(result.getText());
    }
}
```

プログラムを実行すると、次のような出力が得られるはずです。

```
ROI text:
Acme Corp.
Invoice #12345
Date: 2025-12-31
Total Amount: $1,250.00
```

出力が文字化けしている場合は、矩形座標を再確認するか、画像解像度を上げてみてください。OCR エンジンは鮮明で高 DPI のスキャンを好みます。

---

## 完全動作サンプル

以下は `src/main/java/RoiExample.java` にそのまま貼り付けて使用できる、自己完結型の Java ファイルです。外部スニペットは不要です。

```java
import com.aspose.ocr.*;
import com.aspose.ocr.region.*;

public class RoiExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create the OCR engine and load the source image
        OcrEngine engine = new OcrEngine();
        engine.setImage("YOUR_DIRECTORY/invoice.png");

        // Step 2: Define the regions of interest (header and total amount)
        OcrRegion region = OcrRegion.builder()
                .addRectangle(0, 0, 800, 150)      // header area
                .addRectangle(0, 1200, 800, 200)   // total amount area
                .build();

        // Step 3: Apply the ROI configuration to the engine
        engine.setRegion(region);

        // Step 4: Run OCR on the specified regions
        OcrResult result = engine.recognize();

        // Step 5: Output the extracted text
        System.out.println("ROI text:");
        System.out.println(result.getText());
    }
}
```

> **注意:** `YOUR_DIRECTORY` を請求書画像への絶対パスに置き換えてください。相対パスを使用する場合は、`java` コマンドを実行する作業ディレクトリが画像の場所と一致していることを確認してください。

---

## よくある質問とエッジケース

### 請求書のサイズが変わったらどうする？

ROI を動的に計算できます。

```java
int imgWidth = engine.getImage().getWidth();
int imgHeight = engine.getImage().getHeight();

int headerHeight = imgHeight / 10;
int totalHeight = imgHeight / 8;

OcrRegion region = OcrRegion.builder()
        .addRectangle(0, 0, imgWidth, headerHeight)
        .addRectangle(0, imgHeight - totalHeight, imgWidth, totalHeight)
        .build();
```

### 複数言語に対応させるには？

Aspose OCR は言語パックをサポートしています。`recognize()` を呼び出す前に言語を設定してください。

```java
engine.setLanguage(OcrLanguage.Spanish); // or OcrLanguage.English, etc.
```

### OCR が空文字列を返す場合の対処法は？

主な原因は次の通りです。

- 画像解像度が低い（300 DPI 未満）。解像度を上げるか、より高品質なスキャンを用意。
- 背景が暗すぎる／明るすぎる。OCR 前に簡易コントラスト強調フィルタを適用。
- ROI 座標が誤ってテキスト領域を外している。

---

## 本番環境向け OCR のヒント

1. **バッチ処理:** ディレクトリ内の請求書ファイルをループで処理し、結果をログに残して監査可能にする。
2. **エラーハンドリング:** `OcrException` を捕捉し、破損画像はジョブ全体を止めずにスキップ。
3. **パフォーマンス:** 複数画像で同一の `OcrEngine` インスタンスを再利用。ファイルごとに新規作成すると余計なオーバーヘッドが発生。
4. **検証:** 抽出後に合計金額の正規表現チェック（`\$\d{1,3}(,\d{3})*(\.\d{2})?`）を行い、数値が妥当か確認。

これらを実装すれば、シンプルな **java ocr example** が、毎晩請求書画像を処理する堅牢でスケーラブルなソリューションへと進化します。

---

## 結論

本稿では、Aspose OCR を使って Java で **画像からテキストを抽出** する方法を、実務的な請求書処理シナリオを通じて解説しました。関心領域を定義し、OCR エンジンを実行し、**出力 OCR テキスト** を表示する一連の流れを習得したことで、データ自動取得パイプラインの土台ができました。

次のステップは？ ROI を拡張して明細テーブルも対象にしたり、言語設定を変えてみたり、抽出文字列を PDF 生成ライブラリに渡して検索可能文書を作成したりしてみてください。OCR と最新の Java ツールを組み合わせれば、可能性は無限に広がります。

**他の文書タイプからテキストを抽出** したい、または特殊レイアウト向けに ROI を調整したいといった質問があれば、ぜひコメントで教えてください。ハッピーコーディング！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}