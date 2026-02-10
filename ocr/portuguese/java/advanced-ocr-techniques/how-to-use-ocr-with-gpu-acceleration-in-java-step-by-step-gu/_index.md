---
category: general
date: 2026-02-09
description: Como usar OCR rapidamente com Aspose OCR, reconhecer texto de imagem
  e extrair texto de PNG enquanto define o modo e o limite de memória da GPU.
draft: false
keywords:
- how to use ocr
- recognize text from image
- extract text from png
- how to set mode
- set gpu memory limit
language: pt
og_description: Como usar OCR de forma eficiente – aprenda a reconhecer texto a partir
  de imagens, extrair texto de PNG, definir modo e controlar o limite de memória da
  GPU em Java.
og_title: Como usar OCR com aceleração de GPU em Java
tags:
- OCR
- Java
- GPU
- Aspose
title: Como usar OCR com aceleração GPU em Java – Guia passo a passo
url: /pt/java/advanced-ocr-techniques/how-to-use-ocr-with-gpu-acceleration-in-java-step-by-step-gu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como usar OCR com aceleração GPU em Java – Tutorial de programação completo

Já se perguntou **como usar OCR** para extrair texto de uma imagem sem escrever milhões de linhas de código? Você não está sozinho. Em muitos projetos—digitalização de faturas, processamento de recibos ou apenas a digitalização de documentos antigos—os desenvolvedores precisam de uma maneira confiável de **reconhecer texto de imagem** arquivos, especialmente PNGs que frequentemente contêm gráficos limpos e de alta resolução.  

A boa notícia? Aspose OCR torna isso muito fácil, e com alguns ajustes de configuração você pode até delegar o trabalho pesado para sua GPU. Neste tutorial, percorreremos todo o processo: desde o carregamento de um PNG, até **definir modo** para processamento GPU, **definir limite de memória GPU**, e finalmente imprimir o texto extraído. Ao final, você terá um programa Java executável que faz exatamente o que você precisa.

## O que você aprenderá

- Como instalar e importar Aspose OCR para Java.
- Como **reconhecer texto de imagem** arquivos usando a biblioteca.
- Como **extrair texto de PNG** de forma eficiente.
- Como **definir modo** para GPU e controlar a pegada de memória com **definir limite de memória GPU**.
- Armadilhas comuns e dicas para uso em produção.

### Pré-requisitos

- Java 8 ou mais recente (o código compila também com JDK 11).
- Uma GPU NVIDIA com driver compatível com CUDA se você quiser aceleração GPU.
- Aspose OCR for Java JAR (download do site da Aspose ou adicione via Maven/Gradle).
- Uma imagem PNG de exemplo (por exemplo, `sample1.png`) colocada em uma pasta que você possa referenciar.

---

## Como usar OCR – Ativar modo GPU

A primeira coisa que você precisa fazer é dizer ao Aspose OCR que deseja que ele seja executado na GPU em vez da CPU. É aqui que a palavra‑chave **how to set mode** entra em ação.

```java
// Step 1: Create the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Step 2: Grab the configuration object
OcrEngineConfiguration config = ocrEngine.getConfiguration();

// Step 3: Switch processing mode to GPU
config.setProcessingMode(ProcessingMode.GPU);   // requires a CUDA‑compatible driver

// (Optional) Step 4: Limit GPU memory usage to 1024 MB
config.setGpuMemoryLimit(1024);                 // set gpu memory limit (MB)
```

**Por que isso importa:**  
O processamento GPU pode ser drasticamente mais rápido para lotes grandes ou imagens de alta resolução, mas também consome memória de vídeo. Ao chamar `setGpuMemoryLimit`, você impede que sua aplicação monopolize toda a GPU, o que é crucial quando o mesmo dispositivo executa outras cargas de trabalho (por exemplo, uma UI ou um modelo de machine‑learning).

---

## Reconhecer texto de imagem usando Aspose OCR

Agora que o motor está configurado, precisamos apontá‑lo para o arquivo que queremos ler. Este é o núcleo de **recognize text from image**.

```java
// Step 5: Define the image to be processed
ImageRecognitionResult imageInfo = new ImageRecognitionResult();
imageInfo.setImagePath("YOUR_DIRECTORY/sample1.png");

// Step 6: Run the OCR operation
RecognitionResult ocrResult = ocrEngine.recognize(imageInfo);
```

**O que acontece nos bastidores?**  
Aspose OCR carrega o PNG, pré‑processa‑o (binarização, correção de inclinação, etc.), então executa a rede neural OCR na GPU. O objeto de resultado contém o texto bruto mais as pontuações de confiança para cada linha.

---

## Extrair texto de PNG com limite de memória GPU

Após o reconhecimento, extrair a string simples é trivial, porém muitos desenvolvedores esquecem de verificar a saída. Aqui está como você pode **extrair texto de PNG** com segurança e exibi‑lo.

