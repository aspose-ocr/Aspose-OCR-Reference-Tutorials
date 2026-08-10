---
category: general
date: 2026-02-19
description: Crie PDF pesquisável a partir de uma imagem JPG com Aspose OCR em Java.
  Converta JPG para PDF e reconheça texto da imagem rapidamente.
draft: false
keywords:
- create searchable pdf
- image to searchable pdf
- recognize text from image
- extract text from jpg
- convert jpg to pdf
language: pt
og_description: Crie PDF pesquisável a partir de uma imagem JPG com Aspose OCR. Aprenda
  como converter JPG para PDF e reconhecer texto da imagem em Java.
og_title: Criar PDF pesquisável a partir de JPG – Tutorial de OCR em Java
tags:
- aspose-ocr
- java
- pdf
- ocr
title: Criar PDF pesquisável a partir de JPG – Guia Java de Imagem para PDF pesquisável
url: /pt/java/ocr-operations/create-searchable-pdf-from-jpg-image-to-searchable-pdf-java/
---

start? ..." translate.

We need to keep bold formatting.

Proceed.

Will need to translate bullet list under "What You’ll Need". Keep bold parts.

Translate step headings.

Code block placeholders remain unchanged.

Translate table content.

Translate other paragraphs.

Make sure to keep markdown formatting.

Let's produce final content.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar PDF pesquisável a partir de JPG – Guia Java de Imagem para PDF pesquisável

Já precisou **criar PDF pesquisável** a partir de uma foto escaneada, mas não sabia por onde começar? Você não está sozinho — muitos desenvolvedores enfrentam o mesmo obstáculo quando têm um JPG que precisa ser pesquisável. A boa notícia é que, com o Aspose OCR para Java, você pode transformar essa imagem em um PDF totalmente pesquisável em apenas algumas linhas de código.

Neste tutorial, percorreremos todo o processo: carregar um JPG, reconhecer o texto e salvar o resultado como um PDF pesquisável. Ao final, você saberá como **converter jpg para pdf**, como **extrair texto de jpg** e por que essa abordagem costuma ser mais confiável do que tentar fazer OCR no PDF depois de criado.

## O que você precisará

Antes de começarmos, certifique‑se de que tem o seguinte na sua máquina:

* **Java Development Kit (JDK) 8 ou mais recente** – o código usa APIs padrão do Java.  
* Biblioteca **Aspose OCR for Java** – você pode obtê‑la no Maven Central ou baixar o JAR no site da Aspose.  
* Um **JPG de exemplo** que contenha texto legível (por exemplo, uma fatura escaneada ou uma captura de tela de um documento).

Nenhum framework adicional é necessário; o exemplo funciona em um projeto Java simples.

## Etapa 1 – Configurar o projeto e adicionar o Aspose OCR

Primeiro, crie um novo projeto Maven (ou apenas uma pasta com o JAR no classpath). Se estiver usando Maven, adicione esta dependência ao seu `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- check for the latest version -->
</dependency>
```

> **Dica profissional:** Sempre verifique a versão mais recente no repositório Maven da Aspose; lançamentos mais novos incluem ajustes de desempenho e correções de bugs.

Depois que a dependência for resolvida, você está pronto para escrever o código Java que **criará PDF pesquisável**.

## Etapa 2 – Carregar a imagem (image to searchable pdf)

O primeiro passo real é apontar o motor OCR para a imagem de origem. É aqui que a transformação **image to searchable pdf** realmente começa.

```java
import com.aspose.ocr.*;

public class SearchablePdfExample {
    public static void main(String[] args) throws Exception {
        // Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Load the JPG you want to turn into a searchable PDF
        // Replace "YOUR_DIRECTORY/input.jpg" with the actual path to your file
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/input.jpg"));
```

> **Por que isso importa:** `setImage` informa ao Aspose qual bitmap analisar. Se você fornecer uma imagem de baixa resolução, a qualidade do OCR sofrerá, portanto, certifique‑se de que o JPG tenha pelo menos 300 dpi para obter os melhores resultados.

## Etapa 3 – Reconhecer texto da imagem

Agora que o motor sabe qual imagem usar, podemos solicitar que ele **reconheça texto da imagem**. O Aspose OCR faz o trabalho pesado nos bastidores, lidando com detecção de idioma, segmentação de caracteres e pontuação de confiança.

```java
        // Perform OCR and directly output a searchable PDF
        ocrEngine.recognize()
                 .save("YOUR_DIRECTORY/output-searchable.pdf", OcrOutputFormat.SEARCHABLE_PDF);
```

A chamada `recognize()` retorna uma interface fluente, permitindo encadear o método `save`. Ao especificar `OcrOutputFormat.SEARCHABLE_PDF`, a biblioteca incorpora uma camada de texto invisível dentro do PDF enquanto preserva a aparência original da imagem.

