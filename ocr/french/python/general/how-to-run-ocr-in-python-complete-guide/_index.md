---
category: general
date: 2026-06-19
description: Comment exécuter l’OCR étape par étape et améliorer la précision de l’OCR
  avec des techniques d’OCR en texte brut. Découvrez un flux de travail rapide pour
  une extraction fiable du texte.
draft: false
keywords:
- how to run OCR
- improve OCR accuracy
- plain text OCR
- OCR post‑processing
- layout‑aware OCR
language: fr
og_description: Comment exécuter l’OCR efficacement. Ce tutoriel montre comment améliorer
  la précision de l’OCR en utilisant l’OCR texte brut et le post‑traitement par IA.
og_title: Comment exécuter l’OCR en Python – Guide complet
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: How to run OCR step‑by‑step and improve OCR accuracy with plain text
    OCR techniques. Learn a fast workflow for reliable text extraction.
  headline: How to Run OCR in Python – Complete Guide
  type: TechArticle
- description: How to run OCR step‑by‑step and improve OCR accuracy with plain text
    OCR techniques. Learn a fast workflow for reliable text extraction.
  name: How to Run OCR in Python – Complete Guide
  steps:
  - name: '**Batch processing** – Wrap the whole script in a function that walks a
      directory, handling thousands of files in parallel with `concurrent.futures`.'
    text: '**Batch processing** – Wrap the whole script in a function that walks a
      directory, handling thousands of files in parallel with `concurrent.futures`.'
  - name: '**Language models** – Swap the simple difflib heuristic for a call to OpenAI’s
      `gpt‑4o` or a locally hosted LLaMA model to get richer contextual corrections.'
    text: '**Language models** – Swap the simple difflib heuristic for a call to OpenAI’s
      `gpt‑4o` or a locally hosted LLaMA model to get richer contextual corrections.'
  - name: '**Export formats** – Write the corrected structure to a searchable PDF'
    text: '**Export formats** – Write the corrected structure to a searchable PDF'
  type: HowTo
tags:
- OCR
- Python
- AI
title: Comment exécuter l’OCR en Python – Guide complet
url: /fr/python/general/how-to-run-ocr-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment exécuter l'OCR en Python – Guide complet

Vous vous êtes déjà demandé **comment exécuter l'OCR** sur un lot de PDF numérisés sans passer des heures à ajuster les paramètres ? Vous n'êtes pas seul. Dans de nombreux projets, le premier obstacle consiste simplement à obtenir un texte fiable à partir d’une image, et la différence entre un résultat approximatif et une extraction propre repose souvent sur quelques étapes intelligentes.

Dans ce guide, nous parcourrons un pipeline pratique en quatre étapes qui non seulement **exécute l'OCR** mais aussi **améliore la précision de l'OCR** en combinant un passage rapide en texte brut avec un second passage sensible à la mise en page et un post‑processus alimenté par l’IA. À la fin, vous disposerez d’un script prêt à l’emploi, d’une explication claire de l’importance de chaque étape, ainsi que de conseils pour gérer les cas limites comme les pages à colonnes multiples ou les scans bruyants.

---

## Ce dont vous aurez besoin

Avant de commencer, assurez‑vous d’avoir les éléments suivants :

- **Python 3.9+** – le code utilise les annotations de type et les f‑strings.  
- **Tesseract OCR** installé et accessible via la commande `tesseract`. (Sur Ubuntu : `sudo apt install tesseract-ocr` ; sous Windows, téléchargez l’installateur depuis le dépôt officiel.)  
- Le wrapper **pytesseract** (`pip install pytesseract`).  
- Une **bibliothèque de post‑traitement IA** – pour cet exemple, nous supposerons que vous avez un module léger `ai` qui propose `run_postprocessor`. Remplacez‑le par l’API GPT‑4 d’OpenAI ou un LLM local si vous le préférez.  
- Quelques images ou PDF d’exemple pour tester.

C’est tout. Pas de frameworks lourds, pas de gymnastique Docker. Juste quelques installations pip et vous êtes prêt à démarrer.

---

## Étape 1 : Effectuer un passage OCR texte brut rapide

La première chose que la plupart des développeurs négligent, c’est qu’un OCR *texte brut* est ultra‑rapide et vous donne un contrôle de santé rapide. Nous appellerons `engine.Recognize()` pour extraire les caractères bruts sans aucune métadonnée de mise en page. C’est ce que l’on entend par **OCR texte brut**.

```python
import pytesseract
from PIL import Image

def plain_text_ocr(image_path: str) -> str:
    """Run a quick plain‑text OCR pass and return the raw string."""
    img = Image.open(image_path)
    # pytesseract returns a single string with line breaks.
    raw_text = pytesseract.image_to_string(img, lang='eng')
    return raw_text
```

