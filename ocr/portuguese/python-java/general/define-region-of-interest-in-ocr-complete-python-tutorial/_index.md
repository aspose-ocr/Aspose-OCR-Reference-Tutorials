---
category: general
date: 2026-06-16
description: Defina a região de interesse no OCR para extrair texto em espanhol de
  carteiras de identidade. Aprenda como carregar a imagem para OCR e especificar a
  ROI de forma eficiente.
draft: false
keywords:
- define region of interest
- load image for ocr
- how to specify roi
- extract id card text
- extract spanish text image
language: pt
og_description: Defina a região de interesse no OCR para extrair texto em espanhol
  de cartões de identidade. Guia passo a passo sobre como carregar imagens e especificar
  a ROI.
og_title: Defina a região de interesse em OCR – Tutorial completo de Python
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: Define region of interest in OCR to extract Spanish text from ID cards.
    Learn how to load image for OCR and specify ROI efficiently.
  headline: Define region of interest in OCR – Complete Python Tutorial
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
title: Defina a região de interesse em OCR – Tutorial completo de Python
url: /pt/python-java/general/define-region-of-interest-in-ocr-complete-python-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Defina a região de interesse em OCR – Tutorial Completo em Python

Já se perguntou como **definir a região de interesse em OCR** para ler apenas a parte da imagem que realmente precisa? Neste tutorial vamos guiá‑lo passo a passo, além de mostrar como **carregar a imagem para OCR** e extrair texto em espanhol de um documento de identidade em apenas algumas linhas de Python.  

Se você já ficou encarando uma digitalização ruidosa e pensou: “Tem que haver uma forma mais limpa de capturar o campo nome”, está no lugar certo. Ao final, você será capaz de extrair o texto do documento de identidade que lhe interessa sem se atrapalhar com o fundo.

## O que você vai aprender

- Por que você deve **definir a região de interesse** antes de executar OCR.  
- Os passos exatos para **carregar a imagem para OCR** usando um wrapper Python popular.  
- Como **especificar ROI** com coordenadas de pixels.  
- Maneiras de **extrair texto de documento de identidade** de forma confiável, mesmo quando o idioma de origem é espanhol.  
- Dicas para lidar com casos extremos como cartões rotacionados ou digitalizações de baixo contraste.  

Nenhum domínio prévio de OCR é necessário — apenas um ambiente Python 3 funcionando e um JPEG de um documento de identidade que você queira testar.

---

![Define region of interest illustration](placeholder.png){alt="Exemplo de definição de região de interesse mostrando um retângulo destacado em uma imagem de documento de identidade"}

## Etapa 1: Instale e importe a biblioteca de OCR

Primeiro de tudo, você precisa de uma biblioteca que exponha uma classe `OcrEngine` semelhante ao trecho que você viu. Para este guia usaremos o pacote fictício `ocr`, mas os mesmos conceitos se aplicam ao `pytesseract`, `easyocr` ou qualquer wrapper que permita definir um idioma e uma ROI.

```bash
pip install ocr   # Replace with the actual package name you use
```

```python
# Import the library and any helper classes
import ocr
from ocr import Rectangle, Image
```

*Dica:* Se você estiver usando `pytesseract`, a classe `Rectangle` torna‑se uma tupla simples `(left, top, width, height)`. O restante do fluxo permanece idêntico.

## Etapa 2: Carregue a imagem para OCR

Agora nós **carregamos a imagem para OCR**. O motor espera um objeto `ocr.Image`, então apontamos para o arquivo que contém o documento de identidade. Certifique‑se de que o caminho seja absoluto ou relativo ao diretório de trabalho do seu script.

```python
# Create the OCR engine instance
engine = ocr.OcrEngine()

# Tell the engine which language we’re interested in – Spanish in this case
engine.language = ocr.Language.SPANISH

# Load the source image that contains the text to be recognized
engine.image = Image.load_from_file("YOUR_DIRECTORY/id-card.jpg")
```

Se a imagem for muito grande, considere redimensioná‑la primeiro; motores de OCR funcionam mais rápido em imagens com menos de 1500 px de largura.

## Etapa 3: Como especificar ROI (Definir Região de Interesse)

Aqui está o coração do tutorial: **como especificar ROI**. Uma região de interesse é simplesmente um retângulo que diz ao motor de OCR: “Olhe apenas dentro desses limites de pixels.” Pense nisso como desenhar uma caixa ao redor do campo nome em um documento de identidade.

```python
# Define the region of interest – left, top, width, height (all in pixels)
engine.region_of_interest = Rectangle(
    left=120,   # X‑coordinate of the left edge
    top=80,     # Y‑coordinate of the top edge
    width=340,  # Width of the box
    height=200  # Height of the box
)
```

Por que esses números? Na nossa imagem de exemplo o nome está aproximadamente 120 px da borda esquerda e 80 px do topo. Ajuste‑os para combinar com o layout dos documentos que você está processando.  

