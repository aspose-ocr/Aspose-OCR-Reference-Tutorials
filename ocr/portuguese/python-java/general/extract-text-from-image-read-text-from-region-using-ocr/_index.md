---
category: general
date: 2026-07-05
description: Extraia texto de imagens usando OCR em Python. Aprenda como carregar
  a imagem para OCR, ler texto de uma região e extrair texto de uma fatura com poucas
  linhas de código.
draft: false
keywords:
- extract text from image
- read text from region
- load image for ocr
- extract text from invoice
- ocr on region
language: pt
og_description: Extraia texto de imagem com OCR em Python. Este guia mostra como carregar
  a imagem para OCR, ler texto de uma região e extrair texto de faturas rapidamente.
og_title: Extrair texto de imagem – Ler texto de região usando OCR
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Extract text from image using Python OCR. Learn how to load image for
    OCR, read text from region, and extract text from invoice with a few lines of
    code.
  headline: Extract Text from Image – Read Text from Region Using OCR
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
- Text Extraction
title: Extrair Texto de Imagem – Ler Texto de Região Usando OCR
url: /pt/python-java/general/extract-text-from-image-read-text-from-region-using-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrair Texto de Imagem – Ler Texto de Região Usando OCR

Já precisou **extrair texto de imagem** mas apenas uma parte específica importa — como o valor total em uma fatura? Você não está sozinho. Em muitos projetos do mundo real você vai se deparar com a necessidade de **ler texto de região** em vez de analisar a imagem inteira. Felizmente, com algumas linhas de Python você pode carregar uma imagem para OCR, definir uma região de interesse (ROI) e extrair exatamente os caracteres que precisa.

Neste tutorial vamos percorrer um exemplo completo e executável que mostra como **carregar imagem para OCR**, configurar uma ROI e, finalmente, **extrair texto de fatura**. Ao final, você terá um trecho pronto para uso que funciona com qualquer biblioteca OCR popular que suporte reconhecimento baseado em região.

---

## O que você precisará

- Python 3.8+ (o código funciona também no 3.10)  
- Um pacote OCR que exponha a classe `OcrEngine` (para a demonstração usaremos um módulo fictício `ocr`; substitua por `pytesseract`, `easyocr` ou qualquer biblioteca que ofereça suporte a ROI)  
- Uma imagem de exemplo — por exemplo, `invoice.png` — que contenha texto impresso e nítido  
- Familiaridade básica com funções e classes Python (não é necessário conhecimento avançado em deep learning)

Se você já tem tudo isso, ótimo — vamos começar. Caso contrário, obtenha a versão mais recente do Python em python.org e instale o pacote OCR via `pip install your-ocr-lib`.

![Exemplo de extração de texto de imagem](extract-text-from-image.png "Extrair texto de imagem – demonstração de OCR baseada em região")

*A imagem acima ilustra a região (retângulo vermelho) que vamos focar para **extrair texto de imagem**.*

---

## Etapa 1: Instalar e Importar a Biblioteca OCR

Primeiro, certifique-se de que a biblioteca OCR está disponível no seu ambiente. O padrão de importação abaixo funciona para a maioria dos pacotes que expõem uma classe `OcrEngine` de alto nível.

```python
# Install the library (uncomment if you haven't yet)
# pip install your-ocr-lib

import ocr  # replace `ocr` with the actual module name, e.g., `import easyocr`
```

> **Dica profissional:** Se você estiver usando `pytesseract`, precisará instalar o binário do Tesseract separadamente e definir `pytesseract.pytesseract.tesseract_cmd` para o seu caminho.

---

## Etapa 2: Criar o Motor OCR e Definir o Idioma

Criar o motor é simples, mas especificar o idioma melhora drasticamente a precisão, especialmente para faturas que contêm números e palavras em inglês.

```python
# Initialise the OCR engine
ocr_engine = ocr.OcrEngine()

# Set the language to English – this is crucial for invoice text
ocr_engine.language = ocr.Language.ENGLISH
```

Por que fazemos isso? O motor OCR usa modelos de idioma para prever caracteres; informá‑lo que o texto está em inglês reduz falsos positivos, como confundir “0” com “O”.

---

## Etapa 3: Carregar Imagem para OCR

Agora realmente **carregamos a imagem para OCR**. A maioria das bibliotecas aceita um caminho de arquivo ou um objeto de imagem Pillow. Aqui usamos o carregador interno da biblioteca para simplificar.

```python
# Load the source image that contains the text
image_path = "YOUR_DIRECTORY/invoice.png"
image = ocr.Image.load(image_path)   # replace with cv2.imread or PIL.Image.open if needed
```

Certifique‑se de que o caminho aponta para o diretório correto; um erro comum é esquecer o caminho relativo quando o script é executado a partir de um diretório de trabalho diferente.

---

## Etapa 4: Definir a Região de Interesse (ROI)

Definir a ROI é o cerne de **ler texto de região**. Pense nisso como desenhar um retângulo ao redor da parte da fatura que contém o valor total.

```python
# Define the ROI (left, top, width, height) in pixels
# Adjust these numbers to match your invoice layout
region_of_interest = ocr.Rectangle(100, 200, 400, 150)
```

