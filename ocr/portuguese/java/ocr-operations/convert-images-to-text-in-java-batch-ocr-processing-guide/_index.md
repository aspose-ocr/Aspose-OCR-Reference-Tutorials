---
category: general
date: 2026-01-02
description: Converta imagens em texto com Java usando Aspose OCR. Domine o processamento
  em lote de OCR, leia imagens de uma pasta e filtre arquivos por extensão.
draft: false
keywords:
- convert images to text
- batch ocr processing
- read images from folder
- extract text from png
- filter files by extension
language: pt
og_description: Converta imagens em texto rapidamente com Java. Este tutorial aborda
  o processamento OCR em lote, a leitura de imagens a partir de uma pasta e a filtragem
  de arquivos por extensão.
og_title: Converter imagens em texto em Java – Guia completo de OCR em lote
tags:
- OCR
- Java
- Aspose
title: Converter imagens em texto em Java – Guia de processamento OCR em lote
url: /pt/java/ocr-operations/convert-images-to-text-in-java-batch-ocr-processing-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Converter Imagens em Texto em Java – Guia de Processamento em Lote de OCR

Já precisou **converter imagens em texto** mas não sabia como lidar com dezenas de arquivos de uma vez? Você não está sozinho — desenvolvedores lutam constantemente para extrair dados de PNGs, JPGs e outras digitalizações. A boa notícia? Com o Aspose OCR você pode criar um pipeline de processamento em lote de OCR em minutos, ler imagens a partir de estruturas de pastas e até filtrar arquivos por extensão para trabalhar apenas no que importa.

Neste tutorial vamos construir um programa Java autônomo que percorre um diretório, seleciona cada `.png` ou `.jpg`, envia cada imagem ao Aspose OCR de forma assíncrona e imprime o texto extraído na ordem original. Ao final, você terá um trecho reutilizável que pode ser inserido em qualquer projeto que precise **converter imagens em texto** em escala.

---

![Exemplo de conversão de imagens em texto](https://example.com/convert-images-to-text.png "Captura de tela da saída do console Java mostrando texto convertido de arquivos PNG")

## O que Você Vai Construir

- Um único motor `AsposeOCR` compartilhado entre threads (eficiente e thread‑safe).  
- Um `ParallelRecognizer` que executa trabalhos de OCR em paralelo, perfeito para **processamento em lote de OCR**.  
- Lógica que **lê imagens de pastas** usando `java.nio.file.Files`.  
- Filtros simples para **extrair texto de arquivos PNG** enquanto ainda lida com JPGs.  
- Encerramento limpo do pool de threads interno para evitar vazamentos de recursos.

### Pré‑requisitos

- Java 17 (ou qualquer versão LTS recente).  
- Maven ou Gradle para obter a biblioteca Aspose OCR.  
- Uma pasta cheia de imagens PNG/JPG que você deseja processar.  
- Familiaridade básica com streams Java — nada de complicado.

> **Dica de especialista:** Se ainda não tem uma licença, a Aspose oferece uma chave temporária gratuita que pode ser usada para testes.

---

## Etapa 1 – Configurar o Projeto e Adicionar Aspose OCR

Primeiro, crie um novo projeto Maven (ou Gradle, como preferir). Adicione a dependência Aspose OCR ao `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- Check the latest version on Maven Central -->
</dependency>
```

> **Por que isso importa:** Declarar a dependência antecipadamente garante que o compilador reconheça `AsposeOCR`, `ParallelRecognizer` e classes relacionadas. Também assegura que a mesma versão seja usada em todas as máquinas, o que é crucial para um **processamento em lote de OCR** reproduzível.

Quando a compilação terminar, atualize sua IDE e você deverá ver os pacotes Aspose em `External Libraries`.

---

## Etapa 2 – Converter Imagens em Texto – Inicializar o Motor OCR

Precisamos de **apenas uma** instância do motor OCR para toda a execução. Compartilhá‑la entre threads economiza memória e acelera o processo porque o motor carrega os pacotes de idioma apenas uma vez.

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

> **Explicação:** `ParallelRecognizer` encapsula o motor em um pool de threads. Quando você submete muitos arquivos, cada um recebe sua própria thread de trabalho, permitindo paralelismo real em CPUs multi‑core.

---

## Etapa 3 – Ler Imagens de Pasta – Percorrer a Árvore de Diretórios

Agora precisamos **ler imagens de pasta** e coletar todos os PNG ou JPG. A API `Files.walk` transforma isso em uma única linha, mas adicionaremos um filtro para **extrair texto de PNG** apenas quando necessário.

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

> **Por que filtramos aqui:** Usar `filter` nos permite **filtrar arquivos por extensão** logo no início, reduzindo I/O desnecessário depois. Também mantém o código legível — sem necessidade de expressões regulares complexas.

---

## Etapa 4 – Processamento em Lote de OCR – Enviar Trabalhos Assincronamente

Com a lista de arquivos pronta, enviamos cada caminho ao `ParallelRecognizer`. O método `recognizeAsync` devolve um `Future<OcrResult>` que armazenamos para recuperação posterior.

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

> **O que está acontecendo nos bastidores?** Cada chamada enfileira uma tarefa no serviço executor interno do reconhecedor. As tarefas rodam em paralelo, de modo que uma pasta com 100 imagens pode ser processada em uma fração do tempo que um loop monothread levaria.

---

## Etapa 5 – Recuperar Resultados na Ordem Original – Preservar Sequência de Arquivos

Como armazenamos os futures na mesma ordem de `imagePaths`, podemos simplesmente iterar sobre a lista e chamar `get()`. A chamada bloqueia apenas até que aquela imagem específica termine, preservando a ordem sem necessidade de controle extra.

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

**Exemplo de saída no console** (truncado para brevidade):

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

> **Tratamento de casos extremos:** Se uma imagem específica lançar uma exceção (arquivo corrompido, formato não suportado), capturamos a exceção e continuamos processando o restante — um hábito essencial para pipelines de **processamento em lote de OCR** confiáveis.

---

## Etapa 6 – Limpeza – Encerrar o Reconhecedor

Nunca se esqueça de encerrar o pool de threads interno; caso contrário sua JVM pode ficar pendurada ao sair.

```java
// Step 6: Shut down the recognizer to clean up its internal thread pool
parallelRecognizer.shutdown();
```

É isso! O programa agora percorrerá qualquer diretório, filtrará arquivos PNG/JPG, executará OCR em paralelo e imprimirá os resultados.

---

## Exemplo Completo Funcionando

Abaixo está a classe Java completa, pronta para copiar e colar. Substitua `"YOUR_DIRECTORY"` pelo caminho da sua pasta de imagens e execute-a a partir da sua IDE ou linha de comando.

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

Execute a classe, observe o console se encher de strings extraídas e comemore o fato de que você acabou de **converter imagens em texto** sem escrever um único loop que bloqueie I/O.

---

## Perguntas Frequentes (FAQs)

**Q: Posso processar PDFs ou TIFFs também?**  
A: Absolutamente. O Aspose OCR suporta muitos formatos — basta adicionar as extensões de arquivo apropriadas ao filtro na Etapa 2.

**Q: E se eu precisar de outro idioma, como espanhol?**  
A: Altere `RecognitionLanguage.ENGLISH` para `RecognitionLanguage.SPANISH`. Certifique‑se de que o pacote de idioma esteja instalado (a Aspose inclui a maioria dos idiomas principais por padrão).

**Q: Minha pasta contém sub‑pastas — elas serão escaneadas?**  
A: Sim. `Files.walk` percorre toda a árvore recursivamente, então cada PNG/J

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}