---
category: general
date: 2026-06-25
description: Como usar OCR em Python – aprenda como carregar imagem para OCR, reconhecer
  texto em uma região e extrair o texto da região rapidamente.
draft: false
keywords:
- how to use ocr
- load image for ocr
- recognize text in region
- how to extract region text
language: pt
og_description: Como usar OCR em Python – guia passo a passo para carregar uma imagem,
  reconhecer texto em uma região específica e extrair o número da fatura.
og_title: 'Como usar OCR em Python: carregar imagem e extrair texto da região'
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: How to use OCR in Python – learn how to load image for OCR, recognize
    text in region, and extract region text quickly.
  headline: 'How to Use OCR Python: Load Image and Extract Region Text'
  type: TechArticle
- questions:
  - answer: Most modern OCR engines handle a wide range of fonts, but you can boost
      accuracy by training a custom language model or pre‑processing the image (e.g.,
      applying a threshold filter).
    question: What if the invoice number is printed in a fancy font?
  - answer: Absolutely. Define a list of `Rectangle` objects—one per field—and loop
      over them, storing each result in a dictionary.
    question: Can I extract multiple fields at once?
  - answer: 'Convert each page to an image first (using `pdf2image` or similar), then
      apply the same region‑based extraction per page. --- ## Wrapping Up In this
      tutorial we covered **how to use OCR** in Python to load an image, recognize
      text in a specific region, and extract that region’s text—perfect for pull'
    question: Does this work on multi‑page PDFs?
  type: FAQPage
tags:
- OCR
- Python
- Image Processing
title: 'Como usar OCR em Python: carregar imagem e extrair texto da região'
url: /pt/python-java/general/how-to-use-ocr-python-load-image-and-extract-region-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como Usar OCR Python: Carregar Imagem e Extrair Texto da Região

**Como usar OCR em Python** é mais simples do que você imagina. Já ficou olhando para uma nota fiscal escaneada e se perguntou como extrair apenas o número da nota sem analisar a página inteira? Você não está sozinho—muitos desenvolvedores encontram esse obstáculo ao começar a brincar com reconhecimento óptico de caracteres. Neste guia, vamos percorrer o carregamento de uma imagem para OCR, a definição de um retângulo, o reconhecimento de texto nessa região e, finalmente, a extração do texto da região. Ao final, você terá um script pronto‑para‑executar que isola qualquer trecho de texto que precisar.

> *Dica de especialista:* Se você estiver trabalhando com PDFs, converta cada página em uma imagem primeiro—a maioria das bibliotecas de OCR lida melhor com PNG/JPEG.

## O Que Você Precisa

- Python 3.8+ (recomenda‑se a versão estável mais recente)  
- Uma biblioteca de OCR que exponha a classe `OcrEngine` (por exemplo, **ocr** via `pip install ocr-lib`)  
- Uma imagem de exemplo—aqui usaremos `invoice.png` colocada em uma pasta que você controla  
- Familiaridade básica com retângulos (x, y, largura, altura)  

Sem dependências pesadas, sem GPU necessária—apenas trabalho em CPU, o que mantém tudo portátil.

---

## Como Usar OCR: Inicializar o Motor (Passo 1)

Antes que qualquer texto possa ser lido, você precisa de uma instância do motor OCR. Pense nele como o cérebro que analisará os padrões de pixels.

```python
import ocr               # The OCR library
from ocr import Rectangle  # Helper for defining regions

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

*Por que isso importa:* Inicializar o motor carrega os modelos de idioma e define configurações padrão. Pular esta etapa geraria uma exceção no momento em que você chamar `recognize_region`.

---

## Carregar Imagem para OCR (Passo 2)

Agora que o motor está pronto, alimentamos ele com uma imagem. O método `Image.load` da biblioteca lida com formatos comuns e normaliza o bitmap.

```python
# Step 2: Load the image containing the invoice
image_path = "YOUR_DIRECTORY/invoice.png"
image = ocr.Image.load(image_path)
```

Se o arquivo não for encontrado, o Python lançará um `FileNotFoundError`. Certifique‑se de que o caminho seja absoluto ou relativo ao diretório de trabalho do seu script.  

*Caso extremo:* Alguns motores de OCR esperam uma imagem em escala de cinza. Se notar baixa precisão, converta a imagem primeiro:

```python
image = image.convert("L")  # L = 8‑bit pixels, black and white
```

---

## Reconhecer Texto na Região (Passo 3)

Definir a região é onde você indica ao motor *onde* olhar. O `Rectangle` aceita valores de ponto flutuante para precisão sub‑pixel, o que pode ser útil ao lidar com digitalizações de alta resolução.

```python
# Step 3: Define the rectangle that encloses the invoice number
invoice_rect = Rectangle(120.5, 45.2, 300.0, 60.0)
```

- **x, y** – canto superior esquerdo do retângulo (em pixels)  
- **largura, altura** – tamanho da caixa  

Você pode se perguntar como encontrar esses números. Uma maneira rápida é abrir a imagem em qualquer editor (por exemplo, GIMP ou Paint.NET) e usar a ferramenta de seleção para ler as coordenadas.  

*Por que não fazer OCR em toda a página?* Limitar a área reduz ruído, acelera o processamento e melhora drasticamente a precisão para campos pequenos como números de nota fiscal.

---

## Como Extrair Texto da Região (Passo 4)

Com a região definida, peça ao motor que reconheça apenas aquele recorte. O objeto de resultado contém o texto bruto e as pontuações de confiança.

```python
# Step 4: Recognize text only within the specified region
region_result = engine.recognize_region(image, invoice_rect)
```

Se o motor OCR suportar múltiplos idiomas, você pode passar um código de idioma opcional:

```python
region_result = engine.recognize_region(image, invoice_rect, lang="eng")
```

*Armadilha comum:* Alguns motores retornam uma lista de palavras em vez de uma única string. Nesse caso, concatene‑as:

```python
text = " ".join(region_result.words)
```

---

## Exibir o Número da Nota Fiscal Extraído (Passo 5)

Por fim, imprima—ou armazene—o texto extraído. Você também pode pós‑processar a string para remover espaços em branco indesejados ou caracteres não numéricos.

```python
# Step 5: Output the extracted invoice number
raw_text = region_result.text.strip()
# Optional: keep only digits (most invoice numbers are numeric)
invoice_number = "".join(filter(str.isdigit, raw_text))

