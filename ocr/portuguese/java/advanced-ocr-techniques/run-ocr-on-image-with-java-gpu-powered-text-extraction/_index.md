---
category: general
date: 2026-03-07
description: Execute OCR em imagem usando Java. Aprenda como reconhecer texto de PNG,
  extrair texto de recibo e carregar a imagem para OCR com um exemplo completo de
  OCR em Java.
draft: false
keywords:
- run OCR on image
- recognize text from png
- extract text from receipt
- java OCR example
- load image for OCR
language: pt
og_description: Execute OCR em imagem com Java. Este guia mostra como reconhecer texto
  de PNG, extrair texto de recibo e carregar a imagem para OCR usando um exemplo completo
  de OCR em Java.
og_title: Execute OCR em Imagem com Java – Extração de Texto com GPU
tags:
- OCR
- Java
- GPU
- Image Processing
title: Execute OCR em imagem com Java – Extração de texto com GPU
url: /pt/java/advanced-ocr-techniques/run-ocr-on-image-with-java-gpu-powered-text-extraction/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Execute OCR em Imagem com Java – Extração de Texto Acelerada por GPU

Já precisou **executar OCR em arquivos de imagem** mas não sabia por onde começar em Java? Você não está sozinho—muitos desenvolvedores enfrentam a mesma dificuldade ao tentar extrair texto de um recibo escaneado ou de uma captura de tela PNG.  

Neste tutorial vamos guiá‑lo através de um **exemplo completo de OCR em Java** que não só **reconhece texto de arquivos PNG** como também mostra como **extrair texto de imagens de recibos**, tudo aproveitando a aceleração por GPU para maior velocidade. Ao final, você terá um programa pronto‑para‑executar que carrega uma imagem para OCR, processa‑a e imprime o resultado em texto simples.

## O que você vai aprender

- Como **carregar imagem para OCR** usando um simples `ImageInputStream`.
- Habilitar suporte a GPU para que o motor rode mais rápido em hardware moderno.
- Os passos exatos para **reconhecer texto de PNG** e extrair strings úteis de um recibo.
- Armadilhas comuns (ex.: ID de dispositivo GPU incorreto) e dicas de boas práticas.
- Um trecho de código completo e executável que você pode copiar‑colar no seu IDE.

**Pré‑requisitos**

- Java 17 ou superior (o código usa a palavra‑chave `var` para brevidade, mas você pode substituí‑la por tipos explícitos se estiver usando Java 8).
- Uma biblioteca OCR que forneça as classes `OcrEngine`, `ImageInputStream` e `OcrResult` (por exemplo, o fictício *FastOCR* SDK; substitua pela que você realmente usa).
- Uma máquina com GPU habilitada se quiser o ganho de desempenho (opcional, mas recomendado).

---

## Passo 1: Execute OCR em Imagem – Habilite Aceleração por GPU

A primeira coisa a fazer é criar o motor OCR e instruí‑lo a usar a GPU. Esta etapa é crucial porque, sem suporte a GPU, o motor recorre à CPU, o que pode ser visivelmente mais lento para recibos de alta resolução.

```java
// Step 1: Create the OCR engine and enable GPU acceleration
OcrEngine ocrEngine = new OcrEngine();

// Turn on GPU usage – this makes the recognition much faster
ocrEngine.getConfig().setUseGpu(true);          // enable GPU usage

// Optional: select which GPU device to use (0 = first GPU)
ocrEngine.getConfig().setGpuDeviceId(0);
```

**Por que isso importa:**  
A aceleração por GPU descarrega os cálculos de matriz pesados que os motores OCR realizam. Se você tem várias GPUs, pode escolher a que tem mais memória alterando o valor de `setGpuDeviceId`. Esquecer de habilitar a GPU é uma fonte comum de reclamações do tipo “por que meu OCR está tão lento?”.

> **Dica de especialista:** Se sua máquina não possui uma GPU compatível, a chamada `setUseGpu(true)` será simplesmente ignorada—sem travar, apenas com processamento mais lento.

---

## Passo 2: Carregar Imagem para OCR

Agora que o motor está pronto, precisamos alimentá‑lo com uma imagem. O exemplo abaixo mostra como carregar um recibo PNG armazenado em disco. Você pode substituir o caminho por qualquer formato de imagem suportado pela sua biblioteca OCR.

```java
// Step 2: Load the image you want to recognize
ImageInputStream imageStream = new ImageInputStream("YOUR_DIRECTORY/receipt.png");
```

**Caso extremo:**  
Se o arquivo não existir ou o caminho estiver errado, `ImageInputStream` lançará uma `IOException`. Envolva a chamada em um bloco try‑catch e registre uma mensagem útil:

```java
try {
    ImageInputStream imageStream = new ImageInputStream("YOUR_DIRECTORY/receipt.png");
} catch (IOException e) {
    System.err.println("Failed to load image: " + e.getMessage());
    return;
}
```

---

## Passo 3: Reconhecer Texto de PNG

