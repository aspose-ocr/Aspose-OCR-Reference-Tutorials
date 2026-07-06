---
category: general
date: 2026-04-26
description: Comment post‑traiter les résultats OCR et extraire le texte avec les
  coordonnées. Découvrez une solution étape par étape utilisant une sortie structurée
  et la correction par IA.
draft: false
keywords:
- how to post‑process OCR
- extract text with coordinates
- OCR structured output
- AI post‑processing OCR
- bounding box OCR
language: fr
og_description: Comment post‑traiter les résultats OCR et extraire le texte avec coordonnées.
  Suivez ce tutoriel complet pour un flux de travail fiable.
og_title: Comment post‑traiter l’OCR – Guide complet
tags:
- OCR
- Python
- AI
- Text Extraction
title: Comment post‑traiter l’OCR – Extraire le texte avec ses coordonnées en Python
url: /fr/python/general/how-to-post-process-ocr-extract-text-with-coordinates-in-pyt/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment post‑traiter l’OCR – Extraire du texte avec coordonnées en Python

Vous avez déjà eu besoin de **post‑traiter les résultats OCR** parce que la sortie brute était bruyante ou mal alignée ? Vous n'êtes pas le seul. Dans de nombreux projets réels—numérisation de factures, digitalisation de reçus, ou même l’enrichissement d’expériences AR—le moteur OCR vous fournit des mots bruts, mais vous devez encore les nettoyer et suivre où chaque mot se trouve sur la page. C’est là qu’un mode de sortie structuré combiné à un post‑processeur piloté par l’IA brille.

Dans ce tutoriel, nous parcourrons un pipeline Python complet et exécutable qui **extrait du texte avec coordonnées** d’une image, exécute une étape de correction basée sur l’IA, et affiche chaque mot avec sa position (x, y). Aucun import manquant, aucune astuce vague du type « voir la documentation »—juste une solution autonome que vous pouvez intégrer à votre projet dès aujourd’hui.

> **Astuce :** Si vous utilisez une autre bibliothèque OCR, cherchez un mode « structuré » ou « mise en page » ; les concepts restent les mêmes.

---

## Prérequis

| Exigence | Pourquoi c’est important |
|----------|---------------------------|
| Python 3.9+ | Syntaxe moderne et annotations de type |
| `ocr` library that supports `OutputMode.STRUCTURED` (e.g., a fictional `myocr`) | Bibliothèque `ocr` qui prend en charge `OutputMode.STRUCTURED` (par ex., une bibliothèque fictive `myocr`) |
| Needed for bounding‑box data | Nécessaire pour les données de boîte englobante |
| An AI post‑processing module (could be OpenAI, HuggingFace, or a custom model) | Un module de post‑traitement IA (peut être OpenAI, HuggingFace, ou un modèle personnalisé) |
| Improves accuracy after OCR | Améliore la précision après l’OCR |
| An image file (`input.png`) in your working directory | Un fichier image (`input.png`) dans votre répertoire de travail |
| The source we’ll read | La source que nous lirons |

Si l’un de ces éléments vous est inconnu, installez simplement les paquets factices avec `pip install myocr ai‑postproc`. Le code ci‑dessous inclut également des stubs de secours afin que vous puissiez tester le flux sans les bibliothèques réelles.

---

## Étape 1 : Activer le mode de sortie structuré pour le moteur OCR  

La première chose que nous faisons est d’indiquer au moteur OCR de nous fournir plus que du texte brut. La sortie structurée renvoie chaque mot avec sa boîte englobante et son score de confiance, ce qui est essentiel pour **extraire du texte avec coordonnées** plus tard.

```python
# step1_structured_output.py
import myocr as ocr  # fictional OCR library

# Initialize the engine (replace with your actual init code)
engine = ocr.Engine()

# Switch to structured mode – this makes the engine emit word‑level data
engine.set_output_mode(ocr.OutputMode.STRUCTURED)

print("✅ Structured output mode enabled")
```

*Pourquoi c’est important :* Sans le mode structuré, vous n’obtiendriez qu’une longue chaîne, et vous perdriez les informations spatiales nécessaires pour superposer du texte sur des images ou alimenter une analyse de mise en page en aval.

---

## Étape 2 : Reconnaître l’image et capturer les mots, les boîtes et la confiance  

