---
category: general
date: 2026-07-05
description: Comprima imagens de PDF ao converter PNG para PDF usando Java. Aprenda
  pré‑processamento de imagens para OCR, reconheça texto em JPG e faça OCR em lote
  para PDF em um único tutorial.
draft: false
keywords:
- compress pdf images
- convert png to pdf
- image preprocessing for ocr
- recognize text jpg
- batch ocr to pdf
language: pt
og_description: Comprima imagens PDF e converta PNG para PDF usando Java. Este guia
  aborda o pré-processamento de imagens para OCR, reconhecimento de texto em JPG e
  OCR em lote para PDF.
og_title: Compactar Imagens de PDF com Java – Tutorial Completo de OCR em Lote
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Compress PDF images while converting PNG to PDF using Java. Learn image
    preprocessing for OCR, recognize text JPG, and batch OCR to PDF in one tutorial.
  headline: Compress PDF Images with Java – Full Batch OCR to PDF Guide
  type: TechArticle
- description: Compress PDF images while converting PNG to PDF using Java. Learn image
    preprocessing for OCR, recognize text JPG, and batch OCR to PDF in one tutorial.
  name: Compress PDF Images with Java – Full Batch OCR to PDF Guide
  steps:
  - name: Expected Output
    text: 'Running the program prints a line for each image, e.g.:'
  - name: What if my server has no GPU?
    text: Just set `gpuSettings.setEnabled(false)`. The rest of the pipeline remains
      unchanged, and you still get multithreaded CPU processing.
  - name: My PDFs are still too large—can I lower the quality further?
    text: Yes. Adjust `options.setImageQuality(70)` or even `50`. Lower values shrink
      size more aggressively but may blur fine glyphs. Test with a representative
      sample.
  - name: How do I handle other image formats (TIFF, BMP)?
    text: 'Add the extensions to the filter lambda:'
  - name: Can I keep the original color images instead of binarizing?
    text: Replace `.addBinarize()` with `.addGrayscale()` in the preprocessor builder
      if you need color retention for downstream analysis.
  type: HowTo
tags:
- ocr
- java
- pdf
- image-processing
title: Compactar imagens PDF com Java – Guia completo de OCR em lote para PDF
url: /pt/java/advanced-ocr-techniques/compress-pdf-images-with-java-full-batch-ocr-to-pdf-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comprimir Imagens PDF com Java – Guia Completo de OCR em Lote para PDF

Já precisou **compress PDF images** enquanto transformava uma pasta de PNGs em PDFs pesquisáveis? Você não está sozinho. Em muitas pipelines de automação, o maior ponto crítico é equilibrar a qualidade da imagem, a precisão do OCR e o tamanho final do PDF — tudo ao mesmo tempo.  

Neste tutorial vamos percorrer uma solução prática que **converts PNG to PDF**, aplica **image preprocessing for OCR** e, finalmente, **compresses PDF images** para que a saída permaneça leve. Ao final, você saberá como **recognize text JPG** arquivos, configurar um fluxo de trabalho **batch OCR to PDF** e manter seus PDFs organizados.

## O que você aprenderá

- Configurar o Aspose OCR para Java e aplicar uma licença.  
- Configurar o motor para multithreading, aceleração GPU e correção ortográfica.  
- Construir um pipeline reutilizável de **image preprocessing for OCR** (denoise, contrast, binarize).  
- Usar **PdfSaveOptions** para **compress PDF images** sem sacrificar a legibilidade.  
- Percorrer um diretório para **convert PNG to PDF** e **recognize text JPG** em massa.  
- Um programa Java completo, pronto‑para‑executar, que você pode inserir em qualquer projeto.  

> **Pré-requisitos**: Java 8+, Maven ou Gradle, uma licença Aspose OCR para Java e uma pasta de imagens PNG/JPG que você deseja processar.

---

## Etapa 1: Aplicar a Licença Aspose OCR (Essencial para Produção)

Antes de chamar qualquer API de OCR, você deve carregar uma licença válida; caso contrário, ficará limitado à versão de avaliação.

```java
import com.aspose.ocr.*;

public class LicenseSetup {
    public static void loadLicense() throws Exception {
        License license = new License();
        // Point to your license file – keep it out of source control!
        license.setLicense("Aspose.OCR.Java.lic");
    }
}
```

*Por que isso importa*: Um motor licenciado desbloqueia suporte a GPU, maior precisão e remove marcas d'água que, de outra forma, aumentariam o tamanho dos seus arquivos PDF.

---

## Etapa 2: Configurar o Motor OCR – Threads, GPU e Correção Ortográfica

