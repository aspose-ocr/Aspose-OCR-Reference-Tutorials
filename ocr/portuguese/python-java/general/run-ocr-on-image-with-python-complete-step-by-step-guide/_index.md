---
category: general
date: 2026-06-06
description: Execute OCR em imagem usando Python e veja as pontuações de confiança.
  Aprenda como filtrar palavras de baixa confiança, definir limites e lidar com casos
  extremos.
draft: false
keywords:
- run OCR on image
- Python OCR tutorial
- OCR confidence threshold
- low‑confidence word detection
- image text extraction
language: pt
og_description: Execute OCR em imagem no Python, inspecione os níveis de confiança
  e filtre palavras de baixa confiança. Este tutorial guia você por um exemplo completo
  e executável.
og_title: Execute OCR em Imagem com Python – Guia Completo
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: Run OCR on image using Python and see confidence scores. Learn how
    to filter low‑confidence words, set thresholds, and handle edge cases.
  headline: Run OCR on Image with Python – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Run OCR on image using Python and see confidence scores. Learn how
    to filter low‑confidence words, set thresholds, and handle edge cases.
  name: Run OCR on Image with Python – Complete Step‑by‑Step Guide
  steps:
  - name: Install and Import the OCR Engine
    text: First, make sure the OCR library is available. **EasyOCR** works out‑of‑the‑box
      for many languages and gives you a confidence score per word.
  - name: Run OCR on the Image
    text: Now we actually **run OCR on image**. The `recognize_image` method from
      the original example is replaced with EasyOCR’s `readtext` call, which returns
      a list of `(bbox, text, confidence)` tuples.
  - name: Summarize Overall Confidence
    text: 'Unlike the earlier snippet that printed a single `confidence` attribute,
      EasyOCR gives a confidence per word. To get an overall sense, we’ll average
      them:'
  - name: List Low‑Confidence Words
    text: Now comes the part that directly answers the “list words whose confidence
      is below the desired threshold” requirement. We’ll set a **OCR confidence threshold**
      of 0.80 (80 %) by default, but you can adjust it.
  - name: Edge Cases & Variations
    text: 1. **Batch Processing** – If you need to **run OCR on image** files in bulk,
      wrap the above logic in a loop that iterates over a directory. 2. **Multiple
      Languages** – Pass a list like `['en', 'fr']` to `easyocr.Reader` and the engine
      will detect both. 3. **Alternative Engines** – Want to try **pyte
  type: HowTo
