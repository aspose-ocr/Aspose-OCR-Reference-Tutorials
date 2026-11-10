---
category: general
date: 2026-01-12
description: Tutorial de OCR em Python mostrando como extrair texto de tabela de uma
  imagem. Aprenda a ler tabelas de imagens e extrair texto selecionado com o Aspose
  OCR.
draft: false
keywords:
- python ocr tutorial
- extract table text
- read table from image
- extract selected text
- how to extract table
language: pt
og_description: Tutorial de OCR em Python que ensina como extrair texto de tabela
  de uma imagem, ler tabela de imagem e extrair texto selecionado usando o Aspose
  OCR.
og_title: 'Tutorial de OCR em Python: Extrair Texto de Tabelas a partir de Imagens'
tags:
- OCR
- Python
- AsposeOCR
title: 'Tutorial de OCR em Python: Extrair Texto de Tabelas de Imagens'
url: /pt/python-java/general/python-ocr-tutorial-extract-table-text-from-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tutorial de OCR em Python: Extrair Texto de Tabelas de Imagens

Já precisou de um **python ocr tutorial** que realmente mostre como extrair uma tabela de um formulário escaneado? Você não está sozinho. A maioria dos tutoriais para na extração genérica de texto, deixando você adivinhando como isolar aquela grade organizada de dados que lhe interessa.  

Neste guia, percorreremos um cenário do mundo real: ler uma tabela de uma imagem, extrair apenas o texto selecionado que você precisa e, finalmente, imprimir os resultados. Ao longo do caminho, adicionaremos dicas sobre **como extrair tabelas** de forma confiável, para que você não precise reinventar a roda a cada vez.

## O que você aprenderá

- Como configurar o Aspose OCR para Python.
- Como definir uma região retangular que contém uma tabela.
- Os passos exatos para **extrair texto de tabela** e **ler tabela de imagem**.
- Dicas para lidar com múltiplos idiomas ou layouts de tabela irregulares.
- Um script completo e executável que você pode inserir em seu projeto hoje.

**Pré‑requisitos**  
- Python 3.8 ou superior.  
- Familiaridade básica com conceitos de OCR (nenhuma expertise profunda necessária).  
- Uma imagem PNG ou JPEG que contenha uma tabela clara (a chamaremos de `form_with_table.png`).  

Se você tem isso, vamos mergulhar — sem enrolação, apenas código acionável.

![exemplo de tutorial python ocr da região da tabela](table_region_example.png){alt="exemplo de tutorial python ocr mostrando a região da tabela"}

## Etapa 1: Instalar e Importar Aspose OCR

Primeiro de tudo: você precisa da biblioteca Aspose OCR. O pacote está no PyPI, então um único comando `pip` resolve.

```bash
pip install aspose-ocr
```

Agora importe o módulo e quaisquer auxiliares que você precisar.

```python
# Step 1: Import the Aspose OCR package
import asposeocr as ocr
```

*Dica profissional:* Mantenha suas dependências em um arquivo `requirements.txt`. Isso facilita reproduzir o ambiente.

## Etapa 2: Inicializar o Motor OCR (Núcleo do Tutorial de OCR em Python)

Criar o motor é o coração de qualquer **python ocr tutorial**. Aqui também definimos o idioma padrão para Inglês — sinta‑se à vontade para alterá‑lo depois.

```python
# Step 2: Create an OCR engine and set the default language
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.ENGLISH
```

Por que definir o idioma? A precisão do OCR pode melhorar drasticamente quando o motor sabe quais caracteres esperar. Se você estiver lidando com formulários multilíngues, pode definir uma lista de idiomas ou sobrescrever por região (veja mais adiante).

## Etapa 3: Carregar sua Imagem

Aspose OCR funciona com a maioria dos formatos de imagem comuns. Basta apontar para o caminho do arquivo, e você terá um objeto `Image` pronto para processamento.

```python
# Step 3: Load the image that contains the form with the table
image_page = ocr.Image.load("YOUR_DIRECTORY/form_with_table.png")
```

*Caso extremo:* Imagens grandes (acima de 5 MB) podem desacelerar o processamento. Considere redimensionar ou comprimir antes do OCR se o desempenho se tornar um problema.

## Etapa 4: Definir a Região da Tabela (Ler Tabela de Imagem)

Agora vem a parte divertida: dizer ao motor *onde* a tabela está. Você fornece um `OcrRegion` com um `Rectangle` (x, y, largura, altura). As coordenadas são baseadas em pixels, então pode ser necessário experimentar um pouco.

```python
# Step 4: Define the rectangular area where the table is located
# (x, y, width, height) – adjust these values for your image
table_region = ocr.OcrRegion(
    image_page,
    ocr.Rectangle(120, 340, 800, 450)
)

# Optional: override language for this specific region
table_region.language = ocr.Language.ENGLISH
```

Por que usar uma região? Ao limitar o OCR à área da tabela, **extrair texto selecionado** fica mais rápido e evita ruído de rótulos ou gráficos ao redor. Também melhora a precisão porque o motor pode focar em um layout uniforme.

