---
category: general
date: 2026-01-02
description: Aprenda a corrigir a inclinação de imagens e melhorar o contraste para
  obter texto simples rapidamente. Inclui código Python passo a passo e dicas para
  extrair texto.
draft: false
keywords:
- how to deskew image
- boost image contrast
- get plain text
- how to boost contrast
- how to extract text
language: pt
og_description: Como corrigir a inclinação da imagem e aumentar o contraste para obter
  texto simples. Exemplo completo em Python com extração de tabelas e aceleração por
  GPU.
og_title: Como Desinclinar Imagem – Tutorial Completo de OCR com GPU
tags:
- OCR
- Python
- Image Processing
title: Como Corrigir a Inclinação de Imagem – Guia de OCR Acelerado por GPU
url: /pt/python-java/general/how-to-deskew-image-gpu-accelerated-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como Desinclinar Imagem – Guia de OCR Acelerado por GPU

Já se perguntou **como desinclinar imagem** quando seus recibos chegam em um ângulo estranho? Você não está sozinho; uma foto inclinada pode transformar um recibo perfeitamente legível em uma bagunça incompreensível. A boa notícia é que, com algumas linhas de Python, você pode desinclinar automaticamente, aumentar o contraste e extrair texto puro limpo — sem precisar do Photoshop manualmente.  

Neste tutorial vamos percorrer um exemplo completo e executável que não só **como desinclinar imagem**, mas também mostra **como aumentar o contraste**, como **obter texto puro**, e ainda **como extrair texto** de tabelas que o motor OCR detecta. Ao final você terá um script autônomo que pode ser inserido em qualquer projeto.

## O que Você Precisa

- Python 3.9+ instalado (o código usa type hints, então um interpretador recente ajuda)
- A biblioteca `ocr` que fornece `OcrEngine`, `EngineMode`, `ImageProcessingOptions` e `OcrResult` (instale via `pip install ocr‑sdk` – substitua pelo nome real do pacote que você usa)
- Uma GPU com drivers compatíveis se você quiser o ganho de velocidade (opcional, mas recomendado)
- Um arquivo de imagem que esteja levemente rotacionado ou com baixo contraste, por exemplo, `receipt_skewed.jpg`

> **Dica de especialista:** Se você não tem uma GPU, basta mudar `EngineMode.GPU` para `EngineMode.CPU` e o script ainda funciona — apenas um pouco mais lento.

## Implementação Passo a Passo

A seguir dividimos a solução em blocos lógicos. Cada bloco tem um **H2** descritivo que contém a palavra‑chave principal *como desinclinar imagem* ou uma das palavras‑chave secundárias. O código está completo, comentado e pronto para ser executado.

### Como Desinclinar Imagem com OCR Acelerado por GPU

A primeira coisa que fazemos é dizer ao motor OCR para rodar na GPU e habilitar o recurso de auto‑desinclinação. Auto‑desinclinação analisa a geometria da imagem e a rotaciona de volta à posição vertical.

```python
# Import the required classes from the OCR SDK
from ocr import OcrEngine, EngineMode, ImageProcessingOptions, OcrResult

# Step 1: Initialize the OCR engine with GPU acceleration
ocr_engine = OcrEngine()
ocr_engine.set_engine_mode(EngineMode.GPU)  # Enables GPU backend for faster processing
```

> **Por que isso importa:** A aceleração por GPU pode reduzir o tempo de processamento de segundos para milissegundos, o que é crucial quando você está lidando com dezenas de recibos por minuto.

### Aumentar o Contraste da Imagem para Melhor Reconhecimento

Um recibo de baixo contraste é um pesadelo para qualquer sistema OCR. Ao aumentar o contraste damos ao motor bordas mais claras para trabalhar.

```python
# Step 2: Configure image preprocessing (auto‑deskew and contrast boost)
processing_options = ImageProcessingOptions()
processing_options.set_auto_deskew(True)          # Corrects slight rotation
processing_options.set_contrast_boost(30)         # Improves readability
ocr_engine.set_image_processing_options(processing_options)
```

> **Como aumentar o contraste:** O método `set_contrast_boost` aceita uma porcentagem; 30 % é um padrão seguro que funciona para a maioria dos recibos escaneados. Se suas imagens estiverem extremamente escuras, aumente para 50 % ou experimente.

### Obter Texto Puro da Imagem Processada

Agora que a imagem está reta e brilhante, enviamos ao motor e pedimos o resultado em texto puro.

```python
# Step 3: Load the target image and perform OCR
image_path = "YOUR_DIRECTORY/receipt_skewed.jpg"
ocr_result: OcrResult = ocr_engine.recognize_image(image_path)

# Step 4: Output the recognized plain text
print("Detected text:")
print(ocr_result.get_text())
```

**Saída esperada** (truncada para brevidade):

