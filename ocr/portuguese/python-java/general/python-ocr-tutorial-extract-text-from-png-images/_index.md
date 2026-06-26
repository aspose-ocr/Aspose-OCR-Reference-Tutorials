---
category: general
date: 2026-06-25
description: Tutorial de OCR em Python que mostra como extrair texto de arquivos PNG,
  ler imagens de texto e reconhecer texto em imagens usando um mecanismo simples e
  livre de licenças.
draft: false
keywords:
- python ocr tutorial
- extract text png
- read text image
- recognize image text
- load image for ocr
language: pt
og_description: O tutorial de OCR em Python ensina como carregar imagens para OCR,
  extrair texto de arquivos PNG e reconhecer texto em imagens em apenas algumas linhas
  de código.
og_title: Tutorial de OCR em Python – Extrair texto de PNG
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Python OCR tutorial that shows you how to extract text PNG files, read
    text image, and recognize image text using a simple, license‑free engine.
  headline: 'Python OCR Tutorial: Extract Text from PNG Images'
  type: TechArticle
- description: Python OCR tutorial that shows you how to extract text PNG files, read
    text image, and recognize image text using a simple, license‑free engine.
  name: 'Python OCR Tutorial: Extract Text from PNG Images'
  steps:
  - name: Prerequisites
    text: '- Python 3.8 or newer (the library works with 3.7+ but 3.8+ is recommended).
      - Basic familiarity with pip and virtual environments. - An image file named
      `sample.png` (or any PNG you’d like to test) saved in a folder you can reference.'
  - name: 1. Low Contrast or Dark Backgrounds
    text: '```python # Increase contrast before recognition (optional step) image
      = image.adjust_contrast(1.5) # 1.0 = no change, >1 = higher contrast result
      = engine.recognize(image) ```'
  - name: 2. Skewed Text Lines
    text: '```python # Auto‑deskew the image image = image.deskew() result = engine.recognize(image)
      ```'
  - name: 3. Non‑English Characters
    text: 'If your PNG contains accented letters or non‑Latin scripts, initialise
      the engine with the appropriate language pack:'
  - name: 4. Very Large Images
    text: 'Processing a 4000×3000 PNG can be slow. Downscale it while preserving readability:'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
- Tutorial
title: 'Tutorial de OCR em Python: Extraia Texto de Imagens PNG'
url: /pt/python-java/general/python-ocr-tutorial-extract-text-from-png-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tutorial de OCR em Python – Extrair Texto de Imagens PNG

Já se perguntou como o **python ocr tutorial** pode transformar uma captura de tela de um recibo em texto editável? Você não está sozinho. Em muitos projetos do mundo real precisamos *read text image* arquivos rapidamente, e fazer isso você mesmo supera copiar‑colar de uma GUI toda vez.  

Neste guia, percorreremos um exemplo prático que **extracts text PNG** arquivos, mostra como *load image for OCR*, e finalmente imprime o resultado de *recognize image text* — tudo com um motor OCR gratuito, apenas para avaliação. Sem chaves de licença, sem dependências pesadas — apenas Python puro e alguns pacotes pequenos.

## O que você aprenderá

- Como instalar e importar a biblioteca OCR leve.
- Os passos exatos para **load image for OCR** e lidar com armadilhas comuns.
- Maneiras de **read text image** arquivos de qualidade variada.
- Dicas para melhorar a precisão ao **extract text png** arquivos.
- Como exibir a string reconhecida e opcionalmente gravá‑la no disco.

### Pré-requisitos

- Python 3.8 ou superior (a biblioteca funciona com 3.7+ mas 3.8+ é recomendado).
- Familiaridade básica com pip e ambientes virtuais.
- Um arquivo de imagem chamado `sample.png` (ou qualquer PNG que você queira testar) salvo em uma pasta que você possa referenciar.

Se algum desses for desconhecido, pause um minuto e configure‑os — confie em mim, o resultado vale a pena.

---

## Tutorial de OCR em Python – Configurando o Motor

Primeiro de tudo: precisamos de um objeto de motor OCR. A biblioteca que usaremos é um pequeno wrapper em torno de um motor OCR nativo que funciona pronto‑para‑uso para avaliação. Não requer chave de licença, o que torna o *python ocr tutorial* perfeito para protótipos rápidos.

```python
# Step 1: Install the OCR package (run once in your terminal)
# pip install simple-ocr-lib

