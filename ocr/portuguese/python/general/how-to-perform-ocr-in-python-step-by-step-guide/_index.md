---
category: general
date: 2026-01-12
description: Como realizar OCR e converter imagem em texto rapidamente. Aprenda a
  reconhecer caracteres especiais, extrair texto de imagens e carregar a imagem para
  OCR com um exemplo completo em Python.
draft: false
keywords:
- how to perform OCR
- convert image to text
- recognize special characters
- extract text from image
- load image for OCR
language: pt
og_description: Como fazer OCR em Python, converter imagem em texto e reconhecer caracteres
  especiais. Siga este guia prático para extrair texto de imagens.
og_title: Como fazer OCR em Python – Tutorial completo
tags:
- OCR
- Python
- Image Processing
title: Como Realizar OCR em Python – Guia Passo a Passo
url: /pt/python/general/how-to-perform-ocr-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como Realizar OCR em Python – Guia Passo a Passo

Já precisou **realizar OCR** em uma captura de tela que contém caracteres latinos e cirílicos? Você não está sozinho. Em muitos projetos—seja digitalizando recibos, indexando documentos multilíngues ou construindo um arquivo pesquisável—**como realizar OCR** rapidamente se torna uma questão central.  

Neste tutorial vamos percorrer um exemplo completo e executável que mostra como **converter imagem em texto**, **reconhecer caracteres especiais** e **extrair texto de imagem** usando uma biblioteca Python simples. Ao final, você terá um script pronto‑para‑executar que carrega uma imagem para OCR, lida com conteúdo multilíngue e imprime o resultado.

## O Que Você Precisa

Antes de mergulharmos, certifique‑se de que você tem os pré‑requisitos abaixo:

- Python 3.8+ instalado na sua máquina.  
- O pacote `ocr` (ou qualquer biblioteca OCR compatível) instalado via `pip install ocr`.  
- Um arquivo de imagem (`multilingual.png`) que contenha glifos latinos e cirílicos.  
- Um editor de texto ou IDE básico—VS Code, PyCharm ou até um simples Bloco de Notas serve.  

Se você não tem o pacote `ocr`, pode substituí‑lo por `pytesseract` com algumas pequenas alterações; os conceitos principais permanecem os mesmos.

## Etapa 1: Instalar e Importar a Biblioteca OCR

Primeiro, vamos preparar o motor OCR. Importaremos a biblioteca, criaremos uma instância do motor e a configuraremos para suporte multilíngue.

```python
# Install the library (run this once in your terminal)
# pip install ocr

import ocr

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()

# Optional: Enable language packs for Latin and Cyrillic
engine.set_languages(['eng', 'rus'])  # 'eng' = English, 'rus' = Russian
```

**Por que isso importa:**  
Criar o motor é a base—sem ele você não pode **carregar imagem para OCR** depois. Habilitar pacotes de idioma garante que o motor identifique corretamente caracteres como “Ŀ”, “Ҕ” e “Ǣ”. Se pular esta etapa, o resultado será texto corrompido para scripts não latinos.

## Etapa 2: Carregar a Imagem com Texto Multilíngue

Agora apontamos o motor para o arquivo que queremos processar. O caminho pode ser absoluto ou relativo; apenas certifique‑se de que aponta para uma imagem legível.

```python
# Step 2: Load the image containing multilingual text
image_path = "YOUR_DIRECTORY/multilingual.png"  # replace with your actual path
engine.load_image(image_path)
```

> ![exemplo de como realizar OCR](/images/ocr-example.png "como realizar OCR em uma imagem multilíngue")

**Por que isso importa:**  
A chamada `load_image` lê os dados de pixel para a memória, preparando‑os para o algoritmo OCR. Se a imagem for grande, o motor pode redimensioná‑la automaticamente; você pode ajustar isso mais tarde com `engine.set_max_resolution(3000)` para digitalizações de alta resolução.

## Etapa 3: Executar o Processo de Reconhecimento

Com o motor preparado e a imagem carregada, finalmente podemos extrair o conteúdo textual.

```python
# Step 3: Perform OCR recognition on the loaded image
result = engine.recognize()
```

**Por que isso importa:**  
`recognize()` executa a pesada rede neural nos bastidores. Ela retorna um objeto que contém o texto bruto, pontuações de confiança e até caixas delimitadoras caso você precise delas para depuração visual.

## Etapa 4: Exibir o Texto Reconhecido

Vamos ver o que o motor encontrou. Imprimiremos o texto no console, mas você também pode gravá‑lo em um arquivo ou banco de dados.

```python
# Step 4: Output the recognized text, which should include characters like “Ŀ”, “Ҕ”, “Ǣ”
print("=== OCR Result ===")
print(result.text)
```

### Saída Esperada

