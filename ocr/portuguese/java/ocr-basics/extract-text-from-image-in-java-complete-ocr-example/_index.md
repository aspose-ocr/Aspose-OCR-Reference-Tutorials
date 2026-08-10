---
category: general
date: 2026-02-19
description: Extraia texto de imagem usando Java OCR. Aprenda um exemplo de OCR em
  Java que carrega uma imagem para OCR e extrai texto de arquivos de fatura em apenas
  alguns passos.
draft: false
keywords:
- extract text from image
- java ocr example
- load image for ocr
- extract text from invoice
language: pt
og_description: Extraia texto de imagem usando Java OCR. Este guia mostra como carregar
  a imagem para OCR e extrair texto de faturas com um exemplo simples de OCR em Java.
og_title: Extrair Texto de Imagem em Java – Exemplo Completo de OCR
tags:
- OCR
- Java
- Aspose
- Image Processing
title: Extrair Texto de Imagem em Java – Exemplo Completo de OCR
url: /pt/java/ocr-basics/extract-text-from-image-in-java-complete-ocr-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrair Texto de Imagem em Java – Exemplo Completo de OCR

Já precisou **extrair texto de imagem** mas não tinha certeza de qual biblioteca escolher? Você não está sozinho—muitos desenvolvedores enfrentam esse obstáculo ao automatizar o processamento de faturas ou ao criar arquivos pesquisáveis. A boa notícia? Com algumas linhas de Java você pode carregar uma imagem para OCR, definir uma região de interesse e obter o texto exato que precisa.  

Neste tutorial, vamos percorrer um **java ocr example** que mostra exatamente como **load image for OCR**, definir um ROI e **extract text from invoice** usando Aspose.OCR. Ao final, você terá um programa executável que pode inserir em qualquer projeto Java.

## O que você aprenderá

- Como criar uma instância `OcrEngine` e por que isso importa.
- A maneira correta de **load image for OCR** com `ImageStream` da Aspose.
- Definir uma **region of interest (ROI)** para que você processe apenas a parte da imagem que contém o valor da fatura.
- Extrair o texto reconhecido e imprimi-lo no console.
- Armadilhas comuns (por exemplo, coordenadas de retângulo incorretas) e correções rápidas.

**Pré-requisitos**

- Java 8 ou superior instalado.
- Maven ou Gradle para obter a biblioteca Aspose.OCR (`com.aspose:aspose-ocr`).
- Uma imagem de fatura de exemplo (`invoice.png`) colocada em um diretório conhecido.

Tem tudo isso? Ótimo—vamos mergulhar.

![Extrair texto de imagem usando Java OCR](/images/extract-text-from-image-java.png "exemplo de extração de texto de imagem")

## Extrair Texto de Imagem – Exemplo de OCR Java passo a passo

Abaixo está o código-fonte completo. Sinta-se à vontade para copiar e colar em `RoiOcrExample.java` e executá-lo diretamente.

```java
import com.aspose.ocr.*;

public class RoiOcrExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create an OCR engine instance.
        // The engine holds all configuration and performs the heavy lifting.
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the source image.
        // You can point to any PNG, JPG, or TIFF file. Here we use a sample invoice.
        String imagePath = "YOUR_DIRECTORY/invoice.png";
        ocrEngine.setImage(ImageStream.fromFile(imagePath));

        // Step 3: Define the region of interest (ROI) you want to recognize.
        // x = 120, y = 340, width = 500, height = 120 – tweak these values for your own layout.
        Rectangle regionOfInterest = new Rectangle(120, 340, 500, 120);
        ocrEngine.setRegionOfInterest(regionOfInterest);

        // Step 4: Perform OCR on the specified ROI and retrieve the text.
        // recognize() returns an OcrResult object; getText() extracts the plain string.
        String extractedText = ocrEngine.recognize().getText();

        // Step 5: Output the recognized text.
        System.out.println("ROI text: " + extractedText);
    }
}
```

### Por que cada passo é importante