- `left` e `top` representam as coordenadas X e Y do canto superior esquerdo do retângulo.  
- `width` e `height` definem o tamanho da caixa.  
- Você pode experimentar diferentes valores usando um visualizador de imagem que mostre as coordenadas de pixels.

> **Por que a ROI importa:** Executar OCR em toda a página desperdiça ciclos de CPU e frequentemente introduz ruído de texto, tabelas ou gráficos não relacionados. Ao focar em uma região, você obtém resultados mais limpos e processamento mais rápido.

---

## Etapa 5: Executar OCR na Região Especificada

Com tudo configurado, finalmente **extraímos texto da imagem** — mas apenas dentro da ROI que definimos.

```python
# Recognize text only within the defined ROI
ocr_result = ocr_engine.recognize(image, region_of_interest)
```

O método `recognize` retorna um objeto que normalmente contém a string bruta, pontuações de confiança e, às vezes, caixas delimitadoras para cada palavra. Para o nosso caso, precisamos apenas do texto puro.

---

## Etapa 6: Exibir o Texto Extraído

Vamos imprimir o resultado e ver o que obtivemos. Esta etapa demonstra **extrair texto de fatura** em um cenário real.

```python
# Output the extracted text
print("Text inside ROI:")
print(ocr_result.text)
```

### Saída Esperada

```
Text inside ROI:
Total Amount: $1,245.67
```

Se sua fatura usar um layout diferente, você verá o texto que estiver dentro do retângulo — talvez um número de fatura, data ou referência de pedido.

---

## Etapa 7: Envolver Tudo em uma Função Reutilizável (Opcional)

Para tornar a solução reutilizável em várias faturas, encapsule a lógica em uma função. Isso também ilustra **ocr em região** como uma utilidade genérica.

```python
def extract_text_from_region(image_path: str,
                             left: int,
                             top: int,
                             width: int,
                             height: int,
                             language: str = "ENGLISH") -> str:
    """
    Load an image, define a ROI, and return the OCR result as plain text.
    
    Parameters
    ----------
    image_path : str
        Path to the image file.
    left, top, width, height : int
        Coordinates defining the region of interest.
    language : str, optional
        Language code for the OCR engine (default is ENGLISH).
    
    Returns
    -------
    str
        Recognized text inside the ROI.
    """
    # Initialise engine
    engine = ocr.OcrEngine()
    engine.language = getattr(ocr.Language, language.upper(), ocr.Language.ENGLISH)

    # Load image
    img = ocr.Image.load(image_path)

    # Define ROI
    roi = ocr.Rectangle(left, top, width, height)

    # Recognise text
    result = engine.recognize(img, roi)

    return result.text.strip()
```

Agora você pode chamar a função com qualquer fatura:

```python
total_text = extract_text_from_region(
    "invoices/2024-03-15.png",
    left=100, top=200, width=400, height=150
)
print("Extracted total:", total_text)
```

---

## Armadilhas Comuns & Como Evitá‑las

| Problema | Por que acontece | Correção |
|----------|------------------|----------|
| **Saída em branco** | A ROI não cobre realmente nenhum texto (coordenadas erradas). | Verifique novamente os valores de pixel com um editor de imagem; adicione uma sobreposição de depuração visual. |
| **Caracteres estranhos** | Resolução baixa da imagem ou contraste ruim. | Pré‑processar a imagem: converter para escala de cinza, aplicar limiarização (`cv2.threshold`). |
| **Idioma errado** | O motor usa, por padrão, um idioma que não contém o conjunto de caracteres necessário. | Defina explicitamente `ocr_engine.language` para `ENGLISH` ou o locale apropriado. |
| **Atraso de desempenho** | Executar OCR em imagens grandes repetidamente. | Redimensione a imagem antes de carregar, ou processe apenas a ROI recortando primeiro. |

---

## Expandindo o Exemplo: Múltiplas ROIs

Às vezes, uma fatura contém vários campos que você precisa — como **extrair texto de fatura** tanto para o valor total quanto para a data da fatura. Você pode percorrer uma lista de retângulos:

```python
fields = {
    "total": ocr.Rectangle(100, 200, 400, 150),
    "date":  ocr.Rectangle(500, 200, 200, 80)
}

for name, rect in fields.items():
    txt = ocr_engine.recognize(image, rect).text.strip()
    print(f"{name.title()} → {txt}")
```

Esse padrão mantém seu código limpo e facilita a adição de mais regiões posteriormente.

---

## Conclusão

Acabamos de cobrir um fluxo de trabalho completo, de ponta a ponta, para **extrair texto de imagem** usando OCR em Python, focando em uma região específica. Ao **carregar a imagem para OCR**, definir uma **região de interesse** e invocar o motor, você pode **ler texto de região** de forma confiável — perfeito para extrair totais de faturas, datas de recibos ou quaisquer outros dados localizados.  

Sinta‑se à vontade para experimentar

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos estreitamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas de implementação em seus próprios projetos.

- [Extrair Texto de Imagem com Aspose OCR – Guia Passo a Passo](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extrair Texto de Imagem – Otimização de OCR com Aspose.OCR para .NET](/ocr/english/net/ocr-optimization/)
- [Como Extrair Texto de Imagem Preparando Retângulos no OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}