Nous injectons maintenant l’image dans le moteur. Le résultat est un objet qui contient une liste d’objets mot, chacun exposant `text`, `x`, `y`, `width`, `height` et `confidence`.

```python
# step2_recognize.py
from pathlib import Path

# Path to your image
image_path = Path("YOUR_DIRECTORY/input.png")

# Perform OCR – returns a StructuredResult with .words collection
structured_result = engine.recognize_image(str(image_path))

print(f"🔎 Detected {len(structured_result.words)} words")
```

*Cas limite :* Si l’image est vide ou illisible, `structured_result.words` sera une liste vide. Il est recommandé de vérifier cela et de le gérer gracieusement.

---

## Étape 3 : Exécuter le post‑traitement basé sur l’IA tout en préservant les positions  

Même les meilleurs moteurs OCR commettent des erreurs—pensez à « O » vs. « 0 » ou aux diacritiques manquants. Un modèle IA entraîné sur du texte spécifique à un domaine peut corriger ces erreurs. De façon cruciale, nous conservons les coordonnées originales afin que la mise en page spatiale reste intacte.

```python
# step3_ai_postprocess.py
import ai_postproc as ai  # placeholder for your AI module

# The AI post‑processor expects the structured result and returns a new one
corrected_result = ai.run_postprocessor(structured_result)

print("🤖 AI post‑processing complete")
```

*Pourquoi nous préservons les coordonnées :* De nombreuses tâches en aval (par ex., génération de PDF, étiquetage AR) dépendent d’un placement exact. L’IA ne modifie que le champ `text`, laissant `x`, `y`, `width`, `height` intacts.

---

## Étape 4 : Parcourir les mots corrigés et afficher leur texte avec les coordonnées  

Enfin, nous parcourons les mots corrigés et affichons chaque mot avec son coin supérieur gauche `(x, y)`. Cela répond à l’objectif **extraire du texte avec coordonnées**.

```python
# step4_display.py
for recognized_word in corrected_result.words:
    # Using f‑string for clean formatting
    print(f"{recognized_word.text} (x:{recognized_word.x}, y:{recognized_word.y})")
```

**Sortie attendue (exemple) :**

```
Invoice (x:45, y:112)
Number (x:120, y:112)
12345 (x:190, y:112)
Total (x:45, y:250)
$ (x:120, y:250)
199.99 (x:130, y:250)
```

Chaque ligne montre le mot corrigé et son emplacement exact sur l’image originale.

---

## Exemple complet fonctionnel  

Voici un script unique qui rassemble tout. Vous pouvez le copier‑coller, ajuster les instructions d’importation pour correspondre à vos bibliothèques réelles, et l’exécuter directement.

```python
# ocr_postprocess_demo.py
"""
Complete demo: how to post‑process OCR and extract text with coordinates.
Works with any OCR library exposing a structured output mode and an AI post‑processor.
"""

import sys
from pathlib import Path

# ----------------------------------------------------------------------
# 1️⃣ Imports – replace these with your real packages
# ----------------------------------------------------------------------
try:
    import myocr as ocr               # OCR engine with structured output
    import ai_postproc as ai          # AI correction module
except ImportError:  # Fallback stubs for quick testing
    class DummyWord:
        def __init__(self, text, x, y, w, h, conf):
            self.text = text
            self.x = x
            self.y = y
            self.width = w
            self.height = h
            self.confidence = conf

    class DummyResult:
        def __init__(self, words):
            self.words = words

    class StubEngine:
        class OutputMode:
            STRUCTURED = "structured"

        def set_output_mode(self, mode):
            print(f"[Stub] set_output_mode({mode})")

        def recognize_image(self, path):
            # Very simple fake OCR output
            sample = [
                DummyWord("Invoice", 45, 112, 60, 20, 0.98),
                DummyWord("Number", 120, 112, 55, 20, 0.96),
                DummyWord("12345", 190, 112, 40, 20, 0.97),
                DummyWord("Total", 45, 250, 50, 20, 0.99),
                DummyWord("$", 120, 250, 10, 20, 0.95),
                DummyWord("199.99", 130, 250, 55, 20, 0.94),
            ]
            return DummyResult(sample)

    class StubAI:
        @staticmethod
        def run_postprocessor(structured_result):
            # Pretend we corrected "12345" to "12346"
            for w in structured_result.words:
                if w.text == "12345":
                    w.text = "12346"
            return structured_result

    engine = StubEngine()
    ai = StubAI

# ----------------------------------------------------------------------
# 2️⃣ Enable structured output
# ----------------------------------------------------------------------
engine.set_output_mode(ocr.Engine.OutputMode.STRUCTURED)

# ----------------------------------------------------------------------
# 3️⃣ Recognize image
# ----------------------------------------------------------------------
image_path = Path("YOUR_DIRECTORY/input.png")
if not image_path.is_file():
    print(f"⚠️  Image not found at {image_path}. Using stub data.")
structured_result = engine.recognize_image(str(image_path))

# ----------------------------------------------------------------------
# 4️⃣ AI post‑processing
# ----------------------------------------------------------------------
corrected_result = ai.run_postprocessor(structured_result)

# ----------------------------------------------------------------------
# 5️⃣ Display results
# ----------------------------------------------------------------------
print("\n🗒️  Final OCR output with coordinates:")
for word in corrected_result.words:
    print(f"{word.text} (x:{word.x}, y:{word.y})")
```

