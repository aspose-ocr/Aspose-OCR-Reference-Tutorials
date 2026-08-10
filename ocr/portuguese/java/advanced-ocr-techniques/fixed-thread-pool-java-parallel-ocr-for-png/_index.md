---
category: general
date: 2026-02-17
description: Aprenda a usar um pool de threads fixo em Java para extrair texto de
  imagens PNG com processamento OCR paralelo e encerrar corretamente o serviço executor.
draft: false
keywords:
- fixed thread pool java
- extract text from png
- parallel ocr processing
- convert scanned pages text
- shut down executor service
language: pt
og_description: Descubra como um pool de threads fixo em Java pode extrair texto de
  imagens PNG em paralelo, converter o texto de páginas escaneadas e encerrar o serviço
  executor com segurança.
og_title: Pool de threads fixo Java – OCR paralelo para PNG
tags:
- java
- ocr
- multithreading
- aspose
title: Pool de threads fixo Java – OCR paralelo para PNG
url: /pt/java/advanced-ocr-techniques/fixed-thread-pool-java-parallel-ocr-for-png/
---

final content.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# fixed thread pool java – OCR paralelo para PNG

Já se perguntou como acelerar o OCR em um conjunto de arquivos PNG usando um **fixed thread pool java**? Neste tutorial vamos percorrer **extract text from PNG** imagens em paralelo, **convert scanned pages text** em strings editáveis e encerrar com segurança o **shut down executor service** assim que o trabalho terminar.

Se você já ficou encarando um loop de thread única que se arrasta por minutos, conhece a frustração de esperar cada página terminar antes que a próxima sequer comece. A boa notícia? Com algumas linhas de Java e Aspose OCR você pode liberar o poder de todos os seus núcleos de CPU, transformar essas páginas escaneadas em texto pesquisável e manter sua aplicação responsiva.  

Abaixo você encontrará um exemplo completo, pronto‑para‑executar, além de explicações sobre por que cada parte importa, armadilhas comuns e dicas que você pode aplicar a qualquer biblioteca de OCR.

---

## O que você vai precisar

- **Java 17** (ou qualquer JDK recente) – o código usa a sintaxe moderna `var` com moderação, mas funciona em versões mais antigas também.  
- **Aspose.OCR for Java** library – você pode obtê‑la no Maven Central ou baixar uma versão de avaliação no site da Aspose.  
- Um conjunto de arquivos **PNG** que você deseja processar – pense em recibos escaneados, páginas de livros ou capturas de tela.  
- Familiaridade básica com concorrência em Java – não é obrigatório, mas é útil.

É isso. Sem serviços externos, sem Docker, apenas Java puro e um pouco de magia de multithreading.

---

## Etapa 1: Adicionar dependência do Aspose OCR e licença (Opcional)

Primeiro, certifique‑se de que o JAR do Aspose OCR está no seu classpath. Se você usa Maven, adicione:

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version>
</dependency>
```

Se você não tem uma licença, a biblioteca rodará em modo de avaliação; o código funciona da mesma forma. Para carregar uma licença (recomendado para produção), coloque `Aspose.OCR.lic` na sua pasta de recursos e use:

```java
// Load the Aspose OCR license (optional)
License license = new License();
license.setLicense("Aspose.OCR.lic");
```

> **Dica profissional:** Mantenha o arquivo de licença fora do controle de versão para evitar exposição acidental.

---

## Etapa 2: Criar uma instância de `OcrEngine` thread‑safe

O `OcrEngine` do Aspose OCR é thread‑safe desde que você reutilize a mesma instância entre as tarefas. Criá‑lo uma única vez economiza memória e evita a sobrecarga de reinicializar o motor para cada imagem.

```java
// One shared OcrEngine for all threads
OcrEngine ocrEngine = new OcrEngine();
```

Por que reutilizar? Pense no motor como um trabalhador pesado que carrega modelos de linguagem na memória. Criar um novo motor por imagem seria como contratar um novo especialista para cada pequeno trabalho – custoso e desnecessário.

---

## Etapa 3: Configurar um Fixed Thread Pool Java

Agora vem a estrela do espetáculo: um **fixed thread pool java**. Vamos dimensioná‑lo ao número de processadores lógicos para que cada core receba trabalho sem sobrecarga.

```java
// Determine available processors and create a fixed pool
int threadCount = Runtime.getRuntime().availableProcessors();
ExecutorService threadPool = Executors.newFixedThreadPool(threadCount);
```

Usar um pool *fixo* (em vez de um pool em cache) fornece uso de recursos previsível e impede os temidos picos de “out‑of‑memory” quando centenas de imagens chegam de uma vez.

---

## Etapa 4: Listar os arquivos PNG que você deseja processar (Extract Text from PNG)

Colete os caminhos das imagens que você deseja fazer OCR. Em um projeto real você pode escanear um diretório ou ler de um banco de dados; aqui vamos codificar alguns exemplos.

```java
List<String> imageFiles = Arrays.asList(
        "YOUR_DIRECTORY/page1.png",
        "YOUR_DIRECTORY/page2.png",
        "YOUR_DIRECTORY/page3.png"
);
```

> **Observação:** A extensão de arquivo **png** é importante porque o Aspose OCR detecta automaticamente o formato, mas você também pode fornecer JPEG ou TIFF.

---

## Etapa 5: Enviar tarefas de OCR – Processamento OCR paralelo

Cada imagem se torna um callable que retorna o texto reconhecido. Como o `OcrEngine` é compartilhado, só precisamos passar o caminho do arquivo para a tarefa.

```java
List<Future<String>> ocrFutures = new ArrayList<>();

