---
category: general
date: 2026-02-17
description: JavaでAspose OCRを使用して画像をOCR用に前処理します。画像のコントラストを高め、コントラストレベルを設定し、数分で画像からテキストを認識する方法を学びましょう。
draft: false
keywords:
- preprocess image for ocr
- boost image contrast
- recognize text from image
- extract text using OCR
- set contrast level
language: ja
og_description: Aspose OCR Java を使用して OCR 用に画像を前処理します。このガイドでは、画像のコントラストを高め、コントラストレベルを設定し、画像からテキストを迅速に認識する方法を示します。
og_title: OCR用画像前処理 – コントラストを高めテキスト抽出するJavaチュートリアル
tags:
- Java
- OCR
- Image Processing
title: OCR用画像前処理 – コントラストを強化しテキストを抽出する完全Javaガイド
url: /ja/java/advanced-ocr-techniques/preprocess-image-for-ocr-complete-java-guide-to-boost-contra/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR 用画像前処理 – 完全 Java ガイド

OCR 用に画像を **前処理** したいと思ったことはありますか？ でもどの設定が実際に効果があるのか分からない…という方は多いでしょう。ほとんどの開発者は画像を OCR エンジンに投げて魔法が起きるのを期待しますが、結果は文字化けです。このチュートリアルでは、実用的なエンドツーエンドの例として、**画像のコントラストを上げ**、**コントラストレベルを調整**し、最終的に Aspose OCR for Java を使って **画像からテキストを認識** する方法を解説します。

このチュートリアルを終える頃には、ノイズの多いスキャンでも確実に **OCR でテキストを抽出** できる再利用可能なコードスニペットが手に入ります。隠されたテクニックはなく、明確な手順とその背後にある理由だけを示します。

## 必要なもの

- Java 17 以上（コードは最新の JDK でコンパイル可能）
- Aspose OCR for Java ライブラリ（公式 Aspose サイトからダウンロード）
- 有効な Aspose OCR ライセンスファイル（`Aspose.OCR.lic`）
- 読み取り対象の入力画像（`input.jpg`）
- お好みの IDE またはシンプルなコマンドライン環境

これらがすでに揃っているなら、すぐに始めましょう。

## ステップ 1: Aspose OCR ライセンスのロード（基本設定）

OCR エンジンが何かを行う前に、ライセンスがあることを認識させる必要があります。さもなければ、評価版の透かしが表示されます。

```java
import com.aspose.ocr.*;

public class PreprocessDemo {
    public static void main(String[] args) throws Exception {

        // Load the Aspose OCR license – this disables the evaluation limits
        License ocrLicense = new License();
        ocrLicense.setLicense("YOUR_DIRECTORY/Aspose.OCR.lic");
```

**なぜ重要か:** 正しいライセンスがないと、エンジンは評価モードで動作し、結果が切り詰められたり透かしが付いたりします。ライセンスを早めに設定することで、以降の前処理オプションがフル機能モードで適用されます。

## ステップ 2: OCR エンジンの初期化

`OcrEngine` インスタンスを作成すると、認識パイプラインと前処理パイプラインの両方にアクセスできます。

```java
        // Initialise the OCR engine
        OcrEngine ocrEngine = new OcrEngine();
```

**プロのコツ:** バッチで多数の画像を処理する場合は、エンジンをシングルトンとして保持すると、内部リソースがキャッシュされ、後続の呼び出しが高速化します。

## ステップ 3: 前処理の設定 – デスキュー、ノイズ除去、コントラスト強調

ここが **OCR 用画像前処理** を行う箇所です。調整する 3 つの項目は次の通りです：

1. **Deskew** – わずかな回転を補正します。
2. **Denoise** – 文字分割を妨げる斑点を除去します。
3. **Contrast enhancement** – 暗い文字を背景から際立たせます。

```java
        // Access preprocessing settings
        PreprocessingSettings preprocessing = ocrEngine.getPreprocessing();

        // Enable automatic deskew (helps with scanned pages that are a few degrees off)
        preprocessing.setDeskew(true);
        preprocessing.setDeskewAngleTolerance(0.1); // tolerance in degrees

        // Turn on denoising – median works well for salt‑and‑pepper noise
        preprocessing.setDenoise(true);
        preprocessing.setDenoiseMode(DenoiseMode.MEDIAN); // alternatives: GAUSSIAN

        // Boost contrast – this is the “boost image contrast” step
        preprocessing.setContrastEnhance(true);
        preprocessing.setContrastLevel(1.3f); // 1.0 = no change, >1.0 = stronger contrast
```

### なぜコントラストレベルを調整するのか

コントラストレベルを上げると画像のヒストグラムが伸び、暗いピクセルはさらに暗く、明るいピクセルはさらに明るくなります。実際、印刷物では **コントラストレベル** を `1.3f` に設定するとバランスが最適になることが多く、`1.5f` 以上にすると細い線が露出しすぎることがあります。自由に試してみてください。この設定は変更コストが低く、**画像からテキストを認識** の成功率を劇的に向上させます。

