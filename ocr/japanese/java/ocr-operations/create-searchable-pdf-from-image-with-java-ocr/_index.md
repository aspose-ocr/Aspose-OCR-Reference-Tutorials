---
category: general
date: 2026-05-06
description: Aspose OCR を使用して Java で画像から検索可能な PDF を作成します。画像を PDF に変換し、スペル補正を有効にし、OCR
  GPU を利用して高速な結果を得る方法を学びましょう。
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- enable spell correction
- use ocr gpu
- process image ocr
language: ja
og_description: JavaでAspose OCRを使用して画像から検索可能なPDFを作成します。このガイドでは、画像をPDFに変換し、スペル補正を有効にし、OCR
  GPUを使用する方法を示します。
og_title: Java OCRで画像から検索可能なPDFを作成
tags:
- OCR
- Java
- PDF
title: Java OCRで画像から検索可能なPDFを作成
url: /ja/java/ocr-operations/create-searchable-pdf-from-image-with-java-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java OCRで画像から検索可能なPDFを作成する

スキャンした画像から **検索可能な PDF** を作成したいと思ったことはありませんか？でも、どこから始めればいいか分からない…という方は多いです。ほとんどの開発者が画像ベースの PDF に初めて取り組むときにこの壁にぶつかります。幸い、Aspose OCR for Java を使えば **画像を PDF に変換** でき、テキストを選択可能なコンテンツに変換し、さらにスペル補正を加えて仕上げることができます。

このチュートリアルでは、利用可能な場合に **OCR GPU を使用** する方法、**画像 OCR を効率的に処理** する方法、そして下流の検索のためにスペル補正を有効にする重要性を示す、完全に実行可能なサンプルを順に解説します。最後まで読むと、ユーザーに配布したりコンプライアンスのためにアーカイブしたりできる、ワンクリックで検索可能な PDF を生成する方法が手に入ります。

> **プロのコツ:** GPU が搭載されていないマシンで実行する場合、コードは自動的に CPU にフォールバックするので、コードを書き直す必要はありません。

## 必要なもの

- **Java 8+** (コードは JDK 8 以降でコンパイル可能)
- **Aspose OCR for Java** ライブラリ (Aspose サイトから最新の JAR をダウンロード)
- **入力画像** (JPEG、PNG、TIFF など) – 検索可能な PDF に変換したいもの
- (Optional) **GPU** (CUDA 対応) – 可能な限り高速な認識を行いたい場合

余計なフレームワークや Maven/Gradle の設定は不要です。クラスパスに単一の JAR を置くだけで準備完了です。

## ステップ 1: OCR エンジンの初期化 – プロセスの中心  

まず `OcrEngine` インスタンスを作成し、ソースファイルを指定します。このオブジェクトが画像を読み込み、ニューラルネットワークを実行し、テキストを返す主役です。

```java
import com.aspose.ocr.*;

public class QuickStart {
    public static void main(String[] args) throws Exception {
        // Initialise the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Load the image you want to convert
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/input.jpg"));
```

*Why this matters:* エンジンを一度だけ初期化して再利用することで、ネイティブライブラリのロードオーバーヘッドを回避できます。これは、数十ファイルをバッチ処理する際に積み重なる小さなパフォーマンス向上です。

## ステップ 2: 処理デバイスの選択 – 可能なら OCR GPU を使用  

作業ステーションに対応 GPU がある場合、Aspose に重い処理を GPU で実行させることができます。そうでなければエンジンは自動的に CPU に切り替わります。

```java
        // Prefer GPU; fall back to CPU if no compatible device is found
        ocrEngine.getDevice().setDeviceType(OcrDeviceType.GPU);
```

*What’s the benefit?* GPU 加速により、特に高解像度スキャンの場合、ページごとに数秒の短縮が期待できます。フォールバックにより同じコードがどこでも動作するため、デフォルト設定として **use OCR GPU** を推奨しています。

## ステップ 3: スキャンを高速化 – すべての CPU コアを活用  

GPU が使用中でも、周辺の前処理は並列化できます。スレッド数を利用可能なプロセッサ数に設定することで、エンジンは複数のチャンクを同時に処理できます。

```java
        // Use all logical cores for preprocessing and language detection
        ocrEngine.setThreadCount(Runtime.getRuntime().availableProcessors());
```

*Note:* 4 コアのノートパソコンでは 4 スレッドが立ち上がり、16 コアのワークステーションではフルに恩恵を受けられます。ただし、スレッド数が増えるとメモリ使用量も増えることに注意してください。

## ステップ 4: 画像のクリーンアップ – 前処理フィルタ  

ぼやけた画像やノイズの多いスキャンはゴミテキストを生成します。組み込みフィルタを数個追加するだけで精度が大幅に向上します。

```java
        // Deskew the image so text lines are horizontal
        ocrEngine.getPreprocessing().add(new DeskewFilter());

        // Remove speckles and background noise
        ocrEngine.getPreprocessing().add(new NoiseRemovalFilter());
```

*Why these filters?* `DeskewFilter` は、スキャナに斜めに投入された文書でよく起こる回転を補正します。`NoiseRemovalFilter` は、文字と誤認識されやすい不要なピクセルを除去します。OCR エンジンにきれいな紙を渡すイメージです。

## ステップ 5: スマート機能の有効化 – スペル補正と自動言語検出をオンにする  

