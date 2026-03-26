---
category: general
date: 2026-03-26
description: Crie PDF pesquisável usando Aspose.OCR Java – aprenda a carregar imagem
  para OCR, definir o idioma principal, extrair texto da imagem e salvar o PDF OCR.
draft: false
keywords:
- create searchable pdf
- set primary language
- extract text from image
- load image ocr
- save ocr pdf
language: pt
og_description: Crie PDF pesquisável com Aspose.OCR Java. Guia passo a passo para
  carregar OCR de imagem, definir idioma principal, extrair texto da imagem e salvar
  PDF OCR.
og_title: Crie PDF pesquisável com Aspose.OCR – Guia Java
tags:
- Aspose.OCR
- Java
- PDF
- OCR
title: Criar PDF pesquisável com Aspose.OCR – Guia Java
url: /pt/java/ocr-operations/create-searchable-pdf-with-aspose-ocr-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crie PDF pesquisável com Aspose.OCR – Guia Java

Já precisou **criar pdf pesquisável** a partir de um documento escaneado, mas não sabia por onde começar? Você não está sozinho—muitos desenvolvedores encontram essa barreira ao lidar com OCR em Java pela primeira vez. A boa notícia é que o Aspose.OCR torna todo o fluxo—desde o carregamento da imagem até a definição do idioma principal e, finalmente, a gravação de um PDF habilitado para OCR—bastante simples. Neste tutorial, percorreremos um exemplo completo e executável que **extrai texto da imagem**, permite **definir idioma principal** e termina com um **salvar pdf OCR** que pode ser aberto em qualquer leitor.

Também abordaremos algumas dicas práticas, como habilitar a aceleração por GPU para processamento mais rápido e lidar com documentos multilíngues (Tamil + Inglês no nosso caso). Ao final, você terá um trecho de código sólido e pronto para produção que pode inserir em seu projeto.

## O que você precisará

- **Java 17** (ou qualquer JDK recente; Aspose.OCR suporta Java 8+)
- Biblioteca **Aspose.OCR for Java** (baixe do site oficial ou adicione via Maven)
- Um **arquivo de licença** (ou a avaliação de 30 dias)
- Um arquivo de imagem que contenha texto (o demo usa `sample-mixed-tamil-eng.jpg`)

Sem frameworks extras, sem dependências nativas—apenas Java puro e os JARs do Aspose.

---

## Etapa 1: Crie PDF pesquisável – Configurando o Projeto

Antes de mergulharmos no código, vamos garantir que o projeto está pronto para **criar pdf pesquisável**.

```bash
# Maven dependency (add to pom.xml)
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- check the latest version -->
</dependency>
```

> **Dica profissional:** Mantenha o número da versão atualizado; lançamentos mais recentes costumam incluir correções de desempenho para uso de GPU.

Agora crie uma classe Java simples chamada `RecentFeaturesDemo`. A classe conterá toda a lógica necessária para **carregar imagem OCR**, configurar as definições de idioma e, finalmente, **salvar pdf OCR**.

---

## Etapa 2: Carregar Imagem OCR e Inicializar o Engine

O primeiro passo real no fluxo é **carregar imagem OCR**. Isso indica ao Aspose.OCR qual arquivo analisar.

```java
import com.aspose.ocr.*;

public class RecentFeaturesDemo {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Load your Aspose.OCR license (or use the 30‑day trial)
        License license = new License();
        license.setLicense("YOUR_DIRECTORY/Aspose.OCR.Java.lic");

        // 2️⃣ Create and configure the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Enable GPU acceleration – speeds up recognition dramatically
        ocrEngine.getEngineSettings().setUseGpu(true);
        // Use all available CPU cores for parallel processing
        ocrEngine.getEngineSettings().setUseParallelProcessing(true);
```

> **Por que isso importa:** Habilitar a GPU (`setUseGpu(true)`) pode reduzir o tempo de processamento em até 70 % em hardware moderno, enquanto o processamento paralelo garante que a CPU não fique ociosa quando a GPU estiver ocupada.