```
=== OCR Result ===
Hello, world! Ŀ is a Latin‑extended character.
Привет, мир! Ҕ is a Cyrillic character.
Special combo: Ǣ is a ligature.
```

Se você vir algo semelhante, parabéns—você **converteu imagem em texto** e **reconheceu caracteres especiais** com sucesso.

## Lidando com Problemas Comuns

Mesmo com um script simples, você pode encontrar alguns obstáculos. Abaixo estão dicas práticas baseadas na minha experiência.

### 1. Pacotes de Idioma Ausentes

Se você obtiver pontos de interrogação (`?`) em vez de letras cirílicas, verifique se os pacotes de idioma estão instalados. Para muitos motores OCR é necessário baixar os arquivos `.traineddata` correspondentes e colocá‑los na pasta `tessdata` do motor.

```python
# Example for pytesseract
import pytesseract
pytesseract.pytesseract.tesseract_cmd = r"C:\Program Files\Tesseract-OCR\tesseract.exe"
# Ensure 'eng' and 'rus' data files exist in tessdata
```

### 2. Qualidade de Imagem Baixa

Imagens desfocadas ou de baixo contraste produzem pontuações de confiança baixas. Pré‑procese a imagem com OpenCV:

```python
import cv2

# Load, convert to grayscale, and apply thresholding
raw = cv2.imread(image_path)
gray = cv2.cvtColor(raw, cv2.COLOR_BGR2GRAY)
_, thresh = cv2.threshold(gray, 150, 255, cv2.THRESH_BINARY)

# Save a temporary cleaned image and feed it to the OCR engine
cv2.imwrite("cleaned.png", thresh)
engine.load_image("cleaned.png")
```

### 3. Arquivos Grandes e Uso de Memória

Processar uma foto de 10 MB pode consumir muita memória. Use `engine.set_max_image_size(2000)` para limitar a resolução, ou divida a imagem em blocos e faça OCR em cada bloco separadamente.

### 4. Capturando Caixas Delimitadoras

Se precisar destacar onde cada palavra aparece (útil para sobreposições de UI), acesse `result.boxes`:

```python
for box in result.boxes:
    print(f"Word: {box.text} – Coordinates: {box.x0},{box.y0},{box.x1},{box.y1}")
```

## Script Completo – Execução com Um Clique

Juntando tudo, aqui está um único arquivo que você pode executar como `python ocr_demo.py`. Ele inclui tratamento de erros, pré‑processamento opcional e comentários para clareza.

```python
#!/usr/bin/env python3
"""
Complete OCR demo: load image, recognize multilingual text,
and print results. Works with the generic 'ocr' library.
"""

import os
import sys
import ocr

def main(image_path: str):
    # Verify the image exists
    if not os.path.isfile(image_path):
        sys.exit(f"Error: File not found – {image_path}")

    # Initialize the OCR engine
    engine = ocr.OcrEngine()
    engine.set_languages(['eng', 'rus'])          # load language packs
    engine.set_max_image_size(2500)               # limit memory usage

    # Load the image
    try:
        engine.load_image(image_path)
    except Exception as e:
        sys.exit(f"Failed to load image: {e}")

    # Perform recognition
    try:
        result = engine.recognize()
    except Exception as e:
        sys.exit(f"OCR failed: {e}")

    # Output the text
    print("\n=== OCR Result ===")
    print(result.text)

    # Optional: display confidence scores
    if hasattr(result, "confidence"):
        avg_conf = sum(result.confidence) / len(result.confidence)
        print(f"\nAverage confidence: {avg_conf:.1%}")

if __name__ == "__main__":
    # Replace with your actual image path or pass as CLI argument
    img = sys.argv[1] if len(sys.argv) > 1 else "YOUR_DIRECTORY/multilingual.png"
    main(img)
```

Execute com:

```bash
python ocr_demo.py path/to/multilingual.png
```

Você deverá ver a mesma saída mostrada anteriormente, confirmando que você **extraiu texto de imagem** com sucesso.

## Conclusão

Cobrimos **como realizar OCR** em Python do início ao fim: instalando a biblioteca, carregando uma imagem, reconhecendo conteúdo multilíngue e lidando com os casos de borda mais comuns. Seguindo este guia, você agora pode **converter imagem em texto**, **reconhecer caracteres especiais** e **extrair texto de imagem** em seus próprios projetos—sem mais transcrição manual.

O que vem a seguir? Experimente:

- Adicionar mais pacotes de idioma (ex.: `spa` para espanhol).  
- Exportar resultados para JSON para processamento posterior.  
- Integrar a etapa OCR em uma API Flask para que outros serviços a chamem.  

Se encontrar alguma peculiaridade, a comunidade em torno da maioria das bibliotecas OCR é ativa—pesquise por “ocr library language pack installation” ou deixe um comentário abaixo. Boa codificação e aproveite para transformar imagens em texto pesquisável!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}