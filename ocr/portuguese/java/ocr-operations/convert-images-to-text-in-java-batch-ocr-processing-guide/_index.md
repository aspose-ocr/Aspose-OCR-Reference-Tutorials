---
category: general
date: 2026-08-28
description: Aprenda a extrair texto de imagens png em Java usando Aspose OCR. Este
  tutorial aborda o processamento de OCR em lote, a leitura de imagens de uma pasta
  e a filtragem de arquivos por extensão.
draft: false
keywords:
- extract text from png
- read images from folder
- filter files by extension
- how to batch ocr
- aspose ocr java tutorial
lastmod: 2026-08-28
og_description: Aprenda a extrair texto de imagens png em Java usando Aspose OCR.
  Este tutorial aborda o processamento de OCR em lote, a leitura de imagens de uma
  pasta e a filtragem de arquivos por extensão.
og_image_alt: 'Developer guide: extract text from png images in Java using Aspose
  OCR'
og_title: Como extrair texto de png em Java – guia de OCR em lote
schemas:
- author: Aspose
  dateModified: '2026-08-28'
  description: Learn how to extract text from png images in Java using Aspose OCR.
    This tutorial covers batch OCR processing, reading images from a folder, and filtering
    files by extension.
  headline: How to extract text from png in Java – batch OCR guide
  type: TechArticle
- questions:
  - answer: Absolutely. Aspose OCR supports 30+ formats—including PDF, TIFF, BMP,
      and GIF—so just add the desired extensions to the filter in the directory‑walk
      step.
    question: Can I process PDFs or TIFFs as well?
  - answer: Change `RecognitionLanguage.ENGLISH` to `RecognitionLanguage.SPANISH`
      (or any supported language). The language packs are bundled with the library,
      so no extra download is required.
    question: What if I need a language other than English, such as Spanish?
  - answer: Yes. `Files.walk` traverses the entire tree recursively, so every nested
      PNG/J
    question: My folder contains sub‑folders—will they be scanned?
  - answer: Enable streaming mode by calling `ocrEngine.setUseStreaming(true)`. This
      tells the engine to read the image in chunks, dramatically reducing peak memory
      usage.
    question: How do I handle extremely large images that exceed 200 MB?
  - answer: Yes. When constructing `ParallelRecognizer`, pass the desired maximum
      thread count as the second argument (e.g., `new ParallelRecognizer(ocrEngine,
      4)`).
    question: Is there a way to limit the number of concurrent OCR threads?
  type: FAQPage
tags:
- OCR
- Java
- Aspose
title: Como extrair texto de png em Java – guia de OCR em lote
url: /pt/java/ocr-operations/convert-images-to-text-in-java-batch-ocr-processing-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como extrair texto de png em Java – guia de OCR em lote

Se você já precisou **extrair texto de png** arquivos mas não tinha certeza de como dimensionar a operação além de algumas imagens, você está no lugar certo. Muitos desenvolvedores começam com uma chamada OCR de imagem única e rapidamente encontram limites de desempenho quando a pasta cresce para dezenas ou centenas de arquivos. Com Aspose OCR for Java você pode criar um pipeline robusto de OCR em lote que percorre um diretório, filtra apenas os tipos de imagem que lhe interessam, executa o reconhecimento em paralelo e devolve os resultados na mesma ordem dos arquivos de origem. Ao final deste guia você terá um trecho de código Java pronto para uso que lida com **processamento de OCR em lote** de forma confiável e eficiente.

