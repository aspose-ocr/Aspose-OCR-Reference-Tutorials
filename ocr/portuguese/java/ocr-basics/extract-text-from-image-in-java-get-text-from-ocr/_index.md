---
category: general
date: 2026-05-25
description: Extrair texto de imagem em Java usando OCR. Aprenda como carregar a imagem
  para OCR, reconhecer texto da foto e obter o texto do OCR com um exemplo de código
  simples.
draft: false
keywords:
- extract text from image
- get text from ocr
- recognize text from photo
- java image to text
- load image for ocr
language: pt
og_description: Extraia texto de imagens em Java com um guia passo a passo. Aprenda
  a carregar a imagem para OCR, reconhecer texto a partir de foto e obter texto do
  OCR de forma eficiente.
og_title: Extrair texto de imagem em Java – Obter texto via OCR
schemas:
- author: Aspose
  dateModified: '2026-05-25'
  description: Extract text from image in Java using OCR. Learn how to load image
    for OCR, recognize text from photo, and get text from OCR with a simple code example.
  headline: Extract Text from Image in Java – Get Text from OCR
  type: TechArticle
- description: Extract text from image in Java using OCR. Learn how to load image
    for OCR, recognize text from photo, and get text from OCR with a simple code example.
  name: Extract Text from Image in Java – Get Text from OCR
  steps:
  - name: '**Wrong language setting** – If you forget step 2, the engine defaults
      to English, turning Cyrillic characters into gibberish. Always double‑check
      the language code.'
    text: '**Wrong language setting** – If you forget step 2, the engine defaults
      to English, turning Cyrillic characters into gibberish. Always double‑check
      the language code.'
  - name: '**Image quality matters** – Low‑resolution or blurry photos will degrade
      accuracy. Pre‑process with contrast enhancement or binarization if needed.'
    text: '**Image quality matters** – Low‑resolution or blurry photos will degrade
      accuracy. Pre‑process with contrast enhancement or binarization if needed.'
  - name: '**File path quirks** – On Windows, backslashes need escaping (`C:\images\file.jpg`).
      Using `Path.of(...)` from `java.nio.file` sidesteps this.'
    text: '**File path quirks** – On Windows, backslashes need escaping (`C:\images\file.jpg`).
      Using `Path.of(...)` from `java.nio.file` sidesteps this.'
  - name: '**Memory leaks** – `OcrEngine` holds native resources. Call `ocrEngine.dispose()`
      when you’re done, especially in long‑running services.'
    text: '**Memory leaks** – `OcrEngine` holds native resources. Call `ocrEngine.dispose()`
      when you’re done, especially in long‑running services.'
  - name: '**Thread safety** – The engine isn’t thread‑safe out of the box. Create
      a separate instance per thread or synchronize access.'
    text: '**Thread safety** – The engine isn’t thread‑safe out of the box. Create
      a separate instance per thread or synchronize access.'
  type: HowTo
tags:
- OCR
- Java
- Image Processing
title: Extrair texto de imagem em Java – Obter texto via OCR
url: /pt/java/ocr-basics/extract-text-from-image-in-java-get-text-from-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrair Texto de Imagem em Java – Obter Texto via OCR

Já precisou **extrair texto de imagem** mas não sabia qual biblioteca Java escolher? Você não está sozinho. Seja digitalizando recibos, extraindo números de série de fotos de produtos ou apenas brincando com um projeto divertido, transformar uma foto em texto editável é um obstáculo comum.

Neste tutorial vamos percorrer um exemplo completo, pronto‑para‑executar, que mostra como **carregar imagem para OCR**, configurar o motor e, finalmente, **reconhecer texto da foto** para que você possa **obter texto via OCR** com apenas algumas linhas de código. Sem referências vagas — tudo o que você precisa está aqui.

## O que você vai aprender

* Como configurar um motor OCR leve em Java.  
* Os passos exatos para **carregar imagem para OCR** e lidar com diferentes caminhos de arquivo.  
* Por que configurar o idioma importa quando você quer **extrair texto de imagem** que não está em inglês.  
* Como exibir o resultado com segurança e o que fazer quando o motor não retorna nada.  
* Um conjunto de dicas profissionais para evitar as armadilhas mais comuns.

Ao final deste guia você terá um programa autônomo que lê um JPEG (ou PNG) contendo caracteres ucranianos e imprime a string reconhecida no console. Sinta‑se à vontade para trocar o idioma ou a imagem — tudo é modular.

---

![Diagrama mostrando o fluxo de extração de texto de imagem usando o motor OCR Java](/images/extract-text-from-image-java.png)

*Texto alternativo: Diagrama de fluxo do processo de extrair texto de imagem em Java.*

