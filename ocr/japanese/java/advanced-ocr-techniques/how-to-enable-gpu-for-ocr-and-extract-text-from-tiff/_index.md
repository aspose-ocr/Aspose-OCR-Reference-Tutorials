---
category: general
date: 2026-02-14
description: Aspose OCR JavaでGPUを有効にして画像から高速にテキストを抽出する方法。TIFFをテキストに変換し、GPUデバイスIDを設定し、TIFFファイルからテキストを読み取る方法を学びます。
draft: false
keywords:
- how to enable gpu
- extract text from image
- convert tiff to text
- set gpu device id
- read text from tiff
language: ja
og_description: Aspose OCR JavaでGPUを有効にして画像からテキストを高速に抽出する方法。このガイドに従ってTIFFをテキストに変換し、GPUデバイスIDを設定し、TIFFからテキストを読み取ります。
og_title: GPUをOCRで有効にする方法 – TIFFからテキストを抽出
tags:
- OCR
- Java
- GPU acceleration
title: GPUをOCRで有効にし、TIFFからテキストを抽出する方法
url: /ja/java/advanced-ocr-techniques/how-to-enable-gpu-for-ocr-and-extract-text-from-tiff/
---

translate code block placeholders.

Also there are shortcodes at top and bottom. Keep them.

Let's produce final content.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# GPU を有効にして TIFF からテキストを抽出する方法

大容量の TIFF ファイルで OCR を実行するときに **GPU を有効にする方法** を知りたくありませんか？ あなた一人だけではありません。開発者は常に速度向上を追求しており、特にソース画像が数メガバイトの TIFF の場合はなおさらです。朗報です！ Aspose OCR for Java を使えば、スイッチを入れ、適切な GPU を指定するだけで、エンジンが画像を高速に処理します。

このチュートリアルでは、TIFF の読み込み、GPU アクセラレーションの有効化、必要に応じて特定の GPU デバイスを選択、OCR の実行、そして最終的に **画像からテキストを抽出** するまでの全工程を解説します。最後まで読めば、数行のコードで **TIFF をテキストに変換** でき、さらに **TIFF ファイルからテキストを読み取る** 方法もマスターできます。

## 必要な環境

- Java 17 以上（コードは Java 8+ でも動作します）
- Aspose OCR for Java 23.10（執筆時点での最新バージョン）
- CUDA 対応 GPU と最新ドライバー
- サンプルのマルチページ TIFF（ここでは `sample_large.tif` と呼びます）

Maven の設定がなくても大丈夫です。JAR をクラスパスに入れるだけで使用できます。

![GPU を有効にするチュートリアル](gpu-ocr.png)

*画像の代替テキスト: Java で OCR のために GPU を有効にする方法*

## 手順 1: OCR 用に TIFF 画像を読み込む

まずは `OcrEngine` インスタンスとソース画像が必要です。Aspose OCR は事実上すべてのラスタ形式を読み取れますが、TIFF はスキャン文書でよく使われます。

```java
import com.aspose.ocr.*;

public class GpuOcrDemo {
    public static void main(String[] args) throws Exception {
        // Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Load the TIFF file – this is where we "read text from TIFF"
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample_large.tif"));
```

> **重要ポイント:** `setImage` 呼び出しはファイルを `ImageStream` でラップし、エンジンがマルチページ TIFF を手動で分割することなく処理できるようにします。ファイルが見つからない場合は明確な `FileNotFoundException` がスローされるので、パスを再確認してください。

## 手順 2: GPU アクセラレーションを有効にする

ここで魔法が起きます。GPU の有効化は単なるブールフラグですが、処理時間を数秒、場合によっては数分短縮できます。

```java
        // Enable GPU acceleration (requires a supported driver)
        ocrEngine.getEngineOptions().setUseGpu(true);
```

> **プロのコツ:** マシンに GPU が複数ある場合、デフォルトは通常最初のデバイス（device 0）です。Aspose に自動で最適デバイスを選ばせることもできますが、明示的に指定するとマルチ GPU ワークステーションでの予期せぬ挙動を防げます。

## 手順 3: GPU デバイス ID を設定（任意）

特定の GPU を使用したい場合があります――たとえば、2 番目のカードが AI 用に専用化されている場合です。そのときに `setGpuDeviceId` が活躍します。

