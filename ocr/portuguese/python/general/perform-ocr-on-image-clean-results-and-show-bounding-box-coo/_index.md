---
category: general
date: 2026-03-28
description: Execute OCR em imagem e obtenha texto limpo com coordenadas de caixa
  delimitadora. Aprenda como extrair OCR, limpar OCR e exibir os resultados passo
  a passo.
draft: false
keywords:
- perform OCR on image
- how to extract OCR
- how to clean OCR
- display bounding box coordinates
- OCR post‑processing
- OCR bounding boxes
language: pt
og_description: Execute OCR em uma imagem, limpe a saída e exiba as coordenadas da
  caixa delimitadora em um tutorial conciso.
og_title: Realize OCR em imagem – resultados limpos e caixas delimitadoras
tags:
- OCR
- Computer Vision
- Python
title: Realizar OCR em Imagem – Resultados Limpos e Exibir Coordenadas da Caixa Delimitadora
url: /pt/python/general/perform-ocr-on-image-clean-results-and-show-bounding-box-coo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Realizar OCR em Imagem – Limpar Resultados e Mostrar Coordenadas da Caixa Delimitadora

Já precisou **realizar OCR em imagem** mas continuava obtendo texto bagunçado e sem saber onde cada palavra está na foto? Você não está sozinho. Em muitos projetos—digitalização de faturas, escaneamento de recibos ou extração simples de texto—obter a saída bruta do OCR é apenas o primeiro obstáculo. A boa notícia? Você pode limpar essa saída e ver instantaneamente as coordenadas da caixa delimitadora de cada região sem escrever um monte de código boilerplate.

Neste guia vamos percorrer **como extrair OCR**, executar um **como limpar OCR** pós‑processador e, finalmente, **exibir coordenadas da caixa delimitadora** para cada região limpa. Ao final, você terá um único script executável que transforma uma foto borrada em texto estruturado e organizado, pronto para processamento posterior.

## O que Você Precisará

- Python 3.9+ (a sintaxe abaixo funciona em 3.8 e superior)
- Um motor de OCR que suporte `recognize(..., return_structured=True)` – por exemplo, a biblioteca fictícia `engine` usada no trecho. Substitua-a por Tesseract, EasyOCR ou qualquer SDK que retorne dados de região.
- Familiaridade básica com funções e loops em Python
- Um arquivo de imagem que você deseja escanear (PNG, JPG, etc.)

> **Dica profissional:** Se você estiver usando Tesseract, a função `pytesseract.image_to_data` já fornece caixas delimitadoras. Você pode envolver seu resultado em um pequeno adaptador que imita a API `engine.recognize` mostrada abaixo.

---

![perform OCR on image example](image-placeholder.png "perform OCR on image example")

*Alt text: diagrama mostrando como realizar OCR em imagem e visualizar coordenadas da caixa delimitadora*

## Etapa 1 – Realizar OCR em Imagem e Obter Regiões Estruturadas

A primeira coisa é solicitar ao motor de OCR que retorne não apenas texto simples, mas uma lista estruturada de regiões de texto. Essa lista contém a string bruta e o retângulo que a envolve.

```python
import engine   # replace with your actual OCR library
from pathlib import Path

# Load the image you want to process
image_path = Path("sample_invoice.jpg")
image = engine.load_image(image_path)

# Step 1: Perform OCR and request a structured list of text regions
raw_result = engine.recognize(image, return_structured=True)
```

**Por que isso importa:**  
Quando você pede apenas texto simples, perde o contexto espacial. Dados estruturados permitem que você mais tarde **exiba coordenadas da caixa delimitadora**, alinhe texto com tabelas ou forneça localizações precisas a um modelo posterior.

## Etapa 2 – Como Limpar a Saída de OCR com um Pós‑Processador

Motores de OCR são ótimos em detectar caracteres, mas frequentemente deixam espaços estranhos, artefatos de quebras de linha ou símbolos reconhecidos incorretamente. Um pós‑processador normaliza o texto, corrige erros comuns de OCR e remove espaços em branco.

```python
# Step 2: Clean the plain‑text of each region using the post‑processor
processed_result = engine.run_postprocessor(raw_result)
```

Se você estiver construindo seu próprio limpador, considere:

- Remover caracteres não‑ASCII (`re.sub(r'[^\x00-\x7F]+',' ', text)`)
- Colapsar múltiplos espaços em um único espaço
- Aplicar um corretor ortográfico como `pyspellchecker` para erros óbvios

**Por que isso importa:**  
Uma string organizada torna a busca, indexação e pipelines de NLP posteriores muito mais confiáveis. Em outras palavras, **como limpar OCR** costuma ser a diferença entre um conjunto de dados utilizável e uma dor de cabeça.

