---
category: general
date: 2026-03-26
description: Aprenda a executar OCR em imagens PNG em árabe e extrair texto árabe
  rapidamente. Este guia mostra como converter a imagem em texto com código Python
  passo a passo.
draft: false
keywords:
- how to run ocr
- extract arabic text
- recognize arabic text
- convert image to text
- extract text from png
language: pt
og_description: Como executar OCR em imagens PNG em árabe? Siga este guia completo
  para extrair texto em árabe, reconhecer texto em árabe e converter a imagem em texto
  usando Python.
og_title: Como executar OCR em PNG em árabe – Extrair texto da imagem
tags:
- OCR
- Python
- Arabic
title: Como executar OCR em PNG em árabe – Extrair texto da imagem
url: /pt/python-java/general/how-to-run-ocr-on-arabic-png-extract-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como Executar OCR em PNG Árabe – Extrair Texto da Imagem

Já se perguntou **como executar OCR** em uma imagem que contém texto em árabe? Talvez você tenha um recibo escaneado, um manuscrito histórico ou apenas uma captura de tela de uma postagem em rede social e precise do texto em um formato pesquisável. Você não está sozinho—desenvolvedores ao redor do mundo enfrentam esse obstáculo ao lidar com idiomas da direita para a esquerda.

Neste tutorial vamos percorrer um exemplo completo e executável que mostra **como executar OCR** em um arquivo PNG, extrair texto árabe e imprimir o resultado no console. Sem links vagos de “veja a documentação”; apenas o código que você pode copiar‑colar, mais explicações sobre por que cada linha importa. Ao final, você será capaz de **converter imagem em texto** de forma confiável, mesmo quando a fonte for um PNG árabe complicado.

> **O que você aprenderá**
> - Configurar um motor OCR Python para árabe  
> - Carregar uma imagem PNG e lidar com armadilhas comuns  
> - Reconhecer texto árabe e verificar a saída  
> - Dicas para **extrair texto árabe** de diferentes qualidades de imagem  

Antes de mergulharmos, certifique‑se de que tem o Python 3.8+ instalado e uma versão recente da biblioteca `ocr` (a usada no trecho). Se estiver usando um ambiente virtual, ative‑o agora—isso mantém as dependências organizadas.

## Pré-requisitos

- Python 3.8 ou mais recente  
- Pacote `ocr` (`pip install ocr‑engine` – substitua pelo nome real do pacote)  
- Uma imagem PNG em árabe (`arabic_doc.png`) colocada em algum local que você possa referenciar  
- Familiaridade básica com funções e classes Python  

É isso. Sem frameworks pesados, sem contêineres Docker—apenas Python puro.

## Etapa 1: Instalar e Importar a Biblioteca OCR

Primeiro de tudo. Precisamos do próprio motor OCR. A biblioteca que usaremos expõe uma classe `OcrEngine` com uma API simples.

```python
# Install the library (run once in your terminal)
# pip install ocr-engine   # <-- replace with the correct package name

# Import the necessary classes
import ocr
from ocr import Imaging
```

*Por que importar `Imaging` separadamente?* O submódulo `Imaging` nos fornece um método conveniente `Image.load` que entende PNG, JPEG e TIFF imediatamente. Pular essa etapa forçaria você a lidar com bytes crus, o que é desnecessário na maioria dos casos de uso.

## Etapa 2: Criar a Instância do Motor OCR

Agora criamos uma instância do motor. Pense neste objeto como o “cérebro” que processará a imagem.

```python
# Step 2: Create an OCR engine instance
ocr_engine = ocr.OcrEngine()
```

> **Dica profissional:** Se você planeja processar muitas imagens em sequência, reutilize a mesma instância `ocr_engine`. Ela faz cache dos modelos de idioma, o que acelera reconhecimentos subsequentes.

## Etapa 3: Definir o Idioma para Árabe

Árabe não é latim; tem seu próprio conjunto de caracteres, direção da direita para a esquerda e modelagem contextual. Por isso precisamos dizer explicitamente ao motor qual modelo de idioma carregar.

```python
# Step 3: Set the language to Arabic (language code "ar")
ocr_engine.set_language("ar")
```

Se você esquecer esta linha, o motor usará o padrão inglês e você obterá uma saída confusa—algo que já vi acontecer com muita frequência.

## Etapa 4: Carregar Sua Imagem PNG

É aqui que a parte **converter imagem em texto** realmente começa. Vamos carregar o arquivo PNG que contém o script árabe.

```python
# Step 4: Load the image that contains the Arabic text
image_path = "YOUR_DIRECTORY/arabic_doc.png"   # replace with your actual path
ocr_engine.set_image(Imaging.Image.load(image_path))
```

### Casos de Borda Comuns

| Problema | Sintoma | Solução |
|----------|---------|---------|
| A imagem está muito escura | A saída contém muitos espaços em branco | Pré‑processar com Pillow (`ImageEnhance.Brightness`) |
| PNG tem canal alfa | Alguns motores OCR leem mal pixels transparentes | Converter para RGB (`image.convert("RGB")`) antes de carregar |
| Texto está rotacionado | Texto reconhecido fica de cabeça para baixo | Rotacionar a imagem (`image.rotate(90, expand=True)`) antes de passar ao motor |

