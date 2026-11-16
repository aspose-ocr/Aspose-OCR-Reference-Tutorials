---
category: general
date: 2026-03-26
description: Aprenda a girar a imagem e a realizar OCR em Python. Este guia também
  mostra como pré‑processar a imagem para OCR e extrair texto da imagem de forma eficiente.
draft: false
keywords:
- how to rotate image
- how to perform ocr
- preprocess image for ocr
- recognize text from image
- how to extract text from image
language: pt
og_description: Como girar a imagem corretamente e depois reconhecer o texto da imagem
  usando o Aspose OCR. Siga este tutorial passo a passo para pré‑processar a imagem
  para OCR e extrair o texto da imagem.
og_title: Como Rotacionar Imagem e Realizar OCR – Guia Completo de Python
tags:
- Aspose
- Python
- Image Processing
- OCR
title: Como girar imagem e realizar OCR com Aspose em Python
url: /pt/python-java/general/how-to-rotate-image-and-perform-ocr-with-aspose-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como Rotacionar Imagem e Realizar OCR com Aspose em Python

Já se perguntou **how to rotate image** para que um motor OCR realmente consiga ler o texto? Talvez você tenha escaneado um formulário que ficou de lado, ou uma captura de câmera que girou 90° no sentido horário. Nesse caso o texto parece normal ao olho humano, mas o motor OCR vê uma bagunça. A boa notícia? É muito fácil corrigir a orientação, recortar a região de interesse e então extrair o texto — tudo com algumas linhas de Python e das bibliotecas Aspose.

Neste tutorial percorreremos todo o fluxo de trabalho: desde o carregamento de um TIFF rotacionado, correção da sua orientação, **preprocess image for OCR**, e finalmente **recognize text from image**. Ao final, você saberá **how to perform OCR** em qualquer imagem e será capaz de **extract text from image** com confiança.

## O que você precisará

- Python 3.8+ (o código funciona com qualquer versão recente)
- Pacotes `asposeocrjava` e `asposeimaging` instalados via `pip`
- Uma imagem de exemplo que precisa de rotação (por exemplo, `rotated_form.tif`)
- Um pouco de curiosidade sobre processamento de imagens

Nenhum framework pesado é necessário — apenas os dois pacotes Aspose e um pouco de lógica em Python.

---

## Etapa 1: Instalar Pacotes Aspose (How to Perform OCR)

Antes de podermos **rotate image** ou **recognize text from image**, precisamos das bibliotecas que realmente fazem o trabalho pesado.

```bash
pip install asposeocrjava asposeimaging
```

> **Pro tip:** Se você estiver atrás de um proxy corporativo, adicione `--proxy http://proxy:port` ao comando. Os pacotes são wrappers puros em Python ao redor do núcleo Aspose .NET/Java, então a instalação costuma ser instantânea.

---

## Etapa 2: Carregar o Arquivo Fonte e Rotacioná‑lo – A Etapa Central “How to Rotate Image”

```python
from asposeocrjava import OcrEngine, Rectangle
from asposeimaging import Image, RotateFlipType

# Load the original, incorrectly oriented image
source_image = Image.load("YOUR_DIRECTORY/rotated_form.tif")

# Rotate 90° clockwise – this fixes the orientation for OCR
rotated_image = source_image.rotate_flip(RotateFlipType.ROTATE_90_CLOCKWISE)
```

> **Por que rotacionar?** A maioria dos motores OCR assume que o texto vai da esquerda para a direita e de cima para baixo. Se o bitmap estiver de lado, o motor retornará lixo ou nada. Rotacionar alinha a grade de pixels com a ordem de leitura esperada, melhorando drasticamente a precisão.

> **Caso extremo:** Se você não tem certeza se a imagem precisa de rotação de 90°, 180° ou 270°, pode inspecionar `source_image.width` vs `source_image.height` ou usar as tags de orientação `exif`. O método `rotate_flip` da Aspose também suporta `ROTATE_180` e `ROTATE_270_CLOCKWISE`.

> **Image preview (optional):**  
> ![how to rotate image example](/assets/rotate-demo.png "How to rotate image – before and after rotation")

---

## Etapa 3: Recortar a Região de Interesse – Preprocess Image for OCR

Muitas vezes você só precisa de uma pequena parte da página — por exemplo, um campo de assinatura ou um bloco de números. Recortar remove ruído e acelera **how to perform OCR**.

```python
# Define the rectangle that encloses the text you care about
# (x=100, y=200, width=800, height=300) – adjust to your form
roi = Rectangle(100, 200, 800, 300)

# Crop the rotated image to that rectangle
roi_image = rotated_image.crop(roi)
```

> **Por que recortar?** Reduzir o tamanho da imagem limita o espaço de busca do motor OCR, o que diminui falsos positivos e reduz o tempo de processamento. Também ajuda se o arquivo fonte contém marcas d'água ou outros gráficos que podem confundir o motor.

> **Dica:** Se você estiver lidando com múltiplos campos, repita a etapa de recorte com retângulos diferentes e execute OCR em cada parte separadamente.

---

## Etapa 4: Inicializar o Motor OCR – O Núcleo “How to Perform OCR”

```python
# Create an instance of the OCR engine
ocr_engine = OcrEngine()
```

> **Nos bastidores:** O Aspose OCR usa uma combinação de Tesseract e análise de imagem proprietária. Instanciar o motor uma vez e reutilizá‑lo para múltiplas imagens é mais eficiente do que criar um novo objeto a cada vez.

