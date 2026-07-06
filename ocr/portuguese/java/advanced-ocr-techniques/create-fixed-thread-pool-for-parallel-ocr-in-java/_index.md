---
category: general
date: 2026-05-03
description: Crie um pool de threads fixo em Java para extrair texto de imagens rapidamente.
  Aprenda como executar OCR, converter imagem em texto e melhorar o desempenho com
  processamento de OCR em paralelo.
draft: false
keywords:
- create fixed thread pool
- extract text from images
- how to run OCR
- convert image to text
- parallel OCR processing
language: pt
og_description: Crie um pool de threads fixo em Java para extrair texto de imagens
  rapidamente. Aprenda como executar OCR, converter imagem em texto e aumentar o desempenho
  com processamento de OCR em paralelo.
og_title: Criar pool de threads fixas para OCR paralela em Java
tags:
- Java
- OCR
- Multithreading
title: Criar pool de threads fixas para OCR paralela em Java
url: /pt/java/advanced-ocr-techniques/create-fixed-thread-pool-for-parallel-ocr-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar Pool de Threads Fixas para OCR Paralelo em Java

Já precisou **criar pool de threads fixas** para acelerar trabalhos de OCR, mas não sabia por onde começar? Você não está sozinho. Em muitos projetos pesados em imagens, o gargalo é a chamada de OCR de thread única, e a solução é surpreendentemente simples: iniciar um pool de threads de trabalho e deixá‑las processar os arquivos em paralelo.  

Neste tutorial você aprenderá como **extrair texto de imagens** usando Aspose OCR, como **executar OCR** de forma eficiente e como **converter imagem em texto** sem sobrecarregar sua CPU. Ao final, você terá um programa Java pronto‑para‑executar que demonstra **processamento de OCR paralelo** em um conjunto de imagens de exemplo.

## O que você vai construir

Vamos montar um pequeno aplicativo de console que:

* Lê uma lista de caminhos de imagens (PNG, JPG, TIFF, BMP).
* **Cria um pool de threads fixas** dimensionado ao número de núcleos da CPU.
* Dispara uma tarefa de OCR para cada imagem.
* Coleta o texto reconhecido e o imprime no console.
* Encerra o executor de forma limpa.

Sem ferramentas de build externas, sem frameworks sofisticados — apenas Java puro e a biblioteca Aspose OCR. Se você tem Java 8+ e um IDE decente, está pronto.

## Pré‑requisitos

* **Java Development Kit (JDK) 8 ou mais recente** – o código usa lambdas, então versões mais antigas não compilarão.
* **Aspose OCR for Java** – baixe o JAR no site da Aspose ou inclua via Maven (`com.aspose:aspose-ocr`).
* Uma pasta com algumas imagens de teste (o código aponta para `YOUR_DIRECTORY`).  
* Familiaridade básica com concorrência em Java (explicaremos o restante).

> *Dica profissional:* Se você usa Maven, adicione a dependência ao seu `pom.xml` e deixe o IDE cuidar do classpath.  

---

## Etapa 1: Adicionar as Importações Necessárias

Primeiro, traga as classes que precisamos para o escopo. Isso não é apenas boilerplate; cada importação indica à JVM onde encontrar o motor de OCR, as utilidades de manipulação de imagens e as ferramentas de concorrência que nos permitem **criar pool de threads fixas**.

```java
import com.aspose.ocr.*;
import java.util.*;
import java.util.concurrent.*;
```

* `com.aspose.ocr.*` – a API principal de OCR.  
* `java.util.*` – coleções para armazenar caminhos de imagens e resultados.  
* `java.util.concurrent.*` – o pacote de concorrência que contém `ExecutorService` e `Future`.

---

## Etapa 2: Definir as Imagens a Processar

Em seguida, listamos os arquivos dos quais queremos **extrair texto de imagens**. Usar `Arrays.asList` mantém o código conciso e permite trocar para seu próprio diretório sem alterar o restante da lógica.

```java
List<String> imagePaths = Arrays.asList(
        "YOUR_DIRECTORY/image1.png",
        "YOUR_DIRECTORY/image2.jpg",
        "YOUR_DIRECTORY/image3.tif",
        "YOUR_DIRECTORY/image4.bmp"
);
```

Sinta‑se à vontade para adicionar mais entradas; o pool de threads escalará automaticamente com base no número de núcleos da CPU que você possui.

---

## Etapa 3: **Criar Pool de Threads Fixas** Correspondente aos Núcleos da CPU

Aqui está o coração do tutorial. Perguntamos ao runtime quantos núcleos estão disponíveis e pedimos à fábrica `Executors` que nos dê um pool exatamente desse tamanho. Por que fixo? Porque um número previsível de threads evita a temida “explosão de threads” que pode privar o SO de recursos.

```java
int coreCount = Runtime.getRuntime().availableProcessors();
ExecutorService executor = Executors.newFixedThreadPool(coreCount);
```

* `availableProcessors()` devolve a contagem de núcleos lógicos (incluindo hyper‑threads).  
* `newFixedThreadPool(coreCount)` garante que nunca excedamos a capacidade da CPU, que é a forma mais segura de **executar OCR** em paralelo.