## Etapa 5: Executar OCR na Região Definida

Com a região definida, invocamos `process_region`. O método retorna um objeto `OcrResult` que contém o texto bruto, pontuações de confiança e até caixas delimitadoras, caso você precise delas depois.

```python
# Step 5: Run OCR only on the defined region
region_result = ocr_engine.process_region(table_region)
```

Se precisar extrair várias tabelas, basta repetir as Etapas 4‑5 com retângulos diferentes.

## Etapa 6: Exibir o Texto da Tabela Extraído

Finalmente, imprima — ou armazene — a representação textual da tabela. Aspose OCR devolve texto simples com quebras de linha que geralmente se alinham com as linhas, facilitando o pós‑processamento.

```python
# Step 6: Output the extracted table text
print("Table text:\n", region_result.text)
```

**Saída esperada** (exemplo):

```
Table text:
 Item        Qty   Price
 Apple       10    $1.20
 Banana      5     $0.80
 Orange      8     $1.00
```

Agora você pode alimentar essa string em analisadores `csv`, DataFrames pandas ou qualquer pipeline de análise downstream.

## Exemplo Completo Funcional

Juntando tudo, aqui está o script completo que você pode executar imediatamente. Substitua `YOUR_DIRECTORY/form_with_table.png` pelo caminho real da sua imagem.

```python
# -*- coding: utf-8 -*-
"""
Python OCR Tutorial: Extract Table Text from Images
---------------------------------------------------
A self‑contained example that demonstrates how to read a table from an image
using Aspose OCR for Python.
"""

# Install the library first:
# pip install aspose-ocr

import asposeocr as ocr

def extract_table(image_path, rect):
    """
    Extracts text from a rectangular region that contains a table.

    :param image_path: Path to the PNG/JPEG image.
    :param rect: Tuple (x, y, width, height) defining the table region.
    :return: Plain‑text representation of the table.
    """
    # Initialise OCR engine with English language
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.ENGLISH

    # Load the image
    img = ocr.Image.load(image_path)

    # Define the region (override language if needed)
    region = ocr.OcrRegion(img, ocr.Rectangle(*rect))
    region.language = ocr.Language.ENGLISH  # optional per‑region override

    # Process only this region
    result = engine.process_region(region)

    return result.text

if __name__ == "__main__":
    # Adjust these coordinates to match your table location
    table_rect = (120, 340, 800, 450)   # x, y, width, height

    # Path to your image file
    img_file = "YOUR_DIRECTORY/form_with_table.png"

    extracted_text = extract_table(img_file, table_rect)
    print("=== Extracted Table Text ===")
    print(extracted_text)
```

Execute o script com `python extract_table.py`. Se tudo estiver alinhado, você verá a tabela impressa no console.

## Perguntas Frequentes & Tratamento de Casos‑Extremos

**E se a tabela não for perfeitamente retangular?**  
Você pode dividir a tabela em várias regiões sobrepostas ou usar um retângulo maior que cubra toda a área e, em seguida, pós‑processar o texto (por exemplo, dividir por quebras de linha).

**Posso extrair apenas colunas específicas?**  
Depois de obter o texto completo da tabela, use `csv` ou `pandas` do Python para selecionar as colunas que lhe interessam. A etapa de OCR em si retorna tudo dentro do retângulo.

**Como trabalhar com tabelas não‑inglês?**  
Defina `ocr_engine.language` (ou `region.language`) para o enum apropriado, como `ocr.Language.FRENCH` ou combine múltiplos idiomas usando `ocr.Language.ENGLISH | ocr.Language.SPANISH`.

**Existe uma forma de obter caixas delimitadoras para cada célula?**  
Aspose OCR pode retornar `region_result.words`, onde cada palavra inclui uma caixa delimitadora. Você precisará mapear essas caixas de volta a uma grade — útil para análise avançada de layout.

## Dicas para Melhor Precisão

- **Limpe a imagem**: Binarize ou aumente o contraste antes de enviá‑la ao OCR. Bibliotecas como Pillow podem ajudar.
- **Evite artefatos de compressão**: Salve as digitalizações como PNG sempre que possível.
- **Fique atento ao DPI**: 300 dpi é um ponto ideal; valores menores podem causar caracteres perdidos.
- **Teste diferentes tamanhos de retângulo**: Retângulos ligeiramente maiores costumam capturar caracteres soltos que pertencem à tabela.

## Próximos Passos

Agora que você dominou **como extrair tabelas** com Aspose OCR, pode explorar:

- Converter o texto extraído em um arquivo CSV usando o módulo `csv` do Python.
- Inserir os dados em um DataFrame **pandas** para análise.
- Usar OCR para ler formulários manuscritos (requer um motor diferente ou treinamento adicional).
- Automatizar o processamento em lote de dezenas de formulários escaneados usando um simples loop `for`.

Cada uma dessas extensões se baseia nos conceitos centrais abordados neste **python ocr tutorial**, então você está bem posicionado para escalar.

*Feliz codificação! Se encontrar algum problema, deixe um comentário abaixo—terei prazer em ajudá‑lo a ajustar a extração.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}