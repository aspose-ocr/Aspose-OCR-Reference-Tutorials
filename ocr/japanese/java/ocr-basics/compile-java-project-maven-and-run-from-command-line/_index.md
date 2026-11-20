---
category: general
date: 2026-10-18
description: Maven の clean、compile、exec コマンドを使用して、コマンドラインから Java プロジェクトをコンパイルし実行します。Java
  アプリを効率的にビルドおよび実行する方法を学びましょう。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- compile java project maven
- execute java class command line
- maven clean compile run
- build and run java app
- maven compile source code
language: ja
lastmod: 2026-10-18
og_description: ステップバイステップのガイドで、Mavenを使ってJavaプロジェクトをコンパイルし、コマンドラインから実行します。Mavenのclean、compile、runをマスターして、Javaアプリをビルド・実行しましょう。
og_image_alt: Terminal screenshot showing mvn clean compile exec commands
og_title: MavenでJavaプロジェクトをコンパイル – コマンドラインから実行
schemas:
- author: Aspose
  dateModified: '2026-10-18'
  description: Compile java project maven and run from command line using Maven clean,
    compile, and exec commands. Learn how to build and run java app efficiently.
  headline: Compile java project maven and run from command line
  type: TechArticle
- description: Compile java project maven and run from command line using Maven clean,
    compile, and exec commands. Learn how to build and run java app efficiently.
  name: Compile java project maven and run from command line
  steps:
  - name: '**Missing `exec-maven-plugin`**'
    text: '**Missing `exec-maven-plugin`**'
  - name: '**Incorrect classpath**'
    text: '**Incorrect classpath**'
  - name: '**Using the wrong JDK version**'
    text: '**Using the wrong JDK version**'
  - name: '**Shell quoting problems**'
    text: '**Shell quoting problems**'
  type: HowTo
tags:
- Maven
- Java
- Command line
title: JavaプロジェクトをMavenでコンパイルし、コマンドラインから実行する
url: /ja/java/ocr-basics/compile-java-project-maven-and-run-from-command-line/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# MavenでJavaプロジェクトをコンパイルし、コマンドラインから実行する

ターミナルから直接生成されたクラスを起動したい場合、**compile java project maven** が必要です。このガイドではその手順を正確に示します。チュートリアルの最後までに、古いアーティファクトをクリーンし、ソースコードをコンパイルし、単一のMavenコマンドチェーンで **execute java class command line** を実行できるようになります。

このチュートリアルでは、Mavenで **build and run java app** を行うために必要なすべてをカバーします。必要なプラグイン、一般的な落とし穴、Windows と Unix 系シェル向けのヒントを含みます。外部ドキュメントは不要です—以下の手順に従ってください。

## 前提条件

* Java Development Kit (JDK) 8 以上がインストールされ、`JAVA_HOME` が設定されていること。  
* Apache Maven 3.6+ が `PATH` に設定されていること。  
* `pom.xml` を含み、`public static void main(String[] args)` メソッドを持つ Java クラスがある Maven プロジェクト（この例ではクラスは `com.aspose.ocr.examples.SimpleOcrDemo`）。

## MavenでJavaプロジェクトをコンパイルする

最初のステップは、以前にコンパイルされたクラスやその他のビルドアーティファクトを削除することです。`mvn clean` を実行すると、クリーンな状態が保証され、古いバイトコードがランタイムエラーを引き起こすのを防ぎます。

```bash
# Step 1: Clean previous build artifacts
mvn clean
```

*Why clean?* Maven はコンパイルされたクラスを `target/` に保存します。clean フェーズを省略すると、古い `.class` ファイルが残り、特にパッケージ名をリファクタリングした後にコンパイル問題が隠れることがあります。

## Javaクラスをコマンドラインで実行する

クリーン後、ソースファイルをコンパイルします。Maven の `compile` フェーズはすべての `src/main/java` ソースをバイトコードに変換し、結果を `target/classes` に配置します。

```bash
# Step 2: Compile the source code
mvn compile
```

これで **maven compile source code** の出力が実行可能な状態になりました。次のコマンドは、別途 JAR を作成せずにコンパイル済みクラスを実行します。

```bash
# Step 3: Run the Simple OCR demo
mvn exec:java -Dexec.mainClass="com.aspose.ocr.examples.SimpleOcrDemo"
```

`exec:java` ゴール（**maven clean compile run** プラグイン）は、指定されたクラスをコンパイル出力ディレクトリから直接起動します。これは開発中に **execute java class command line** を行う最速の方法です。

### 期待される出力

デモが正常に実行されると、以下のような出力が表示されます。

```
[INFO] Scanning for projects...
[INFO] ------------------------------------------------------------------------
[INFO] Building SimpleOCR Demo 1.0
[INFO] ------------------------------------------------------------------------
Hello, OCR world!
Processing completed in 1.23 seconds.
```

`ClassNotFoundException` が発生した場合は、完全修飾クラス名を再確認し、`src/main/java` 配下に存在することを確認してください。

## Maven clean compile run ワークフロー

3 つのコマンドを組み合わせると、コンパクトで再現可能なワークフローが得られます。

```bash
mvn clean compile exec:java -Dexec.mainClass="com.aspose.ocr.examples.SimpleOcrDemo"
```

