---
category: general
date: 2026-06-22
description: Aspose OCR を使用して Java で検索可能な PDF を作成します。スキャンした PDF の変換方法、混合言語 OCR の処理方法、精度向上のコツを学びましょう。
draft: false
keywords:
- create searchable pdf
- convert scanned pdf
- how to ocr document
- mixed language ocr
- aspose ocr java
language: ja
og_description: Aspose OCR を使用して Java で検索可能な PDF を作成します。このチュートリアルでは、ドキュメントを OCR する方法、混在言語テキストを処理する方法、検索可能な
  PDF を出力する方法を示します。
og_title: スキャン画像から検索可能なPDFを作成 – Java OCRガイド
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Create searchable PDF in Java with Aspose OCR. Learn how to convert
    scanned PDF, handle mixed language OCR and boost accuracy.
  headline: Create Searchable PDF from Scanned Images – Java OCR Guide
  type: TechArticle
- description: Create searchable PDF in Java with Aspose OCR. Learn how to convert
    scanned PDF, handle mixed language OCR and boost accuracy.
  name: Create Searchable PDF from Scanned Images – Java OCR Guide
  steps:
  - name: Expected Output
    text: 'When you open `processed.pdf` in Adobe Reader (or any PDF viewer), you
      should be able to:'
  - name: 1. What if my document contains more than two languages?
    text: '`config.setLanguage` accepts a var‑args list, so you can pass as many `OcrLanguage`
      constants as you need:'
  - name: 2. Can I run this on a headless server without a GPU?
    text: Absolutely. Set `config.setUseGpu(false)` or simply omit the call. The engine
      will fall back to multi‑core CPU processing, which is still fast thanks to the
      thread pool we configured.
  - name: 3. How do I handle huge PDFs (hundreds of pages)?
    text: Aspose OCR streams pages one‑by‑one, so memory usage stays modest. However,
      you might want to split the PDF into smaller chunks using Aspose PDF’s `split`
      method, process each chunk, then merge the results back together.
  - name: 4. Is there a way to keep the original PDF’s metadata (author, creation
      date)?
    text: 'Yes. After you obtain `searchablePdf`, you can copy metadata from the original
      PDF:'
  type: HowTo
tags:
- OCR
- Java
- PDF
title: スキャン画像から検索可能なPDFを作成 – Java OCRガイド
url: /ja/java/advanced-ocr-techniques/create-searchable-pdf-from-scanned-images-java-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# スキャン画像から検索可能なPDFを作成 – Java OCR ガイド

スキャンしたページの山から**searchable PDF**を作成する方法を、サードパーティのサービスに高額な費用をかけずに知りたくありませんか？同じ壁にぶつかる開発者は多いです。多くの開発者は**scanned PDF**ファイルをユーザーが実際に検索できる形に変換する必要があるときに同じ問題に直面します。

このガイドでは、**Aspose OCR for Java** を使用して **OCR ドキュメント** レベルのタスクを実行し、**mixed language OCR** に対応し、最終的に洗練された検索可能な PDF を出力する、完全に実行可能なサンプルを順を追って解説します。最後まで読めば、Maven または Gradle プロジェクトに組み込んですぐにドキュメント処理を開始できる、自己完結型のプログラムが手に入ります。

## 前提条件 – 必要なもの

コードに取り掛かる前に、以下を用意してください。