---

## Etapa 5: Alimentar a Imagem Recortada e Reconhecer Texto – How to Extract Text from Image

```python
# Set the cropped image as the input for OCR
ocr_engine.set_image(roi_image)

# Run the recognition process
result = ocr_engine.recognize()

# Extract the plain text
extracted_text = result.get_text()
print(extracted_text)
```

### Saída Esperada

Se a ROI contém a frase “Invoice #12345 – Paid”, você verá algo como:

```
Invoice #12345 – Paid
```

Se o OCR tiver dificuldades, você pode obter espaços extras ou caracteres lidos incorretamente (por exemplo, “Invo1ce #I2345 – Pa1d”). É aí que os truques de **preprocess image for OCR** — como ajustar contraste ou aplicar binarização — entram em ação. A Aspose oferece filtros adicionais que podem ser encadeados antes da etapa 5, mas o fluxo básico acima funciona para a maioria das digitalizações limpas.

---

## Etapa 6: Opcional – Ajustar Finamente as Configurações OCR (Advanced “How to Perform OCR”)

```python
# Example: Restrict recognition to English alphanumerics only
ocr_engine.get_recognition_settings().set_recognition_language("en")
ocr_engine.get_recognition_settings().set_characters_blacklist("!@#$%^&*()")
```

> **Quando usar:** Use isso quando o documento contém muitos símbolos decorativos que você não se importa. A lista negra reduz detecções falsas.

---

## Script Completo de Ponta a Ponta

Juntando tudo, aqui está um script pronto‑para‑executar que **how to rotate image**, **preprocess image for OCR**, e finalmente **recognize text from image**:

```python
# -*- coding: utf-8 -*-
"""
Complete example: rotate, crop, and OCR an image with Aspose.
Author: Your Name
Date: 2026-03-26
"""

from asposeocrjava import OcrEngine, Rectangle
from asposeimaging import Image, RotateFlipType

def ocr_rotated_image(
    input_path: str,
    output_path: str = None,
    crop_rect: Rectangle = Rectangle(100, 200, 800, 300)
) -> str:
    """
    Loads an image, rotates it 90° clockwise, crops the region of interest,
    runs OCR, and returns the extracted text.

    Parameters
    ----------
    input_path : str
        Path to the original (possibly rotated) image file.
    output_path : str, optional
        If provided, saves the processed (rotated + cropped) image for inspection.
    crop_rect : Rectangle, optional
        Rectangle defining the ROI. Adjust to match your document layout.

    Returns
    -------
    str
        The plain text extracted from the ROI.
    """
    # Load and rotate
    src = Image.load(input_path)
    rotated = src.rotate_flip(RotateFlipType.ROTATE_90_CLOCKWISE)

    # Crop to region of interest
    roi = rotated.crop(crop_rect)

    # Optionally save the processed image for debugging
    if output_path:
        roi.save(output_path)

    # OCR
    engine = OcrEngine()
    engine.set_image(roi)
    result = engine.recognize()
    return result.get_text()

if __name__ == "__main__":
    text = ocr_rotated_image(
        "YOUR_DIRECTORY/rotated_form.tif",
        output_path="processed_roi.png"
    )
    print("=== Extracted Text ===")
    print(text)
```

Executar este script imprime o texto reconhecido no console e salva uma visualização da ROI processada como `processed_roi.png`. Você pode abrir esse PNG para verificar se a rotação e o recorte se comportaram como esperado.

---

## Perguntas Frequentes & Armadilhas

| Pergunta | Resposta |
|----------|----------|
| **E se a imagem já estiver na posição correta?** | O passo de rotação é idempotente — rotacionar uma imagem já corretamente orientada em 90° obviamente a quebrará, portanto você deve inspecionar `source_image.width` vs `height` ou usar os dados de orientação EXIF antes de chamar `rotate_flip`. |
| **Minha saída OCR contém quebras de linha extras.** | Use `result.get_text().replace("\n", " ").strip()` para limpar, ou habilite `ocr_engine.get_recognition_settings().set_remove_line_breaks(True)`. |
| **Posso processar PDFs diretamente?** | Sim — Aspose Imaging pode carregar páginas PDF como imagens (`Image.load("file.pdf")`), após o que você segue os mesmos passos de rotação e OCR. |
| **Existe uma forma de processar em lote muitos arquivos?** | Envolva `ocr_rotated_image` em um loop sobre um diretório, ou use `concurrent.futures` do Python para paralelizar. |
| **Como lidar com idiomas diferentes do inglês?** | Defina o idioma de reconhecimento via `ocr_engine.get_recognition_settings().set_recognition_language("fr")` para francês, etc. |

---

## Conclusão

Cobrimos **how to rotate image** corretamente, **preprocess image for OCR** recortando, e finalmente **how to perform OCR** para **recognize text from image** e **extract text from image** usando as bibliotecas Python da Aspose. O script completo demonstra um fluxo de trabalho prático e pronto para produção que você pode inserir em qualquer pipeline de automação.

Se você está pronto para avançar, experimente:

- **Aprimoramento de imagem** (contraste, binarização) antes do OCR
- **Extração de múltiplas ROI** para formulários com vários campos
- **Processamento em lote** de pastas inteiras de documentos escaneados
- **Integração** com sistemas downstream (por exemplo, alimentando dados extraídos em um banco de dados)

Sinta‑se à vontade para adaptar o código ao seu caso de uso, e boa codificação! 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}