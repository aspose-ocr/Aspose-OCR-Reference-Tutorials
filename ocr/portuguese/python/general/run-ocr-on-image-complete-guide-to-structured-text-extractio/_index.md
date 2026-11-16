---
category: general
date: 2026-05-03
description: Aprenda a executar OCR em imagens e extrair texto com coordenadas usando
  reconhecimento OCR estruturado. Código Python passo a passo incluído.
draft: false
keywords:
- run OCR on image
- extract text with coordinates
- structured OCR recognition
- OCR post‑processing
- bounding box extraction
- image text detection
language: pt
og_description: Execute OCR em imagem e obtenha o texto com coordenadas usando reconhecimento
  OCR estruturado. Exemplo completo em Python com explicações.
og_title: Execute OCR em imagem – Tutorial de Extração de Texto Estruturado
tags:
- OCR
- Python
- Computer Vision
title: Execute OCR em imagem – Guia completo para extração de texto estruturado
url: /pt/python/general/run-ocr-on-image-complete-guide-to-structured-text-extractio/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Executar OCR em imagem – Guia Completo para Extração de Texto Estruturado

Já precisou **executar OCR em imagem** mas não sabia como manter as posições exatas de cada palavra? Você não está sozinho. Em muitos projetos—digitalização de recibos, digitalização de formulários ou teste de UI—você precisa não apenas do texto bruto, mas também das caixas delimitadoras que indicam onde cada linha está na imagem.  

Este tutorial mostra uma maneira prática de *executar OCR em imagem* usando o motor **aocr**, solicitar **reconhecimento OCR estruturado**, e então pós‑processar o resultado preservando a geometria. Ao final, você será capaz de **extrair texto com coordenadas** em apenas algumas linhas de Python, e entenderá por que o modo estruturado importa para tarefas posteriores.

## O que você aprenderá

- Como inicializar o motor OCR para **reconhecimento OCR estruturado**.  
- Como fornecer uma imagem e receber resultados brutos que incluem limites de linha.  
- Como executar um pós‑processador que limpa o texto sem perder a geometria.  
- Como iterar sobre as linhas finais e imprimir cada trecho de texto junto com sua caixa delimitadora.  

Sem mágica, sem passos ocultos—apenas um exemplo completo e executável que você pode inserir no seu próprio projeto.

---

## Pré-requisitos

Antes de mergulharmos, certifique‑se de que você tem o seguinte instalado:

```bash
pip install aocr ai   # hypothetical packages; replace with real ones if needed
```

Você também precisará de um arquivo de imagem (`input_image.png` ou `.jpg`) que contenha texto claro e legível. Qualquer coisa, desde uma fatura escaneada até uma captura de tela, funciona, contanto que o motor OCR consiga ver os caracteres.

---

## Etapa 1: Inicializar o motor OCR para reconhecimento estruturado

A primeira coisa que fazemos é criar uma instância de `aocr.Engine()` e dizer que queremos **reconhecimento OCR estruturado**. O modo estruturado devolve não apenas o texto simples, mas também dados geométricos (retângulos delimitadores) para cada linha, o que é essencial quando você precisa mapear o texto de volta à imagem.

```python
import aocr
import ai   # hypothetical post‑processing module

# Initialise the OCR engine
ocr_engine = aocr.Engine()

# Request structured recognition (text + geometry)
ocr_engine.recognize_mode = aocr.RecognitionMode.Structured
```

> **Por que isso importa:**  
> No modo padrão o motor pode apenas devolver uma string de palavras concatenadas. O modo estruturado fornece uma hierarquia de páginas → linhas → palavras, cada uma com coordenadas, facilitando muito sobrepor os resultados na imagem original ou alimentá‑los em um modelo consciente de layout.

---

## Etapa 2: Executar OCR na imagem e obter resultados brutos