## Pré‑requisitos

* **Java Development Kit (JDK) 11+** – o código usa o sistema de módulos moderno, mas versões anteriores funcionam com pequenos ajustes.  
* **Maven ou Gradle** – para baixar a biblioteca OCR (usaremos **Asprise OCR** como uma opção leve e gratuita para desenvolvimento).  
* Um arquivo de imagem de exemplo (por exemplo, `ukrainian_sign.jpg`) colocado em um local que seu programa possa ler.  
* Familiaridade básica com o método `main` do Java e tratamento de exceções.

Se você tem tudo isso, está pronto para começar. Caso contrário, baixe o JDK da Oracle ou AdoptOpenJDK e configure um projeto Maven simples — nada muito elaborado.

---

## Etapa 1: Adicionar a dependência OCR

Primeiro, informe sua ferramenta de build para buscar o motor OCR. Para Maven, adicione isto ao `pom.xml`:

```xml
<dependency>
    <groupId>com.asprise.ocr</groupId>
    <artifactId>asprise-ocr</artifactId>
    <version>1.0.2</version>
</dependency>
```

Se preferir Gradle, o equivalente é:

```gradle
implementation 'com.asprise.ocr:asprise-ocr:1.0.2'
```

Essas coordenadas baixam um JAR compacto que inclui `OcrEngine`, `OcrLanguage` e as classes auxiliares que usaremos. Nenhum binário nativo extra é necessário para scripts latinos e cirílicos básicos.

---

## Etapa 2: Criar uma classe Java para **Extrair Texto de Imagem**

Agora vamos escrever o programa propriamente dito. Salve o seguinte como `ExtractTextDemo.java` dentro de `src/main/java/com/example/ocr/`.

```java
package com.example.ocr;

import com.asprise.ocr.OcrEngine;
import com.asprise.ocr.OcrLanguage;

/**
 * Demonstrates how to extract text from image using Asprise OCR.
 * The example loads a JPEG, sets the language to Ukrainian,
 * runs recognition, and prints the result.
 */
public class ExtractTextDemo {

    public static void main(String[] args) {
        // ---- 1️⃣  Initialize the OCR engine ---------------------------------
        OcrEngine ocrEngine = new OcrEngine();

        // ---- 2️⃣  Configure the engine to recognize Ukrainian text -----------
        // This is crucial if your image contains non‑Latin characters.
        ocrEngine.getEngineOptions().setLanguage(OcrLanguage.UKRAINIAN);

        // ---- 3️⃣  Load the image that contains Ukrainian characters ----------
        // Replace the path with the location of your own picture.
        String imagePath = "YOUR_DIRECTORY/ukrainian_sign.jpg";
        try {
            ocrEngine.getImage().loadFromFile(imagePath);
        } catch (Exception e) {
            System.err.println("Failed to load image: " + e.getMessage());
            return;
        }

        // ---- 4️⃣  Perform OCR recognition and obtain the extracted text -------
        String recognizedText;
        try {
            recognizedText = ocrEngine.recognize().getText();
        } catch (Exception e) {
            System.err.println("Recognition error: " + e.getMessage());
            return;
        }

        // ---- 5️⃣  Output the recognized text to the console -------------------
        System.out.println("=== OCR Result ===");
        System.out.println(recognizedText);
    }
}
```

### Por que essa estrutura funciona

* **Blocos numerados separados** facilitam o acompanhamento, especialmente quando você está procurando onde **carregar imagem para OCR** ou **reconhecer texto da foto**.  
* O `try/catch` ao redor do carregamento da imagem e do reconhecimento garante que o programa falhe de forma graciosa — útil quando o caminho do arquivo está errado ou o motor OCR não encontra os dados de idioma.  
* Definir o idioma logo no início (etapa 2) melhora drasticamente a precisão para scripts não‑inglês. Se mais tarde precisar de **java image to text** para outros idiomas, basta trocar `OcrLanguage.UKRAINIAN` por `OcrLanguage.ENGLISH`, `FRENCH` etc.

---

## Etapa 3: Compilar e Executar o Programa

Na raiz do projeto, execute:

```bash
mvn clean compile exec:java -Dexec.mainClass="com.example.ocr.ExtractTextDemo"
```

Ou, se estiver usando Gradle:

```bash
./gradlew run --args="com.example.ocr.ExtractTextDemo"
```

Assumindo que `ukrainian_sign.jpg` contenha o texto *«Ласкаво просимо»* (ucraniano para “Bem‑vindo”), você deverá ver algo como:

```
=== OCR Result ===
Ласкаво просимо
```

