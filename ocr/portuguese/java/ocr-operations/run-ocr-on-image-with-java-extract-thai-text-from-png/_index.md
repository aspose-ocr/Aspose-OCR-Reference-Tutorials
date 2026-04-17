---
category: general
date: 2026-03-28
description: Execute OCR em imagem em Java usando Aspose OCR para converter a imagem
  em texto, extraindo texto tailandês de PNG de forma rápida e confiável.
draft: false
keywords:
- run OCR on image
- convert image to text
- extract text from PNG
- extract Thai text
- recognize Thai text
language: pt
og_description: Execute OCR em imagem usando Java e Aspose OCR. Aprenda como converter
  imagem em texto, extrair texto tailandês de PNG e lidar com armadilhas comuns.
og_title: Execute OCR em Imagem com Java – Extraia Texto Tailandês Rapidamente
tags:
- OCR
- Java
- Aspose
- Image Processing
title: Execute OCR em Imagem com Java – Extraia Texto Tailandês de PNG
url: /pt/java/ocr-operations/run-ocr-on-image-with-java-extract-thai-text-from-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Execute OCR em Imagem com Java – Tutorial Completo

Já se perguntou como **executar OCR em arquivos de imagem** diretamente a partir de código Java? Talvez você tenha uma coleção de recibos tailandeses, documentos escaneados ou capturas de tela e precise do texto sem digitá‑lo manualmente. Esse é um ponto de dor comum, especialmente quando a origem é um PNG e o idioma não é latino.  

Neste guia mostraremos exatamente como **executar OCR em imagem** usando a biblioteca Aspose OCR, converter a foto em texto simples e extrair caracteres tailandeses de forma confiável. Ao final, você será capaz de **converter imagem em texto**, **extrair texto de PNG** e até **reconhecer texto tailandês** com apenas algumas linhas de código.

## O Que Este Tutorial Abrange

* Configurar a dependência Aspose OCR em um projeto Maven/Gradle.  
* Inicializar o `OcrEngine` e configurá‑lo para o idioma tailandês.  
* Executar OCR em um arquivo PNG e tratar possíveis erros.  
* Imprimir o resultado no console e verificar a saída.  

Nenhuma experiência prévia com Aspose é necessária — apenas um IDE Java básico e um arquivo de imagem que você deseja processar.

## Pré‑requisitos

* Java 8 ou superior instalado (a biblioteca funciona também com Java 11+).  
* Uma ferramenta de build – Maven ou Gradle (mostraremos o trecho Maven).  
* Uma licença Aspose OCR (o teste gratuito serve para experimentação, mas uma licença remove os limites de avaliação).  
* Um PNG que contenha texto tailandês, por exemplo, `input.png` colocado na pasta de recursos do seu projeto.

---

## Etapa 1: Adicionar Aspose OCR ao Seu Projeto

### Maven

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- Use the latest version -->
</dependency>
```

### Gradle (Kotlin DSL)

```kotlin
implementation("com.aspose:aspose-ocr:23.9")
```

> **Dica profissional:** Mantenha a versão da biblioteca sincronizada com as notas de lançamento oficiais da Aspose; versões mais recentes adicionam pacotes de idiomas e aprimoramentos de desempenho.

Depois que a dependência for resolvida, seu IDE deve importar automaticamente as classes necessárias.

## Etapa 2: Inicializar o Motor OCR

O motor é o coração do processo – pense nele como o “cérebro” que analisa padrões de pixels. Também informaremos a ele que nos interessam apenas caracteres tailandeses.

```java
import com.aspose.ocr.*;