---

## Etapa 3: Definir Idioma Principal (e um Secundário)

Se você pular esta etapa, o Aspose.OCR tentará adivinhar o idioma, o que é mais lento e menos preciso. Veja como **definir idioma principal** para Tamil e adicionar Inglês como fallback.

```java
        // 3️⃣ Define languages – primary is Tamil, secondary is English
        ocrEngine.getLanguageSettings().setLanguage(Language.Tamil);
        ocrEngine.getLanguageSettings().setSecondaryLanguage(Language.English);
```

> **Explicação:** O idioma principal influencia o conjunto de caracteres e o dicionário usados durante o reconhecimento. Adicionar um idioma secundário é crucial para documentos de script misto (pense em um recibo com texto em Tamil e Inglês).  
> **Caso extremo:** Se seu documento contiver mais de dois idiomas, você pode chamar `addAdditionalLanguage(...)` para cada idioma extra.

---

## Etapa 4: Pré‑processar a Imagem – Correção de Inclinação e Redução de Ruído

Imagens escaneadas costumam sofrer rotação ou ruído de fundo. O pré‑processamento ajuda o motor OCR a **extrair texto da imagem** de forma mais confiável.

```java
        // 4️⃣ Pre‑processing options
        ocrEngine.getPreprocessingSettings()
                 .setDeskew(true)   // auto‑rotate tilted pages
                 .setDenoise(true); // suppress speckles and background patterns
```

> **Dica:** Se você souber que a imagem já está limpa, pode pular `setDenoise(true)` para economizar alguns milissegundos.

---

## Etapa 5: Carregar o Arquivo de Imagem

Agora que o engine está pronto, apontamos para o arquivo que queremos analisar.

```java
        // 5️⃣ Load the image you want to recognize
        String imagePath = "YOUR_DIRECTORY/sample-mixed-tamil-eng.jpg";
        ocrEngine.setImage(ImageStream.fromFile(imagePath));
```

> **E se o caminho estiver errado?** O Aspose.OCR lança uma clara `FileNotFoundException`. Envolva a chamada em um try‑catch se precisar de tratamento de erro mais elegante.

---

## Etapa 6: Executar OCR e Extrair Texto da Imagem

Com tudo configurado, é hora de realmente executar o reconhecimento. Esta etapa **extrai texto da imagem** e prepara os dados necessários para a criação do PDF.

```java
        // 6️⃣ Perform recognition
        if (ocrEngine.recognize()) {
            String recognizedText = ocrEngine.getText();

            // Print the raw OCR output – handy for debugging
            System.out.println("Recognized text:");
            System.out.println(recognizedText);
```

A saída típica no console para a imagem de demonstração é:

```
வணக்கம் World
This is a mixed language sample.
```

Você notará que a linha em Tamil é renderizada corretamente, seguida do Inglês. Esse é o resultado de **definir idioma principal** corretamente.

---

## Etapa 7: Salvar PDF OCR – A Peça Final

A última peça do quebra‑cabeça é **salvar pdf OCR**. O Aspose.OCR pode incorporar uma camada de texto invisível sobre a imagem original, tornando o PDF pesquisável.

```java
            // 7️⃣ (Optional) Save a searchable PDF with an OCR layer
            String pdfPath = "YOUR_DIRECTORY/searchable.pdf";
            ocrEngine.save(pdfPath, SaveFormat.PdfSearchable);

            System.out.println("\nSearchable PDF saved to: " + pdfPath);
        } else {
            System.err.println("Recognition failed: " + ocrEngine.getErrorMessage());
        }
    }
}
```

Abra `searchable.pdf` no Adobe Reader, pressione **Ctrl + F**, e você poderá buscar tanto palavras em Tamil quanto em Inglês—exatamente o que um fluxo de **criar pdf pesquisável** promete.

---

## Exemplo Completo (Copiar‑Colar)

Abaixo está o programa completo que você pode compilar e executar tal como está. Substitua os caminhos de placeholder pelos seus próprios diretórios.