## Etapa 5: Executar o Processo de Reconhecimento

Com tudo configurado, finalmente pedimos ao motor que faça seu trabalho.

```python
# Step 5: Run the recognition process
ocr_result = ocr_engine.recognize()
```

O método `recognize` retorna um objeto que contém a string Unicode bruta, pontuações de confiança e caixas delimitadoras. Para a maioria dos desenvolvedores, o texto puro é tudo que você precisa.

## Etapa 6: Exibir o Texto Árabe Reconhecido

Agora imprimimos o resultado. Em uma aplicação real você pode gravar em um arquivo, em um banco de dados ou enviá‑lo para uma API de tradução.

```python
# Step 6: Output the recognized text
print(ocr_result.get_text())
```

Ao executar o script, você deverá ver os caracteres árabes exibidos no seu console (certifique‑se de que o terminal suporta Unicode). Se aparecerem pontos de interrogação ou strings vazias, verifique novamente a configuração de idioma e a qualidade da imagem.

### Saída Esperada

```
هذا نص عربي من صورة PNG تم استخراجها باستخدام OCR.
```

Se a saída se parecer com a linha acima, parabéns—você extraiu **texto árabe** de um PNG com sucesso!

## Exemplo Completo Funcional

A seguir está o script inteiro, pronto para copiar‑colar. Substitua `YOUR_DIRECTORY/arabic_doc.png` pelo caminho do seu próprio arquivo.

```python
import ocr
from ocr import Imaging

def main():
    # Create OCR engine
    ocr_engine = ocr.OcrEngine()
    
    # Set Arabic language
    ocr_engine.set_language("ar")
    
    # Load the PNG image
    image_path = "YOUR_DIRECTORY/arabic_doc.png"
    ocr_engine.set_image(Imaging.Image.load(image_path))
    
    # Recognize text
    ocr_result = ocr_engine.recognize()
    
    # Print the extracted Arabic text
    print(ocr_result.get_text())

if __name__ == "__main__":
    main()
```

Execute‑o com `python run_ocr.py` (ou como você nomeou o arquivo). Se tudo estiver instalado corretamente, você verá a frase árabe impressa no console.

## Como Executar OCR em Diferentes Formatos de Imagem

O mesmo código funciona para JPEG, TIFF ou BMP—basta mudar a extensão do arquivo. O método `Image.load` detecta automaticamente o formato, então você pode **converter imagem em texto** sem código extra.

```python
# Example for a JPEG file
ocr_engine.set_image(Imaging.Image.load("sample.jpg"))
```

Lembre‑se, a qualidade da imagem de origem influencia fortemente a precisão da etapa **reconhecer texto árabe**. Imagens de alta resolução e baixa compressão dão os melhores resultados.

## Extrair Texto de PNG: Dicas para Melhor Precisão

1. **DPI Importa** – Almeje pelo menos 300 dpi. DPI menor costuma gerar caracteres perdidos.  
2. **Contraste é Rei** – Use ferramentas de processamento de imagem (por exemplo, OpenCV) para aumentar o contraste antes de enviar a imagem ao motor OCR.  
3. **Remoção de Ruído** – Pequenas manchas podem confundir o modelo; filtragem mediana ajuda.  

Aqui está um trecho rápido usando Pillow para melhorar um PNG antes do OCR:

```python
from PIL import Image, ImageEnhance, ImageFilter

def preprocess_png(path):
    img = Image.open(path).convert("L")          # grayscale
    img = ImageEnhance.Contrast(img).enhance(2)  # boost contrast
    img = img.filter(ImageFilter.MedianFilter()) # denoise
    return img

# Use the preprocessed image
prepped = preprocess_png("arabic_doc.png")
ocr_engine.set_image(Imaging.Image.from_pil(prepped))
```

## Perguntas Frequentes

**Q: Isso funciona com idiomas da direita para a esquerda além do árabe?**  
A: Absolutamente. Basta mudar o código de idioma (`"ar"` → `"he"` para hebraico, `"fa"` para persa) e o motor carregará o modelo apropriado.

**Q: E se eu precisar extrair texto de vários PNGs em uma pasta?**  
A: Percorra os arquivos, reutilize a mesma instância `ocr_engine` e cole os resultados em uma lista ou grave cada um em um arquivo `.txt` separado.

**Q: Posso obter pontuações de confiança para cada palavra?**  
A: Sim. `ocr_result` geralmente expõe um método `get_confidences()`. Associe cada confiança à palavra correspondente para controle de qualidade.

## Próximos Passos

Agora que você sabe **como executar OCR** em PNGs árabes, considere estas ideias de continuação:

- **Processamento em lote:** Combine o script com `os.listdir` para **extrair texto árabe** de um diretório inteiro.  
- **Pós‑processamento:** Use as bibliotecas `arabic_reshaper` e `python-bidi` para exibir corretamente a saída da direita para a esquerda em PDFs.  
- **Integração:** Alimente o texto extraído em um índice de busca (por exemplo, Elasticsearch) para tornar documentos escaneados pesquisáveis.  

Cada um desses tópicos se baseia nos fundamentos abordados aqui e ajudará você a transformar um simples script de **converter imagem em texto** em um pipeline pronto para produção.

---

![como executar OCR em PNG árabe](

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}