# Step 2: Import the library and create an engine instance
import ocr

# No license needed for evaluation mode – the engine is ready to go
engine = ocr.OcrEngine()
```

**Por que isso importa:** Criar o motor isola o runtime OCR do resto do seu código, permitindo reutilizá‑lo para múltiplas imagens sem re‑inicializar recursos pesados a cada vez.

---

## Carregar Imagem para OCR – Lendo um Arquivo PNG

Agora que o motor existe, precisamos *load image for OCR*. O método `Image.load` da biblioteca aceita um caminho e decodifica automaticamente PNG, JPEG, BMP e alguns outros formatos.

```python
# Step 3: Load the PNG you want to process
image_path = "YOUR_DIRECTORY/sample.png"   # replace with your actual path
image = ocr.Image.load(image_path)
```

> **Dica profissional:** Se seu PNG contém um canal alfa, a biblioteca o descartará automaticamente. Contudo, para obter os melhores resultados em tarefas de *read text image*, mantenha a imagem em escala de cinza — isso reduz ruído e acelera o reconhecimento.

---

## Reconhecer Texto da Imagem – Executando o Motor OCR

Com o objeto de imagem pronto, podemos finalmente **recognize image text**. Este é o núcleo do *python ocr tutorial* e requer apenas uma única linha de código.

```python
# Step 4: Perform OCR on the loaded image
result = engine.recognize(image)
```

**O que acontece nos bastidores?** O motor executa uma série de filtros de pré‑processamento (deskew, binarização) antes de alimentar o bitmap em uma rede neural treinada com milhões de caracteres. Por isso você costuma obter resultados surpreendentemente precisos mesmo em PNGs de baixa resolução.

---

## Exibir e Salvar o Texto Extraído

Ter o resultado é ótimo, mas provavelmente você quer vê‑lo ou armazená‑lo em algum lugar. O objeto `result` expõe um atributo `text` que contém a saída em forma de string simples.

```python
# Step 5: Print the recognized text to the console
print("Eval-mode result:", result.text)

# Optional: Save the text to a .txt file for later use
with open("extracted_text.txt", "w", encoding="utf-8") as f:
    f.write(result.text)
```

**Saída esperada** (supondo que `sample.png` contenha “Hello, OCR!”):

```
Eval-mode result: Hello, OCR!
```

Se você obtiver lixo em vez de caracteres legíveis, verifique a próxima seção para correções comuns.

---

## Lidando com Problemas Comuns ao Extrair Texto PNG

Mesmo os melhores motores OCR tropeçam em certas imagens. Abaixo estão obstáculos típicos e como superá‑los.

### 1. Baixo Contraste ou Fundos Escuros

```python
# Increase contrast before recognition (optional step)
image = image.adjust_contrast(1.5)   # 1.0 = no change, >1 = higher contrast
result = engine.recognize(image)
```

### 2. Linhas de Texto Inclinadas

```python
# Auto‑deskew the image
image = image.deskew()
result = engine.recognize(image)
```

### 3. Caracteres Não‑Inglês

Se seu PNG contém letras acentuadas ou scripts não‑latinos, inicialize o motor com o pacote de idioma apropriado:

```python
engine = ocr.OcrEngine(languages=["eng", "spa"])   # English + Spanish
```

### 4. Imagens Muito Grandes

Processar um PNG 4000×3000 pode ser lento. Reduza a escala preservando a legibilidade:

```python
image = image.resize(width=1024)   # keep aspect ratio
result = engine.recognize(image)
```

Esses ajustes fazem parte de um *python ocr tutorial* robusto que funciona além do cenário ideal.

---

## Script Completo – Solução de Um Arquivo

Abaixo está o script completo, pronto‑para‑executar, que incorpora todas as etapas e melhorias opcionais discutidas. Copie‑e‑cole em `ocr_extract.py` e execute `python ocr_extract.py`.

```python
# ocr_extract.py
# Complete Python OCR tutorial – extract text from PNG images

