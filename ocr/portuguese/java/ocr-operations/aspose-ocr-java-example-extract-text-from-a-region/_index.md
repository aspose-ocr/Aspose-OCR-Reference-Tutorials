---
category: general
date: 2026-05-03
description: O exemplo Aspose OCR Java mostra como carregar uma imagem para OCR e
  extrair texto de uma região em apenas algumas linhas de código.
draft: false
keywords:
- aspose ocr java example
- load image for OCR
- extract text from region
language: pt
og_description: O exemplo Aspose OCR Java demonstra o carregamento de uma imagem para
  OCR e a extração de texto de uma região específica, perfeito para o processamento
  de faturas.
og_title: Exemplo de OCR Aspose Java – Extração de Texto por Região
tags:
- Aspose OCR
- Java
- Image Processing
title: 'Exemplo Aspose OCR Java: Extrair Texto de uma Região'
url: /pt/java/ocr-operations/aspose-ocr-java-example-extract-text-from-a-region/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Exemplo Aspose OCR Java: Extrair Texto de uma Região

Procurando um **exemplo Aspose OCR Java** que permita extrair apenas a parte que você precisa de uma imagem? Neste guia vamos percorrer **carregamento de imagem para OCR** e **extração de texto de uma região**, ideal para números de nota fiscal, campos de formulário ou qualquer dado escondido dentro de uma imagem maior.

Você pode estar se perguntando por que limitar o OCR a um retângulo em vez de escanear a página inteira. A resposta curta: velocidade e precisão. Quando o mecanismo olha apenas para um recorte definido, ele ignora ruídos irrelevantes, executa mais rápido e costuma produzir resultados mais limpos. Ao final deste tutorial você terá um programa Java autônomo que faz exatamente isso, além de algumas dicas para evitar armadilhas comuns que atrapalham iniciantes.

## O que você precisará

Antes de mergulharmos, certifique‑se de que tem:

- **Java Development Kit (JDK) 11** ou superior instalado.  
- Biblioteca **Aspose.OCR for Java** (você pode baixar o JAR mais recente do repositório Maven Central ou do portal de download da Aspose).  
- Um arquivo de imagem que contenha o texto que você deseja ler – para a demonstração usaremos `invoice.png`, que possui o número da nota fiscal próximo ao canto superior direito.  
- Seu IDE favorito ou um editor de texto simples mais um terminal; qualquer ferramenta de build (Maven, Gradle ou apenas `javac`) serve.

É isso. Sem motores OCR adicionais, sem binários nativos, apenas Java puro e Aspose.

![Captura de tela do exemplo Aspose OCR Java](/images/aspose-ocr-java-example.png "Exemplo Aspose OCR Java mostrando extração de região")

## Exemplo Aspose OCR Java – Inicializar o Motor OCR

A primeira coisa que qualquer fluxo de OCR precisa é uma instância do motor. Aspose fornece a classe leve `OcrEngine` que cuida de tudo, desde o carregamento da imagem até a seleção de idioma.

```java
import com.aspose.ocr.*;

public class RegionOcrExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();
```

**Por que isso importa:** Criar o motor antecipadamente fornece um objeto limpo para configuração. Você pode reutilizar o mesmo `OcrEngine` para várias imagens se estiver processando um lote, o que economiza memória e tempo de inicialização.

## Carregar Imagem para OCR

Em seguida, informamos ao motor qual imagem escanear. Aspose oferece o auxiliar `ImageStream.fromFile`, que abstrai o boilerplate de baixo nível do `FileInputStream`.

```java
        // Step 2: Load the image that contains the invoice
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/invoice.png"));
```

**Dica:** Substitua `YOUR_DIRECTORY` por um caminho absoluto ou relativo que aponte para onde você armazenou `invoice.png`. Se o arquivo não for encontrado, Aspose lança uma `IOException`, então pode ser interessante envolver isso em um bloco try‑catch para código de produção.

## Definir e Extrair Texto de uma Região

Agora vem a estrela do show: o retângulo que indica ao motor onde olhar. O construtor `java.awt.Rectangle` recebe `(x, y, width, height)` – todos medidos em pixels.

```java
        // Step 3: Define the region where the invoice number is located (x, y, width, height)
        java.awt.Rectangle invoiceRegion = new java.awt.Rectangle(120, 250, 300, 80);
        ocrEngine.setRegion(invoiceRegion);   // restrict recognition to this area
```

**Como funciona:** Ao chamar `setRegion`, você limita a varredura OCR a um recorte de 300 pixels de largura que começa 120 pixels da borda esquerda e 250 pixels do topo. Ajuste esses números para combinar com seu próprio layout; uma maneira rápida de encontrá‑los é abrir a imagem em qualquer editor gráfico que mostre coordenadas de pixel.