*Caso extremo:* Se o documento estiver rotacionado 90°, troque `width` e `height` e ajuste `left`/`top` de acordo, ou pré‑rotate a imagem com Pillow antes de enviá‑la ao motor.

## Etapa 4: Execute OCR dentro da ROI

Com a ROI definida, o motor ignorará tudo fora do retângulo. Isso não só acelera o processamento como também reduz falsos positivos causados por gráficos de fundo.

```python
# Run OCR only inside the defined ROI
roi_result = engine.recognize()
```

A chamada `recognize()` retorna um objeto que contém o texto reconhecido, pontuações de confiança e caixas delimitadoras para cada palavra.

## Etapa 5: Extraia o texto do documento de identidade (e verifique a saída em espanhol)

Por fim, nós **extraímos o texto do documento de identidade** do resultado da ROI e o imprimimos. Como definimos o idioma como espanhol anteriormente, o motor de OCR aplicará dicionários específicos do idioma, melhorando a precisão para caracteres acentuados como “ñ” ou “á”.

```python
# Output the recognized text from the ROI
print("ROI text:", roi_result.text)
```

### Saída esperada

```
ROI text: JUAN PÉREZ GARCÍA
```

Se você vir caracteres estranhos, verifique se a imagem está realmente em espanhol e se os arquivos de dados de idioma da biblioteca OCR estão instalados.

## Armadilhas comuns & como evitá‑las

| Sintoma | Causa provável | Solução |
|---------|----------------|--------|
| String vazia retornada | ROI não intersecta nenhum texto | Verifique as coordenadas com um visualizador de imagens; use `engine.debug_draw_roi()` se disponível. |
| Muitos caracteres lixo | Pacote de idioma errado | Reinstale os dados de idioma espanhol ou troque para `ocr.Language.AUTO`. |
| Baixas pontuações de confiança | Imagem borrada ou de baixo contraste | Pré‑processar com OpenCV – aplique `cv2.GaussianBlur` e `cv2.threshold`. |
| OCR roda na imagem inteira apesar da ROI | Uso de versão antiga da biblioteca | Atualize para a última versão do pacote `ocr`; versões antigas ignoravam ROI. |

## Expandindo o exemplo: Múltiplas ROIs

Às vezes você precisa extrair mais de um campo (ex.: nome e número de identidade). O padrão permanece o mesmo: altere `engine.region_of_interest` e chame `recognize()` novamente.

```python
# ROI for the ID number (different coordinates)
engine.region_of_interest = Rectangle(120, 300, 340, 80)
id_result = engine.recognize()
print("ID Number:", id_result.text)
```

Você também pode processar em lote uma lista de retângulos se a biblioteca suportar, o que economiza idas ao motor de OCR.

## Script completo funcional

Juntando tudo, aqui está um script pronto‑para‑executar que **define a região de interesse**, **carrega a imagem para OCR** e **extrai texto em espanhol** de um documento de identidade.

```python
import ocr
from ocr import Rectangle, Image

def extract_name_from_id(image_path):
    """
    Loads an image, defines a ROI around the name field,
    runs OCR in Spanish, and returns the recognized text.
    """
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.SPANISH
    engine.image = Image.load_from_file(image_path)

    # Adjust these numbers to match your card layout
    engine.region_of_interest = Rectangle(left=120, top=80, width=340, height=200)

    result = engine.recognize()
    return result.text.strip()

if __name__ == "__main__":
    name = extract_name_from_id("YOUR_DIRECTORY/id-card.jpg")
    print("Extracted Name:", name)
```

Execute o script e você deverá ver o nome impresso no console. Troque os valores do retângulo para alcançar outros campos, e você terá uma utilidade reutilizável para qualquer documento do tipo identidade.

## Próximos passos

- **Processamento em lote:** Percorra uma pasta de documentos de identidade e salve cada nome extraído em um arquivo CSV.  
- **Detecção de idioma:** Permita que o usuário escolha o idioma dinamicamente; `ocr.Language.AUTO` pode ser útil.  
- **Pós‑processamento:** Aplique padrões regex para limpar erros comuns de OCR (ex.: substituir “0” por “O” quando aparecer em nomes).  

Ao dominar como **definir a região de interesse** você desbloqueou uma forma poderosa de **extrair texto de documento de identidade** de maneira rápida e precisa, especialmente ao lidar com documentos em espanhol.

---

### TL;DR

Mostramos como **definir a região de interesse em OCR**, **carregar a imagem para OCR** e **especificar ROI** para **extrair texto em espanhol de uma imagem** de um documento de identidade. O exemplo completo roda em menos de um minuto e pode ser adaptado a qualquer layout com alguns ajustes de coordenadas. Experimente, ajuste o retângulo e veja o OCR focar como um laser.

Happy coding!

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [How to Extract Text from Image by Preparing Rectangles in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}