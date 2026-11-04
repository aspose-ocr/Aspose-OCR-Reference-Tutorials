---
category: general
date: 2026-01-12
description: Execute OCR em arquivos PNG rapidamente com Python. Aprenda como extrair
  texto de imagens e faturas e carregar a imagem para OCR usando Aspose.OCR.
draft: false
keywords:
- run OCR on PNG
- extract text from image
- extract text from invoice
- load image for OCR
- Aspose OCR Python
- JSON to CSV conversion
language: pt
og_description: Execute OCR em PNG instantaneamente. Este guia mostra como extrair
  texto de imagem e fatura, carregar a imagem para OCR e salvar os resultados como
  JSON e CSV.
og_title: Execute OCR em PNG – Tutorial completo de Python
tags:
- OCR
- Python
- Image Processing
title: Execute OCR em PNG – Guia Completo em Python para Extrair Texto de Imagens
url: /pt/python-java/general/run-ocr-on-png-complete-python-guide-to-extract-text-from-im/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Executar OCR em PNG – Guia Completo em Python para Extrair Texto de Imagens

Já precisou **executar OCR em PNG** mas não tinha certeza de qual biblioteca forneceria resultados limpos e estruturados? Você não está sozinho. Em muitos projetos do mundo real—pense em automação de faturas ou digitalização de recibos—o primeiro passo é **extrair texto de imagens**, e PNG é um formato comum porque preserva qualidade sem perdas.

Neste tutorial, percorreremos um exemplo prático usando o pacote Aspose.OCR para Python. Ao final do guia, você saberá como **carregar imagem para OCR**, extrair cada linha de texto, transformar esses dados em um objeto JSON organizado e até exportá‑los para CSV para processamento posterior. Sem enrolação, apenas uma solução prática e pronta para usar.

## O que você aprenderá

- Como instalar e importar a biblioteca Aspose.OCR.  
- Os passos exatos para **executar OCR em PNG** e manipular o objeto de resultado.  
- Formas de **extrair texto de fatura** e formatar a saída como JSON ou CSV.  
- Dicas para lidar com imagens de baixo contraste, documentos multilíngues e pontuações de confiança.  
- Um exemplo completo de código copiar‑e‑colar que você pode executar hoje.

> **Pré‑requisito:** Python 3.8+ e familiaridade básica com pip. Se você nunca usou Aspose antes, não se preocupe—este guia cobre tudo que você precisa para começar.

---

## Etapa 1 – Instalar Aspose.OCR e Preparar seu Ambiente

Antes de podermos **executar OCR em PNG**, a biblioteca precisa estar presente no seu sistema.

```bash
pip install aspose-ocr
```

> **Dica profissional:** Use um ambiente virtual (`python -m venv venv`) para manter as dependências isoladas. Isso evita conflitos de versão se você estiver lidando com vários projetos.

Depois de instalado, importe os módulos que precisaremos:

```python
# Step 1: Import the OCR and JSON modules
import asposeocr as ocr
import json
```

Aqui trazemos `asposeocr` para o processamento pesado e a biblioteca interna `json` para serialização posterior.

---

## Etapa 2 – Criar o Motor OCR e Definir o Idioma

O motor OCR é o componente central que realmente lê os pixels. Para a maioria das faturas em inglês, você desejará o pacote de idioma English:

```python
# Step 2: Create an OCR engine and set the language to English
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.ENGLISH
```

> **Por que isso importa:** Especificar o idioma reduz o conjunto de caracteres, o que aumenta a precisão e acelera o processamento. Se precisar lidar com faturas multilíngues, basta trocar `ocr.Language.ENGLISH` pelo enum apropriado.

---

## Etapa 3 – Carregar a Imagem para OCR

Agora vamos **carregar a imagem para OCR**. O método `Image.load` aceita um caminho de arquivo e funciona com PNG, JPEG, BMP e outros.

```python
# Step 3: Load the image you want to analyze
image_path = "YOUR_DIRECTORY/invoice.png"
image = ocr.Image.load(image_path)
```

> **Caso extremo:** Se o PNG for incomumente grande (mais de 5 MB), considere redimensioná‑lo primeiro para manter o uso de memória razoável. Pillow pode fazer isso em uma única linha:

```python
# Optional: Resize large PNGs
from PIL import Image as PilImage
pil_img = PilImage.open(image_path)
pil_img.thumbnail((2000, 2000), PilImage.ANTIALIAS)
pil_img.save("temp_resized.png")
image = ocr.Image.load("temp_resized.png")
```

---

## Etapa 4 – Executar OCR em PNG e Capturar o Resultado

Com o motor pronto e a imagem carregada, é hora de **executar OCR em PNG** e recuperar o resultado estruturado.

```python
# Step 4: Run the OCR process on the loaded image
ocr_result = ocr_engine.process(image)
```

O objeto `ocr_result` contém uma coleção de itens `OcrRegion`, cada um com o texto reconhecido e uma pontuação de confiança (0‑100). É aqui que você obtém os dados granulares necessários para **extrair texto de fatura**.

---

## Etapa 5 – Converter o Resultado para JSON e Imprimi‑lo de Forma Legível

A maioria dos sistemas downstream adora JSON, então vamos transformar a saída OCR em uma string bem formatada.

```python
# Step 5: Convert the OCR result to a formatted JSON string and display it
json_str = ocr_result.to_json()
ocr_data = json.loads(json_str)

# Pretty‑print with indentation
print(json.dumps(ocr_data, indent=2))
```