## Habilitar Idioma e Executar o Reconhecimento

Aspose OCR suporta dezenas de idiomas, mas para um número de nota fiscal precisamos apenas de Inglês. Habilitar o idioma correto reduz falsos positivos drasticamente.

```java
        // Step 4: Enable English language for recognition
        ocrEngine.getLanguage().setEnglish(true);

        // Step 5: Perform recognition and output the extracted text
        if (ocrEngine.recognize()) {
            System.out.println("Extracted region text: " + ocrEngine.getText());
        } else {
            System.err.println("OCR recognition failed.");
        }
    }
}
```

**Por que habilitar apenas o Inglês?** O motor OCR tentará combinar caracteres de todos os idiomas habilitados, o que pode confundi‑lo quando o texto é apenas alfanumérico simples. Restringir o escopo de idioma melhora tanto a velocidade quanto a precisão.

### Saída Esperada

Quando tudo estiver configurado, você verá algo como:

```
Extracted region text: INV-12345
```

Se o retângulo estiver deslocado alguns pixels, a saída pode ficar corrompida ou vazia. Essa é uma verificação simples de sanidade: execute o programa, observe o console e verifique se o texto corresponde ao que você vê na imagem.

## Executar o Código e Verificar a Saída

Assumindo que você usa Maven, adicione a dependência Aspose OCR ao seu `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- Use the latest version available -->
</dependency>
```

Compile e execute:

```bash
mvn compile exec:java -Dexec.mainClass=RegionOcrExample
```

Ou, se preferir usar apenas `javac`:

```bash
javac -cp "aspose-ocr-23.10.jar" RegionOcrExample.java
java -cp ".:aspose-ocr-23.10.jar" RegionOcrExample
```

Você deverá ver a linha **Extracted region text** impressa no console. Se receber “OCR recognition failed”, verifique novamente o caminho do arquivo e assegure‑se de que a região realmente contém caracteres legíveis.

## Casos Limite & Variações Comuns

| Situação | O que mudar |
|-----------|----------------|
| **Múltiplos idiomas** (ex.: Inglês + Espanhol) | Chame `ocrEngine.getLanguage().setSpanish(true);` juntamente com o Inglês. |
| **Região fora dos limites da imagem** | Aspose recortará silenciosamente o retângulo, mas você perderá dados. Use `ImageInfo` (`ocrEngine.getImage().getWidth()`) para verificar as dimensões antes de definir a região. |
| **Notas fiscais dinâmicas** (layouts diferentes) | Considere fazer uma pré‑varredura leve na imagem inteira para localizar palavras‑chave como “Invoice #” e então calcular o retângulo programaticamente. |
| **Imagens com DPI alto** | Aumente `ocrEngine.getImage().setResolution(300);` para melhorar a precisão em documentos escaneados. |
| **Ajuste de desempenho** | Desabilite idiomas desnecessários, mantenha a região o menor possível e reutilize uma única instância de `OcrEngine` em vários arquivos. |

## Dicas Profissionais da Linha de Frente

- **Dica pro:** Se você precisa apenas de dígitos (comum para números de nota fiscal), habilite o modo numérico com `ocrEngine.getLanguage().setDigits(true);`. Isso elimina ruído alfabético.  
- **Cuidado com:** PNGs transparentes. Aspose às vezes interpreta mal o canal alfa; converter a imagem para JPEG com fundo sólido primeiro pode resolver saídas vazias estranhas.  
- **Lembre‑se:** O retângulo usa o sistema de coordenadas nativo da imagem, não qualquer escala de UI que você veja na tela. Sempre teste com o arquivo exato que será processado em produção.

## E agora?

Agora que você tem um **exemplo Aspose OCR Java** robusto para extração baseada em região, pode expandi‑lo em várias direções úteis:

- **Processamento em lote:** Percorra uma pasta de notas fiscais, reutilizando o mesmo `OcrEngine` para melhorar o throughput.  
- **Validação de dados:** Encaminhe o texto extraído por uma expressão regular como `INV-\\d{5}` para garantir que você capturou um número de nota válido.  
- **Integração com PDF:** Use Aspose.PDF para sobrepor o texto extraído de volta ao documento original para trilhas de auditoria.  
- **Implantação na nuvem:** Empacote o código em um serviço REST leve (Spring Boot) para que outros sistemas possam chamá‑lo sob demanda.  

Cada um desses passos envolve naturalmente os mesmos conceitos centrais — **carregar imagem para OCR**, **extrair texto de uma região** e lidar com os resultados — então a transição será tranquila.

---

*Feliz codificação! Se encontrar algum obstáculo, deixe um comentário abaixo ou consulte os fóruns da Aspose, onde a comunidade compartilha ajustes reais para layouts complicados.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}