Um motor OCR rápido é a espinha dorsal de qualquer trabalho **batch OCR to PDF**. Vamos iniciar quantas threads a CPU do host puder suportar, habilitar a aceleração GPU (se você tiver uma placa compatível) e apertar a correção ortográfica para limpar erros de OCR.

```java
import com.aspose.ocr.*;
import com.aspose.ocr.gpu.GPUSettings;
import com.aspose.ocr.spell.SpellCorrectionOptions;

public class EngineConfig {
    public static OcrEngine createEngine() {
        OcrEngine ocrEngine = new OcrEngine();

        // Use all available logical processors
        ocrEngine.setThreadCount(Runtime.getRuntime().availableProcessors());

        // Enable GPU – huge speedup for large batches
        GPUSettings gpu = new GPUSettings();
        gpu.setEnabled(true);
        ocrEngine.setGpuSettings(gpu);

        // Light spell correction: fix common typos without over‑correcting
        SpellCorrectionOptions spellOpts = new SpellCorrectionOptions();
        spellOpts.setMaxEditDistance(1);
        ocrEngine.getSpellCorrection().setOptions(spellOpts);

        return ocrEngine;
    }
}
```

*Dica profissional*: Se você estiver executando em um servidor sem interface gráfica e sem GPU, basta definir `gpu.setEnabled(false)` – o código ainda funcionará, apenas um pouco mais lento.

---

## Etapa 3: Construir um Pipeline de Pré‑Processamento de Imagem

Digitalizações brutas costumam sofrer de ruído, baixo contraste ou iluminação desigual. **Image preprocessing for OCR** melhora drasticamente as taxas de reconhecimento, especialmente em cenários **recognize text JPG**.

```java
import com.aspose.ocr.*;

public class PreprocessorSetup {
    public static ImagePreprocessor createPreprocessor() {
        return new ImagePreprocessor.Builder()
                .addDenoise(0.7)      // Reduce grain while preserving edges
                .addContrast(1.15)    // Boost contrast for clearer glyphs
                .addBinarize()        // Convert to black‑and‑white for OCR
                .build();
    }
}
```

*Por que encadeamos esses passos*: A remoção de ruído primeiro impede que o binarizador amplifique manchas; o contraste então garante que os caracteres se destaquem; finalmente, a binarização fornece ao motor OCR uma imagem binária limpa para trabalhar.

---

## Etapa 4: Preparar Opções de Salvamento PDF – **Compress PDF Images** Eficientemente

Aspose permite ajustar finamente a saída PDF. Ativaremos a compressão de imagens e definiremos um nível de qualidade que equilibra tamanho e legibilidade.

```java
import com.aspose.ocr.pdf.PdfSaveOptions;

public class PdfOptions {
    public static PdfSaveOptions createOptions() {
        PdfSaveOptions options = new PdfSaveOptions();
        options.setCompressImages(true);   // This is the key to compress PDF images
        options.setImageQuality(90);       // 90% retains sharp text while shrinking file size
        return options;
    }
}
```

*Resultado*: Cada PDF pesquisável será visivelmente menor — ideal para arquivamento ou envio por e‑mail.

---

## Etapa 5: Processar a Pasta – **Convert PNG to PDF** e **Recognize Text JPG** em um Loop

Agora juntamos tudo. O loop percorre um diretório de entrada, executa OCR em cada PNG ou JPG e grava um PDF pesquisável em uma pasta de saída. O nome do PDF espelha o nome da imagem original.

```java
import com.aspose.ocr.*;
import com.aspose.ocr.pdf.PdfSaveOptions;
import java.io.File;

public class BatchOcrTutorial {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load license
        LicenseSetup.loadLicense();

        // 2️⃣ Engine & preprocessing
        OcrEngine ocrEngine = EngineConfig.createEngine();
        ocrEngine.setPreprocessor(PreprocessorSetup.createPreprocessor());

        // 3️⃣ PDF options (compress PDF images)
        PdfSaveOptions pdfOptions = PdfOptions.createOptions();

        // 4️⃣ Define input / output folders
        File inputFolder = new File("YOUR_DIRECTORY/input");
        File outputFolder = new File("YOUR_DIRECTORY/output");
        if (!outputFolder.exists()) outputFolder.mkdirs();

        // 5️⃣ Filter PNG & JPG files
        File[] imageFiles = inputFolder.listFiles((dir, name) ->
                name.toLowerCase().endsWith(".png") || name.toLowerCase().endsWith(".jpg"));

        if (imageFiles == null || imageFiles.length == 0) {
            System.out.println("No PNG or JPG files found in the input folder.");
            return;
        }

        // 6️⃣ Process each file
        for (File image : imageFiles) {
            // Recognize text – works for both PNG and JPG
            ocrEngine.recognizeImage(image.getAbsolutePath());

            // Build output PDF path (same base name)
            String pdfPath = outputFolder.getAbsolutePath() + File.separator +
                    image.getName().replaceAll("\\.(png|jpg)$", ".pdf");

            // Save as searchable PDF – this step also compresses images
            ocrEngine.saveAsSearchablePdf(pdfPath, pdfOptions);

            System.out.println("✅ Processed: " + image.getName() + " → " + pdfPath);
        }

        System.out.println("🎉 All files have been converted and compressed!");
    }
}
```

