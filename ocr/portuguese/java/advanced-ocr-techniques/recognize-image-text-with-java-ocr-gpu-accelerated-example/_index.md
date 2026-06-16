---
category: general
date: 2026-03-28
description: Aprenda a reconhecer texto em imagens em Java usando Aspose OCR, extrair
  texto de arquivos PNG e usar aceleração por GPU para OCR rápido de imagens grandes.
draft: false
keywords:
- recognize image text
- extract text png
- use gpu acceleration
- ocr large image
- java ocr example
language: pt
og_description: Descubra como reconhecer texto em imagens em Java, extrair texto de
  arquivos PNG e usar aceleração GPU para OCR de imagens grandes.
og_title: reconhecer texto de imagem com Java OCR – Exemplo acelerado por GPU
tags:
- OCR
- Java
- GPU
title: reconhecer texto em imagem com Java OCR – Exemplo acelerado por GPU
url: /pt/java/advanced-ocr-techniques/recognize-image-text-with-java-ocr-gpu-accelerated-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# reconhecer texto em imagem com Java OCR – Exemplo Acelerado por GPU

Já precisou **reconhecer texto em imagem** de um PNG enorme, mas a versão CPU estava lenta? Você não está sozinho. Em muitos pipelines do mundo real — pense em digitalização de faturas ou arquivamento de documentos históricos — o tamanho da imagem pode crescer muito, e o motor OCR padrão simplesmente não consegue acompanhar.  

Boa notícia: o Aspose OCR for Java permite que você **use aceleração GPU** para turbinar o processo, e o código é surpreendentemente compacto. Neste tutorial você verá um exemplo completo e executável de OCR em Java que **extrai texto de arquivos PNG**, utiliza uma GPU com suporte a CUDA e lida com uma **imagem grande de OCR** com apenas algumas linhas de código. Ao final, você saberá exatamente como integrar isso ao seu próprio projeto Java e por que cada configuração importa.

## O que você aprenderá

- Como configurar o Aspose OCR em um projeto Maven ou Gradle.  
- O processo passo a passo para **reconhecer texto em imagem** na GPU.  
- Por que configurar o número de streams da GPU pode melhorar o rendimento.  
- Como verificar a saída e solucionar armadilhas comuns.  

> **Pré-requisitos** – Java 17 (ou superior), uma GPU compatível com CUDA com o driver mais recente e uma licença válida do Aspose OCR for Java (o teste gratuito funciona para avaliação). Nenhuma outra biblioteca externa é necessária.

---

## Passo 1: Adicionar a dependência Aspose OCR

Primeiro, inclua a biblioteca Aspose OCR na sua construção. Se você usa **Maven**, adicione o trecho a seguir ao seu `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- check Maven Central for the latest version -->
</dependency>
```

Para **Gradle**, coloque isto em `build.gradle`:

```gradle
implementation 'com.aspose:aspose-ocr:23.9'
```

> **Dica profissional:** A versão mais recente (a partir de março 2026) inclui melhorias de desempenho para cargas de trabalho GPU, portanto sempre obtenha a versão mais nova.

---

## Passo 2: Inicializar o Motor OCR e Habilitar a GPU

Criar um motor OCR é simples. A parte crucial é ativar a flag da GPU — caso contrário, o motor recai para o modo CPU.

```java
import com.aspose.ocr.*;

public class GpuExample {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Enable GPU acceleration (requires a CUDA‑enabled GPU and driver)
        ocrEngine.getRecognitionSettings().setUseGpu(true);

        // 3️⃣ (Optional) Set the number of GPU streams for parallel processing
        //    More streams can improve throughput on multi‑core GPUs.
        ocrEngine.getRecognitionSettings().setGpuStreams(2);
```

### Por que habilitar a GPU?

Quando você habilita `setUseGpu(true)`, o Aspose delega os pesados cálculos de redes neurais convolucionais para a placa gráfica. Isso pode reduzir segundos do tempo de processamento de uma **imagem grande de OCR**, especialmente quando a imagem ultrapassa 4000 × 4000 px. Se seu ambiente não possuir uma GPU compatível, a chamada simplesmente se torna um no‑op e o motor continua na CPU — sem travar, apenas com desempenho mais lento.

---

## Passo 3: Reconhecer uma Imagem PNG e Extrair Seu Texto

Agora aponte o motor para o arquivo que deseja processar. O exemplo usa `sample-large.png`, mas você pode substituí-lo por qualquer PNG ou JPEG.

