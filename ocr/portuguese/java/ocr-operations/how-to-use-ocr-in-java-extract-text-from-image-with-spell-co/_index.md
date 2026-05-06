---
category: general
date: 2026-05-06
description: Como usar OCR para extrair texto de imagem em Java. Aprenda a conversão
  de imagem para texto com OCR, corrija erros de OCR e carregue a imagem para OCR
  com Aspose OCR.
draft: false
keywords:
- how to use ocr
- extract text from image
- ocr image to text
- correct ocr errors
- load image for ocr
language: pt
og_description: Como usar OCR em Java para extrair texto de uma imagem, corrigir erros
  de OCR e carregar a imagem para OCR usando Aspose OCR.
og_title: Como usar OCR em Java – Guia completo
tags:
- OCR
- Java
- Aspose
title: Como usar OCR em Java – Extrair texto de imagem com correção ortográfica
url: /pt/java/ocr-operations/how-to-use-ocr-in-java-extract-text-from-image-with-spell-co/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como Usar OCR em Java – Extrair Texto de Imagem com Correção Ortográfica

Já se perguntou **como usar OCR** para transformar uma foto borrada de um recibo em texto limpo e pesquisável? Você não está sozinho. Em muitos projetos—aplicativos de controle de despesas, pipelines de digitalização de faturas ou até mesmo um script rápido de anotações—obter texto confiável de uma imagem é o primeiro obstáculo.  

Este tutorial mostra exatamente como usar OCR em Java, cobrindo tudo, desde o carregamento da imagem para OCR até a correção de erros de OCR para que o resultado pareça ter sido digitado por um humano. Ao final, você será capaz de **extrair texto de imagem**, realizar a conversão **OCR image to text** e corrigir automaticamente os erros de reconhecimento mais comuns.

## O Que Você Vai Construir

Criaremos um pequeno programa Java de console que:

1. Carrega um PNG (ou qualquer formato suportado) no motor Aspose OCR.  
2. Habilita o recurso interno de correção ortográfica para **corrigir erros de OCR**.  
3. Executa o processo de reconhecimento e imprime o texto limpo.  

Sem serviços externos, sem frameworks pesados—apenas um JAR único e algumas linhas de código.

### Pré‑requisitos

- Java Development Kit (JDK) 8 ou superior.  
- Maven (ou qualquer ferramenta de build) para obter a biblioteca Aspose OCR.  
- Um arquivo de imagem (por exemplo, `receipt.png`) que você deseja analisar.  

Se estiver faltando o JAR do Aspose OCR, adicione esta dependência ao seu `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- use the latest stable version -->
</dependency>
```

> **Dica de especialista:** A versão de avaliação gratuita funciona para testes, mas uma licença remove a marca d'água de avaliação.

## Etapa 1 – Inicializar o Motor OCR (Palavra‑chave Principal em Ação)

A primeira coisa que você precisa fazer é criar uma instância de `OcrEngine`. Pense nele como o cérebro que lerá os pixels e os transformará em caracteres.

```java
import com.aspose.ocr.*;

public class SpellCorrectDemo {
    public static void main(String[] args) throws Exception {

        // Initialise the OCR engine – this is where we start using OCR
        OcrEngine ocrEngine = new OcrEngine();
```

*Por que isso importa:* Inicializar o motor configura recursos internos (modelos de linguagem, dicionários, etc.). Pular esta etapa causaria um `NullPointerException` mais tarde, quando você tentar carregar uma imagem.

## Etapa 2 – Carregar Imagem para OCR

Agora realmente **carregamos a imagem para OCR**. A Aspose fornece um auxiliar conveniente `ImageStream.fromFile`, mas você também pode fornecer um `byte[]` se preferir.

```java
        // Load the image you want to analyse – replace the path with your own file
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/receipt.png"));
```

*Armadilha comum:* O caminho do arquivo deve ser absoluto ou relativo ao diretório de trabalho. Se a imagem não for encontrada, o motor lança um `IOException`. Verifique o caminho, especialmente ao executar a partir de uma IDE versus um JAR empacotado.

## Etapa 3 – Habilitar Correção Ortográfica para **Corrigir Erros de OCR**

O OCR padrão pode ser barulhento—pense em “l0ve” ao invés de “love” ou “0” ao invés de “O”. Habilitar a correção ortográfica indica ao motor que execute uma passagem de pós‑processamento que corrige erros típicos.

```java
        // Turn on the spell‑correction feature – this helps to correct OCR errors
        ocrEngine.getSettings().setEnableSpellCorrection(true);
```

*Por que você quer isso:* Sem correção ortográfica, você teria que limpar a saída manualmente, o que anula o propósito da automação. O dicionário interno funciona bem para inglês e vários outros idiomas.