for (String imagePath : imageFiles) {
    ocrFutures.add(threadPool.submit(() -> {
        // Prepare input for this image
        OcrInput input = new OcrInput();
        input.add(imagePath);

        // Perform OCR using the shared engine
        OcrResult result = ocrEngine.recognize(input);

        // Return the plain text
        return result.getText();
    }));
}
```

Por que envolver em um `Future`? Ele nos permite disparar todos os trabalhos instantaneamente, e depois coletar os resultados na ordem em que foram enviados – perfeito para preservar a ordem das páginas ao **convert scanned pages text** de volta para um documento.

---

## Etapa 6: Recuperar resultados e exibir (Convert Scanned Pages Text)

Agora esperamos cada `Future` terminar e imprimimos a saída. A chamada `get()` bloqueia apenas até que a tarefa específica seja concluída, não todo o pool.

```java
for (Future<String> future : ocrFutures) {
    System.out.println("----");
    System.out.println(future.get()); // prints OCR result for one PNG
}
```

A saída típica no console se parece com:

```
----
The quick brown fox jumps over the lazy dog.
----
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
----
Page 3 content goes here…
```

Se preferir gravar os resultados em arquivos, substitua o `System.out.println` por uma chamada `Files.writeString`.

---

## Etapa 7: Encerrar o Executor Service de forma limpa

Quando todas as tarefas estiverem concluídas, é crucial **shut down executor service**; caso contrário, sua JVM pode manter threads não‑daemon vivas, impedindo uma saída graciosa.

```java
threadPool.shutdown();               // No new tasks accepted
if (!threadPool.awaitTermination(60, TimeUnit.SECONDS)) {
    threadPool.shutdownNow();        // Force shutdown after timeout
}
```

O padrão `awaitTermination` dá ao pool a chance de terminar o trabalho em andamento antes de forçá‑lo. Ignorar esta etapa é uma fonte comum de vazamentos de memória em aplicações de longa duração.

---

## Exemplo completo em funcionamento

Juntando tudo, aqui está o programa completo que você pode copiar‑colar em `ParallelBatchDemo.java` e executar:

```java
import com.aspose.ocr.*;

import java.util.*;
import java.util.concurrent.*;

public class ParallelBatchDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load license (optional)
        License license = new License();
        license.setLicense("Aspose.OCR.lic");

        // 2️⃣ Shared, thread‑safe OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 3️⃣ Fixed thread pool java – one thread per core
        int threadCount = Runtime.getRuntime().availableProcessors();
        ExecutorService threadPool = Executors.newFixedThreadPool(threadCount);

        // 4️⃣ Files to process – extract text from png
        List<String> imageFiles = Arrays.asList(
                "YOUR_DIRECTORY/page1.png",
                "YOUR_DIRECTORY/page2.png",
                "YOUR_DIRECTORY/page3.png"
        );

        // 5️⃣ Submit tasks – parallel OCR processing
        List<Future<String>> ocrFutures = new ArrayList<>();
        for (String imagePath : imageFiles) {
            ocrFutures.add(threadPool.submit(() -> {
                OcrInput input = new OcrInput();
                input.add(imagePath);
                OcrResult result = ocrEngine.recognize(input);
                return result.getText();
            }));
        }

        // 6️⃣ Retrieve and print – convert scanned pages text
        for (Future<String> future : ocrFutures) {
            System.out.println("----");
            System.out.println(future.get());
        }

        // 7️⃣ Shut down executor service cleanly
        threadPool.shutdown();
        if (!threadPool.awaitTermination(60, TimeUnit.SECONDS)) {
            threadPool.shutdownNow();

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}