*Why chain them?* フェーズを結合することで **Enter** を 3 回押す必要がなくなり、ステップを忘れる可能性が減ります。Maven はフェーズを記述された順に実行し、実行前にクリーンビルドが保証されます。

### スムーズなワークフローのためのヒント

| Tip | Description |
|-----|-------------|
| **プロファイルを使用する** | `clean`、`compile`、`exec:java` をまとめた Maven プロファイルを定義し、フルチェーンを入力する代わりに `mvn demo` を実行できるようにします。 |
| **JVM オプションを追加する** | `-Dexec.args="-Xmx512m"` を渡して、メモリ集約型アプリのヒープサイズを増やします。 |
| **クロスプラットフォーム** | Windows では `mvn.cmd`、Unix シェルでは `mvn` を使用します。同じコマンドが両環境で動作します。 |

## MavenでJavaアプリをビルド＆実行する

配布可能なアーティファクトが必要な場合は、Maven にコンパイル済みクラスを実行可能 JAR にパッケージさせ、標準の `java -jar` コマンドで実行できます。

```bash
# Package the app into a JAR (includes dependencies if you use the shade plugin)
mvn clean package

# Run the packaged JAR
java -jar target/simple-ocr-demo-1.0.jar
```

この方法は、Maven がインストールされていないサーバー上で **build and run java app** が必要な場合に便利です。ただし、迅速な開発には **maven clean compile run** シーケンスの方がパッケージ手順を省くため高速です。

## Maven compile source code – よくある落とし穴

コマンドはシンプルですが、開発者は以下の問題に直面しがちです。

1. **Missing `exec-maven-plugin`**  
   Maven が `exec:java` ゴールを見つけられない場合は、`pom.xml` にプラグインを追加してください：

   ```xml
   <build>
     <plugins>
       <plugin>
         <groupId>org.codehaus.mojo</groupId>
         <artifactId>exec-maven-plugin</artifactId>
         <version>3.1.0</version>
         <configuration>
           <mainClass>com.aspose.ocr.examples.SimpleOcrDemo</mainClass>
         </configuration>
       </plugin>
     </plugins>
   </build>
   ```

2. **Incorrect classpath**  
   Maven は `target/classes` にコンパイルします。手動でファイルを移動したり、デフォルトの出力ディレクトリを変更した場合、`exec:java` ゴールがクラスを見つけられないことがあります。特別な理由がない限り、デフォルトのレイアウトを維持してください。

3. **Using the wrong JDK version**  
   Maven は `JAVA_HOME` から JDK を継承します。JDK 11 のソースコードでコンパイルし、JDK 8 で実行すると `UnsupportedClassVersionError` が発生します。`java -version` と `mvn -v` で JDK バージョンを確認してください。

4. **Shell quoting problems**  
   Unix では、`-Dexec.mainClass` の値に特殊文字が含まれる場合、シングルクォートで囲んでください：  
   `mvn exec:java -Dexec.mainClass='com.example.Main'`。  
   Windows ではダブルクォートで問題なく動作します。

これらの点に対処すれば、どの環境でも確実に **execute java class command line** が実行できます。

## プロのコツ：スクリプトで自動化する

デモを頻繁に再構築するチーム向けに、簡易シェルまたはバッチスクリプトを作成します：

```bash
#!/usr/bin/env bash
# run-demo.sh – clean, compile, and execute the OCR demo
mvn clean compile exec:java -Dexec.mainClass="com.aspose.ocr.examples.SimpleOcrDemo"
```

実行権限を付与します（`chmod +x run-demo.sh`）そして `./run-demo.sh` を実行します。これにより入力ミスがなくなり、全開発者が正確な **maven clean compile run** シーケンスを実行できます。

## 結論

これで **compile java project maven** の方法と、Maven の clean、compile、exec ゴールを使用して即座に **execute java class command line** する方法が分かりました。ステップバイステップのワークフローにより、クリーンなビルドが保証され、古いアーティファクトが排除され、単一のコマンドラインで **build and run java app** が可能になります。  

次に、以下を検討できます：

* デプロイ用に **shade plugin** を追加して uber‑JAR を作成する。  
* 環境別（dev、test、prod）に Maven プロファイルを設定する。  
* コンパイル前に `mvn test` でユニットテストを統合する。

これらのバリエーションを試してワークフローを自分のプロジェクトに合わせれば、Windows、macOS、Linux で動作する堅牢で再現可能なビルドパイプラインが手に入ります。コーディングを楽しんでください！

## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示した手法を基にした密接に関連するトピックを扱っています。各リソースには、完全な動作コード例とステップバイステップの解説が含まれ、追加の API 機能を習得し、独自プロジェクトで代替実装アプローチを探求するのに役立ちます。

- [JavaでOCRを使用する方法 – 完全ステップバイステップガイド](/ocr/english/java/ocr-operations/how-to-use-ocr-in-java-complete-step-by-step-guide/)
- [Javaで画像にOCRを実行する – 完全 Aspose OCR ガイド](/ocr/english/java/ocr-operations/run-ocr-on-image-with-java-complete-aspose-ocr-guide/)
- [Javaで Aspose OCR を使用して OCR を実行する方法 – ステップバイステップガイド](/ocr/english/java/ocr-operations/how-to-perform-ocr-with-aspose-ocr-in-java-step-by-step-guid/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}