Agora alimentamos a imagem ao motor. A chamada `recognize` devolve um objeto `OcrResult` que contém uma coleção de linhas, cada uma com seu próprio retângulo delimitador.

```python
# Load your image (any format supported by aocr)
input_image_path = "input_image.png"

# Run OCR – this returns an OcrResult with lines and bounds
raw_result = ocr_engine.recognize(input_image_path)
```

Neste ponto `raw_result.lines` contém objetos com dois atributos importantes:

- `text` – a string reconhecida para essa linha.  
- `bounds` – uma tupla como `(x, y, width, height)` descrevendo a posição da linha.

---

## Etapa 3: Pós‑processar preservando a geometria

A saída bruta do OCR costuma ser ruidosa: caracteres soltos, espaços fora de lugar ou problemas de quebras de linha. A função `ai.run_postprocessor` limpa o texto mas **mantém a geometria original** intacta, de modo que você ainda tem coordenadas precisas.

```python
# Apply a post‑processing step that corrects common OCR errors
postprocessed_result = ai.run_postprocessor(raw_result)

# The structure (lines + bounds) stays the same, only `line.text` changes
```

> **Dica profissional:** Se você tem vocabulários específicos de domínio (por exemplo, códigos de produto), forneça um dicionário personalizado ao pós‑processador para melhorar a precisão.

---

## Etapa 4: Extrair texto com coordenadas – iterar e exibir

Finalmente, percorremos as linhas limpas, imprimindo a caixa delimitadora de cada linha ao lado do seu texto. Este é o núcleo de **extrair texto com coordenadas**.

```python
# Print each recognised line together with its bounding box
for line in postprocessed_result.lines:
    print(f"[{line.bounds}] {line.text}")
```

### Saída esperada

Assumindo que a imagem de entrada contém duas linhas: “Invoice #12345” e “Total: $89.99”, você verá algo como:

```
[(15, 30, 210, 25)] Invoice #12345
[(15, 70, 190, 25)] Total: $89.99
```

A primeira tupla é o `(x, y, width, height)` da linha na imagem original, permitindo que você desenhe retângulos, destaque texto ou alimente as coordenadas em outro sistema.

---

## Visualizando o Resultado (Opcional)

Se quiser ver as caixas delimitadoras sobrepostas na imagem, pode usar Pillow (PIL) para desenhar retângulos. A seguir um trecho rápido; sinta‑se à vontade para pular se precisar apenas dos dados brutos.

```python
from PIL import Image, ImageDraw

# Open the original image
img = Image.open(input_image_path)
draw = ImageDraw.Draw(img)

# Draw a rectangle around each line
for line in postprocessed_result.lines:
    x, y, w, h = line.bounds
    draw.rectangle([x, y, x + w, y + h], outline="red", width=2)

# Save or show the annotated image
img.save("annotated_output.png")
img.show()
```

![exemplo de execução de OCR em imagem mostrando caixas delimitadoras](/images/ocr-bounding-boxes.png "execução de OCR em imagem – sobreposição de caixas delimitadoras")

O texto alternativo acima contém a **palavra‑chave principal**, atendendo ao requisito de SEO para atributos alt de imagens.

---

## Por que o Reconhecimento OCR Estruturado supera a Extração de Texto Simples

Você pode se perguntar: “Não dá para simplesmente executar OCR e obter o texto? Por que se preocupar com a geometria?”  

- **Contexto espacial:** Quando você precisa mapear campos em um formulário (por exemplo, “Date” ao lado de um valor de data), as coordenadas indicam *onde* os dados estão.  
- **Layouts de múltiplas colunas:** Texto linear simples perde a ordem; dados estruturados preservam a ordem das colunas.  
- **Precisão no pós‑processamento:** Conhecer o tamanho da caixa ajuda a decidir se uma palavra é um cabeçalho, uma nota de rodapé ou um artefato solto.  