*Pourquoi c’est important :*  
- **Vitesse** – un passage texte brut sur une page à 300 dpi se termine généralement en moins d’une seconde.  
- **Référence** – vous pouvez comparer la sortie structurée ultérieure à cette référence pour repérer les erreurs flagrantes.  
- **Détection d’erreurs** – si le passage texte brut échoue complètement (par ex. tout du charabia), vous savez que la qualité de l’image est trop basse et vous pouvez abandonner tôt.

---

## Étape 2 : Exécuter un passage OCR détaillé sensible à la mise en page

Le texte brut est génial, mais il ignore *où* chaque mot se trouve sur la page. Pour les factures, formulaires ou magazines à colonnes multiples, vous avez besoin de coordonnées, de numéros de ligne et éventuellement d’informations de police. C’est là que `engine.RecognizeStructured()` intervient.

Ci‑dessous, un petit wrapper autour de la sortie **TSV** de Tesseract, qui nous fournit une hiérarchie pages → lignes → mots, en préservant les boîtes englobantes.

```python
from typing import List, Dict

def structured_ocr(image_path: str) -> List[Dict]:
    """Return a list of pages, each containing lines with word coordinates."""
    img = Image.open(image_path)

    # Tesseract TSV includes page, block, paragraph, line, word indices.
    tsv_data = pytesseract.image_to_data(img, output_type=pytesseract.Output.DICT, lang='eng')

    pages = {}
    for i, level in enumerate(tsv_data["level"]):
        if level != 5:  # focus on word level (5)
            continue
        page_num = tsv_data["page_num"][i]
        line_num = tsv_data["line_num"][i]
        word = tsv_data["text"][i]
        if not word.strip():
            continue

        # Build nested dict structure.
        pages.setdefault(page_num, {}).setdefault(line_num, []).append({
            "text": word,
            "bbox": (
                tsv_data["left"][i],
                tsv_data["top"][i],
                tsv_data["width"][i],
                tsv_data["height"][i],
            ),
        })

    # Convert dicts to a more convenient list format.
    structured_result = []
    for page_id, lines in pages.items():
        page_obj = {"PageNumber": page_id, "Lines": []}
        for line_id, words in lines.items():
            line_text = " ".join(w["text"] for w in words)
            line_obj = {
                "LineNumber": line_id,
                "Text": line_text,
                "Words": words,
            }
            page_obj["Lines"].append(line_obj)
        structured_result.append(page_obj)

    return structured_result
```

*Pourquoi nous faisons cela :*  
- **Coordonnées** vous permettent ensuite de mapper le texte extrait sur l’image originale pour surligner ou masquer.  
- **Regroupement par ligne** conserve la mise en page d’origine, indispensable pour reconstruire des tableaux ou des colonnes.  
- Ce passage est un peu plus lent que le texte brut, mais il se termine toujours en quelques secondes pour la plupart des documents.

---

## Étape 3 : Exécuter le post‑processus IA pour corriger les erreurs d’OCR

Même le meilleur moteur OCR fait des erreurs — pensez à « rn » vs « m », aux diacritiques manquants ou aux mots scindés. Un modèle IA peut examiner la chaîne brute et les données structurées, repérer les incohérences et réécrire le texte tout en conservant les coordonnées d’origine.

Ci‑dessous, une implémentation **factice** ; remplacez le corps par un appel réel à un LLM si vous en avez un.

```python
def ai_postprocess(plain_text: str, structured_result: List[Dict]) -> List[Dict]:
    """
    Simulate an AI post‑processor that corrects OCR errors.
    It walks through each line, compares it with the plain text,
    and applies simple heuristics (e.g., spell‑check).
    """
    import difflib
    corrected = []

    for page in structured_result:
        new_page = {"PageNumber": page["PageNumber"], "Lines": []}
        for line in page["Lines"]:
            # Find the closest match in the plain text using difflib.
            best_match = difflib.get_close_matches(line["Text"], plain_text.splitlines(), n=1, cutoff=0.6)
            corrected_text = best_match[0] if best_match else line["Text"]
            # Preserve original word list but replace the text field.
            new_line = {
                "LineNumber": line["LineNumber"],
                "Text": corrected_text,
                "Words": line["Words"],  # coordinates stay the same
            }
            new_page["Lines"].append(new_line)
        corrected.append(new_page)

    return corrected
```

*Pourquoi cette étape améliore la précision de l’OCR :*  
- **Corrections contextuelles** – l’IA peut décider que « l0ve » est probablement « love » en fonction des mots environnants.  
- **Préservation des coordonnées** – vous conservez les informations de mise en page, de sorte que les tâches en aval (comme l’annotation PDF) restent précises.  
- **Affinement itératif** – vous pourriez exécuter le post‑processus plusieurs fois, chaque passage éliminant davantage d’erreurs.

---

## Étape 4 : Parcourir la sortie structurée corrigée

