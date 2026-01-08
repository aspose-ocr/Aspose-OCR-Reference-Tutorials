---
category: general
date: 2026-01-07
description: Crie PDF pesquisável a partir de uma imagem usando Aspose OCR em Java.
  Aprenda como converter imagem em PDF, reconhecer texto da imagem e gerar PDF a partir
  de JPG.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- recognize text from image
- how to use ocr
- generate pdf from jpg
language: pt
og_description: Crie PDF pesquisável a partir de uma imagem com Aspose OCR em Java.
  Guia passo a passo para converter imagem em PDF, reconhecer texto da imagem e gerar
  PDF a partir de JPG.
og_title: Criar PDF pesquisável a partir de imagem – Guia de OCR em Java
tags:
- OCR
- Java
- PDF
- Aspose
title: Criar PDF pesquisável a partir de imagem com OCR – Tutorial Java
url: /pt/java/ocr-operations/create-searchable-pdf-from-image-with-ocr-java-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar PDF pesquisável a partir de imagem com OCR – Tutorial Java

Já precisou **criar PDF pesquisável** a partir de uma foto escaneada, mas não sabia por onde começar? Você não está sozinho—muitos desenvolvedores encontram essa barreira na primeira vez que tentam transformar um JPEG em um PDF que realmente pode ser pesquisado.  

Neste guia vamos percorrer um exemplo completo e executável que mostra como **converter imagem em PDF**, **reconhecer texto da imagem**, e finalmente **gerar PDF a partir de JPG** usando Aspose OCR para Java. Sem referências vagas, apenas código que você pode copiar‑colar e executar hoje.

## O que você precisará

Antes de mergulharmos, certifique‑se de que tem o seguinte na sua máquina:

* **Java 17** ou mais recente (a API funciona com qualquer JDK recente).  
* Biblioteca **Aspose.OCR for Java** – você pode obter o JAR mais recente no Maven Central ou no site da Aspose.  
* Uma imagem de exemplo, por exemplo, `sample.jpg`, colocada em uma pasta que você possa referenciar.  
* Uma IDE ou um editor de texto simples mais um terminal—o que for mais confortável para você.

É isso. Sem frameworks pesados, sem dependências nativas extras. Vamos começar.

## Etapa 1 – Criar PDF pesquisável: Inicializar o mecanismo OCR

A primeira coisa que fazemos é instanciar um `OcrEngine` e apontá‑lo para a imagem de origem. Esse objeto é o coração do Aspose OCR; ele cuida de tudo, desde o carregamento do bitmap até a exposição do texto reconhecido.

```java
import com.aspose.ocr.*;

public class HelloOcrTutorial {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the image you want to turn into a searchable PDF
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample.jpg"));
```

> **Por que isso importa:** Inicializar o mecanismo corretamente garante que a biblioteca possa ler o formato da imagem que você está fornecendo. Se o caminho estiver errado, você receberá um `FileNotFoundException` e todo o pipeline será interrompido.

## Etapa 2 – Aumentar desempenho: habilitar GPU, CPU multi‑core e correção ortográfica

OCR pode consumir muito CPU, especialmente em documentos grandes. Aspose oferece alguns parâmetros que você pode ajustar para tornar o processo mais rápido e preciso.

```java
        // 2️⃣ Turn on performance helpers – GPU, multi‑core CPU, and spell correction
        ocrEngine.getEngineOptions()
                 .setUseGpu(true)                 // uses GPU if one is available
                 .setUseMultiCore(true)           // spreads work across CPU cores
                 .setEnableSpellCorrection(true); // cleans up common OCR mistakes
```

> **Dica profissional:** Se você estiver rodando em um servidor sem GPU, `setUseGpu(false)` não causará problemas—você simplesmente retornará ao processamento em CPU multi‑core.

## Etapa 3 – Melhorar qualidade da imagem: corrigir inclinação e remover ruído (Opcional, mas recomendado)

Digitalizações raramente são perfeitas. Um pequeno desvio ou ruído pode atrapalhar o reconhecedor. A classe `ImageProcessingOptions` permite limpar a imagem antes que o mecanismo tente lê‑la.

```java
        // 3️⃣ Pre‑process the image – straighten it and remove noise
        ocrEngine.getImageProcessingOptions()
                 .setDeskew(true)   // automatically rotates tilted text
                 .setDespeckle(true); // reduces background speckles
```

> **Caso extremo:** Se sua imagem de origem já estiver limpa, você pode pular esta etapa. Não causará danos, mas adiciona alguns milissegundos de sobrecarga.

## Etapa 4 – Reconhecer texto da imagem e gerar PDF

Agora a mágica acontece. Chamamos `recognize()` e o mecanismo devolve um `OcrResult`. A partir daí podemos salvar a saída em vários formatos—PDF sendo o mais comum para documentos pesquisáveis.

