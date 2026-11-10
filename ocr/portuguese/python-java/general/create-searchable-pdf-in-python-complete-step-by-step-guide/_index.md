---
category: general
date: 2026-06-19
description: Crie PDF pesquisável a partir de uma imagem usando OCR em Python. Aprenda
  a converter OCR em PDF, extrair texto de imagens e realizar OCR em imagens rapidamente.
draft: false
keywords:
- create searchable pdf
- convert ocr to pdf
- extract text from image
- convert image to pdf
- perform ocr on image
language: pt
og_description: Crie PDF pesquisável a partir de uma imagem com OCR em Python. Este
  guia mostra como converter OCR para PDF, extrair texto de uma imagem e realizar
  OCR em uma imagem.
og_title: Criar PDF pesquisável em Python – Guia completo de programação
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Create searchable PDF from an image using Python OCR. Learn to convert
    OCR to PDF, extract text from image, and perform OCR on image quickly.
  headline: Create Searchable PDF in Python – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Create searchable PDF from an image using Python OCR. Learn to convert
    OCR to PDF, extract text from image, and perform OCR on image quickly.
  name: Create Searchable PDF in Python – Complete Step‑by‑Step Guide
  steps:
  - name: The OCR confidence scores (`conf` values). Low confidence may mean the image
      is blurry.
    text: The OCR confidence scores (`conf` values). Low confidence may mean the image
      is blurry.
  - name: Bounding box coordinates—sometimes EasyOCR reports them in a different orientation.
    text: Bounding box coordinates—sometimes EasyOCR reports them in a different orientation.
  - name: That the PDF viewer isn’t set to “image‑only” mode (rare, but some viewers
      have that option).
    text: That the PDF viewer isn’t set to “image‑only” mode (rare, but some viewers
      have that option).
  type: HowTo
tags:
- OCR
- Python
- PDF
- ImageProcessing
title: Criar PDF pesquisável em Python – Guia completo passo a passo
url: /pt/python-java/general/create-searchable-pdf-in-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar PDF pesquisável em Python – Guia completo passo a passo

Já precisou **criar PDF pesquisável** a partir de um recibo escaneado, mas não sabia por onde começar? Você não está sozinho—muitos desenvolvedores encontram o mesmo obstáculo quando tentam transformar uma foto de texto em um PDF que realmente pode ser pesquisado.  

Neste tutorial vamos percorrer uma solução prática que permite que você **perform OCR on image**, transforme esse resultado OCR em um **searchable PDF**, e ainda extraia o texto bruto caso precise dele para processamento adicional. Sem enrolação, apenas um exemplo funcional que você pode copiar‑colar no seu projeto hoje.

## O que você aprenderá

- Como configurar um motor OCR leve em Python  
- Os passos exatos para **convert OCR to PDF** e salvá‑lo como um documento pesquisável  
- Maneiras de **extract text from image** para análise posterior  
- Dicas para lidar com armadilhas comuns, como orientação da imagem e arquivos grandes  
- Um script completo e executável que você pode adaptar ao seu próprio caso de uso

### Pré-requisitos

- Python 3.8+ instalado na sua máquina  
- Familiaridade básica com pip e ambientes virtuais (opcional, mas recomendado)  
- Um arquivo de imagem (PNG, JPEG, etc.) que contenha texto claro e legível por máquina  

Se você tem isso, vamos mergulhar.

## Etapa 1: Instale a Biblioteca Necessária

O trecho de código que você viu antes usa um pacote fictício `ocr`, mas as mesmas ideias se aplicam a bibliotecas reais como **EasyOCR**, **pytesseract**, ou **pdfminer.six**. Para este guia usaremos **EasyOCR** porque é puro Python, suporta muitas línguas e fornece um método prático de conversão para PDF via um helper auxiliar.

```bash
pip install easyocr pillow
```

> **Pro tip:** Instale dentro de um ambiente virtual (`python -m venv venv && source venv/bin/activate`) para manter suas dependências organizadas.

## Etapa 2: Inicialize o Motor OCR – Realize OCR na Imagem

Agora que a biblioteca está pronta, criamos um motor OCR e instruímos que trabalhe com texto em inglês. Este é o primeiro ponto onde **perform OCR on image**.

```python
import easyocr
from PIL import Image
import io

# Create an EasyOCR reader for English
reader = easyocr.Reader(['en'])  # ← performs OCR on image
```

Por que precisamos de um objeto leitor dedicado? O EasyOCR pré‑carrega os modelos de idioma, então reutilizar o mesmo `reader` para múltiplas imagens é muito mais eficiente do que reinicializá‑lo a cada vez.