```java
        // 4️⃣ Perform OCR on the input image
        OcrResult ocrResult = ocrEngine.recognizeImage("YOUR_DIRECTORY/sample-large.png");

        // 5️⃣ Print the recognized text to the console
        System.out.println("=== Recognized Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

Ao executar o programa, você deverá ver algo como:

```
=== Recognized Text ===
Invoice #12345
Date: 2026‑03‑27
Total: $1,234.56
...
```

Essa saída confirma que a operação de **reconhecer texto em imagem** foi bem‑sucedida e que você **extraiu texto de PNG** com sucesso.

---

## Passo 4: Verificar a Utilização da GPU (Opcional, mas Útil)

Se você está curioso para saber se a GPU está realmente sendo usada, abra a ferramenta de monitoramento de GPU do seu sistema (por exemplo, `nvidia-smi` no Linux). Enquanto o processo Java roda, você deverá ver um pequeno pico no uso de memória e na utilização de computação.

```bash
$ nvidia-smi
+-----------------------------------------------------------------------------+
| Processes:                                                                  |
|  GPU   PID   Type   Process name                  GPU Memory               |
|  0    12345 C++    java                           1024MiB                  |
+-----------------------------------------------------------------------------+
```

Se não houver atividade, verifique novamente que:

1. O driver CUDA corresponde ao modelo da GPU.  
2. A chamada `setUseGpu(true)` não está sendo sobrescrita mais tarde no código.  
3. Seu arquivo de licença (se houver) não está restringindo o uso da GPU.

---

## Passo 5: Lidando com Casos de Borda Comuns

### Imagens Grandes Excedendo a Memória da GPU

Quando uma imagem é enorme (por exemplo, 8000 × 8000 px), a GPU pode ficar sem memória. Uma solução rápida é reduzir a escala da imagem antes de enviá‑la ao Aspose:

```java
import java.awt.image.BufferedImage;
import javax.imageio.ImageIO;
import java.io.File;

BufferedImage original = ImageIO.read(new File("sample-large.png"));
int maxDim = 4000; // target max dimension
int width = original.getWidth();
int height = original.getHeight();

float scale = Math.min((float)maxDim / width, (float)maxDim / height);
int newWidth = Math.round(width * scale);
int newHeight = Math.round(height * scale);

BufferedImage resized = new BufferedImage(newWidth, newHeight, original.getType());
// Simple scaling (for demo purposes)
resized.getGraphics().drawImage(original, 0, 0, newWidth, newHeight, null);
ImageIO.write(resized, "png", new File("sample-resized.png"));
```

Em seguida, passe `"sample-resized.png"` para `recognizeImage`. Isso mantém o OCR preciso enquanto permanece dentro dos limites da GPU.

### PDFs Multi‑Página

O Aspose OCR também pode lidar com PDFs página a página. Percorra cada página, converta‑a em uma imagem e alimente‑a ao motor. A mesma flag **use gpu acceleration** se aplica, proporcionando um pipeline rápido de PDF‑para‑texto.

---

## Exemplo Completo Funcional (Pronto para Copiar‑Colar)

Abaixo está a classe Java completa, pronta para compilar e executar. Substitua `YOUR_DIRECTORY` pelo caminho do seu arquivo PNG.

```java
import com.aspose.ocr.*;

public class GpuExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Enable GPU acceleration (requires a CUDA‑enabled GPU and driver)
        ocrEngine.getRecognitionSettings().setUseGpu(true);

        // Step 3: (Optional) Set the number of GPU streams for parallel processing
        // Using 2 streams works well on most modern GPUs.
        ocrEngine.getRecognitionSettings().setGpuStreams(2);

        // Step 4: Perform OCR on the input image
        // This will **recognize image text** from a PNG file.
        OcrResult ocrResult = ocrEngine.recognizeImage("YOUR_DIRECTORY/sample-large.png");

        // Step 5: Print the recognized text to the console
        System.out.println("=== Recognized Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

**Saída esperada** – uma representação em texto simples de tudo que o motor conseguiu ler da imagem. Se a imagem contiver uma tabela, você receberá o conteúdo das células concatenado com quebras de linha; o Aspose não preserva o layout, mas você pode pós‑processar a string se necessário.

---

## Perguntas Frequentes

| Pergunta | Resposta |
|----------|----------|
| **Preciso de uma licença paga?** | O teste gratuito funciona para até 200 páginas e desativa a marca d'água para OCR. Para produção, uma licença remove limites e desbloqueia todo o stack de GPU. |
| **E se minha GPU for mais antiga (ex.: GTX 750)?** | GPUs mais antigas podem ainda funcionar, mas com velocidade reduzida; certifique‑se de que possui ao menos Compute Capability 3.0. |
| **Posso processar arquivos JPG ou BMP?** | Com certeza — `recognizeImage` aceita qualquer formato suportado pelo Java ImageIO. |
| **Existe uma forma de processar em lote muitas imagens?** | Envolva a chamada OCR em um loop e considere aumentar `setGpuStreams` para corresponder ao número de streams concorrentes que deseja. |
| **E se eu precisar preservar o layout?** | Use `LayoutOptions` do Aspose OCR para obter caixas delimitadoras; isso está fora do escopo deste guia rápido, mas está documentado na API. |

---

## Conclusão

Agora você tem um **exemplo java ocr** conciso e completo que **reconhece texto em imagem**, **extrai texto png** e **usa aceleração GPU** para acelerar o processamento de uma **imagem grande de OCR**. Ajustando a contagem de streams da GPU e, se necessário, reduzindo a escala de imagens excessivamente grandes, você pode adaptar a solução a praticamente qualquer configuração de hardware.

Pronto para o próximo passo? Tente alimentar uma pasta de recibos digitalizados na mesma pipeline, ou experimente a API `TextRegion` do Aspose para manter o layout original intacto. E se encontrar algum problema, os fóruns da Aspose e o Javadoc são excelentes recursos — apenas lembre‑se dos fundamentos que cobrimos aqui.

Feliz codificação, e que seu OCR seja ultra‑rápido!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}