Essa saída confirma que você **extraiu texto de imagem** e **obteve texto via OCR** em uma única execução.

---

## Etapa 4: Ajustar o fluxo – De **Java Image to Text** em projetos reais

Embora a demonstração seja mínima, aplicações reais costumam precisar de um pouco mais:

| Cenário | O que ajustar | Motivo |
|----------|----------------|--------|
| **Processamento em lote** | Percorrer um `List<Path>` e armazenar cada resultado em um banco de dados. | Reduz o trabalho manual quando há centenas de fotos. |
| **Formatos de imagem diferentes** | Usar `ImageIO.read(new File(path))` para pré‑processar, então passar o `BufferedImage` para `ocrEngine.getImage().loadFromBufferedImage(bufImg)`. | Lida com PNG, BMP ou até PDFs após conversão. |
| **Ajuste de desempenho** | Chamar `ocrEngine.getEngineOptions().setSpeed(OcrEngine.Speed.FAST)` se você aceitar uma leve queda de precisão. | Acelera o reconhecimento em hardware de baixa potência. |
| **Pós‑processamento** | Remover espaços em branco, substituir leituras comuns errôneas do OCR (`0` → `O`, `1` → `I`). | Melhora a qualidade dos dados para etapas posteriores. |

Essas variações mantêm a ideia central — **reconhecer texto da foto** — intacta, oferecendo flexibilidade para cargas de trabalho de produção.

---

## Armadilhas Comuns & Dicas Profissionais

1. **Configuração de idioma incorreta** – Se esquecer a etapa 2, o motor usa inglês por padrão, transformando caracteres cirílicos em lixo. Sempre verifique o código do idioma.  
2. **Qualidade da imagem importa** – Fotos de baixa resolução ou desfocadas reduzem a precisão. Pré‑procese com aumento de contraste ou binarização, se necessário.  
3. **Problemas com caminhos de arquivo** – No Windows, as barras invertidas precisam ser escapadas (`C:\\images\\file.jpg`). Usar `Path.of(...)` de `java.nio.file` contorna isso.  
4. **Vazamento de memória** – `OcrEngine` mantém recursos nativos. Chame `ocrEngine.dispose()` quando terminar, especialmente em serviços de longa execução.  
5. **Segurança de threads** – O motor não é thread‑safe por padrão. Crie uma instância separada por thread ou sincronize o acesso.

---

## Exemplo Completo (Tudo‑em‑Um)

Abaixo está um único arquivo que você pode copiar‑colar em qualquer IDE. Ele inclui a chamada `dispose()` e um pequeno método auxiliar para deixar o código mais limpo.

```java
package com.example.ocr;

import com.asprise.ocr.OcrEngine;
import com.asprise.ocr.OcrLanguage;
import java.nio.file.Path;

/**
 * Complete, runnable demo that extracts text from an image using Java OCR.
 */
public class FullDemo {

    public static void main(String[] args) {
        // Path to the image – change this to your own file.
        Path imgPath = Path.of("YOUR_DIRECTORY/ukrainian_sign.jpg");

        // Run the OCR workflow and capture the output.
        String result = extractTextFromImage(imgPath, OcrLanguage.UKRAINIAN);
        if (result != null) {
            System.out.println("=== OCR Result ===");
            System.out.println(result);
        }
    }

    /**
     * Core method that encapsulates the 5‑step OCR process.
     *
     * @param imagePath Path to the image file.
     * @param language  Desired OCR language.
     * @return Recognized text, or {@code null} if something went wrong.
     */
    private static String extractTextFromImage(Path imagePath, OcrLanguage language) {
        OcrEngine engine = new OcrEngine();
        try {
            // 1️⃣ Set language
            engine.getEngineOptions().setLanguage(language);

            // 2️⃣ Load image
            engine.getImage().loadFromFile(imagePath.toString());

            // 3️⃣ Recognize and return text
            return engine.recognize().getText();
        } catch (Exception e) {
            System.err.println("Error during OCR: " + e.getMessage());
            return null;
        } finally {
            // 4️⃣ Release native resources
            engine.dispose();
        }
    }
}
```

Executar este programa produz a mesma saída mostrada anteriormente. Sinta‑se à vontade para substituir `OcrLanguage.UKRAINIAN` por `OcrLanguage.ENGLISH` ou outro idioma suportado para ver como o motor se adapta.

---

## Conclusão

Percorremos tudo que você precisa para **extrair texto de imagem** usando Java: desde a adição da dependência OCR, até **carregar imagem para OCR**,


## Tutoriais Relacionados

- [recognize text image with Aspose OCR – Full Java OCR Tutorial](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [Convert Image to Text in Java using Aspose.OCR BufferedImage](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}