## Etapa 3 – Exibir Coordenadas da Caixa Delimitadora para Cada Região Limpa

Agora que o texto está organizado, iteramos sobre cada região, imprimindo seu retângulo e a string limpa. Esta é a parte onde finalmente **exibimos coordenadas da caixa delimitadora**.

```python
# Step 3 – Iterate over the cleaned regions and display their bounding box and text
for text_region in processed_result.regions:
    # Each region has a .bounding_box attribute (x, y, width, height)
    bbox = text_region.bounding_box
    print(f"[{bbox}] {text_region.text}")
```

**Saída de exemplo**

```
[(34, 120, 210, 30)] Invoice #12345
[(34, 160, 420, 28)] Date: 2026‑03‑01
[(34, 200, 380, 28)] Total Amount: $1,254.00
```

Você pode agora alimentar essas coordenadas em uma biblioteca de desenho (por exemplo, OpenCV) para sobrepor caixas na imagem original, ou armazená‑las em um banco de dados para consultas posteriores.

## Script Completo, Pronto‑para‑Executar

A seguir está o programa completo que une as três etapas. Substitua as chamadas placeholder `engine` pelo seu SDK de OCR real.

```python
#!/usr/bin/env python3
"""
Perform OCR on image → clean results → display bounding box coordinates.
Author: Your Name
Date: 2026‑03‑28
"""

import engine               # <-- replace with your OCR library
from pathlib import Path
import sys

def main(image_path: str):
    # Load image
    image = engine.load_image(Path(image_path))

    # 1️⃣ Perform OCR and ask for structured output
    raw_result = engine.recognize(image, return_structured=True)

    # 2️⃣ Clean the raw text using the built‑in post‑processor
    processed_result = engine.run_postprocessor(raw_result)

    # 3️⃣ Show each region's bounding box and cleaned text
    print("\n=== Cleaned OCR Regions ===")
    for region in processed_result.regions:
        bbox = region.bounding_box  # (x, y, w, h)
        print(f"[{bbox}] {region.text}")

if __name__ == "__main__":
    if len(sys.argv) != 2:
        print("Usage: python perform_ocr.py <image_file>")
        sys.exit(1)
    main(sys.argv[1])
```

### Como Executar

```bash
python perform_ocr.py sample_invoice.jpg
```

Você deverá ver uma lista de caixas delimitadoras emparelhadas com texto limpo, exatamente como a saída de exemplo acima.

## Perguntas Frequentes e Casos Limítrofes

| Pergunta | Resposta |
|----------|----------|
| **E se o motor de OCR não suportar `return_structured`?** | Escreva um wrapper leve que converta a saída bruta do motor (geralmente uma lista de palavras com coordenadas) em objetos com atributos `text` e `bounding_box`. |
| **Posso obter pontuações de confiança?** | Muitos SDKs expõem uma métrica de confiança por região. Anexe‑a à instrução de impressão: `print(f"[{bbox}] {region.text} (conf: {region.confidence:.2f})")`. |
| **Como lidar com texto rotacionado?** | Pré‑procese a imagem com `cv2.minAreaRect` do OpenCV para corrigir a inclinação antes de chamar `recognize`. |
| **E se eu precisar da saída em JSON?** | Serialize `processed_result.regions` com `json.dumps([r.__dict__ for r in processed_result.regions], indent=2)`. |
| **Existe uma forma de visualizar as caixas?** | Use OpenCV: `cv2.rectangle(img, (x, y), (x+w, y+h), (0,255,0), 2)` dentro do loop, então `cv2.imwrite("annotated.jpg", img)`. |

## Conclusão

Você acabou de aprender **como realizar OCR em imagem**, limpar a saída bruta e **exibir coordenadas da caixa delimitadora** para cada região. O fluxo de três etapas—reconhecer → pós‑processar → iterar—é um padrão reutilizável que pode ser inserido em qualquer projeto Python que precise de extração de texto confiável.

### O que vem a seguir?

- **Explore diferentes back‑ends de OCR** (Tesseract, EasyOCR, Google Vision) e compare a precisão.
- **Integre com um banco de dados** para armazenar dados de regiões para arquivos pesquisáveis.
- **Adicione detecção de idioma** para direcionar cada região ao corretor ortográfico apropriado.
- **Sobreponha caixas na imagem original** para verificação visual (veja o snippet OpenCV acima).

Se você encontrar peculiaridades, lembre‑se de que o maior ganho vem de um passo sólido de pós‑processamento; uma string limpa é muito mais fácil de trabalhar do que um despejo bruto de caracteres.

Feliz codificação, e que seus pipelines de OCR estejam sempre organizados!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}