```java
import com.aspose.ocr.*;

public class RecentFeaturesDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Load your Aspose.OCR license (or use the 30‑day trial)
        License license = new License();
        license.setLicense("YOUR_DIRECTORY/Aspose.OCR.Java.lic");

        // Step 2: Create and configure the OCR engine
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.getEngineSettings().setUseGpu(true);                     // enable CUDA GPU acceleration
        ocrEngine.getEngineSettings().setUseParallelProcessing(true);     // use multiple CPU cores
        ocrEngine.getLanguageSettings().setLanguage(Language.Tamil);      // primary language
        ocrEngine.getLanguageSettings().setSecondaryLanguage(Language.English); // secondary language
        ocrEngine.getPreprocessingSettings()
                 .setDeskew(true)   // correct image rotation
                 .setDenoise(true); // reduce background noise

        // Step 3: Load the image you want to recognize
        String imagePath = "YOUR_DIRECTORY/sample-mixed-tamil-eng.jpg";
        ocrEngine.setImage(ImageStream.fromFile(imagePath));

        // Step 4: Run OCR and obtain the plain‑text result
        if (ocrEngine.recognize()) {
            String recognizedText = ocrEngine.getText();

            // Step 5: (Optional) Save a searchable PDF with an OCR layer
            String pdfPath = "YOUR_DIRECTORY/searchable.pdf";
            ocrEngine.save(pdfPath, SaveFormat.PdfSearchable);

            System.out.println("Recognized text:");
            System.out.println(recognizedText);
            System.out.println("\nSearchable PDF saved to: " + pdfPath);
        } else {
            System.err.println("Recognition failed: " + ocrEngine.getErrorMessage());
        }
    }
}
```

Execute com:

```bash
javac -cp "path/to/aspose-ocr.jar" RecentFeaturesDemo.java
java -cp ".:path/to/aspose-ocr.jar" RecentFeaturesDemo
```

Você deverá ver o texto extraído impresso no console, seguido de uma confirmação de que o **pdf pesquisável** foi gravado no disco.

---

## Perguntas Frequentes & Casos de Borda

### E se eu precisar **carregar imagem OCR** a partir de um array de bytes?

Você pode substituir `ImageStream.fromFile(imagePath)` por `ImageStream.fromBytes(byteArray)`. Isso é útil quando a imagem vem de um banco de dados ou de um serviço web.

### Como lidar com PDFs que já contêm imagens?

O Aspose.OCR pode trabalhar diretamente nas páginas de PDF: `ocrEngine.setDocument(PdfDocument.fromFile("input.pdf"))`. O engine rasteriza cada página internamente antes do reconhecimento.

### Minha GPU não foi detectada—devo manter `setUseGpu(true)`?

Se `setUseGpu(true)` falhar, o Aspose.OCR recai automaticamente para a CPU. Você pode verificar `ocrEngine.getEngineSettings().isGpuAvailable()` antes de habilitá‑la.

### Posso **salvar pdf OCR** com metadados personalizados?

Sim. Após o reconhecimento, use `ocrEngine.getPdfSaveOptions().setTitle("Meu Documento")` ou `setAuthor("John Doe")` antes de chamar `save`.

---

## Dicas de Performance para Grandes Lotes

- **Processamento em lote:** Reutilize a mesma instância de `OcrEngine` para várias imagens. Apenas chame `ocrEngine.clear()` entre as execuções.
- **Pool de threads:** Envolva cada tarefa de imagem em um `Callable` e envie para um `ExecutorService`. Como habilitamos o processamento paralelo, cada thread se beneficiará do uso de múltiplos núcleos.
- **Gerenciamento de memória:** Para imagens de gigapixels, considere reduzir a resolução com `ocrEngine.getPreprocessingSettings().setResizeFactor(0.5)` para manter o uso de RAM sob controle.

---

## Conclusão

Acabamos de percorrer um fluxo completo de **criar pdf pesquisável** usando Aspose.OCR para Java. Partindo de **carregar imagem OCR**, nós

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}