print("Invoice number:", invoice_number)
```

Executar o script com um retângulo corretamente alinhado deve gerar algo como:

```
Invoice number: 20231578
```

Se aparecerem caracteres estranhos, verifique novamente as coordenadas do retângulo ou considere aumentar a resolução da imagem.

---

## Exemplo Completo Funcional

Juntando tudo, aqui está um script autocontido que você pode copiar‑colar e executar:

```python
import ocr
from ocr import Rectangle

def extract_invoice_number(image_path: str,
                          rect: Rectangle,
                          lang: str = "eng") -> str:
    """
    Loads an image, runs OCR on the specified rectangle, and returns
    a cleaned invoice number string.
    """
    engine = ocr.OcrEngine()
    image = ocr.Image.load(image_path)

    # Optional: force grayscale for better accuracy
    image = image.convert("L")

    result = engine.recognize_region(image, rect, lang=lang)
    raw = result.text.strip()
    cleaned = "".join(filter(str.isdigit, raw))
    return cleaned

if __name__ == "__main__":
    # Adjust these values to match your invoice layout
    invoice_rect = Rectangle(120.5, 45.2, 300.0, 60.0)
    invoice_path = "YOUR_DIRECTORY/invoice.png"

    number = extract_invoice_number(invoice_path, invoice_rect)
    print("Invoice number:", number)
```

Salve o arquivo como `extract_invoice.py`, substitua `YOUR_DIRECTORY` pela pasta real e execute:

```bash
python extract_invoice.py
```

Você deverá ver o número da nota fiscal impresso no console.

---

## Perguntas Frequentes

**Q: E se o número da nota fiscal estiver em uma fonte estilizada?**  
A: A maioria dos motores OCR modernos lida com uma ampla variedade de fontes, mas você pode melhorar a precisão treinando um modelo de idioma personalizado ou pré‑processando a imagem (por exemplo, aplicando um filtro de limiar).

**Q: Posso extrair vários campos de uma vez?**  
A: Absolutamente. Defina uma lista de objetos `Rectangle`—um por campo—e itere sobre eles, armazenando cada resultado em um dicionário.

**Q: Isso funciona em PDFs de várias páginas?**  
A: Converta cada página em uma imagem primeiro (usando `pdf2image` ou similar), então aplique a mesma extração baseada em região em cada página.

---

## Conclusão

Neste tutorial abordamos **como usar OCR** em Python para carregar uma imagem, reconhecer texto em uma região específica e extrair o texto dessa região—perfeito para obter números de nota fiscal, IDs de pedido ou qualquer pequeno trecho de dados de documentos escaneados. Ao isolar a área de interesse, você ganha velocidade, precisão e menos trabalho de pós‑processamento.

Pronto para o próximo passo? Experimente estender o script para **carregar imagem para OCR** a partir de uma pasta de notas fiscais em lote, ou experimente **reconhecer texto na região** para campos diferentes, como datas e totais. O mesmo padrão se aplica—basta mudar as coordenadas do retângulo.

Se encontrou algum problema ou tem ideias de melhoria, deixe um comentário abaixo. Boa codificação, e que seus pipelines de OCR sejam sempre precisos!

## O Que Você Deve Aprender a Seguir

Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas de implementação em seus próprios projetos.

- [Extrair Texto de Imagem com Aspose OCR – Guia Passo a Passo](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Como Extrair Texto de Imagem Preparando Retângulos no OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [Como Usar AspOCR: Filtros de Pré‑Processamento de Imagem para OCR em .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}