public class ThaiOcrDemo {
    public static void main(String[] args) throws Exception {
        // Step 2: Create the OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Tell the engine to look for Thai language patterns
        ocrEngine.getRecognitionSettings().setLanguage("th");
```

Por que definir o idioma explicitamente? Porque especificar `"th"` restringe o conjunto de caracteres, o que acelera o reconhecimento e reduz leituras incorretas de glifos semelhantes.

## Etapa 3: Executar OCR no Arquivo PNG

Agora fornecemos ao motor a imagem que queremos decodificar. O método `recognizeImage` retorna um objeto `OcrResult` que contém a string extraída e as pontuações de confiança.

```java
        // Step 3: Perform OCR on the target image
        String imagePath = "src/main/resources/input.png";
        OcrResult ocrResult = ocrEngine.recognizeImage(imagePath);
```

Se o arquivo não for encontrado, a Aspose lança uma `FileNotFoundException`. É uma boa prática envolver a chamada em um bloco `try‑catch` para código de produção, mas para este tutorial manteremos a simplicidade.

## Etapa 4: Exibir o Texto Reconhecido

Por fim, imprimimos o resultado. O método `getText()` devolve uma `String` Java simples que você pode armazenar, enviar por rede ou gravar em um arquivo.

```java
        // Step 4: Display the extracted Thai text
        System.out.println("=== Recognized Thai Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

Ao executar o programa, você deverá ver algo como:

```
=== Recognized Thai Text ===
สวัสดีครับ นี่คือข้อความจากรูปภาพ
```

Se a saída parecer corrompida, verifique se o PNG de origem tem alta resolução (pelo menos 300 dpi) e se o código de idioma `"th"` corresponde ao idioma desejado.

### Listagem Completa

Abaixo está o arquivo Java completo, pronto para ser executado. Copie‑e cole no seu IDE, substitua o caminho da imagem se necessário e pressione **Run**.

```java
import com.aspose.ocr.*;

public class ThaiOcrDemo {
    public static void main(String[] args) throws Exception {
        // Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Select Thai language for recognition
        ocrEngine.getRecognitionSettings().setLanguage("th");

        // Run OCR on the PNG image
        String imagePath = "src/main/resources/input.png";
        OcrResult ocrResult = ocrEngine.recognizeImage(imagePath);

        // Output the recognized text
        System.out.println("=== Recognized Thai Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

![executar OCR em exemplo de imagem](image.png "executar OCR em exemplo de imagem – código Java extraindo texto tailandês de PNG")

## Etapa 5: Variações Comuns & Casos de Borda

### Converter Imagem em Texto em Outros Formatos

Se precisar **converter imagem em texto** para um JPEG ou BMP, basta alterar a extensão do arquivo em `imagePath`. Aspose OCR suporta PNG, JPEG, BMP, TIFF e até páginas PDF.

### Extrair Texto de PNG com Múltiplos Idiomas

Você pode solicitar ao motor que detecte vários idiomas simultaneamente:

```java
ocrEngine.getRecognitionSettings().setLanguage("th,en");
```

O resultado conterá uma mistura de caracteres tailandeses e ingleses, o que é útil para recibos bilíngues.

### Lidando com Imagens de Baixa Qualidade

Para digitalizações borradas, considere habilitar o pré‑processamento:

```java
ocrEngine.getRecognitionSettings().setPreprocessMode(PreprocessMode.Auto);
```

Isso ativa algoritmos internos de remoção de ruído e aprimoramento de contraste, melhorando a etapa **extrair texto de PNG**.

### Ativação de Licença

Sem uma licença, a Aspose insere uma linha de marca d'água na saída após 100 páginas. Ative sua licença logo no início:

```java
License license = new License();
license.setLicense("Aspose.OCR.lic");
```

Coloque o arquivo `.lic` ao lado do seu JAR ou faça referência a ele via caminho absoluto.

## Perguntas Frequentes

**Q: Isso funciona no Linux?**  
A: Absolutamente. Aspose OCR é puro Java, portanto qualquer OS compatível com JVM funciona.

**Q: E se o PNG contiver tailandês manuscrito?**  
A: O reconhecimento de escrita à mão é limitado; pode ser necessário um modelo de rede neural dedicado. Aspose OCR se destaca com texto impresso.

**Q: Posso processar em lote uma pasta de imagens?**  
A: Envolva a chamada `recognizeImage` em um loop sobre `Files.list(Paths.get("folder"))`. Lembre‑se de reutilizar a mesma instância de `OcrEngine` para melhorar o desempenho.

## Conclusão

Percorremos um exemplo completo, de ponta a ponta, de como **executar OCR em arquivos de imagem** em Java, especificamente para **extrair texto tailandês** de um PNG. Ao inicializar o `OcrEngine`, definir o idioma, invocar `recognizeImage` e imprimir o resultado, você agora dispõe de um método confiável para **converter imagem em texto** sem serviços de terceiros.

A partir daqui, você pode:

* **extrair texto de PNG** em massa para projetos de mineração de dados.  
* Combinar a saída OCR com uma API de tradução para obter equivalentes em inglês.  
* Explorar outros idiomas suportados pela Aspose, como chinês ou árabe, trocando o código de idioma.

Experimente com suas próprias imagens — ajuste as configurações de pré‑processamento, teste diferentes formatos de arquivo e veja como a solução se comporta no seu fluxo de trabalho real.

Boa codificação, e que seus pipelines de OCR sejam sempre precisos!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}