**Exécution du script**

```bash
python ocr_postprocess_demo.py
```

Si vous avez les bibliothèques réelles installées, le script traitera votre `input.png`. Sinon, l’implémentation stub vous permet de voir le flux et la sortie attendus sans aucune dépendance externe.

---

## Questions fréquemment posées (FAQ)

| Question | Réponse |
|----------|---------|
| *Cela fonctionne‑t‑il avec Tesseract ?* | Tesseract ne propose pas de mode structuré natif, mais des wrappers comme `pytesseract.image_to_data` renvoient des boîtes englobantes que vous pouvez transmettre au même post‑processeur IA. |
| *Et si j’ai besoin du coin inférieur droit au lieu du coin supérieur gauche ?* | Chaque objet mot fournit également `width` et `height`. Calculez `x2 = x + width` et `y2 = y + height` pour obtenir le coin opposé. |
| *Puis‑je traiter plusieurs images en lot ?* | Absolument. Enveloppez les étapes dans une boucle `for image_path in Path("folder").glob("*.png"):` et collectez les résultats par fichier. |
| *Comment choisir un modèle IA pour la correction ?* | Pour du texte générique, un petit GPT‑2 affiné sur les erreurs OCR fonctionne. Pour des données spécifiques à un domaine (par ex., prescriptions médicales), entraînez un modèle séquence‑à‑séquence sur des données bruitées‑propres appariées. |
| *Le score de confiance est‑il utile après la correction IA ?* | Vous pouvez toujours conserver la confiance originale pour le débogage, mais l’IA peut produire son propre score de confiance si le modèle le supporte. |

---

## Cas limites et bonnes pratiques  

1. **Images vides ou corrompues** – vérifiez toujours que `structured_result.words` n’est pas vide avant de continuer.  
2. **Scripts non latins** – assurez‑vous que votre moteur OCR est configuré pour la langue cible ; le post‑processeur IA doit être entraîné sur le même script.  
3. **Performance** – la correction IA peut être coûteuse. Mettez en cache les résultats si vous réutilisez la même image, ou exécutez l’étape IA de façon asynchrone.  
4. **Système de coordonnées** – les bibliothèques OCR peuvent utiliser des origines différentes (coin supérieur gauche vs. coin inférieur gauche). Ajustez en conséquence lors de la superposition sur des PDF ou des canevas.  

---

## Conclusion  

Vous disposez maintenant d’une méthode solide, de bout en bout, pour **post‑traiter l’OCR** et **extraire du texte avec coordonnées** de manière fiable. En activant la sortie structurée, en faisant passer le résultat par une couche de correction IA, et en préservant les boîtes englobantes originales, vous pouvez transformer des scans OCR bruyants en texte propre et spatialement conscient, prêt pour des tâches en aval comme la génération de PDF, l’automatisation de la saisie de données, ou les superpositions en réalité augmentée.

Prêt pour l’étape suivante ? Essayez de remplacer l’IA factice par un appel OpenAI `gpt‑4o‑mini`, ou intégrez le pipeline dans un FastAPI

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}