### Exemplo de Saída

```json
{
  "pages": [
    {
      "regions": [
        {
          "text": "Invoice #12345",
          "confidence": 98.7,
          "bounds": { "x": 50, "y": 20, "width": 200, "height": 30 }
        },
        {
          "text": "Date: 2025‑12‑01",
          "confidence": 96.4,
          "bounds": { "x": 50, "y": 60, "width": 180, "height": 25 }
        },
        {
          "text": "Total Amount: $1,250.00",
          "confidence": 99.1,
          "bounds": { "x": 50, "y": 300, "width": 250, "height": 30 }
        }
      ]
    }
  ]
}
```

Observe como cada linha inclui uma métrica de confiança—perfeito para filtrar entradas de baixa confiança se você pretende **extrair texto de fatura** automaticamente.

---

## Etapa 6 – Salvar os Dados OCR como CSV (Uma Linha por Texto + Confiança)

CSV é ideal para planilhas ou importações rápidas de dados. Aspose oferece uma linha única para exportar tudo para um arquivo CSV.

```python
# Step 6: Save the OCR result as a CSV file (each line → text + confidence)
csv_path = "YOUR_DIRECTORY/invoice_output.csv"
ocr_result.save_as_csv(csv_path)
```

O CSV gerado terá a seguinte aparência:

```
"Invoice #12345",98.7
"Date: 2025-12-01",96.4
"Total Amount: $1,250.00",99.1
```

Agora você pode abri‑lo no Excel, Google Sheets ou inseri‑lo em um banco de dados.

---

## Bônus – Lidando com Texto de Baixa Confiança e PDFs Multiplas Páginas

### Filtrando por Confiança

Se você quiser apenas linhas de alta certeza, filtre o JSON antes de gravá‑lo:

```python
high_confidence = [
    region for page in ocr_data["pages"]
    for region in page["regions"]
    if region["confidence"] >= 95
]
print(json.dumps(high_confidence, indent=2))
```

### Documentos Multiplas Páginas

Aspose.OCR cria automaticamente uma nova entrada `page` para cada página em um PNG ou PDF de várias páginas. Percorra `ocr_data["pages"]` para processá‑las todas—nenhum código extra necessário.

---

## Exemplo Completo em Funcionamento

Abaixo está o **script completo** que você pode copiar, colar e executar imediatamente. Substitua `YOUR_DIRECTORY` pela pasta que contém seu arquivo PNG.

```python
import asposeocr as ocr
import json

# 1️⃣ Initialize OCR engine
engine = ocr.OcrEngine()
engine.language = ocr.Language.ENGLISH

# 2️⃣ Load the PNG image
image_path = "YOUR_DIRECTORY/invoice.png"
image = ocr.Image.load(image_path)

# 3️⃣ Perform OCR
result = engine.process(image)

# 4️⃣ Convert to JSON and pretty‑print
json_str = result.to_json()
data = json.loads(json_str)
print("=== OCR JSON Output ===")
print(json.dumps(data, indent=2))

# 5️⃣ Save as CSV (text + confidence)
csv_path = "YOUR_DIRECTORY/invoice_output.csv"
result.save_as_csv(csv_path)
print(f"\n✅ CSV saved to {csv_path}")

# 6️⃣ (Optional) Filter high‑confidence lines
high_conf = [
    r for page in data["pages"]
    for r in page["regions"]
    if r["confidence"] >= 95
]
print("\n=== High‑Confidence Regions ===")
print(json.dumps(high_conf, indent=2))
```

Execute o script com `python run_ocr.py` e você verá o dump JSON no console, um arquivo CSV no disco e uma lista filtrada de entradas de alta confiança.

---

## Perguntas Frequentes

**Q: Posso usar isso para extrair texto de um recibo escaneado em vez de uma fatura?**  
A: Absolutamente. O mesmo fluxo de trabalho se aplica—basta apontar `image_path` para o seu PNG de recibo. Se o recibo usar um idioma diferente, troque `engine.language` adequadamente.

**Q: E se meu PNG contiver texto girado?**  
A: Aspose.OCR detecta automaticamente a orientação, mas para casos difíceis você pode girar manualmente a imagem com Pillow antes de enviá‑la ao motor.

**Q: Preciso de uma licença paga para Aspose.OCR?**  
A: A biblioteca oferece um modo de avaliação gratuito com marca d'água na saída. Para uso em produção, você precisará de uma licença, que pode ser obtida no site da Aspose.

---

## Conclusão

Cobrimos tudo o que você precisa para **executar OCR em PNG** usando Python: instalar o SDK, carregar a imagem, extrair texto estruturado e salvar o resultado como JSON ou CSV. Seja para **extrair texto de imagem** em um script simples ou **extrair texto de fatura** para um pipeline de contabilidade automatizado, os passos acima fornecem uma base sólida e pronta para produção.

Em seguida, você pode explorar:

- Integrar a saída CSV com um banco de dados para armazenamento em massa de faturas.  
- Adicionar pós‑processamento com expressões regulares para extrair datas, valores ou IDs fiscais.  
- Usar o recurso `ocr_engine.recognize_barcode` se suas faturas incluírem códigos QR.

Tente, ajuste os limites de confiança e veja seu fluxo de processamento de documentos se tornar simples. Tem mais perguntas ou um caso de uso interessante para compartilhar? Deixe um comentário abaixo—feliz OCR!

![exemplo de execução de OCR em PNG](run-ocr-on-png.png "executar OCR em PNG – exemplo visual do resultado OCR")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}