- Java 17（または最近の JDK）をインストールし、PATH に設定済み  
- お好みの IDE またはエディタ（IntelliJ IDEA、Eclipse、VS Code など）  
- Aspose.OCR for Java ライブラリ – 最新の JAR は [Aspose Maven リポジトリ](https://repo.aspose.com/repo/com/aspose/aspose-ocr/) から取得できます  
- 検索可能にしたいマルチページのスキャン PDF  
- （オプション）`setUseGpu(true)` を利用して高速化したい場合は GPU 対応マシン

これらが揃っていれば、以下のコードをコピー＆ペーストして **Run** するだけで、依存関係を探す手間が省けます。

## Step 1: プロジェクトをセットアップし Aspose OCR をインポート

まず、Maven モジュール（または Gradle プロジェクト）を作成し、Aspose OCR の依存関係を追加します。

```xml
<!-- pom.xml snippet -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- replace with the latest version -->
</dependency>
```

Gradle を使用する場合は、同等の行は次のとおりです。

```gradle
implementation 'com.aspose:aspose-ocr:23.10'
```

ビルドが同期したら、必要なクラスをインポートできるようになります。

## Step 2: OCR エンジンを初期化

エンジンの作成はシンプルですが、早めに行う理由を理解しておくと良いでしょう。`OcrEngine` オブジェクトは設定、スレッド、GPU 設定を保持し、以降のすべての操作に影響します。

```java
import com.aspose.ocr.*;

public class AdvancedOcr {
    public static void main(String[] args) throws Exception {
        // Initialize the OCR engine – this is the heart of the create searchable pdf process
        OcrEngine ocrEngine = new OcrEngine();
```

> **プロのコツ:** エンジンを一度だけインスタンス化し、複数ファイルで再利用すると、特にバッチ処理時のオーバーヘッドが削減されます。

## Step 3: スキャン PDF（または画像ストリーム）をロード

Aspose OCR は画像ストリームを扱うため、スキャン PDF を直接渡します。ライブラリは内部で各ページをラスタライズするので、PDF から検索可能な PDF への変換を一括で行えます。

```java
        // Load the source PDF – replace the path with your actual file location
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/multi_page_scanned.pdf"));
```

代わりに TIFF や JPEG のコレクションがある場合は、`ImageStream.fromFile` にそれらのファイルを指定すれば、パイプラインは同じままです。

## Step 4: Mixed Language 対応のため OCR 設定を微調整

ここが **mixed language OCR** の見せ場です。複数の `OcrLanguage` 列挙子を渡すことで、同一ページ内で英語とロシア語（または任意の組み合わせ）を同時に認識させます。

```java
        // Grab the mutable config object
        OcrConfig config = ocrEngine.getConfig();

        // Enable English + Russian detection – you can add more languages as needed
        config.setLanguage(OcrLanguage.ENGLISH, OcrLanguage.RUSSIAN);

        // Speed vs. accuracy trade‑off: use all available cores
        config.setThreadCount(Runtime.getRuntime().availableProcessors());

        // Turn on GPU acceleration if the runtime detects a compatible device
        config.setUseGpu(true);

        // Spell‑check improves accuracy for noisy scans
        config.setEnableSpellCorrection(true);

        // Tell Aspose we want a searchable PDF as the final output
        config.setOutputFormat(OcrOutputFormat.PDF_SEARCHABLE);
```

> **なぜ重要か:** 言語を指定しない場合、エンジンはデフォルトで英語のみとなり、キリル文字やその他のスクリプトを含む文書の認識率が大幅に低下します。

## Step 5: スキャンをクリーンアップする前処理フィルタを追加

スキャン PDF は歪みやノイズ、コントラスト低下が起こりやすいです。`DeskewFilter` と `DenoiseFilter` を追加すると、OCR エンジンが文字をより鮮明に認識できます。

```java
        // Set up image preprocessing
        ImagePreprocessOptions preprocess = new ImagePreprocessOptions();
        preprocess.addFilter(new DeskewFilter());   // Straighten tilted pages
        preprocess.addFilter(new DenoiseFilter()); // Reduce background noise
        ocrEngine.setPreprocessOptions(preprocess);
```

ソースが特に汚れている場合は、`ContrastFilter` や `BinarizationFilter` などの追加フィルタもチェーンできます。

## Step 6: OCR を実行し検索可能な PDF を生成

いよいよ本番です。`recognizeToPdf()` 呼び出しが OCR パイプラインを実行し、前処理ステップを適用し、認識したテキストを PDF 内の不可視テキスト層に書き込みます。

```java
        // Perform OCR and retrieve a searchable PDF document object
        PdfDocument searchablePdf = ocrEngine.recognizeToPdf();
```

返される `PdfDocument` は完全な Aspose PDF オブジェクトなので、メタデータの編集、ブックマークの追加、他の PDF との結合など、保存前にさらに加工できます。

## Step 7: 結果を保存し検証

最後に、出力をディスクに永続化します。コンソールメッセージで処理が正常に完了したことをすぐに確認できます。

```java
        // Save the searchable PDF to the desired location
        searchablePdf.save("YOUR_DIRECTORY/processed.pdf");
        System.out.println("OCR completed – searchable PDF saved at YOUR_DIRECTORY/processed.pdf");
    }
}
```

### 期待される出力

`processed.pdf` を Adobe Reader（または任意の PDF ビューア）で開くと、次のことが可能です。

1. **テキスト選択** – 任意の単語をクリック＆ドラッグしてコピーできる  
2. **検索** – `Ctrl+F` を押して、元のスキャンに含まれるフレーズを入力できる  
3. **レイアウト保持** – 見た目は元のスキャンと全く同じで、不可視テキスト層だけが追加されている

文字化けやページ欠損が発生した場合は、言語設定を再確認し、元 PDF がパスワードで保護されていないか確認してください。

## よくある質問 & エッジケース

### 1. 文書に 2 つ以上の言語が含まれる場合は？

`config.setLanguage` は可変長引数を受け取るので、必要なだけ `OcrLanguage` 定数を渡せます。

```java
config.setLanguage(OcrLanguage.ENGLISH, OcrLanguage.RUSSIAN, OcrLanguage.CHINESE_SIMPLIFIED);
```

ただし、言語を増やすごとに処理時間がやや長くなることを覚えておいてください。

### 2. GPU が無いヘッドレスサーバーで実行できる？

もちろんです。`config.setUseGpu(false)` と設定するか、呼び出し自体を省略すれば、エンジンはマルチコア CPU にフォールバックします。スレッドプールのおかげで依然として高速です。

### 3. ページ数が数百に及ぶ巨大 PDF を扱うには？

Aspose OCR はページを 1 つずつストリーム処理するため、メモリ使用量は抑えられます。必要に応じて Aspose PDF の `split` メソッドで PDF を小分けにし、各チャンクを個別に処理して最後に結合すると良いでしょう。

### 4. 元 PDF のメタデータ（作者、作成日など）を保持できるか？

可能です。`searchablePdf` を取得した後、元 PDF からメタデータをコピーします。

```java
PdfDocument original = new PdfDocument("YOUR_DIRECTORY/multi_page_scanned.pdf");
searchablePdf.getInfo().setAuthor(original.getInfo().getAuthor());
// repeat for other metadata fields
```

## 本番環境向け OCR のプロ・ティップ

- **バッチ処理:** ディレクトリ内のファイルをループで回すフローに全体を包み、`OcrEngine` インスタンスは 1 つだけ使い回すことで初期化コストを削減  
- **エラーハンドリング:** `OcrException` を捕捉して失敗したファイルをログに残し、次のドキュメントへ継続  
- **パフォーマンス監視:** `recognizeToPdf()` 前後で `System.nanoTime()` を計測し、ファイルごとの処理時間を記録。これによりクラウドワーカーへのスケールアウト判断がしやすくなる  
- **セキュリティ:** 機密文書を扱う場合は、保存前に `searchablePdf.encrypt(...)` で出力 PDF を暗号化することを検討

## 結論

本稿では、**Aspose OCR for Java** を用いてスキャンソースから **searchable PDF** を作成するために必要なすべてを網羅しました。**scanned PDF** の変換、**mixed language OCR** の設定、前処理フィルタの微調整方法を示し、コードは簡潔で本番環境でもすぐに使える形に仕上げました。

ここからは、OCR で生成したサムネイルの追加、ドキュメント管理システムとの統合、抽出テキストを Elasticsearch などの検索インデックスに流し込むといった拡張が考えられます。デジタル化したい文書が増えるほど、可能性は広がります。

**Java での OCR ドキュメント** に関するさらなる質問や、PDF 操作の深掘りを希望する方はコメントを残してください。Happy coding!

## 次に学ぶべきこと

以下のチュートリアルは、本ガイドで示したテクニックを応用した関連トピックを扱っています。各リソースには、ステップバイステップの解説と完全動作サンプルが含まれているので、API の追加機能習得や代替実装の検討に役立ちます。

- [Recognize PDF Text – OCR Operations with Aspose.OCR for Java](/ocr/english/java/ocr-operations/)
- [OCR Recognizing PDF Documents in Aspose.OCR for Java](/ocr/english/java/ocr-operations/recognize-pdf/)
- [How to OCR PDF in .NET with Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}