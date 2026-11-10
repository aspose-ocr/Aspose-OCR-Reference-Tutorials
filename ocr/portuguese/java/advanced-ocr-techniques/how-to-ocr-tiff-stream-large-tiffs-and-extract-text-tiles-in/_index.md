---
category: general
date: 2026-04-29
description: Aprenda a fazer OCR de arquivos TIFF usando o modo de streaming do Aspose
  OCR. Este guia mostra como extrair blocos de texto de imagens TIFF em mosaico de
  forma eficiente.
draft: false
keywords:
- how to ocr tiff
- extract text tiles
language: pt
og_description: como fazer OCR de TIFF usando streaming do Aspose OCR. Código passo
  a passo para extrair blocos de texto de imagens TIFF grandes.
og_title: Como fazer OCR de TIFF – Guia completo de streaming
tags:
- OCR
- Java
- Aspose
- TIFF
title: Como fazer OCR de TIFF – Transmitir TIFFs grandes e extrair blocos de texto
  em Java
url: /pt/java/advanced-ocr-techniques/how-to-ocr-tiff-stream-large-tiffs-and-extract-text-tiles-in/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# como fazer ocr tiff – Transmitir TIFFs Grandes e Extrair Blocos de Texto em Java

Já se perguntou **como fazer ocr tiff** em arquivos que são grandes demais para serem carregados na memória de uma só vez? Você não está sozinho. Muitos desenvolvedores se deparam com um obstáculo quando suas imagens TIFF são divididas em dezenas de blocos, e a chamada usual `ocrEngine.recognize()` simplesmente falha.  

A boa notícia? O modo de streaming do Aspose OCR permite que você alimente cada bloco como um fluxo separado, para que você possa **extrair blocos de texto** sem estourar o heap. Neste tutorial vamos percorrer um exemplo completo, pronto‑para‑executar em Java, explicar por que cada linha importa e apontar as armadilhas que você deve evitar.

> **O que você receberá:** um programa executável que costura TIFFs em blocos em tempo real, imprime o texto combinado e mostra como adaptar o código para outras linguagens ou formatos de imagem.

---

## Pré‑requisitos

- **Java 17** ou superior (o código usa try‑with‑resources, então JDK 8+ funciona, mas JDK 17 é a LTS atual).
- Biblioteca **Aspose.OCR for Java** (v23.10 ou posterior). Adicione via Maven:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version>
</dependency>
```

- Uma pasta contendo os blocos TIFF individuais (por exemplo, `tile_0.tif`, `tile_1.tif`, …).  
- Opcional: uma IDE como IntelliJ IDEA ou VS Code – mas um editor de texto simples também serve.

---

## Etapa 1 – Preparar os Caminhos dos Blocos (Por que Importa)

Antes que o motor OCR faça qualquer coisa, ele precisa saber onde cada parte da imagem está. Codificar os caminhos diretamente está ok para uma demonstração, mas em produção você provavelmente escaneará um diretório ou lerá um arquivo de manifesto.

```java
// Define the absolute or relative paths to each TIFF tile
String[] tilePaths = {
    "YOUR_DIRECTORY/tile_0.tif",
    "YOUR_DIRECTORY/tile_1.tif",
    "YOUR_DIRECTORY/tile_2.tif"
};
```

> **Dica profissional:** mantenha os blocos em ordem lexical (0, 1, 2…) porque o motor concatenará o texto reconhecido na mesma sequência em que você fornece os fluxos.

---

## Etapa 2 – Habilitar o Modo de Streaming no Motor OCR (Palavra‑chave Principal)

Agora criamos a instância `OcrEngine` e ativamos o streaming. Este é o núcleo de **como fazer ocr tiff** sem carregar a imagem inteira na RAM.

```java
// Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Activate streaming – essential for large or tiled TIFFs
ocrEngine.getProcessingSettings().setEnableStreaming(true);

// Set the language to English; change as needed (e.g., "fr", "de")
ocrEngine.getLanguageSettings().setLanguage("en");
```

**Por que streaming?**  
Quando `setEnableStreaming(true)` é chamado, o motor trata cada `ImageStream` recebido como continuação do anterior. Ele constrói uma tela virtual interna, costura os blocos virtualmente e executa o OCR apenas ao final. Isso evita o “OutOfMemoryError” que ocorreria se você tentasse carregar um TIFF de vários gigabytes de uma só vez.

---

## Etapa 3 – Anexar Cada Bloco como um Fluxo de Entrada (Palavra‑chave Secundária)

Aqui está o loop que alimenta cada bloco ao motor. O bloco `try‑with‑resources` garante que o manipulador de arquivo seja fechado rapidamente, o que é crucial quando se lida com dezenas de arquivos.

```java
for (String tilePath : tilePaths) {
    try (InputStream stream = new FileInputStream(tilePath)) {
        // Wrap the raw InputStream in Aspose's ImageStream wrapper
        ocrEngine.appendImage(ImageStream.fromStream(stream));
    } catch (IOException e) {
        // If a single tile fails, we log and continue – you might want to abort instead
        System.err.println("Failed to load tile: " + tilePath);
        e.printStackTrace();
    }
}
```

Observe que a expressão **extrair blocos de texto** está naturalmente inserida: cada iteração *extrai* o texto de um bloco e o adiciona ao conjunto de resultados em crescimento.

---

## Etapa 4 – Executar o Reconhecimento e Exibir o Texto Combinado (Palavra‑chave Principal)

Depois que todos os blocos são enfileirados, uma única chamada realiza o OCR na imagem virtual. O resultado contém o texto completo, como se você tivesse um único TIFF massivo.

```java
// Perform OCR on the combined virtual image
OcrResult ocrResult = ocrEngine.recognize();