![Convert images to text example](https://example.com/convert-images-to-text.png "Screenshot of Java console output showing converted text from PNG files")

## Respostas rápidas
- **Qual biblioteca lida com OCR?** Aspose OCR for Java.
- **Posso processar PNG e JPG juntos?** Sim – o exemplo filtra ambas as extensões.
- **O motor OCR é thread‑safe?** Uma única instância compartilhada de `AsposeOCR` é segura para uso concorrente.
- **Preciso de licença para testes?** Uma chave temporária gratuita está disponível na Aspose.
- **Pastas‑sub serão escaneadas automaticamente?** `Files.walk` percorre toda a árvore recursivamente.

## O que é extrair texto de png?

`extract text from png` refere-se ao processo de aplicar reconhecimento óptico de caracteres (OCR) a arquivos Portable Network Graphics para que os caracteres visíveis se tornem cadeias pesquisáveis e editáveis. O motor do Aspose OCR lê os dados de pixels, identifica formas de glifos e devolve texto Unicode em uma única chamada de método.

## Por que usar Aspose OCR for Java?

Aspose OCR suporta **30+ idiomas**, processa até **500 imagens por minuto** em um servidor padrão de 8 núcleos, e pode lidar com arquivos de até **200 MB** sem carregar a imagem inteira na memória. Essas capacidades quantificadas significam que você pode executar de forma confiável trabalhos em lote de grande escala em hardware comum sem atingir limites de memória.

## Pré-requisitos
- Java 17 (ou qualquer versão LTS recente).
- Maven ou Gradle para gerenciamento de dependências.
- Um diretório contendo imagens PNG/JPG que você deseja processar.
- Familiaridade básica com streams Java e o pacote `java.nio.file`.
- (Opcional) Uma chave de licença temporária do Aspose OCR para avaliação.

> **Dica profissional:** A chave temporária gratuita expira após 30 dias, mas fornece acesso total à API para testes.

## Como o pipeline de OCR em lote mantém a ordem?

`Future<OcrResult>` representa um resultado OCR pendente que pode ser recuperado quando o processamento termina. O pipeline preserva a ordem original dos arquivos armazenando os objetos `Future<OcrResult>` em uma lista que espelha a ordem da coleção de `Path` de entrada. Quando você posteriormente itera sobre os futures e chama `get()`, cada chamada bloqueia apenas para sua imagem correspondente, de modo que a sequência de saída corresponde à sequência de entrada sem lógica de ordenação extra.

## O que é Aspose OCR for Java?

`AsposeOCR` é a classe central da biblioteca Aspose OCR que encapsula todos os pacotes de idiomas, configurações de reconhecimento e recursos nativos internos. Ela foi projetada para ser instanciada uma única vez durante a vida da aplicação e compartilhada com segurança entre múltiplas threads. Como carrega os dados de idioma apenas uma vez, reutilizar a mesma instância reduz a sobrecarga de inicialização e melhora a taxa de transferência para operações em lote.

## Como configurar o projeto e adicionar Aspose OCR

First, create a Maven (or Gradle) project and add the Aspose OCR dependency to your `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>24.10</version>
</dependency>
```

> **Por que isso importa:** Declarar a dependência antecipadamente garante que o compilador possa ver `AsposeOCR`, `ParallelRecognizer` e classes relacionadas. Também garante que a mesma versão seja usada em todas as máquinas, o que é crucial para um **processamento de OCR em lote** reproduzível.

Atualize seu IDE após a conclusão da compilação; agora você deve ver os pacotes Aspose em **External Libraries**.

## Como inicializar o motor OCR – compartilhar uma única instância

`AsposeOCR` é a classe principal do motor OCR fornecida pela biblioteca Aspose OCR. Nós precisamos apenas de **uma** instância do motor OCR para toda a execução. Compartilhá‑la entre threads economiza memória e acelera as coisas porque o motor carrega os pacotes de idioma apenas uma vez.

```java
AsposeOCR ocrEngine = new AsposeOCR("YOUR_LICENSE_KEY");
```

> **Explicação:** `ParallelRecognizer` encapsula o motor em um pool de threads. Quando você submete muitos arquivos, cada um recebe sua própria thread de trabalho, permitindo paralelismo real em CPUs multi‑core.

## Como ler imagens da pasta – percorrer a árvore de diretórios

`Files.walk` é um método Java NIO que percorre recursivamente uma árvore de arquivos e devolve um stream de objetos `Path`. Agora precisamos **ler imagens da pasta** e coletar todos os PNG ou JPG. A API `Files.walk` torna isso uma única linha, mas adicionaremos um filtro para **extrair texto de png** somente quando necessário.

```java
List<Path> imagePaths = Files.walk(Paths.get("YOUR_DIRECTORY"))
    .filter(Files::isRegularFile)
    .filter(p -> {
        String lower = p.toString().toLowerCase();
        return lower.endsWith(".png") || lower.endsWith(".jpg");
    })
    .collect(Collectors.toList());
```

> **Por que filtramos aqui:** Usar `filter` nos permite **filtrar arquivos por extensão** cedo, o que reduz I/O desnecessário depois. Também mantém o código legível — sem necessidade de expressões regulares complexas.

## Como submeter trabalhos OCR assincronamente

`recognizeAsync` submete uma imagem ao motor OCR para processamento assíncrono e devolve um `Future<OcrResult>` representando o resultado pendente. Com a lista de arquivos pronta, enviamos cada caminho ao `ParallelRecognizer`. O método `recognizeAsync` devolve um `Future<OcrResult>` que armazenamos para recuperação posterior.

```java
ParallelRecognizer recognizer = new ParallelRecognizer(ocrEngine, Runtime.getRuntime().availableProcessors());
List<Future<OcrResult>> futures = new ArrayList<>();

for (Path imagePath : imagePaths) {
    futures.add(recognizer.recognizeAsync(imagePath));
}
```

> **O que está acontecendo nos bastidores?** Cada chamada enfileira uma tarefa no serviço executor interno do recognizer. As tarefas são executadas em paralelo, de modo que uma pasta com 100 imagens pode ser processada em uma fração do tempo que um loop de thread única levaria.

## Como recuperar resultados preservando a sequência dos arquivos

`Future<OcrResult>` contém o resultado de uma tarefa OCR assíncrona e fornece um método `get()` para obter o texto reconhecido. Como armazenamos os futures na mesma ordem de `imagePaths`, podemos simplesmente iterar sobre a lista e chamar `get()`. A chamada bloqueia apenas até que aquela imagem específica termine, preservando a ordem sem contabilidade extra.

```java
for (int i = 0; i < futures.size(); i++) {
    try {
        OcrResult result = futures.get(i).get();
        System.out.println("File: " + imagePaths.get(i).getFileName());
        System.out.println("Text: " + result.getText());
    } catch (Exception e) {
        System.err.println("Failed to process " + imagePaths.get(i) + ": " + e.getMessage());
    }
}
```

**Sample console output** (truncated for brevity):

```
File: invoice1.png
Text: Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00
...
```

> **Tratamento de casos extremos:** Se uma imagem específica lançar uma exceção (arquivo corrompido, formato não suportado), nós a capturamos e continuamos processando o restante — um hábito essencial para pipelines de **processamento de OCR em lote** confiáveis.

## Como limpar recursos – encerrar o recognizer

`ParallelRecognizer.shutdown()` interrompe o pool de threads interno, garantindo que todas as tarefas OCR concluam antes que a aplicação saia. Nunca se esqueça de encerrar o pool de threads interno; caso contrário sua JVM pode travar ao encerrar.

```java
recognizer.shutdown();
```

É isso! O programa agora percorre qualquer diretório, filtra arquivos PNG/JPG, executa OCR em paralelo e imprime os resultados na ordem original.

---

## Exemplo completo (copiar‑e‑colar)

Abaixo está a classe Java completa, pronta para execução. Substitua `"YOUR_DIRECTORY"` pelo caminho da sua pasta de imagens e execute-a a partir da sua IDE ou da linha de comando.

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.ParallelRecognizer;
import com.aspose.ocr.OcrResult;
import java.nio.file.*;
import java.util.*;
import java.util.concurrent.*;
import java.util.stream.*;

public class BatchOcrDemo {
    public static void main(String[] args) throws Exception {
        // Initialise the OCR engine (single shared instance)
        AsposeOCR ocrEngine = new AsposeOCR("YOUR_LICENSE_KEY");

        // Create a parallel recognizer that uses a thread pool
        ParallelRecognizer recognizer = new ParallelRecognizer(ocrEngine,
                Runtime.getRuntime().availableProcessors());

        // Walk the directory and collect PNG/JPG files
        List<Path> imagePaths = Files.walk(Paths.get("YOUR_DIRECTORY"))
                .filter(Files::isRegularFile)
                .filter(p -> {
                    String lower = p.toString().toLowerCase();
                    return lower.endsWith(".png") || lower.endsWith(".jpg");
                })
                .collect(Collectors.toList());

        // Submit OCR jobs asynchronously
        List<Future<OcrResult>> futures = new ArrayList<>();
        for (Path imagePath : imagePaths) {
            futures.add(recognizer.recognizeAsync(imagePath));
        }

        // Retrieve results in the original order
        for (int i = 0; i < futures.size(); i++) {
            try {
                OcrResult result = futures.get(i).get();
                System.out.println("File: " + imagePaths.get(i).getFileName());
                System.out.println("Text: " + result.getText());
            } catch (Exception e) {
                System.err.println("Failed to process " + imagePaths.get(i) + ": " + e.getMessage());
            }
        }

        // Clean up the recognizer's thread pool
        recognizer.shutdown();
    }
}
```

Execute a classe, observe o console se encher com as strings extraídas e comemore o fato de que você acabou de **converter imagens em texto** sem escrever nenhum loop que bloqueie em I/O.

---

## Perguntas frequentes (FAQs)

**Q: Posso processar PDFs ou TIFFs também?**  
A: Absolutamente. Aspose OCR suporta mais de 30 formatos — incluindo PDF, TIFF, BMP e GIF — então basta adicionar as extensões desejadas ao filtro na etapa de percorrer o diretório.

**Q: E se eu precisar de um idioma diferente do inglês, como espanhol?**  
A: Altere `RecognitionLanguage.ENGLISH` para `RecognitionLanguage.SPANISH` (ou qualquer idioma suportado). Os pacotes de idioma vêm incluídos na biblioteca, portanto nenhum download extra é necessário.

**Q: Minha pasta contém sub‑pastas — elas serão escaneadas?**  
A: Sim. `Files.walk` percorre toda a árvore recursivamente, então cada PNG/J

**Q: Como lidar com imagens extremamente grandes que excedem 200 MB?**  
A: Ative o modo de streaming chamando `ocrEngine.setUseStreaming(true)`. Isso instrui o motor a ler a imagem em blocos, reduzindo drasticamente o uso máximo de memória.

**Q: Existe uma maneira de limitar o número de threads OCR concorrentes?**  
A: Sim. Ao construir `ParallelRecognizer`, passe a contagem máxima de threads desejada como segundo argumento (por exemplo, `new ParallelRecognizer(ocrEngine, 4)`).

---

**Última atualização:** 2026-08-28  
**Testado com:** Aspose OCR for Java 24.10  
**Autor:** Aspose  






```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- Check the latest version on Maven Central -->
</dependency>
```

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.ParallelRecognizer;
import com.aspose.ocr.OcrResult;
import com.aspose.ocr.RecognitionLanguage;

// ...

// Step 2: Create a single OCR engine instance and a parallel recognizer that uses it
AsposeOCR ocrEngine = new AsposeOCR();               // Loads language data internally
ParallelRecognizer parallelRecognizer = new ParallelRecognizer(ocrEngine);
```

```java
import java.nio.file.*;
import java.util.*;
import java.util.stream.Collectors;

// ...

// Step 3: Find all PNG and JPG images in the target directory
Path imagesRoot = Paths.get("YOUR_DIRECTORY"); // <-- replace with your path
List<Path> imagePaths = Files.walk(imagesRoot)
        .filter(p -> {
            String name = p.toString().toLowerCase();
            return name.endsWith(".png") || name.endsWith(".jpg");
        })
        .collect(Collectors.toList());

if (imagePaths.isEmpty()) {
    System.out.println("No PNG or JPG files found in " + imagesRoot);
    return;
}
```

```java
import java.util.concurrent.*;

// ...

// Step 4: Submit each image for asynchronous recognition
List<Future<OcrResult>> recognitionFutures = new ArrayList<>();

for (Path image : imagePaths) {
    Future<OcrResult> future = parallelRecognizer.recognizeAsync(
            image.toString(),
            RecognitionLanguage.ENGLISH); // Change language if needed
    recognitionFutures.add(future);
}
```

```java
// Step 5: Retrieve and display the OCR results in the original order
for (int i = 0; i < recognitionFutures.size(); i++) {
    try {
        OcrResult result = recognitionFutures.get(i).get(); // blocks if not ready
        System.out.println("File: " + imagePaths.get(i).getFileName());
        System.out.println(result.getText()); // The extracted text
        System.out.println("-----");
    } catch (InterruptedException | ExecutionException e) {
        System.err.println("Failed to process " + imagePaths.get(i) + ": " + e.getMessage());
    }
}
```

```
File: invoice_001.png
Invoice #001
Date: 2024‑03‑15
Total: $1,250.00
-----
File: receipt_202403.jpg
Receipt
Item A - $45.00
Item B - $30.00
Grand Total: $75.00
-----
```

```java
// Step 6: Shut down the recognizer to clean up its internal thread pool
parallelRecognizer.shutdown();
```

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.ParallelRecognizer;
import com.aspose.ocr.OcrResult;
import com.aspose.ocr.RecognitionLanguage;

import java.nio.file.*;
import java.util.*;
import java.util.concurrent.*;
import java.util.stream.Collectors;

public class BatchParallelExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create a single OCR engine instance and a parallel recognizer that uses it
        AsposeOCR ocrEngine = new AsposeOCR();
        ParallelRecognizer parallelRecognizer = new ParallelRecognizer(ocrEngine);

        // Step 2: Find all PNG and JPG images in the target directory
        List<Path> imagePaths = Files.walk(Paths.get("YOUR_DIRECTORY"))
                .filter(p -> {
                    String lower = p.toString().toLowerCase();
                    return lower.endsWith(".png") || lower.endsWith(".jpg");
                })
                .collect(Collectors.toList());

        if (imagePaths.isEmpty()) {
            System.out.println("No images found – nothing to convert.");
            parallelRecognizer.shutdown();
            return;
        }

        // Step 3: Submit each image for asynchronous recognition
        List<Future<OcrResult>> recognitionFutures = new ArrayList<>();
        for (Path image : imagePaths) {
            recognitionFutures.add(
                    parallelRecognizer.recognizeAsync(
                            image.toString(),
                            RecognitionLanguage.ENGLISH));
        }

        // Step 4: Retrieve and display the OCR results in the original order
        for (int i = 0; i < recognitionFutures.size(); i++) {
            try {
                OcrResult result = recognitionFutures.get(i).get(); // blocks until processed
                System.out.println("File: " + imagePaths.get(i).getFileName());
                System.out.println(result.getText());
                System.out.println("-----");
            } catch (InterruptedException | ExecutionException e) {
                System.err.println("Error processing " + imagePaths.get(i) + ": " + e.getMessage());
            }
        }

        // Step 5: Shut down the recognizer to clean up its internal thread pool
        parallelRecognizer.shutdown();
    }
}
```

## Tutoriais Relacionados

- [Converter imagens em texto em Java – Guia de processamento OCR em lote](/ocr/java/ocr-operations/convert-images-to-text-in-java-batch-ocr-processing-guide/)
- [Ler texto de imagem em Java – Guia completo Aspose OCR](/ocr/java/ocr-basics/read-text-from-image-in-java-complete-aspose-ocr-guide/)
- [Extrair texto de imagens usando Aspose.OCR – Caracteres permitidos](/ocr/java/advanced-ocr-techniques/specify-allowed-characters/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}