- questions:
  - answer: Not directly. Convert each PDF page to an image first (e.g., with `pdf2image`)
      and then feed the PNG/JPEG into the script.
    question: Does this work with PDFs?
  - answer: 'Try image preprocessing: increase contrast, remove background noise,
      or rotate the image to a horizontal baseline. EasyOCR also accepts a `contrast_ths`
      parameter you can tweak.'
    question: My confidence numbers are all low—what can I do?
  - answer: Absolutely. After the low‑confidence loop, write `ocr_results` to a `csv.DictWriter`
      where each row contains `text`, `confidence`, and bounding‑box coordinates.
    question: Can I export the results to CSV?
  - answer: 'EasyOCR automatically uses CUDA if a compatible GPU and PyTorch are installed.
      Verify with `torch.cuda.is_available()` before running the script. --- ## Conclusion
      We’ve just **run OCR on image** using Python, inspected the overall confidence,
      and isolated any low‑confidence words that need a {{< /b'
    question: Is there a GPU‑accelerated version?
  type: FAQPage
tags:
- OCR
- Python
- Image Processing
title: Execute OCR em Imagem com Python – Guia Completo Passo a Passo
url: /pt/python-java/general/run-ocr-on-image-with-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Executar OCR em Imagem com Python – Guia Completo Passo a Passo

Já precisou **executar OCR em arquivos de imagem** mas não sabia como obter texto confiável deles? Você não está sozinho—muitos desenvolvedores enfrentam o mesmo problema quando as palavras extraídas parecem instáveis e a pontuação de confiança é um mistério.  

Neste guia mergulharemos direto em uma solução funcional: você verá como executar OCR em imagem, ler a confiança geral e extrair quaisquer palavras de baixa confiança que possam precisar de revisão manual. Ao final você terá um script reutilizável, entenderá por que cada linha importa e saberá como ajustar o limite de confiança para seus próprios projetos.

## O que este tutorial cobre

Percorreremos todo o fluxo de trabalho—from carregar uma imagem até imprimir um relatório organizado das palavras que ficaram abaixo de 80 % de confiança. Ao longo do caminho discutiremos:

* Escolher um motor de OCR sólido (usaremos **EasyOCR**, uma biblioteca Python de OCR popular)  
* Interpretar o atributo `confidence` que todo resultado de OCR retorna  
* Filtrar palavras com um **limite de confiança de OCR** personalizado  
* Estender o script para processamento em lote ou motores alternativos como **pytesseract**  

Nenhuma experiência prévia com OCR é necessária, apenas familiaridade básica com Python e um ambiente de trabalho (Python 3.9+ recomendado).  

Pronto para transformar capturas de tela desfocadas em texto limpo e pesquisável? Vamos começar.

---

## ## Como Executar OCR em Imagem com Python

O coração do tutorial é um trecho de três etapas que espelha o código que você já viu. A seguir, vamos dividir cada linha, explicar o porquê e, depois, fornecer um script completo pronto para copiar‑e‑colar.

### Etapa 1: Instalar e Importar o Motor de OCR

Primeiro, certifique‑se de que a biblioteca de OCR está disponível. **EasyOCR** funciona pronto para uso em muitas línguas e fornece uma pontuação de confiança por palavra.

```bash
pip install easyocr
```

```python
import easyocr  # The engine that will run OCR on image files
import os
```

*Por que EasyOCR?* Ele inclui um modelo de deep‑learning treinado em conjuntos de dados diversos, então você costuma obter valores de confiança mais altos que o motor Tesseract mais antigo, especialmente em imagens de qualidade mista.

> **Dica profissional:** Se você estiver em um ambiente restrito (por exemplo, um contêiner Docker pequeno), `pytesseract` pode ser mais leve, mas você perderá parte da precisão moderna que o EasyOCR oferece.

### Etapa 2: Executar OCR na Imagem

Agora realmente **executamos OCR em imagem**. O método `recognize_image` do exemplo original é substituído pela chamada `readtext` do EasyOCR, que devolve uma lista de tuplas `(bbox, text, confidence)`.

```python
# Initialize the OCR reader for English (you can add more languages as needed)
reader = easyocr.Reader(['en'])

# Path to the image you want to process
image_path = os.path.join("YOUR_DIRECTORY", "mixed_quality.png")

# Perform OCR – this is the step where we run OCR on image
ocr_results = reader.readtext(image_path, detail=1, paragraph=False)
```

Cada entrada em `ocr_results` tem a forma:

```python
[
    ((x1, y1, x2, y2, x3, y3, x4, y4), "Detected text", 0.92),
    ...
]
```

O terceiro elemento (`0.92` no exemplo) é a pontuação de confiança, variando de 0 a 1.

### Etapa 3: Resumir a Confiança Geral

Ao contrário do trecho anterior que imprimia um único atributo `confidence`, o EasyOCR fornece confiança por palavra. Para ter uma ideia geral, vamos calcular a média delas:

```python
# Extract just the confidence numbers
confidences = [item[2] for item in ocr_results]

# Compute the mean confidence (overall confidence)
overall_confidence = sum(confidences) / len(confidences) if confidences else 0

print(f"Overall confidence: {overall_confidence:.2%}")
```

*Por que a média?* Ela oferece uma verificação rápida de saúde—se a confiança geral estiver abaixo, digamos, 70 %, provavelmente será necessário melhorar a imagem (melhor iluminação, pré‑processamento, etc.).

### Etapa 4: Listar Palavras de Baixa Confiança

Agora vem a parte que responde diretamente ao requisito “listar palavras cuja confiança está abaixo do limite desejado”. Definiremos um **limite de confiança de OCR** de 0.80 (80 %) por padrão, mas você pode ajustá‑lo.

```python
# Define the confidence threshold – tweak as needed
THRESHOLD = 0.80

print("\nLow‑confidence words:")
low_confidence_found = False
for bbox, text, conf in ocr_results:
    if conf < THRESHOLD:
        low_confidence_found = True
        print(f"  • '{text}' ({conf:.2%})")
if not low_confidence_found:
    print("  All words meet the confidence threshold.")
```

O laço imprime cada palavra que não atingiu o corte, junto com sua confiança percentual. Este é o análogo exato do laço original `for recognized_word in recognition_result.words`, mas agora funciona com o formato de saída do EasyOCR.

---

## ## Entendendo as Pontuações de Confiança do OCR

Confiança não é um número mágico; é a estimativa do modelo sobre quão certo ele está de uma transcrição específica. Aqui estão alguns pontos a ter em mente:

| Situação | Confiança Típica | O que Fazer |
|-----------|-------------------|------------|
| Digitalização clara e de alta resolução | 0.95 – 1.00 | Nenhum trabalho extra necessário |
| Leve desfoque ou iluminação desigual | 0.80 – 0.94 | Considerar pré‑processamento leve (aumento de contraste) |
| Muito ruído, texto rotacionado | < 0.70 | Aplicar pré‑processamento de imagem (deskew, denoise) ou mudar para outro motor de OCR |

> **Atenção:** Algumas línguas (por exemplo, escrita cursiva) naturalmente produzem pontuações mais baixas. Ajuste o limite conforme necessário.

### Casos Limite e Variações

1. **Processamento em Lote** – Se precisar **executar OCR em imagem** em massa, envolva a lógica acima em um laço que itere sobre um diretório.  
2. **Múltiplas Línguas** – Passe uma lista como `['en', 'fr']` para `easyocr.Reader` e o motor detectará ambas.  
3. **Motores Alternativos** – Quer tentar **pytesseract**? Substitua o bloco do leitor por:

   ```python
   import pytesseract
   from PIL import Image

   img = Image.open(image_path)
   raw_text = pytesseract.image_to_string(img, output_type=pytesseract.Output.DICT)
   # raw_text['text'] contains the full string,
   # raw_text['conf'] holds per‑character confidence.
   ```

   Você então precisará agregar as confidências por caractere em valores por palavra—um pouco mais de trabalho, mas viável.

4. **Truques de Pré‑processamento** – Aplicar filtros OpenCV (`cv2.threshold`, `cv2.GaussianBlur`) pode aumentar a confiança em digitalizações ruidosas.  

---

## ## Script Completo, Pronto para Executar

Abaixo está o arquivo Python completo que você pode colocar no seu projeto. Salve como `ocr_report.py` e execute `python ocr_report.py`. Certifique‑se de que o caminho da imagem aponta para um arquivo real.

```python
#!/usr/bin/env python3
"""
run_ocr_on_image.py

A self‑contained script that:
  1. Runs OCR on an image using EasyOCR.
  2. Prints the overall confidence.
  3. Lists any words whose confidence falls below a configurable threshold.

Author: Your Name
Date: 2026‑06‑06
"""

import os
import easyocr

# --------------------------- Configuration --------------------------- #
IMAGE_DIR = "YOUR_DIRECTORY"          # <-- Change to your folder
IMAGE_NAME = "mixed_quality.png"      # <-- Change to your file name
THRESHOLD = 0.80                       # Confidence threshold (0‑1)

# --------------------------- Helper Functions ----------------------- #
def load_image_path():
    """Construct the absolute path to the target image."""
    return os.path.join(IMAGE_DIR, IMAGE_NAME)

def run_ocr(image_path):
    """Run OCR on the image and return detailed results."""
    reader = easyocr.Reader(['en'])
    return reader.readtext(image_path, detail=1, paragraph=False)

def compute_overall_confidence(results):
    """Return the mean confidence across all detected words."""
    if not results:
        return 0.0
    confidences = [item[2] for item in results]
    return sum(confidences) / len(confidences)

def report_low_confidence_words(results, threshold):
    """Print words whose confidence is below the given threshold."""
    low_conf = [(text, conf) for _, text, conf in results if conf < threshold]
    if not low_conf:
        print("All words meet the confidence threshold.")
    else:
        for text, conf in low_conf:
            print(f"Low‑confidence word: '{text}' ({conf:.2%})")

# --------------------------- Main Execution ------------------------ #
def main():
    image_path = load_image_path()
    if not os.path.isfile(image_path):
        print(f"❌ Image not found: {image_path}")
        return

    # Step 1: Run OCR on image
    ocr_results = run_ocr(image_path)

    # Step 2: Show overall confidence
    overall = compute_overall_confidence(ocr_results)
    print(f"Overall confidence: {overall:.2%}")

    # Step 3: List low‑confidence words
    print("\n--- Low‑confidence words (threshold: {0:.0%}) ---".format(THRESHOLD))
    report_low_confidence_words(ocr_results, THRESHOLD)

if __name__ == "__main__":
    main()
```

**Saída esperada** (seus números variarão):

```
Overall confidence: 78.45%

--- Low‑confidence words (threshold: 80%) ---
Low‑confidence word: 'recgnition' (62.13%)
Low‑confidence word: 'imgae' (57.90%)
```

Se todas as palavras ultrapassarem a barra de 80 % você verá a mensagem amigável “All words meet the confidence threshold.” em vez disso.

---

## ## Perguntas Frequentes (FAQ)

**Q: Isso funciona com PDFs?**  
A: Não diretamente. Converta cada página do PDF em uma imagem primeiro (por exemplo, com `pdf2image`) e então alimente o PNG/JPEG ao script.

**Q: Meus números de confiança estão todos baixos—o que posso fazer?**  
A: Experimente pré‑processamento de imagem: aumente o contraste, remova ruído de fundo ou rotacione a imagem para uma linha de base horizontal. EasyOCR também aceita um parâmetro `contrast_ths` que você pode ajustar.

**Q: Posso exportar os resultados para CSV?**  
A: Absolutamente. Após o laço de baixa confiança, escreva `ocr_results` em um `csv.DictWriter` onde cada linha contém `text`, `confidence` e as coordenadas da caixa delimitadora.

**Q: Existe uma versão acelerada por GPU?**  
A: EasyOCR usa CUDA automaticamente se uma GPU compatível e o PyTorch estiverem instalados. Verifique com `torch.cuda.is_available()` antes de executar o script.

---

## Conclusão

Acabamos de **executar OCR em imagem** usando Python, inspecionar a confiança geral e isolar quaisquer palavras de baixa confiança que precisam de revisão manual.

## O que Você Deve Aprender a Seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Como Definir Valor de Limiar em Reconhecimento de Imagem OCR](/ocr/english/net/ocr-settings/set-threshold-value/)
- [Como Usar Aspose OCR para Resultado JSON em Reconhecimento de Imagem](/ocr/english/net/text-recognition/get-result-as-json/)
- [Extrair Texto de Imagem – Otimização OCR com Aspose.OCR para .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}