```java
        // 4️⃣ Perform OCR and get the result object
        OcrResult ocrResult = ocrEngine.recognize();

        // 5️⃣ Save the result as a searchable PDF (you could also choose TXT, DOCX, etc.)
        ocrResult.save("YOUR_DIRECTORY/sample-output.pdf", OcrOutputFormat.PDF);
    }
}
```

> **O que você verá:** `sample-output.pdf` contém a imagem original como camada de fundo, enquanto o texto reconhecido fica sobreposto como uma camada invisível. Abra‑o no Adobe Reader e tente selecionar texto—você ficará surpreso.

## Etapa 5 – Verificar a saída do PDF pesquisável criado

Depois que o arquivo for escrito, é boa prática confirmar que o PDF é realmente pesquisável.

```java
import java.awt.Desktop;
import java.io.File;

public class VerifyPdf {
    public static void main(String[] args) throws Exception {
        File pdf = new File("YOUR_DIRECTORY/sample-output.pdf");
        if (pdf.exists() && Desktop.isDesktopSupported()) {
            Desktop.getDesktop().open(pdf); // opens the PDF in the default viewer
        } else {
            System.out.println("PDF not found or cannot be opened on this platform.");
        }
    }
}
```

Abra o PDF, pressione **Ctrl F**, digite uma palavra que você sabe que aparece na imagem—se a busca encontrá‑la, você criou com sucesso um **PDF pesquisável**!

## Como usar OCR em cenários reais (Bônus)

* **Processamento em lote:** Envolva o código em um loop que itere sobre uma pasta de JPGs. Lembre‑se de reutilizar uma única instância de `OcrEngine` para manter o uso de memória baixo.  
* **Suporte a idiomas:** Aspose OCR suporta mais de 60 idiomas. Basta chamar `ocrEngine.getEngineOptions().setLanguage(Language.English);` (ou qualquer outro valor do enum).  
* **Tratamento de erros:** Capture `OcrException` para lidar graciosamente com arquivos corrompidos.  

Essas ajustes tornam a solução robusta o suficiente para pipelines de produção.

## Exemplo completo em Java – Criar PDF pesquisável a partir de JPG

Abaixo está o programa completo e autocontido que você pode compilar e executar tal como está. Substitua `YOUR_DIRECTORY` pelo caminho real na sua máquina.

```java
import com.aspose.ocr.*;

public class CreateSearchablePdf {
    public static void main(String[] args) throws Exception {
        // -------------------------------------------------
        // 1️⃣ Load the source image
        // -------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample.jpg"));

        // -------------------------------------------------
        // 2️⃣ Performance helpers
        // -------------------------------------------------
        ocrEngine.getEngineOptions()
                 .setUseGpu(true)
                 .setUseMultiCore(true)
                 .setEnableSpellCorrection(true);

        // -------------------------------------------------
        // 3️⃣ Image pre‑processing (optional but helpful)
        // -------------------------------------------------
        ocrEngine.getImageProcessingOptions()
                 .setDeskew(true)
                 .setDespeckle(true);

        // -------------------------------------------------
        // 4️⃣ Run OCR and save as searchable PDF
        // -------------------------------------------------
        OcrResult result = ocrEngine.recognize();
        result.save("YOUR_DIRECTORY/sample-output.pdf", OcrOutputFormat.PDF);

        System.out.println("✅ Searchable PDF created at YOUR_DIRECTORY/sample-output.pdf");
    }
}
```

**Saída esperada:**  

```
✅ Searchable PDF created at YOUR_DIRECTORY/sample-output.pdf
```

Abra o PDF gerado e você deverá ser capaz de buscar qualquer palavra que apareceu em `sample.jpg`. Se você não vir a camada de texto, verifique novamente o caminho da imagem e assegure‑se de que o mecanismo OCR não está lançando exceções ocultas.

## Conclusão

Acabamos de mostrar como **criar PDF pesquisável** a partir de um JPEG usando Aspose OCR para Java. Desde o carregamento da imagem, ajuste das configurações de desempenho, limpeza da foto, até o reconhecimento final do texto e a gravação de um PDF pesquisável—cada etapa foi explicada com o *porquê* e o *como*.  

Agora você pode **converter imagem em PDF**, **reconhecer texto da imagem**, e **gerar PDF a partir de JPG** em suas próprias aplicações. Em seguida, experimente processar uma pasta inteira de digitalizações, testar diferentes idiomas, ou adicionar proteção por senha ao PDF de saída. O céu é o limite.

Tem dúvidas sobre casos extremos, licenciamento ou ajuste de desempenho? Deixe um comentário abaixo, e feliz codificação! 

![Diagrama ilustrando o pipeline de OCR – criar PDF pesquisável](/images/ocr-pipeline.png "Diagrama de PDF pesquisável")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}