## Etapa 4 – Executar o Reconhecimento (**OCR Image to Text**)

Com a imagem carregada e a correção ortográfica habilitada, podemos finalmente pedir ao motor que reconheça o texto.

```java
        // Run the OCR process – this converts the image to text
        OcrResult ocrResult = ocrEngine.recognize();
```

*Caso extremo:* Se a imagem for de baixo contraste ou estiver muito inclinada, o resultado ainda pode conter lixo. Considere pré‑processamento (por exemplo, binarização, correção de inclinação) antes de enviá‑la ao motor.

## Etapa 5 – Exibir o Texto Limpo

A etapa final é simplesmente imprimir o resultado. Em uma aplicação real você poderia gravá‑lo em um banco de dados ou em um arquivo, mas para esta demonstração `System.out` basta.

```java
        // Display the corrected text
        System.out.println("Corrected text:");
        System.out.println(ocrResult.getText());
    }
}
```

### Saída Esperada

Assumindo que `receipt.png` contenha uma lista clara de itens, você pode ver algo como:

```
Corrected text:
Item           Qty   Price
Apple          2     $1.20
Banana         5     $0.75
Total               $5.55
```

Observe como “Qty” e “Price” estão escritos corretamente mesmo que a digitalização original tivesse um “Qy” estranho.

## Exemplo Completo Funcional

Abaixo está o programa completo que você pode copiar‑colar em um arquivo chamado `SpellCorrectDemo.java`. Certifique‑se de que o JAR da Aspose OCR esteja no seu classpath.

```java
import com.aspose.ocr.*;

public class SpellCorrectDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Initialise the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the image you want to process
        // Replace "YOUR_DIRECTORY/receipt.png" with the actual path
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/receipt.png"));

        // Step 3: Enable spell correction to improve accuracy
        ocrEngine.getSettings().setEnableSpellCorrection(true);

        // Step 4: Perform OCR recognition (OCR image to text)
        OcrResult ocrResult = ocrEngine.recognize();

        // Step 5: Output the corrected text
        System.out.println("Corrected text:");
        System.out.println(ocrResult.getText());
    }
}
```

Execute com:

```bash
javac -cp "aspose-ocr-23.9.jar" SpellCorrectDemo.java
java -cp ".:aspose-ocr-23.9.jar" SpellCorrectDemo
```

Agora você deverá ver o texto limpo impresso no console.

## Bônus: Ajustando Configurações para Melhor Precisão

Embora a configuração padrão funcione para a maioria dos documentos impressos, pode ser necessário ajustar alguns parâmetros para cenários especializados:

| Configuração | O Que Faz | Quando Alterar |
|--------------|-----------|----------------|
| `setLanguage(OcrLanguage.English)` | Força o dicionário em inglês (reduz falsos positivos) | Se sua imagem contiver apenas texto em inglês. |
| `setResolution(300)` | Informa ao motor o DPI da imagem de origem | Para digitalizações de alta resolução. |
| `setEnableAutoSkewCorrection(true)` | Corrige automaticamente páginas levemente inclinadas | Quando as imagens são capturadas por um telefone. |

```java
ocrEngine.getSettings().setLanguage(OcrLanguage.English);
ocrEngine.getSettings().setResolution(300);
ocrEngine.getSettings().setEnableAutoSkewCorrection(true);
```

## Perguntas Frequentes

**P: Isso funciona com PDFs?**  
R: Sim. Converta cada página do PDF em uma imagem (por exemplo, usando Aspose PDF) e alimente a imagem ao motor OCR.

**P: E se minha imagem estiver no formato BMP?**  
R: `ImageStream.fromFile` suporta PNG, JPEG, BMP, TIFF e GIF nativamente. Basta mudar a extensão do arquivo.

**P: Posso desabilitar a correção ortográfica?**  
R: Absolutamente—defina `setEnableSpellCorrection(false)` se precisar da saída bruta do OCR para processamento posterior.

## Conclusão

Agora você sabe **como usar OCR** em Java para **extrair texto de imagem**, corrigir automaticamente **erros de OCR** e carregar **imagem para OCR** usando Aspose OCR. O fluxo de cinco etapas—inicializar, carregar, habilitar correção ortográfica, reconhecer e exibir—cobre a maioria das tarefas cotidianas de OCR.  

A partir daqui, considere encadear essa lógica com gravação em banco de dados, um endpoint REST ou um processador em lote para lidar com dezenas de recibos de uma vez. Experimente as configurações adicionais da tabela acima para extrair o máximo de precisão possível.

Feliz codificação, e que seus resultados de OCR sejam sempre mais limpos que seus recibos manchados de café! 

![como usar ocr diagrama mostrando imagem → motor OCR → fluxo de texto corrigido]

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}