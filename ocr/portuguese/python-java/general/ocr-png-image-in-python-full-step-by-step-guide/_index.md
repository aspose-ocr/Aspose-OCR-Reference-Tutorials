---
category: general
date: 2026-06-06
description: OCR de imagem PNG com Python – aprenda como extrair texto de uma imagem,
  execute um exemplo de OCR em Python e até leia texto em grego antigo facilmente.
draft: false
keywords:
- ocr png image
- extract text from image
- python ocr example
- read ancient greek
- recognize image text
language: pt
og_description: OCR de imagem PNG em Python explicado. Este guia mostra como extrair
  texto de uma imagem, executar um exemplo de OCR em Python e ler grego antigo com
  facilidade.
og_title: OCR de Imagem PNG em Python – Tutorial Completo
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: OCR PNG image with Python – learn how to extract text from image, run
    a python OCR example and even read ancient greek text easily.
  headline: OCR PNG Image in Python – Full Step‑by‑Step Guide
  type: TechArticle
- description: OCR PNG image with Python – learn how to extract text from image, run
    a python OCR example and even read ancient greek text easily.
  name: OCR PNG Image in Python – Full Step‑by‑Step Guide
  steps:
  - name: Prerequisites
    text: '| Requirement | Why it matters | |-------------|----------------| | Python
      3.8+ | Modern syntax and type hints | | `pytesseract` package | Thin wrapper
      around the Tesseract engine | | Tesseract OCR binaries (≥ 5.0) | The actual
      engine that does the heavy lifting | | Greek language data (`grc.trained'
  - name: How do I improve accuracy on a noisy PNG?
    text: '- Convert the image to grayscale: `img = img.convert(''L'')` - Apply a
      binary threshold: `img = img.point(lambda x: 0 if x < 128 else 255, ''1'')`
      - Upscale with `img = img.resize((img.width*2, img.height*2), Image.LANCZOS)`'
  - name: Can I process a whole folder of PNGs?
    text: Absolutely. Wrap the `recognize_image` call in a `for` loop over `Path.glob("*.png")`.
      Store each result in a dictionary or write to a CSV for later analysis.
  - name: What if I need to extract numbers only?
    text: 'Pass a custom **config** string to `image_to_string`:'
  - name: Is there a way to get confidence scores?
    text: Yes—use `pytesseract.image_to_data` which returns a TSV with confidence
      per word. You can filter out low‑confidence tokens before assembling the final
      string.
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: OCR de Imagem PNG em Python – Guia Completo Passo a Passo
url: /pt/python-java/general/ocr-png-image-in-python-full-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR de Imagem PNG em Python – Guia Completo Passo a Passo

Já se perguntou como **OCR PNG image** arquivos diretamente de um script Python? Talvez você tenha uma pasta cheia de manuscritos antigos digitalizados e precise **extract text from image** arquivos sem digitar tudo manualmente. A boa notícia é que você não precisa de um PhD em visão computacional—apenas algumas linhas de código e a biblioteca certa, e você estará lendo grego antigo em segundos.

Neste tutorial vamos percorrer um **python OCR example** que reconhece texto de um PNG, define o idioma para grego politônico e imprime o resultado. Ao final você saberá exatamente como **recognize image text**, lidar com armadilhas comuns e adaptar o script para outros idiomas ou formatos de imagem.

## O que você aprenderá

- Instalar e configurar uma biblioteca Python OCR (pytesseract + Tesseract OCR)
- Criar uma instância do motor OCR e carregar um arquivo PNG
- Definir o idioma de reconhecimento para grego politônico para que você possa **read ancient greek**
- Exibir o texto reconhecido e solucionar problemas típicos
- Estender o script para processar em lote múltiplos PNGs ou mudar para outro idioma

### Pré-requisitos

| Requisito | Por que importa |
|-------------|----------------|
| Python 3.8+ | Sintaxe moderna e dicas de tipo |
| `pytesseract` package | Wrapper leve ao redor do motor Tesseract |
| Tesseract OCR binaries (≥ 5.0) | O motor real que faz o trabalho pesado |
| Greek language data (`grc.traineddata`) | Necessário para **read ancient greek** corretamente |
| Uma imagem PNG que você deseja analisar (ex., `ancient_greek.png`) | Nosso alvo para a demonstração **ocr png image** |

Você pode instalar a parte Python com:

```bash
pip install pytesseract Pillow
```

E no Ubuntu/macOS você adicionaria o próprio motor:

```bash
# Ubuntu
sudo apt-get install tesseract-ocr libtesseract-dev

# macOS (Homebrew)
brew install tesseract
```

Não se esqueça de baixar os dados treinados do grego politônico:

```bash
wget https://github.com/tesseract-ocr/tessdata/blob/main/greek.traineddata -P /usr/share/tesseract-ocr/4.00/tessdata/
```

*(O caminho pode ser diferente; ajuste `TESSDATA_PREFIX` se necessário.)*

## OCR PNG Image: Criar a Instância do Motor

A primeira coisa que precisamos é um objeto que se comunica com o Tesseract. No `pytesseract` o motor é acessado através de funções ao nível do módulo, mas para clareza vamos encapsulá‑lo em uma classe pequena. Isso espelha o conceito de “engine” que você viu no snippet original.

```python
from pathlib import Path
from PIL import Image
import pytesseract

class OcrEngine:
    """
    Simple wrapper around pytesseract to keep the API similar to the original example.
    """
    def __init__(self, tess_cmd: str = "tesseract"):
        # You can point pytesseract to a custom binary if you installed it somewhere unusual.
        pytesseract.pytesseract.tesseract_cmd = tess_cmd

    def set_recognition_language(self, language: str):
        """
        Store the language code for later calls.
        Example: 'grc' for Greek polytonic.
        """
        self.lang = language

    def recognize_image(self, image_path: str):
        """
        Open the PNG, run OCR, and return the raw result object.
        """
        img = Image.open(image_path)
        # pytesseract returns a string; we wrap it for consistency with the original code.
        text = pytesseract.image_to_string(img, lang=self.lang)
        return OcrResult(text=text)

class OcrResult:
    """Container for OCR output – mimics the .text attribute used in the example."""
    def __init__(self, text: str):
        self.text = text
```

**Por que encapsular?**  
- Mantém a API pública idêntica ao snippet que você começou, tornando a migração indolor.  
- Permite adicionar logging ou tratamento de erros mais tarde sem tocar no fluxo principal.  
- Demonstrar boa prática de OOP—algo que desenvolvedores seniores apreciam.

## Extrair Texto da Imagem: Definir o Idioma para Grego Politônico

Agora que temos um motor, precisamos dizer a ele qual idioma esperar. O grego politônico usa diacríticos que não são cobertos pelos dados padrão “greek”, então apontamos o Tesseract para o arquivo treinado `grc`.

```python
# Step 2: Set the recognition language to Greek polytonic
engine = OcrEngine()
engine.set_recognition_language("grc")   # 'grc' is the ISO‑639‑2 code for ancient Greek
```

Se você quiser **extract text from image** arquivos em outro idioma, basta substituir `"grc"` por `"eng"` para Inglês, `"fra"` para Francês, etc. A mesma linha funciona para qualquer idioma que você tenha instalado.

## Reconhecer Texto da Imagem: Executar o OCR em um PNG

Com o idioma definido, alimentamos o PNG no motor. O exemplo original usava um caminho codificado; vamos torná‑lo um pouco mais flexível usando objetos `Path`.

```python
# Step 3: Recognize text from the image file
image_path = Path("YOUR_DIRECTORY/ancient_greek.png")
ocr_result = engine.recognize_image(str(image_path))
```

**Dicas e Casos Limite**

- **File not found** – envolva a chamada em um `try/except FileNotFoundError` para fornecer uma mensagem amigável.  
- **Low‑resolution PNG** – considere pré‑processamento (ex., redimensionamento, binarização) com Pillow antes do OCR.  
- **Non‑Greek text** – o Tesseract ainda tentará decodificar, mas a precisão cai drasticamente. Sempre combine o idioma.  

## Exibir o Texto Reconhecido

Finalmente, imprimimos o resultado. Em um projeto real você pode gravar em um banco de dados, um CSV, ou até mesmo alimentá‑lo em um pipeline de tradução.

```python
# Step 4: Output the recognized text
print("=== OCR Result ===")
print(ocr_result.text)
```

Quando você executar o script contra uma varredura clara de uma inscrição grega antiga, você deverá ver algo como:

```
=== OCR Result ===
Ἀνδρὸς ἐστὶν ὁ ἥλιος...
```

Se a saída parecer confusa, verifique novamente se o arquivo **greek.traineddata** está na pasta correta e se o PNG não está muito ruidoso.

## Exemplo Completo Funcional (Todas as Etapas em Um Script)

Abaixo está o programa completo, pronto‑para‑executar. Salve como `ocr_greek.py` e execute `python ocr_greek.py`.

```python
# ocr_greek.py
from pathlib import Path
from PIL import Image
import pytesseract

class OcrEngine:
    def __init__(self, tess_cmd: str = "tesseract"):
        pytesseract.pytesseract.tesseract_cmd = tess_cmd
        self.lang = "eng"  # default fallback

    def set_recognition_language(self, language: str):
        self.lang = language

    def recognize_image(self, image_path: str):
        img = Image.open(image_path)
        text = pytesseract.image_to_string(img, lang=self.lang)
        return OcrResult(text)

class OcrResult:
    def __init__(self, text: str):
        self.text = text

def main():
    # 1️⃣ Create an OCR engine instance
    engine = OcrEngine()

    # 2️⃣ Set the language to Greek polytonic (read ancient greek)
    engine.set_recognition_language("grc")

    # 3️⃣ Path to the PNG you want to analyse
    png_path = Path("YOUR_DIRECTORY/ancient_greek.png")
    if not png_path.is_file():
        raise FileNotFoundError(f"Cannot find image at {png_path}")

    # 4️⃣ Recognize and retrieve the text
    result = engine.recognize_image(str(png_path))

    # 5️⃣ Print the extracted text
    print("=== OCR PNG Image Result ===")
    print(result.text)

if __name__ == "__main__":
    main()
```

**Saída esperada** (truncada para brevidade):

```
=== OCR PNG Image Result ===
Ἀνδρὸς ἐστὶν ὁ ἥλιος·
Καὶ ὁ ἥλιος ἀνατέλλει·
```

Se você vir os caracteres gregos corretos, parabéns—você realizou com sucesso uma operação **ocr png image** em Python!

## Perguntas Frequentes & Dicas Profissionais

### Como melhorar a precisão em um PNG ruidoso?

- Converter a imagem para escala de cinza: `img = img.convert('L')`
- Aplicar um limiar binário: `img = img.point(lambda x: 0 if x < 128 else 255, '1')`
- Aumentar a escala com `img = img.resize((img.width*2, img.height*2), Image.LANCZOS)`

Esses passos costumam transformar um pesadelo de **recognize image text** em um resultado limpo.

### Posso processar uma pasta inteira de PNGs?

Absolutamente. Envolva a chamada `recognize_image` em um loop `for` sobre `Path.glob("*.png")`. Armazene cada resultado em um dicionário ou grave em um CSV para análise posterior.

```python
for png in Path("my_folder").glob("*.png"):
    res = engine.recognize_image(str(png))
    print(f"{png.name}: {res.text[:50]}...")
```

### E se eu precisar extrair apenas números?

Passe uma string **config** personalizada para `image_to_string`:

```python
digits = pytesseract.image_to_string(img, lang=self.lang, config='outputbase digits')
```

Dessa forma você pode **extract text from image** arquivos que contenham tabelas, números de série ou timestamps.

### Existe uma maneira de obter pontuações de confiança?

Sim—use `pytesseract.image_to_data` que retorna um TSV com confiança por palavra. Você pode filtrar tokens de baixa confiança antes de montar a string final.

## Expandindo o Tutorial

Agora que você dominou o básico, considere explorar estes tópicos relacionados:

- **Batch OCR with multiprocessing** – acelere grandes corpora de PNGs.  
- **Hybrid OCR + NLP pipelines** – traduza automaticamente o grego antigo extraído para o inglês moderno.  
- **Alternative engines** – experimente `easyocr` ou métodos baseados em `opencv` para casos de uso específicos.  
- **Cloud OCR services** – Google Vision, Azure Computer Vision ou AWS Textract para escalabilidade serverless.  

Cada um desses se baseia no núcleo **python ocr example** que acabamos de cobrir, então você se sentirá confortável em aprofundar.

## Conclusão

Transformamos um snippet simples em um fluxo robusto de **ocr png image** em Python. Ao criar um `OcrEngine`, definir o idioma para grego politônico, alimentar um PNG e imprimir o resultado, você agora sabe como **extract text from image** arquivos, **recognize image text**, e até **read ancient greek**.

## O que Você Deve Aprender a Seguir?

Os tutoriais a seguir cobrem tópicos estreitamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Extrair Texto de Imagem com Aspose OCR – Guia Passo a Passo](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Como Definir Valor de Limiar no Reconhecimento de Imagem OCR](/ocr/english/net/ocr-settings/set-threshold-value/)
- [reconhecer texto de imagem com Aspose OCR para múltiplos idiomas](/ocr/english/net/ocr-settings/working-with-different-languages/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}