import ocr
import sys
import os

def main(image_path):
    # Verify the file exists
    if not os.path.isfile(image_path):
        print(f"Error: File not found → {image_path}")
        sys.exit(1)

    # 1️⃣ Create the OCR engine (evaluation mode, no license needed)
    engine = ocr.OcrEngine()

    # 2️⃣ Load the image – this is the "load image for OCR" step
    image = ocr.Image.load(image_path)

    # Optional preprocessing for better accuracy
    # Uncomment any of the following lines as needed:
    # image = image.adjust_contrast(1.5)   # boost contrast
    # image = image.deskew()               # correct skew
    # image = image.resize(width=1024)     # downscale large images

    # 3️⃣ Recognize the text
    result = engine.recognize(image)

    # 4️⃣ Output the result
    print("Eval-mode result:", result.text)

    # 5️⃣ Save to a .txt file (useful for batch processing)
    txt_path = os.path.splitext(image_path)[0] + "_extracted.txt"
    with open(txt_path, "w", encoding="utf-8") as out_file:
        out_file.write(result.text)
    print(f"Extracted text saved to {txt_path}")

if __name__ == "__main__":
    # Pass the image path as a command‑line argument, e.g.:
    # python ocr_extract.py ./samples/sample.png
    if len(sys.argv) < 2:
        print("Usage: python ocr_extract.py <path_to_png>")
        sys.exit(1)
    main(sys.argv[1])
```

**Execute:**  
```bash
python ocr_extract.py ./sample.png
```

Você deverá ver a string reconhecida impressa e um arquivo `sample_extracted.txt` criado ao lado da imagem.

---

## Visão Geral Visual

![Tutorial de OCR em Python – carregar imagem para OCR e extrair texto de PNG](/images/python-ocr-flow.png)

*Texto alternativo:* *Diagrama do tutorial de OCR em Python mostrando o fluxo de carregar uma imagem para OCR até extrair texto PNG.*

O diagrama ilustra a progressão linear de **load image for OCR** → **recognize image text** → **extract text PNG** e destaca onde você pode inserir etapas de pré‑processamento.

---

## Conclusão

Acabamos de concluir um **python ocr tutorial** que demonstra como *load image for OCR*, *recognize image text*, e finalmente **extract text png** arquivos com apenas alguns comandos Python. O script está totalmente funcional, trata casos de borda comuns e pode ser expandido para processamento em lote ou suporte multilíngue.

Pronto para o próximo desafio? Experimente alimentar o motor com PDFs convertidos em imagens, experimente diferentes pacotes de idioma, ou integre a etapa OCR em uma API Flask para que sua aplicação web possa ler capturas de tela enviadas em tempo real. As possibilidades para automação de *read text image* são praticamente infinitas.

Tem perguntas ou uma imagem difícil que você não consegue decifrar? Deixe um comentário abaixo, e vamos solucionar juntos. Feliz codificação!

## O que Você Deve Aprender a Seguir?

Os tutoriais a seguir cobrem tópicos estreitamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Extrair Texto de Imagem com Aspose OCR – Guia Passo a Passo](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extrair Texto de Imagem – Otimização OCR com Aspose.OCR para .NET](/ocr/english/net/ocr-optimization/)
- [Como Fazer OCR de Texto de Imagem com Idioma Usando Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}