## ステップ 4: 入力画像の準備

`OcrInput` クラスはファイル処理を抽象化します。バッチ処理が必要な場合は、複数の画像を追加できます。

```java
        // Prepare the image for OCR – you can add more files to the same OcrInput
        OcrInput ocrInput = new OcrInput();
        ocrInput.add("YOUR_DIRECTORY/input.jpg");
```

**エッジケース:** 画像が非標準形式（例: 複数ページの TIFF）の場合、各ページを個別にロードするか、まず PNG/JPEG に変換してください。

## ステップ 5: 認識の実行

これでエンジンは先ほど設定した前処理パイプラインを実行し、クリーンになった画像をコア OCR アルゴリズムに渡します。

```java
        // Run OCR – this returns a result object containing the extracted text
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);
```

**内部で何が起きているか？** Aspose OCR はまずデスキュー変換を適用し、次にノイズ除去フィルタを実行、最後にコントラストを調整してから、ニューラルネットワークベースの認識器に画像を渡します。この順序は意図的で、変更すると結果が最適でなくなる可能性があります。

## ステップ 6: 認識結果の出力

最後に、抽出した文字列をコンソールに出力します。実際のアプリケーションではファイルに書き込んだり、ネットワーク越しに送信したりすることもあります。

```java
        // Print the recognized text to the console
        System.out.println(ocrResult.getText());
    }
}
```

### 期待される出力

`input.jpg` に “Hello World!” というフレーズが含まれていれば、コンソールには次のように表示されます：

```
Hello World!
```

出力が文字化けしている場合は、前処理の値、特に **コントラストレベル** と **ノイズ除去モード** を再確認し、別の画像形式で試してください。

## ボーナス: 前処理画像の可視化（オプション）

デスキュー、ノイズ除去、コントラスト強化の後にエンジンがどのように画像を見ているか確認したくなることがあります。Aspose OCR は中間ビットマップをエクスポートできます：

```java
        // Export the pre‑processed image for debugging
        BufferedImage processed = preprocessing.getProcessedImage();
        ImageIO.write(processed, "png", new File("processed.png"));
```

`processed.png` を元画像と並べて開くと、水平線がまっすぐになり、文字がより鮮明になることが分かります。この手順は、特定のスキャンが失敗する原因をトラブルシュートする際に便利です。

![OCR 用画像前処理例](/images/ocr-preprocess-example.png "OCR 用画像前処理 – コントラスト強化前後")

*上の画像は、コントラストを上げてノイズ除去することで、ぼやけたスキャンがクリーンで OCR 対応の画像になる様子を示しています。*

## よくある落とし穴と回避策

| 落とし穴 | 発生原因 | 対策 |
|---------|----------|------|
| **コントラスト過剰** (`setContrastLevel` が高すぎる) | 背景が白くなり、薄い文字が消えてしまう | ほとんどの印刷物ではレベルを 1.1〜1.4 の間に保つ |
| **デスキュー許容度が低すぎる** | 小さな回転が補正されないまま残る | `setDeskewAngleTolerance` を 0.2 または 0.3 に上げる（書籍スキャン向け） |
| **二値画像に GAUSSIAN ノイズ除去を使用** | エッジがぼやけ、文字が結合してしまう | 白黒スキャンでは `DenoiseMode.MEDIAN` を使用する |
| **ライセンス未設定** | エンジンが評価モードにフォールバックし、出力が切り詰められる | `Aspose.OCR.lic` のパスとファイルの読み取り権限を確認する |

## 次のステップ: 基本前処理を超えて

これで **OCR 用画像前処理** と **OCR でテキスト抽出** ができるようになったので、以下の拡張を検討してください：

- **Language packs** – 非英語テキストの精度向上のために特定の言語辞書をロードします。
- **Region‑of‑interest (ROI) cropping** – ページの一部だけが必要な場合に、画像のサブセクションに焦点を当てます。
- **Batch processing** – 画像ディレクトリをループし、同じ `OcrEngine` インスタンスを再利用して高速化します。
- **Integrate with PDF** – Aspose OCR と Aspose PDF を組み合わせ、スキャンした PDF を検索可能な PDF に一括変換します。

これらのトピックはすべて、**画像のコントラストを上げる**、**コントラストレベルを設定**、そして多くのシナリオで **画像からテキストを認識** し続けるという二次キーワードを自然に含みます。

## 結論

ここまでで、Aspose OCR for Java を使用した **OCR 用画像前処理** に必要なすべてを網羅しました：ライセンスのロード、デスキュー、ノイズ除去、コントラスト強化の設定、画像の投入、そして最終的な **画像からテキストを認識**。上記の完全な実行可能サンプルにより、適切に準備された画像から **OCR でテキストを抽出** できるようになります。

コードを実行し、**コントラストレベル** を調整して精度向上を体感してください。準備ができたら、言語固有のモデルやバッチパイプラインを検討し、この単一画像デモを本番レベルのソリューションへと拡張しましょう。

*コーディングを楽しんで、スキャンが常に鮮明でありますように！*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}