> **Caso especial:** Se o seu JPG contiver várias páginas (por exemplo, um TIFF multipágina salvo como JPGs separados), será necessário percorrer cada arquivo e mesclar os PDFs resultantes posteriormente. O mesmo motor OCR pode ser reutilizado em cada iteração.

## Etapa 4 – Verificar o resultado

Após a operação de salvamento ser concluída, uma simples mensagem no console indica que tudo ocorreu sem problemas.

```java
        // Let the user know the PDF is ready
        System.out.println("Searchable PDF created.");
    }
}
```

Quando você abrir `output-searchable.pdf` em um visualizador como o Adobe Acrobat, deverá ser capaz de selecionar o texto oculto, copiá‑lo ou realizar uma busca — exatamente o que se espera de um **PDF pesquisável**.

### Saída esperada

Executando o programa, a impressão será:

```
Searchable PDF created.
```

E o PDF gerado exibirá o JPG original enquanto permite a seleção de texto. Se você abrir “Propriedades → Descrição → PDF Producer” do PDF, verá algo como `Aspose.OCR for Java`.

## Exemplo completo funcional

Abaixo está o arquivo fonte completo, pronto para ser executado. Copie‑e cole no seu IDE, ajuste os caminhos dos arquivos e execute.

```java
import com.aspose.ocr.*;

public class SearchablePdfExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the source image containing the text to be recognized
        // Make sure the path points to a real JPG on your disk
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/input.jpg"));

        // Step 3: Recognize the text and directly save it as a searchable PDF
        ocrEngine.recognize()
                 .save("YOUR_DIRECTORY/output-searchable.pdf", OcrOutputFormat.SEARCHABLE_PDF);

        // Step 4: Notify that the PDF has been created
        System.out.println("Searchable PDF created.");
    }
}
```

> **E se o OCR falhar?**  
> * Normalmente isso ocorre porque a imagem está muito ruidosa ou o idioma não é suportado nativamente. Você pode melhorar a precisão pré‑processando a imagem (aumentar contraste, corrigir inclinação) ou definindo explicitamente o idioma com `ocrEngine.getLanguage().setLanguage(OcrLanguage.English);`.

## Perguntas frequentes & Armadilhas

| Pergunta | Resposta |
|----------|----------|
| **Posso extrair o texto puro em vez de um PDF?** | Sim. Use `ocrEngine.recognize().save("output.txt", OcrOutputFormat.TEXT);` |
| **E se eu precisar processar um PNG?** | A mesma API funciona; basta mudar a extensão do arquivo em `fromFile`. |
| **O PDF resultante é realmente pesquisável em todos os visualizadores?** | Visualizadores modernos (Adobe Reader, Foxit, Chrome) reconhecem a camada de texto oculto. Ferramentas mais antigas podem ignorá‑la. |
| **Como controlo o tamanho da página do PDF?** | O Aspose OCR usa as dimensões da imagem por padrão. Para tamanhos personalizados, gere um PDF manualmente e sobreponha a camada de texto OCR — cenário avançado. |

## Dicas de desempenho

* **Processamento em lote:** Reuse uma única instância de `OcrEngine` para muitas imagens, evitando carregamentos repetidos da biblioteca nativa.  
* **Segurança de threads:** O motor **não** é thread‑safe; crie uma instância por thread se for paralelizar.  
* **Uso de memória:** Imagens grandes podem consumir muita RAM. Se ocorrer `OutOfMemoryError`, reduza a escala da imagem antes de enviá‑la ao motor.

## Próximos passos

Agora que você sabe como **criar PDF pesquisável**, pode explorar tarefas relacionadas:

* **Converter jpg para pdf** sem OCR (use a biblioteca Aspose PDF para um PDF de imagem simples).  
* **Extrair texto de jpg** para um arquivo `.txt` para indexação.  
* **Combinar vários PDFs pesquisáveis** em um único documento usando o `PdfFileEditor` da Aspose PDF.  

Todas essas funcionalidades se baseiam na mesma fundação que você acabou de montar.

---

### Resumo rápido

* Criamos um **PDF pesquisável** a partir de um JPG usando o Aspose OCR para Java.  
* O processo incluiu carregar a imagem, reconhecer o texto e salvar como PDF pesquisável.  
* Agora você tem um padrão reutilizável para **image to searchable PDF**, **recognize text from image**, **extract text from jpg** e **convert jpg to pdf**.

Teste com seus próprios documentos, ajuste as configurações de idioma se necessário e deixe o OCR fazer o trabalho pesado por você. Boa codificação!  

![Create searchable PDF example](placeholder.png){alt="Create searchable PDF"}

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}