多言語文書を扱う場合や、誤字を減らしたい場合は、組み込みのスペルチェッカーを有効にし、エンジンに言語を自動判別させます。

```java
        // Activate spell correction to fix common OCR mistakes
        ocrEngine.getSettings().setEnableSpellCorrection(true);

        // Let the engine automatically detect the language of the input
        ocrEngine.getSettings().setAutoDetectLanguage(true);
```

*When is this useful?* 例えば、スキャンに英語とスペイン語のセクションが混在している場合です。自動検出機能は辞書をリアルタイムで切り替え、スペル補正は “0” を “O” といった誤認識文字を修正します。このステップは、正しい検索結果を返す **検索可能な PDF** を作成するために不可欠です。

## ステップ 6: 結果の保存 – 画像を PDF に変換して検索可能にする  

最後に、エンジンに元画像の背後に不可視のテキストレイヤーを持つ PDF を出力させます。これが従来の **画像を PDF に変換** ワークフローですが、PDF が検索可能になります。

```java
        // Generate a searchable PDF – the text layer sits behind the original image
        ocrEngine.save("YOUR_DIRECTORY/output-searchable.pdf", OcrSaveFormat.PDF_SEARCHABLE);

        System.out.println("Searchable PDF generated successfully.");
    }
}
```

出力ファイル (`output-searchable.pdf`) は任意の PDF ビューアで開くことができ、テキストを選択・コピー・検索できるようになります。追加ツールは不要です。

## 完全動作サンプル – コピーして実行  

以下はコンパイル可能な完全なプログラムです。`YOUR_DIRECTORY` を `input.jpg` が格納されているフォルダーに置き換えてください。

```java
import com.aspose.ocr.*;

public class QuickStart {
    public static void main(String[] args) throws Exception {
        // Step 1: Create the OCR engine and load the source image
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/input.jpg"));

        // Step 2: Select the processing device (GPU if available, otherwise CPU)
        ocrEngine.getDevice().setDeviceType(OcrDeviceType.GPU);

        // Step 3: Use all available CPU cores to speed up recognition
        ocrEngine.setThreadCount(Runtime.getRuntime().availableProcessors());

        // Step 4: Add preprocessing filters to improve image quality
        ocrEngine.getPreprocessing().add(new DeskewFilter());
        ocrEngine.getPreprocessing().add(new NoiseRemovalFilter());

        // Step 5: Enable spell correction and automatic language detection
        ocrEngine.getSettings().setEnableSpellCorrection(true);
        ocrEngine.getSettings().setAutoDetectLanguage(true);

        // Step 6: Perform OCR and save the result as a searchable PDF
        ocrEngine.save("YOUR_DIRECTORY/output-searchable.pdf", OcrSaveFormat.PDF_SEARCHABLE);

        System.out.println("Searchable PDF generated successfully.");
    }
}
```

**期待される出力:** プログラムを実行するとコンソールに *“Searchable PDF generated successfully.”* と表示されます。Adobe Reader で `output-searchable.pdf` を開き、元画像の単語を検索ボックスに入力すれば、即座に該当箇所へジャンプします。

## よくある質問とエッジケース  

- **GPU が検出されない場合は？**  
  `setDeviceType(OcrDeviceType.GPU)` 呼び出しは例外を投げず、エンジンにまず GPU を試すよう指示するだけです。失敗した場合はエンジンが静かに CPU にフォールバックします。

- **1 回の実行で複数画像を処理できるか？**  
  はい。コードをループで囲み、イテレーションごとにファイル名を変更し、同じ `OcrEngine` インスタンスを再利用すればメモリ使用量を抑えられます。

- **PDF が巨大になる—どうやって縮小するか？**  
  OCR 後に Aspose の PDF 最適化 API を使用するか、エンジンに渡す前に元画像をダウンサンプルします（例: `ImageStream.fromFile(...).setResolution(150)` で 150 DPI に設定）。

- **法的コンプライアンスのために元画像の解像度を保持したい。**  
  `PDF_SEARCHABLE` フォーマットは元のビットマップを完全に保持し、不可視のテキストレイヤーが上に追加されるだけで視覚品質は変わりません。

## ビジュアルサマリー  

![検索可能な PDF 作成例](placeholder-image.png "検索可能な PDF 作成例")

*Alt text:* *検索可能な PDF 作成例 – Java OCR エンジンがスキャンした JPG を検索可能な PDF に変換する例。*

## 結論  

これで、Aspose OCR for Java を使用して任意の画像を **検索可能な PDF** に変換する **完全なエンドツーエンドソリューション** が手に入りました。**画像を PDF に変換**し、**スペル補正を有効化**、そして可能な限り **OCR GPU を使用** することで、クロスプラットフォームで高速かつ正確な検索可能な結果が得られます。

次は何をすべきか？以下を試してみてください：

- **異なる出力フォーマット** (`PDF`, `DOCX`, `HTML`) – テキストレイヤーの挙動を確認
- **カスタム辞書** – ドメイン固有の用語を処理する場合
- **バッチ処理** – 数千枚のスキャンを自動で処理

スレッド数を調整したり、フィルタを入れ替えたり、独自の前処理パイプラインを組み込んでも構いません。基本的な流れは変わりません: load → preprocess → configure → OCR → save.

コーディングを楽しんで、あなたの PDF が常に検索可能でありますように！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}