// Print the extracted text to the console
System.out.println("=== OCR Output ===");
System.out.println(ocrResult.getText());
```

**Saída esperada** (supondo que os blocos contenham a frase “Hello World” dividida entre eles):

```
=== OCR Output ===
Hello World
```

Se seus blocos contiverem mais linhas, elas aparecerão na mesma ordem em que foram fornecidas. Você também pode gravar `ocrResult.getText()` em um arquivo para processamento posterior.

---

## Etapa 5 – Exemplo Completo e Executável (Todas as Etapas em Um Só Lugar)

Abaixo está o programa completo que você pode copiar‑colar em `StreamingExample.java`. Ele inclui todas as importações, comentários e tratamento de erros.

```java
import com.aspose.ocr.*;
import java.io.*;

public class StreamingExample {
    public static void main(String[] args) throws Exception {
        // ------------------------------------------------------------
        // Step 1: List the TIFF tile files
        // ------------------------------------------------------------
        String[] tilePaths = {
            "YOUR_DIRECTORY/tile_0.tif",
            "YOUR_DIRECTORY/tile_1.tif",
            "YOUR_DIRECTORY/tile_2.tif"
        };

        // ------------------------------------------------------------
        // Step 2: Set up the OCR engine in streaming mode
        // ------------------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.getProcessingSettings().setEnableStreaming(true);
        ocrEngine.getLanguageSettings().setLanguage("en");

        // ------------------------------------------------------------
        // Step 3: Feed each tile as a separate stream
        // ------------------------------------------------------------
        for (String tilePath : tilePaths) {
            try (InputStream stream = new FileInputStream(tilePath)) {
                ocrEngine.appendImage(ImageStream.fromStream(stream));
            } catch (IOException e) {
                System.err.println("Unable to read tile: " + tilePath);
                e.printStackTrace();
                // Optionally: return; // abort on missing tile
            }
        }

        // ------------------------------------------------------------
        // Step 4: Recognize the combined image and display the text
        // ------------------------------------------------------------
        OcrResult ocrResult = ocrEngine.recognize();
        System.out.println("=== OCR Output ===");
        System.out.println(ocrResult.getText());
    }
}
```

Salve, compile e execute:

```bash
javac -cp "path/to/aspose-ocr.jar" StreamingExample.java
java -cp ".:path/to/aspose-ocr.jar" StreamingExample
```

Você deverá ver o texto OCR concatenado impresso no console.

---

## Dicas Avançadas & Armadilhas Comuns (Por que Isso Funciona)

| Problema | Por que Acontece | Como Corrigir / Otimizar |
|----------|------------------|--------------------------|
| **Erros de falta de memória** | Carregar um TIFF de tamanho completo em um `BufferedImage` consome todo o heap. | Use o modo streaming (`setEnableStreaming(true)`) – o motor nunca materializa a imagem inteira. |
| **Descompasso na ordem dos blocos** | Arquivos são ordenados alfabeticamente em vez de numericamente (ex.: `tile_10.tif` antes de `tile_2.tif`). | Preencha os números com zeros (`tile_00.tif`, `tile_01.tif`) ou ordene programaticamente usando `Comparator`. |
| **Idioma errado** | OCR padrão é inglês; texto em outro idioma fica corrompido. | Chame `ocrEngine.getLanguageSettings().setLanguage("fr")` (ou qualquer código ISO suportado). |
| **Falhas parciais** | Um bloco corrompido interrompe todo o processo. | Capture `IOException` por bloco, registre e decida se continua ou aborta. |
| **Gargalo de desempenho** | I/O de disco domina ao ler muitos arquivos pequenos. | Agrupe os blocos em um ZIP e faça streaming da memória, ou use um SSD rápido. |

---

## Quando Usar Streaming vs. OCR de Imagem Única

- **Streaming** é ideal para:
  - TIFFs multipágina ou digitalizações gigapixel.
  - Situações com memória limitada (ex.: containers Docker, dispositivos móveis).
  - Pipelines que já recebem fragmentos de imagem (ex.: fluxos de câmera).

- **OCR de imagem única** funciona bem para:
  - Arquivos PNG/JPEG pequenos (< 5 MB).
  - Digitalizações pontuais onde a simplicidade supera a performance.

---

## Conclusão

Agora você tem um entendimento sólido de **como fazer ocr tiff** usando os recursos de streaming do Aspose OCR, e sabe como **extrair blocos de texto** de forma eficiente. A solução completa — inicializando o motor, habilitando streaming, anexando cada bloco e, finalmente, reconhecendo a tela virtual — cobre o “o quê”, “por quê” e “como” necessários para código pronto para produção.

Próximos passos? Experimente trocar `"en"` por outro idioma, ou teste diferentes formatos de imagem (`.png`, `.jpg`). Você também pode alimentar o resultado OCR diretamente a um índice de busca ou a um gerador de PDF. O padrão permanece o mesmo: stream, stitch, recognize.

Tem dúvidas sobre escalar para centenas de blocos, ou precisa de ajuda com tratamento de erros? Deixe um comentário abaixo, e feliz codificação!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}