```
Detected text:
Store: Coffee Corner
Date: 2025-12-31
Item          Qty   Price
Latte          1    $3.50
Muffin         2    $5.00
Total                $8.50
```

> **Como obter texto puro:** O método `get_text()` remove qualquer informação de layout e devolve uma string limpa, que você pode então armazenar em um banco de dados, enviar para uma API ou alimentar em análises posteriores.

### Como Extrair Texto de Tabelas Detectadas

Frequentemente os recibos contêm dados tabulares (itens, quantidades, preços). O SDK OCR pode detectar tabelas e permitir que você itere sobre linhas e células.

```python
# Step 5: If tables are detected, print their contents
if ocr_result.get_tables():
    for idx, table in enumerate(ocr_result.get_tables()):
        print(f"\nTable {idx + 1}:")
        for row in table.get_rows():
            # Join each cell's text with a tab for easy copy‑paste
            print("\t".join(cell.get_text() for cell in row.get_cells()))
```

**Exemplo de saída de tabela**:

```
Table 1:
Item	Qty	Price
Latte	1	$3.50
Muffin	2	$5.00
Total		$8.50
```

> **Por que extrair tabelas:** Dados estruturados facilitam o cálculo de totais, a geração de relatórios ou a alimentação de softwares de contabilidade.

### Script Completo Funcionando

Juntando tudo, aqui está o script que você pode copiar‑colar em `deskew_and_ocr.py`:

```python
# deskew_and_ocr.py
from ocr import OcrEngine, EngineMode, ImageProcessingOptions, OcrResult

def main(image_path: str) -> None:
    # Initialize OCR engine with GPU acceleration
    ocr_engine = OcrEngine()
    ocr_engine.set_engine_mode(EngineMode.GPU)

    # Configure preprocessing: auto‑deskew + contrast boost
    opts = ImageProcessingOptions()
    opts.set_auto_deskew(True)
    opts.set_contrast_boost(30)  # Adjust if needed
    ocr_engine.set_image_processing_options(opts)

    # Perform OCR
    result: OcrResult = ocr_engine.recognize_image(image_path)

    # Print plain text
    print("Detected text:")
    print(result.get_text())

    # Print tables, if any
    if result.get_tables():
        for i, tbl in enumerate(result.get_tables(), start=1):
            print(f"\nTable {i}:")
            for row in tbl.get_rows():
                print("\t".join(cell.get_text() for cell in row.get_cells()))

if __name__ == "__main__":
    # Replace with your actual image location
    main("YOUR_DIRECTORY/receipt_skewed.jpg")
```

Execute-o com:

```bash
python deskew_and_ocr.py
```

Você deverá ver o texto limpo e quaisquer tabelas detectadas impressas no console.

## Casos de Borda Comuns & Como Lidar com Eles

| Situação | O Que Fazer |
|-----------|------------|
| **Imagem está de cabeça para baixo** | Aumente a confiança de `set_auto_deskew(True)` também chamando `set_rotation_correction(True)` se o SDK oferecer essa opção. |
| **Aumento de contraste deixa a imagem muito clara** | Reduza a porcentagem passada para `set_contrast_boost` (por exemplo, 15 %). |
| **GPU não está disponível** | Troque `EngineMode.GPU` por `EngineMode.CPU`; o resto do pipeline permanece inalterado. |
| **Tabelas são perdidas** | Experimente uma digitalização em resolução maior ou habilite `set_table_detection(True)` se a biblioteca disponibilizar. |

## Próximos Passos: Do Texto Puro aos Dados Estruturados

Agora que você sabe **como desinclinar imagem**, **como aumentar o contraste** e **como obter texto puro**, pode querer:

- Analisar o texto puro com expressões regulares para extrair pares chave‑valor (ex.: `total`, `date`).
- Armazenar os resultados em um banco SQLite ou PostgreSQL para relatórios futuros.
- Conectar o script a uma função serverless (AWS Lambda, Azure Functions) para processar uploads automaticamente.

Todas essas extensões se baseiam na mesma fundação que cobrimos aqui.

## Conclusão

Percorremos **como desinclinar imagem** usando um motor OCR acelerado por GPU, demonstramos **como aumentar o contraste** para um reconhecimento mais nítido, mostramos exatamente **como obter texto puro** e ainda abordamos **como extrair texto** de tabelas. O script completo e executável une tudo, permitindo que você o insira em qualquer projeto Python e comece a extrair dados limpos de fotos inclinadas e de baixo contraste imediatamente.

Experimente com alguns dos seus próprios recibos, ajuste o nível de contraste e deixe o OCR fazer o trabalho pesado. Se encontrar alguma peculiaridade, volte à tabela de casos de borda acima — a maioria dos problemas se resolve com um pequeno ajuste.

Boa codificação, e que suas imagens estejam sempre retas e brilhantes!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}