1. **Creating the OCR engine** – sem um engine não há contexto para o processamento de imagens. O objeto também permite ajustar pacotes de idioma mais tarde, se precisar de suporte multilíngue.  
2. **Loading the image** – `ImageStream.fromFile` abstrai o formato do arquivo, garantindo que o engine leia os bytes corretamente. Se você pular isso, receberá um `NullPointerException`.  
3. **Setting the ROI** – processar a página inteira pode ser desperdiçador. Ao reduzir o retângulo para a área do total da fatura, você acelera o reconhecimento e reduz o ruído.  
4. **Calling `recognize()`** – é aqui que a mágica acontece. O método executa o algoritmo OCR sobre a ROI e produz um objeto de resultado.  
5. **Printing the output** – em projetos reais você provavelmente armazenaria o texto em um banco de dados, mas `System.out.println` é perfeito para uma demonstração rápida.

## Carregar Imagem para OCR

Se você está se perguntando se o caminho precisa ser absoluto ou relativo, a resposta é que ambos funcionam—basta garantir que o processo Java possa ler o arquivo. No Windows, as barras invertidas devem ser escapadas (`C:\\images\\invoice.png`) ou você pode usar barras normais (`C:/images/invoice.png`).  

**Dica profissional:** Se você estiver processando muitas faturas em um loop, reutilize a mesma instância `OcrEngine`; ela faz cache de recursos internos e melhora o rendimento.

## Definir Região de Interesse (ROI)

Escolher o retângulo correto pode ser um pouco de tentativa e erro. Uma maneira prática de encontrar as coordenadas é abrir a imagem em qualquer editor gráfico (como GIMP ou Paint.NET) e passar o mouse sobre a área—você verá os valores X/Y na barra de status.  

Caso extremo: algumas faturas têm layouts variáveis. Nesse cenário, você pode executar uma pré‑varredura rápida na imagem inteira, localizar palavras‑chave como “Total:” com uma expressão regular, e então ajustar a ROI dinamicamente.

## Executar OCR e Obter Texto

A chamada `recognize()` é síncrona—seu thread fica bloqueado até que o engine termine. Para lotes grandes, você pode querer criar um pool de threads e processar imagens em paralelo. Apenas lembre‑se de que cada thread precisa de sua própria instância `OcrEngine`; elas não são thread‑safe.

## Executar e Verificar Saída

Compile e execute:

```bash
javac -cp "path/to/aspose-ocr.jar" RoiOcrExample.java
java -cp ".:path/to/aspose-ocr.jar" RoiOcrExample
```

Você deve ver algo como:

```
ROI text: $1,254.00
```

Se a saída parecer confusa, verifique novamente as coordenadas da ROI e assegure que a qualidade da imagem seja alta (300 dpi ou mais funciona melhor).  

### Armadilhas Comuns e Como Corrigi‑las

| Sintoma | Causa provável | Correção |
|---------|----------------|----------|
| String vazia | ROI fora dos limites da imagem | Verifique os valores do retângulo em relação às dimensões da imagem |
| Palavras com erros | Baixa resolução | Use uma fonte de maior resolução ou aplique pré‑processamento de imagem (por exemplo, binarização) |
| `java.lang.NoClassDefFoundError` | JAR da Aspose ausente no classpath | Adicione `aspose-ocr.jar` ao `-cp` ou use o gerenciamento de dependências Maven/Gradle |

## Conclusão

Agora você sabe como **extract text from image** em Java usando um conciso **java ocr example**. Ao carregar a imagem corretamente, definir uma ROI focada e chamar `recognize()`, você pode **extract text from invoice** de forma confiável e alimentar esses dados em sistemas posteriores.

O que vem a seguir? Experimente trocar a ROI por diferentes campos (data, nome do fornecedor), experimente pacotes de idioma para faturas multilíngues, ou integre a etapa de OCR em um microserviço Spring Boot. O mesmo padrão funciona para recibos, passaportes ou qualquer documento onde você precise de extração de texto precisa.

Se você tem dúvidas sobre escalar esta solução ou lidar com digitalizações ruidosas, deixe um comentário abaixo—bom código!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}