## Etapa 3: Carregue a Imagem – Extraia Texto da Imagem

Vamos trazer a foto para a memória. Esta etapa é onde **extract text from image** será feita mais adiante, mas primeiro apenas a carregamos.

```python
# Replace with the path to your receipt or scanned document
image_path = "YOUR_DIRECTORY/receipt.png"

# Open the image with Pillow (helps with format handling)
pil_image = Image.open(image_path).convert("RGB")
```

Se sua imagem estiver de cabeça para baixo ou inclinada, considere usar os métodos `rotate` ou `transpose` do Pillow antes de enviá‑la ao motor OCR. Uma verificação visual rápida pode economizar horas de depuração depois.

## Etapa 4: Execute o Motor OCR e Capture os Resultados

Aqui está o núcleo do processo—enviar a imagem ao motor OCR e receber de volta dados estruturados.

```python
# EasyOCR returns a list of (bbox, text, confidence) tuples
ocr_result = reader.readtext(image_path, detail=1, paragraph=True)
```

A flag `detail=1` nos fornece caixas delimitadoras, que precisaremos quando mais tarde **convert OCR to PDF**. Se você se importa apenas com strings brutas, defina `detail=0`.

## Etapa 5: Converta o Resultado OCR em um PDF Pesquisável – Converter OCR em PDF

O EasyOCR não fornece um escritor de PDF direto, mas podemos montar o PDF nós mesmos usando Pillow e a biblioteca `reportlab`. Para manter o tutorial leve, usaremos `fpdf2`, que nos permite incorporar a imagem original e sobrepor texto invisível.

```bash
pip install fpdf2
```

```python
from fpdf import FPDF

class SearchablePDF(FPDF):
    def __init__(self, image_path):
        super().__init__()
        self.add_page()
        self.image(image_path, x=0, y=0, w=self.w, h=self.h)

    def add_ocr_text(self, ocr_data):
        # Set invisible text style
        self.set_text_color(255, 255, 255)   # white on white background
        self.set_font("Helvetica", size=12)

        for bbox, text, conf in ocr_data:
            # bbox = [(x1,y1), (x2,y2), (x3,y3), (x4,y4)]
            x_min = min(point[0] for point in bbox)
            y_min = min(point[1] for point in bbox)
            self.set_xy(x_min, y_min)
            self.cell(0, 0, txt=text, border=0)

# Create PDF instance with the original image as background
pdf = SearchablePDF(image_path)

# Add invisible OCR text on top of the image
pdf.add_ocr_text(ocr_result)

# Save the searchable PDF
output_path = "YOUR_DIRECTORY/receipt_searchable.pdf"
pdf.output(output_path)
```

O que acabou de acontecer? Colocamos a imagem escaneada como camada visível e, em seguida, escrevemos as palavras reconhecidas por cima usando texto branco que se mistura ao fundo branco. As ferramentas de busca ainda leem a camada oculta, de modo que o PDF se torna **searchable** sem alterar a aparência visual.

## Etapa 6: Salve os Bytes do PDF – Converter Imagem em PDF

Se preferir manipular o PDF na memória (por exemplo, enviando‑o por uma API), pode capturar os bytes ao invés de gravar diretamente no disco.

```python
pdf_bytes = pdf.output(dest='S').encode('latin1')  # returns a byte string

# Example: write bytes to a file (same as Step 5 but shows the conversion)
with open(output_path, "wb") as f:
    f.write(pdf_bytes)
```

Essa linha demonstra o fluxo clássico de **convert image to PDF**: você começa com uma imagem, executa OCR, sobrepõe texto e, finalmente, emite um stream de PDF.

## Etapa 7: Verifique o Resultado – Verificações Rápidas

Depois de executar o script, abra `receipt_searchable.pdf` em qualquer visualizador de PDF e teste a caixa de busca (Ctrl + F). Digite uma palavra que você sabe que aparece no recibo—se ele pular para o ponto correto, você **create searchable pdf** com sucesso!  

Se a busca falhar, verifique:

1. As pontuações de confiança do OCR (`conf` values). Baixa confiança pode indicar que a imagem está borrada.  
2. Coordenadas da caixa delimitadora—às vezes o EasyOCR as relata em uma orientação diferente.  
3. Que o visualizador de PDF não esteja configurado no modo “apenas imagem” (raro, mas alguns visualizadores têm essa opção).

## Script Completo Funcional

Juntando tudo, aqui está o arquivo Python completo, pronto para ser executado:

```python
# searchable_pdf.py
import easyocr
from PIL import Image
from fpdf import FPDF

# ---------- Configuration ----------
IMAGE_PATH = "YOUR_DIRECTORY/receipt.png"
OUTPUT_PDF = "YOUR_DIRECTORY/receipt_searchable.pdf"
# ----------------------------------

class SearchablePDF(FPDF):
    def __init__(self, image_path):
        super().__init__()
        self.add_page()
        # Fit the image to the page size
        self.image(image_path, x=0, y=0, w=self.w, h=self.h)

    def add_ocr_text(self, ocr_data):
        self.set_text_color(255, 255, 255)   # invisible white text
        self.set_font("Helvetica", size=12)
        for bbox, text, conf in ocr_data:
            x_min = min(p[0] for p in bbox)
            y_min = min(p[1] for p in bbox)
            self.set_xy(x_min, y_min)
            self.cell(0, 0, txt=text, border=0)

def main():
    # 1️⃣ Initialize OCR engine – perform OCR on image
    reader = easyocr.Reader(['en'])

    # 2️⃣ Load the image – extract text from image later
    pil_image = Image.open(IMAGE_PATH).convert("RGB")

    # 3️⃣ Run OCR and capture results
    ocr_result = reader.readtext(IMAGE_PATH, detail=1, paragraph=True)

    # 4️⃣ Convert OCR result to searchable PDF – convert OCR to PDF
    pdf = SearchablePDF(IMAGE_PATH)
    pdf.add_ocr_text(ocr_result)

    # 5️⃣ Save the PDF – convert image to PDF (or keep bytes in memory)
    pdf.output(OUTPUT_PDF)
    print(f"✅ Searchable PDF saved to {OUTPUT_PDF}")

if __name__ == "__main__":
    main()
```

Salve isso como `searchable_pdf.py`, substitua os placeholders `YOUR_DIRECTORY` por caminhos reais e execute:

```bash
python searchable_pdf.py
```

Você deverá ver uma mensagem de confirmação e um PDF recém‑criado e pesquisável na sua pasta.

## Perguntas Frequentes & Casos Limite

**E se a imagem estiver em cores?**  
EasyOCR funciona tanto com imagens em escala de cinza quanto em cores, mas converter para escala de cinza (`pil_image.convert("L")`) pode às vezes melhorar a precisão em digitalizações ruidosas.

**Posso lidar com PDFs de várias páginas?**  
Sim—faça um loop sobre cada imagem de página, execute as etapas de OCR e anexe cada página ao mesmo objeto `FPDF`. Apenas lembre‑se de resetar o cursor (`self.add_page()`) para cada nova imagem.

**Existe uma forma de manter a camada de texto original ao invés de texto branco invisível?**  
Se precisar de um PDF verdadeiro “texto‑sob‑imagem” (por exemplo, para acessibilidade), considere usar `pdfminer` ou `pikepdf` para incorporar uma camada de texto oculta com tags PDF adequadas. É mais avançado, mas o princípio permanece: imagem de fundo + texto sobreposto.

**E se a confiança do OCR for baixa?**  
Você pode filtrar palavras de baixa confiança:

```python
filtered = [item for item in ocr_result if item[2] > 0.8]  # keep >80% confidence
pdf.add_ocr_text(filtered)
```

## Conclusão – O que alcançamos

Começamos com uma imagem simples de um recibo, **performed OCR on image**, extraímos as strings reconhecidas e, finalmente, **create searchable pdf** que se comporta como qualquer documento escaneado profissionalmente. O processo cobriu todas as palavras‑chave secundárias—**convert OCR to PDF**, **extract text from image**, **convert image to PDF**, e **perform OCR on image**—para que você agora tenha uma caixa de ferramentas reutilizável para qualquer projeto similar.

### Próximos passos

- Experimente outras línguas passando seus códigos ISO para `easyocr.Reader(['en', 'es'])`.  
- Troque EasyOCR por Tesseract se precisar de uma solução totalmente offline; o restante do pipeline permanece o mesmo.  
- Adicione visualização da confiança OCR (desenhe caixas delimitadoras na imagem) para depurar digitalizações problemáticas.  

Tem uma variação que gostaria de compartilhar? Deixe um comentário, faça um fork

## O que você deve aprender a seguir?

Os tutoriais a seguir cobrem tópicos intimamente relacionados que expandem as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas de implementação em seus próprios projetos.

- [Extrair Texto de Imagem com Aspose OCR – Guia passo a passo](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Converter Imagens em PDF C# – Salvar Resultado OCR de Múltiplas Páginas](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)
- [Como fazer OCR em Imagem – Realizar OCR em Imagem no Reconhecimento de Imagem OCR](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}