```java
        // Optional: select the GPU device (0 = first device, 1 = second, etc.)
        ocrEngine.getEngineOptions().setGpuDeviceId(0);
```

> **エッジケース:** 無効な ID を渡すとエンジンは `IllegalArgumentException` をスローします。`System.out.println(ocrEngine.getEngineOptions().getAvailableGpuDevices())` で利用可能な ID を一覧表示できます。

## 手順 4: 画像を処理し **画像からテキストを抽出** する

エンジンの設定が完了したら、いよいよ OCR を実行します。結果オブジェクトは生の文字列と、必要に応じて信頼度スコアを提供します。

```java
        // Perform OCR – this is where we "convert TIFF to text"
        OcrResult ocrResult = ocrEngine.process();

        // Output the recognized text
        System.out.println("Recognized text:");
        System.out.println(ocrResult.getText());
    }
}
```

### 期待される出力

TIFF に “Hello, World!” というフレーズが含まれている場合、次のような出力が得られるはずです。

```
Recognized text:
Hello, World!
```

エンジンは改行、句読点、基本的なレイアウト検出も自動で処理します。ページ単位でテキストを取得したい場合は `ocrResult.getPages()` を活用してください。

## 手順 5: 出力を確認し、一般的な問題に対処する

### GPU が使用されない原因は？

- **ドライバの不一致:** GPU ドライバは Aspose が推奨するバージョン以上である必要があります（リリースノートを確認）。
- **メモリ不足:** 非常に大きな画像は GPU の VRAM を超えることがあります。その場合、エンジンは自動的に CPU にフォールバックし、コンソールに警告が表示されます。
- **非対応ハードウェア:** 統合型グラフィックスは必要な計算能力を満たさないことが多いです。

### プログラム上で CPU にフォールバックする方法

```java
if (!ocrEngine.getEngineOptions().isGpuAvailable()) {
    System.out.println("GPU not available – switching to CPU.");
    ocrEngine.getEngineOptions().setUseGpu(false);
}
```

### ループで TIFF からテキストを読み取る

フォルダ内の TIFF をまとめて処理したい場合は次のようにイテレートできます。

```java
File folder = new File("YOUR_DIRECTORY");
for (File file : folder.listFiles((dir, name) -> name.toLowerCase().endsWith(".tif"))) {
    ocrEngine.setImage(ImageStream.fromFile(file.getAbsolutePath()));
    OcrResult result = ocrEngine.process();
    System.out.println("File: " + file.getName());
    System.out.println(result.getText());
}
```

このスニペットは、**TIFF ファイルからテキストを読み取る** 処理をバルクで実行しつつ、GPU アクセラレーションの恩恵を受ける方法を示しています。

## よくある質問 (FAQ)

**Q: Linux でも動作しますか？**  
A: はい。Aspose OCR はクロスプラットフォームです。CUDA ツールキットとドライバがインストールされていれば問題ありません。

**Q: GPU がない場合はどうすれば？**  
A: `setUseGpu(false)` を呼ぶか、呼び出し自体を省略してください。エンジンはデフォルトで CPU を使用します。

**Q: 他のフォーマットからもテキスト抽出できますか？**  
A: 可能です。同じ `setImage` メソッドで JPEG、PNG、BMP、さらには PDF ストリームも受け取れます。

**Q: 低解像度の TIFF では精度はどうですか？**  
A: 300 dpi 未満では精度が低下します。エンジンに渡す前に二値化やデスキューなどの前処理を検討してください。

## 結論

これで **Aspose OCR Java で GPU を有効にする方法**、**GPU デバイス ID の設定方法**、そして最も重要な **画像からテキストを抽出する方法**、特に **TIFF をテキストに変換** し **TIFF からテキストを読む** 方法がマスターできました。フラグ一つで、デバイスを指定すれば、OCR ロジックを書き換えることなく大幅なパフォーマンス向上が得られます。

次のステップに挑戦してみませんか？

- **数百枚の TIFF を並列スレッドでバッチ処理** する
- **カスタム言語パック** を導入して、特殊文書の認識精度を向上させる
- **正規表現で抽出文字列を後処理** し、フォーマットを整える

質問や問題があればコメントで教えてください。ハッピーコーディング！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}