```java
// Step 7: Output the recognized text
System.out.println("Recognized text:");
System.out.println(ocrResult.getText());
```

**Saída esperada (exemplo):**

```
Recognized text:
Invoice #12345
Date: 2026-02-09
Total: $1,250.00
Thank you for your business!
```

Se a imagem contiver ruído ou fontes incomuns, você pode ver caracteres embaralhados. Nesse caso, considere ajustar as opções de pré‑processamento (por exemplo, `config.setLanguage(Language.ENGLISH)` ou `config.setAutoSkewCorrection(true)`).

---

## Exemplo completo e executável

Abaixo está o programa Java completo que reúne tudo. Copie‑e cole em um arquivo chamado `GpuExample.java`, ajuste o caminho da imagem e execute com `javac`/`java` ou a partir da sua IDE.

```java
import com.aspose.ocr.*;
import com.aspose.ocr.configuration.*;

public class GpuExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Specify the image to be processed
        ImageRecognitionResult imageInfo = new ImageRecognitionResult();
        imageInfo.setImagePath("YOUR_DIRECTORY/sample1.png");

        // Step 2: Create the OCR engine and enable GPU processing
        OcrEngine ocrEngine = new OcrEngine();
        OcrEngineConfiguration config = ocrEngine.getConfiguration();

        // Step 3: Set processing mode to GPU (requires CUDA driver)
        config.setProcessingMode(ProcessingMode.GPU);

        // Step 4 (optional): Limit GPU memory usage to 1024 MB
        config.setGpuMemoryLimit(1024);

        // Step 5: Perform recognition
        RecognitionResult ocrResult = ocrEngine.recognize(imageInfo);

        // Step 6: Print the extracted text
        System.out.println("Recognized text:");
        System.out.println(ocrResult.getText());
    }
}
```

**Executando o programa**

```bash
javac -cp "path/to/aspose-ocr.jar" GpuExample.java
java -cp ".:path/to/aspose-ocr.jar" GpuExample
```

Certifique‑se de que o JAR está no seu classpath; caso contrário, você receberá `ClassNotFoundException`.

---

## Dicas profissionais e armadilhas comuns

- **Versão do driver GPU:** O sinalizador `ProcessingMode.GPU` lançará uma exceção se o driver CUDA estiver ausente ou incompatível. Verifique novamente com `nvidia-smi`.
- **Orçamento de memória:** Se você processar muitas imagens simultaneamente, aumente o valor de `setGpuMemoryLimit` ou execute os trabalhos sequencialmente para evitar erros de falta de memória.
- **Formato de imagem:** Embora PNG funcione muito bem, JPEGs com alta compressão podem causar erros de reconhecimento. Considere converter para PNG sem perdas antes do OCR.
- **Suporte a idiomas:** Por padrão o Aspose OCR assume inglês. Para outros idiomas, chame `config.setLanguage(Language.SPANISH)` (ou o enum apropriado) antes de `recognize`.
- **Teste de desempenho:** Execute um benchmark rápido (`System.nanoTime()`) com e sem GPU para verificar se o ganho de velocidade justifica a complexidade adicional.

---

## Perguntas Frequentes

**Isso funciona no macOS ou Linux?**  
Sim—Aspose OCR é multiplataforma. Basta garantir que você tenha uma GPU compatível com CUDA e o driver adequado instalado para o seu sistema operacional.

**E se eu não tiver uma GPU?**  
Você pode simplesmente omitir a linha `setProcessingMode(ProcessingMode.GPU)`; o motor retornará ao modo CPU automaticamente.

**Posso processar PDFs diretamente?**  
Aspose OCR foca em imagens rasterizadas. Para PDFs, extraia cada página como imagem primeiro (por exemplo, usando Aspose PDF) e então alimente os PNGs no fluxo OCR.

---

## Conclusão

Em resumo, **como usar OCR** com Aspose em Java se resume a três passos claros: configurar o motor (incluindo **how to set mode** e **set GPU memory limit**), apontá‑lo para seu PNG e ler a string resultante. O trecho acima é uma solução totalmente funcional, de ponta a ponta, que você pode inserir em qualquer projeto Java.

Agora que você dominou **recognize text from image** e **extract text from PNG**, pode expandir o fluxo de trabalho: processar pastas em lote, armazenar resultados em um banco de dados ou até alimentar o texto em pipelines de NLP posteriores. O céu é o limite—apenas lembre‑se de ficar de olho na memória da GPU e na compatibilidade do driver.

Tem mais perguntas sobre OCR, aceleração GPU ou recursos da Aspose? Sinta‑se à vontade para deixar um comentário ou explorar a documentação oficial do Aspose OCR para opções de personalização mais avançadas. Feliz codificação! 🚀

![diagrama de como usar OCR](https://example.com/images/ocr-gpu-diagram.png "diagrama de como usar OCR")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}