### Saída Esperada

Executar o programa imprime uma linha para cada imagem, por exemplo:

```
✅ Processed: invoice1.png → /output/invoice1.pdf
✅ Processed: receipt23.jpg → /output/receipt23.pdf
🎉 All files have been converted and compressed!
```

Abra qualquer PDF resultante em um visualizador e você verá texto selecionável e pesquisável, enquanto o tamanho do arquivo costuma ser **30‑50 % smaller** em relação a um equivalente não comprimido.

---

## Perguntas Frequentes & Casos de Borda

### E se o meu servidor não tiver GPU?

Basta definir `gpuSettings.setEnabled(false)`. O restante do pipeline permanece inalterado, e você ainda obtém processamento multithreaded na CPU.

### Meus PDFs ainda estão muito grandes — posso reduzir ainda mais a qualidade?

Sim. Ajuste `options.setImageQuality(70)` ou até `50`. Valores menores reduzem o tamanho de forma mais agressiva, mas podem borrar glifos finos. Teste com uma amostra representativa.

### Como lidar com outros formatos de imagem (TIFF, BMP)?

Adicione as extensões ao filtro lambda:

```java
name.toLowerCase().endsWith(".png") ||
name.toLowerCase().endsWith(".jpg") ||
name.toLowerCase().endsWith(".tif") ||
name.toLowerCase().endsWith(".bmp")
```

### Posso manter as imagens coloridas originais em vez de binarizar?

Substitua `.addBinarize()` por `.addGrayscale()` no construtor do pré‑processador se precisar manter a cor para análises posteriores.

---

## Dicas Profissionais para OCR em Lote Pronto para Produção

- **Memory management**: Reuse a single `OcrEngine` instance (as shown) to avoid the overhead of creating/destroying objects per image.  
- **Error handling**: Wrap the per‑file block in a `try/catch` to log failures without aborting the whole batch.  
- **Logging**: Use a proper logging framework (SLF4J, Log4j) instead of `System.out.println` for scalable solutions.  
- **Parallelism**: For massive folders, consider processing sub‑directories in parallel streams, but keep an eye on GPU contention.  
- **Security**: Store the license file outside the repository and protect it with file system permissions.

---

## Conclusão

Acabamos de demonstrar como **compress PDF images** enquanto realizamos uma conversão **batch OCR to PDF** que **convert PNG to PDF**, **recognize text JPG** e aplica um pipeline robusto de **image preprocessing for OCR**. O programa Java completo é autocontido, roda em qualquer JDK moderno e produz PDFs pesquisáveis leves, prontos para arquivamento ou análise posterior.

Próximos passos? Experimente diferentes parâmetros de pré‑processamento, teste idiomas de OCR além do inglês ou integre o fluxo a um microserviço Spring Boot que monitora um diretório e processa arquivos em tempo real. Os conceitos‑chave — carregamento de licença, configuração do motor, pré‑processamento e compressão PDF — permanecem os mesmos, oferecendo uma base sólida para qualquer projeto orientado a OCR.

Tem perguntas ou quer compartilhar suas próprias adaptações? Deixe um comentário abaixo e feliz codificação!

![Diagram of batch OCR workflow showing input images, preprocessing, OCR engine, and compressed PDF output](alt="Diagrama do fluxo de OCR em lote mostrando imagens de entrada, pré-processamento, motor OCR e saída PDF comprimida")

## O que Você Deve Aprender a Seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas de implementação em seus próprios projetos.

- [Reconhecer Texto em PDF – Operações OCR com Aspose.OCR para Java](/ocr/english/java/ocr-operations/)
- [reconhecer imagem de texto com Aspose OCR – Tutorial Completo de OCR Java](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [Converter Imagem em Texto em Java usando Aspose.OCR BufferedImage](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}