---

## Etapa 4: Enviar uma Tarefa de OCR para Cada Imagem

Agora transformamos cada caminho de arquivo em um `Callable` que **executa OCR**, reconhece o texto e devolve o resultado. Observe que instanciamos um novo `OcrEngine` dentro da lambda — isso evita o compartilhamento não‑thread‑safe do estado do motor.

```java
List<Future<String>> ocrResults = new ArrayList<>();
for (String path : imagePaths) {
    ocrResults.add(executor.submit(() -> {
        OcrEngine engine = new OcrEngine();          // fresh engine per task
        engine.setImage(ImageStream.fromFile(path));
        engine.getLanguage().setEnglish(true);
        return engine.recognize() ? engine.getText()
                                   : "Failed: " + path;
    }));
}
```

* Cada chamada a `submit` entrega a lambda ao pool, que a agenda em uma thread ociosa.  
* Os objetos `Future<String>` nos permitem recuperar o texto reconhecido mais tarde, preservando a ordem se necessário.

---

## Etapa 5: Recuperar e Exibir o Texto Reconhecido

Com todas as tarefas enfileiradas, simplesmente iteramos sobre a lista de `Future`, chamando `get()` para bloquear até que cada trabalho de OCR termine. É aqui que o passo **converter imagem em texto** se torna visível: a chamada `engine.getText()` devolve a string bruta.

```java
for (Future<String> result : ocrResults) {
    System.out.println("OCR result:\n" + result.get());
}
```

A saída típica no console se parece com:

```
OCR result:
Hello world!
OCR result:
Invoice #12345
Date: 2026‑04‑30
...
```

Se um arquivo falhar (por exemplo, estiver corrompido), você verá uma linha que começa com `Failed:` seguida do caminho — útil para depuração rápida.

---

## Etapa 6: Limpar o Serviço de Executor

Nunca se esqueça de encerrar o pool; caso contrário a JVM pode permanecer ativa, pensando que ainda há trabalho a ser feito. Um encerramento gracioso permite que tarefas em execução terminem antes que o processo finalize.

```java
executor.shutdown();
```

Você também pode chamar `awaitTermination` se precisar impor um timeout, mas para a maioria das utilidades de linha de comando um simples `shutdown()` é suficiente.

---

## Exemplo Completo Funcional

Abaixo está o programa completo, pronto‑para‑executar. Copie‑e‑cole em um arquivo chamado `ParallelOcrTutorial.java`, ajuste os caminhos das imagens e execute `javac` + `java` como de costume.

```java
import com.aspose.ocr.*;
import java.util.*;
import java.util.concurrent.*;

public class ParallelOcrTutorial {
    public static void main(String[] args) throws Exception {
        // Step 2: Define the images to be processed
        List<String> imagePaths = Arrays.asList(
                "YOUR_DIRECTORY/image1.png",
                "YOUR_DIRECTORY/image2.jpg",
                "YOUR_DIRECTORY/image3.tif",
                "YOUR_DIRECTORY/image4.bmp"
        );

        // Step 3: Create a fixed‑size thread pool matching the CPU cores
        int coreCount = Runtime.getRuntime().availableProcessors();
        ExecutorService executor = Executors.newFixedThreadPool(coreCount);

        // Step 4: Submit an OCR task for each image
        List<Future<String>> ocrResults = new ArrayList<>();
        for (String path : imagePaths) {
            ocrResults.add(executor.submit(() -> {
                OcrEngine engine = new OcrEngine();          // fresh engine per task
                engine.setImage(ImageStream.fromFile(path));
                engine.getLanguage().setEnglish(true);
                return engine.recognize() ? engine.getText()
                                           : "Failed: " + path;
            }));
        }

        // Step 5: Retrieve and display the recognized text
        for (Future<String> result : ocrResults) {
            System.out.println("OCR result:\n" + result.get());
        }

        // Step 6: Clean up the executor service
        executor.shutdown();
    }
}
```

**Resultado esperado:** o conteúdo textual de cada imagem impresso no console, na mesma ordem da lista `imagePaths`. Se alguma imagem não puder ser processada, você verá um aviso de falha em vez de uma linha em branco.

---

## Perguntas Frequentes & Casos de Borda

### E se eu tiver mais imagens do que threads?

O pool de threads fixas enfileirará automaticamente as tarefas excedentes. Assim que uma thread terminar seu trabalho atual de OCR, ela pegará a próxima. Esse comportamento de enfileiramento é a essência do **processamento de OCR paralelo** — você obtém o máximo de throughput sem sobrecarregar a CPU.

### Posso mudar o idioma?

Com certeza. Substitua `engine.getLanguage().setEnglish(true);` pela flag de idioma apropriada, por exemplo `setFrench(true)` ou habilite múltiplos idiomas chamando vários setters antes de `recognize()`.

### Como lidar com imagens muito grandes?

Arquivos grandes podem consumir muita memória por thread. Se você notar `OutOfMemoryError`, considere reduzir a escala da imagem antes de enviá‑la ao motor, ou aumente o tamanho do heap com `-Xmx`. Outra abordagem é usar um **cached thread pool** (`

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}