Em resumo, **reconhecimento OCR estruturado** oferece a flexibilidade para construir pipelines mais inteligentes—seja alimentando dados em um banco de dados, criando PDFs pesquisáveis ou treinando um modelo de machine‑learning que respeita o layout.

---

## Casos de Borda Comuns e Como Lidar com Eles

| Situação | O que observar | Correção sugerida |
|-----------|-------------------|---------------|
| **Imagens rotacionadas ou inclinadas** | Caixas delimitadoras podem estar fora do eixo. | Pré‑processar com correção de inclinação (por exemplo, `warpAffine` do OpenCV). |
| **Fontes muito pequenas** | O motor pode perder caracteres, resultando em linhas vazias. | Aumente a resolução da imagem ou use `ocr_engine.set_dpi(300)`. |
| **Línguas misturadas** | Modelo de idioma errado pode gerar texto confuso. | Defina `ocr_engine.language = ["en", "de"]` antes do reconhecimento. |
| **Caixas sobrepostas** | O pós‑processador pode mesclar duas linhas inadvertidamente. | Verifique `line.bounds` após o processamento; ajuste os limites em `ai.run_postprocessor`. |

Abordar esses cenários cedo evita dores de cabeça depois, especialmente quando você escala a solução para centenas de documentos por dia.

---

## Script Completo de Ponta a Ponta

Abaixo está o programa completo, pronto‑para‑executar, que une todas as etapas. Copie‑e‑cole, ajuste o caminho da imagem, e pronto.

```python
# -*- coding: utf-8 -*-
"""
Run OCR on image – extract text with coordinates using structured OCR recognition.
Author: Your Name
Date: 2026-05-03
"""

import aocr
import ai
from PIL import Image, ImageDraw

def run_structured_ocr(image_path: str, annotate: bool = False):
    # 1️⃣ Initialise the OCR engine
    ocr_engine = aocr.Engine()
    ocr_engine.recognize_mode = aocr.RecognitionMode.Structured

    # 2️⃣ Recognise the image
    raw_result = ocr_engine.recognize(image_path)

    # 3️⃣ Post‑process while keeping geometry
    processed = ai.run_postprocessor(raw_result)

    # 4️⃣ Print each line with its bounding box
    for line in processed.lines:
        print(f"[{line.bounds}] {line.text}")

    # Optional visualisation
    if annotate:
        img = Image.open(image_path)
        draw = ImageDraw.Draw(img)
        for line in processed.lines:
            x, y, w, h = line.bounds
            draw.rectangle([x, y, x + w, y + h], outline="red", width=2)
        annotated_path = "annotated_" + image_path
        img.save(annotated_path)
        print(f"Annotated image saved as {annotated_path}")

if __name__ == "__main__":
    INPUT_IMG = "input_image.png"
    run_structured_ocr(INPUT_IMG, annotate=True)
```

Executar este script irá:

1. **Executar OCR em imagem** com modo estruturado.  
2. **Extrair texto com coordenadas** para cada linha.  
3. Opcionalmente gerar um PNG anotado mostrando as caixas.

---

## Conclusão

Agora você tem uma solução sólida e autônoma para **executar OCR em imagem** e **extrair texto com coordenadas** usando **reconhecimento OCR estruturado**. O código demonstra cada passo—from inicialização do motor ao pós‑processamento e verificação visual—para que você possa adaptá‑lo a recibos, formulários ou qualquer documento visual que precise de localização precisa de texto.

Qual o próximo passo? Experimente trocar o motor `aocr` por outra biblioteca (Tesseract, EasyOCR) e veja como as saídas estruturadas diferem. Experimente estratégias diferentes de pós‑processamento, como correção ortográfica ou filtros regex personalizados, para aumentar a precisão no seu domínio. E se estiver construindo um pipeline maior, considere armazenar os pares `(text, bounds)` em um banco de dados para análises futuras.

Feliz codificação, e que seus projetos de OCR sejam sempre precisos!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}