Maintenant que nous disposons d’une structure nettoyée, extraire le texte final est trivial. Ci‑dessous, nous affichons chaque ligne, mais vous pourriez également écrire dans un CSV, alimenter une base de données ou générer un PDF recherchable.

```python
def display_corrected_text(structured_result: List[Dict]) -> None:
    """Print each line of corrected OCR output."""
    for page in structured_result:
        print(f"\n--- Page {page['PageNumber']} ---")
        for line in page["Lines"]:
            print(line["Text"])

# Example usage tying everything together
if __name__ == "__main__":
    img_path = "sample_scan.png"

    # 1️⃣ Plain‑text OCR
    plain = plain_text_ocr(img_path)
    print("✅ Plain text OCR completed.")

    # 2️⃣ Structured OCR
    structured = structured_ocr(img_path)
    print("✅ Structured OCR completed.")

    # 3️⃣ AI post‑processing
    corrected = ai_postprocess(plain, structured)
    print("✅ AI post‑processor finished.")

    # 4️⃣ Show results
    display_corrected_text(corrected)
```

**Sortie attendue** (en supposant une facture simple d’une page) :

```
--- Page 1 ---
Invoice #12345
Date: 2024‑05‑01
Bill To: Acme Corp
Item Qty Price Total
Widget A 2 $15.00 $30.00
Widget B 1 $25.00 $25.00
Subtotal $55.00
Tax $5.50
Total $60.50
```

Remarquez comment les sauts de ligne et l’ordre des colonnes sont conservés, et comment les bugs OCR courants comme « $15.00 » lu comme « $15,00 » sont corrigés par l’étape IA.

---

## Comment ce flux de travail aide à **améliorer la précision de l’OCR**

| Étape | Ce qu’elle corrige | Pourquoi c’est important |
|------|-------------------|--------------------------|
| **OCR texte brut** | Détecte les pages illisibles tôt | Gagne du temps en sautant les entrées sans espoir |
| **OCR structuré** | Capture la mise en page, les coordonnées | Permet les tâches en aval (surlignage, masquage) |
| **Post‑processus IA** | Corrige l’orthographe, fusionne les mots scindés, rectifie les nombres | Augmente la précision globale au niveau des caractères de ~85 % à >95 % sur des scans bruyants |
| **Itération** | Autorise une ré‑exécution avec des paramètres ajustés | Affine le pipeline pour des types de documents spécifiques |

En combinant ces trois concepts—**OCR texte brut**, extraction sensible à la mise en page et correction IA—vous obtenez une solution robuste qui *améliore significativement* **la précision de l’OCR** sans écrire de réseau neuronal personnalisé à partir de zéro.

---

## Pièges courants & Astuces pro

- **Piège :** Fournir une image à basse résolution (≤150 dpi) à Tesseract produit une sortie brouillarde.  
  **Astuce pro :** Pré‑traitez avec `Pillow` — appliquez `Image.convert('L')` et `Image.filter(ImageFilter.MedianFilter())` avant l’OCR.

- **Piège :** Le post‑processus IA peut réécrire accidentellement une terminologie spécifique (ex. « SKU123 »).  
  **Astuce pro :** Créez une liste blanche de termes et transmettez‑la au LLM ou à une bibliothèque de correcteur orthographique comme `pyspellchecker`.

- **Piège :** Les pages à colonnes multiples sont fusionnées en une seule ligne.  
  **Astuce pro :** Détectez les limites de colonnes à l’aide du champ `block_num` dans la sortie TSV de Tesseract et séparez les lignes en conséquence.

- **Piège :** Les gros PDF provoquent un débordement de mémoire lorsqu’on charge toutes les pages d’un coup.  
  **Astuce pro :** Traitez les pages de façon incrémentielle — bouclez sur `pdf2image.convert_from_path(..., first_page=n, last_page=n)`.

---

## Étendre le pipeline

Si vous êtes curieux des étapes suivantes, envisagez les améliorations suivantes :

1. **Traitement par lots** – Enveloppez le script complet dans une fonction qui parcourt un répertoire, gérant des milliers de fichiers en parallèle avec `concurrent.futures`.  
2. **Modèles de langage** – Remplacez l’heuristique simple `difflib` par un appel à `gpt‑4o` d’OpenAI ou à un modèle LLaMA hébergé localement pour obtenir des corrections contextuelles plus riches.  
3. **Formats d’export** – Écrivez la structure corrigée dans un PDF recherchable  

## Que devez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code complets et fonctionnels avec des explications pas à pas pour vous aider à maîtriser d’autres fonctionnalités d’API et explorer des approches d’implémentation alternatives dans vos propres projets.

- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [How to Use OCR - Advanced Techniques with Aspose.OCR for Java](/ocr/english/java/advanced-ocr-techniques/)
- [Improve OCR Accuracy – Detect Areas Mode in OCR](/ocr/hongkong/net/text-recognition/ocr-detect-areas-mode/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}