Com a imagem carregada, o motor OCR pode fazer sua mágica. Esta etapa realmente **reconhece texto de PNG** (ou qualquer outro formato suportado) e devolve um objeto `OcrResult`.

```java
// Step 3: Run the OCR process on the image
OcrResult ocrResult = ocrEngine.recognize(imageStream);
```

**O que está acontecendo nos bastidores?**  
O motor realiza pré‑processamento (deskew, binarização), executa uma rede neural para detectar caracteres e, em seguida, os reúne em linhas de texto. Como habilitamos a GPU antes, esses cálculos de rede neural acontecem na placa gráfica, economizando segundos no tempo total de execução.

---

## Passo 4: Extrair Texto do Recibo

Após o reconhecimento, você normalmente quer apenas o texto bruto. A classe `OcrResult` costuma oferecer um método `getText()` que devolve uma única `String`. Você pode então pós‑processá‑la (ex.: usar regex para extrair totais, datas, etc.).

```java
// Step 4: Print the recognized plain‑text result
System.out.println("Recognized text:");
System.out.println(ocrResult.getText());
```

**Saída típica de recibo:**  

```
Store: Coffee Corner
Date: 2026-03-07
Item      Qty   Price
Latte      2    $5.80
Muffin     1    $2.50
TOTAL           $8.30
```

Agora você pode alimentar essa string ao seu próprio parser para extrair o valor total, itens de linha ou informações de impostos.

---

## Passo 5: Exemplo Completo de OCR em Java – Pronto para Executar

Juntando tudo, aqui está o **exemplo completo de OCR em Java** que você pode colocar em um arquivo `Main.java`. Certifique‑se de que a biblioteca OCR esteja no seu classpath.

```java
import com.fastocr.OcrEngine;
import com.fastocr.ImageInputStream;
import com.fastocr.OcrResult;

public class Main {
    public static void main(String[] args) {
        // 1️⃣ Create OCR engine and enable GPU
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.getConfig().setUseGpu(true);          // enable GPU usage
        ocrEngine.getConfig().setGpuDeviceId(0);        // optional: select GPU #0

        // 2️⃣ Load the image you want to recognize
        ImageInputStream imageStream;
        try {
            imageStream = new ImageInputStream("YOUR_DIRECTORY/receipt.png");
        } catch (Exception e) {
            System.err.println("Error loading image: " + e.getMessage());
            return;
        }

        // 3️⃣ Run OCR on the image
        OcrResult ocrResult = ocrEngine.recognize(imageStream);

        // 4️⃣ Output the plain‑text result
        System.out.println("Recognized text:");
        System.out.println(ocrResult.getText());
    }
}
```

**Saída esperada no console** (considerando o recibo de exemplo acima):

```
Recognized text:
Store: Coffee Corner
Date: 2026-03-07
Item      Qty   Price
Latte      2    $5.80
Muffin     1    $2.50
TOTAL           $8.30
```

Se a saída parecer corrompida, verifique se a imagem está nítida (alta DPI) e se o pacote de idioma do OCR corresponde ao idioma do seu recibo.

---

## Perguntas Frequentes & Armadilhas

| Pergunta | Resposta |
|----------|----------|
| *E se minha GPU não for detectada?* | O motor recairá automaticamente para a CPU. Verifique os drivers e se o `setGpuDeviceId` corresponde a um dispositivo existente (`nvidia-smi` no Linux pode ajudar). |
| *Posso processar arquivos JPEG ou TIFF?* | Sim—basta mudar a extensão do arquivo em `ImageInputStream`. A biblioteca OCR geralmente detecta o formato automaticamente. |
| *Existe uma forma de processar lotes de muitos recibos?* | Envolva o código de reconhecimento em um loop e reutilize a mesma instância de `OcrEngine`; reinicializar por imagem desperdiça memória da GPU. |
| *Como melhorar a precisão em recibos de baixo contraste?* | Pré‑procese a imagem (aumente o contraste, converta para escala de cinza) antes de enviá‑la ao motor OCR. Algumas bibliotecas expõem uma API `preprocess`. |

---

## Conclusão

Agora você sabe **como executar OCR em arquivos de imagem** em Java, desde o carregamento da foto até a extração de texto limpo de um recibo. O passo‑a‑passo cobriu **reconhecimento de texto de PNG**, **extração de texto de recibo**, e mostrou um **exemplo de OCR em Java** que pode ser adaptado a qualquer projeto.  

Próximos passos? Experimente desativar a flag de GPU para observar a diferença de desempenho, teste com diferentes resoluções de imagem, ou integre um parser baseado em regex para extrair totais automaticamente. Se quiser aprofundar, explore **pós‑processamento de OCR**, **correção com modelo de linguagem**, ou **pipelines de processamento em lote**.

Bom código, e que seus recibos estejam sempre legíveis!  

![exemplo de execução de OCR em imagem](/images/run-ocr-on-image.png "execução de OCR em imagem – exemplo Java")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}