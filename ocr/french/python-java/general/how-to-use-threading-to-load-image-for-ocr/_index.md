---
category: general
date: 2026-04-26
description: Comment utiliser le threading pour charger une image pour l’OCR en Python.
  Apprenez le traitement OCR asynchrone avec des callbacks, des threads en arrière‑plan
  et le chargement d’images en quelques étapes seulement.
draft: false
keywords:
- how to use threading
- load image for OCR
- python threading OCR
- async OCR callback
- background thread image processing
language: fr
og_description: Comment utiliser le multithreading pour charger une image pour l'OCR
  en Python. Ce guide présente un exemple complet, exécutable, avec des callbacks
  et une exécution en arrière-plan.
og_title: Comment utiliser le multithreading pour charger une image pour l'OCR
tags:
- Python
- Threading
- OCR
- Image Processing
title: Comment utiliser le multithreading pour charger une image pour l’OCR
url: /fr/python-java/general/how-to-use-threading-to-load-image-for-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment utiliser le threading pour charger une image pour l'OCR

Vous vous êtes déjà demandé **comment utiliser le threading** pour charger une image pour l'OCR sans bloquer votre application ? C’est un scénario qui apparaît que vous construisiez un scanner de bureau, un service web ou un simple script qui traite d’énormes images. La bonne nouvelle ? Quelques lignes de Python et le bon modèle de threading garderont votre interface réactive pendant que le moteur OCR fait sa magie.

Dans ce tutoriel, nous parcourrons un exemple complet, de bout en bout : charger un PNG volumineux, lancer l’OCR sur un thread d’arrière‑plan, et gérer le résultat avec un callback. À la fin, vous saurez non seulement **comment utiliser le threading**, mais aussi **comment charger une image pour l'OCR** de manière propre et réutilisable.

## Ce dont vous avez besoin

- Python 3.9+ (la syntaxe que nous utilisons fonctionne sur toute version récente)
- `pillow` pour la gestion des images (`pip install pillow`)
- `pytesseract` comme un léger wrapper autour de Tesseract OCR (`pip install pytesseract`)
- Moteur Tesseract OCR installé sur votre machine (téléchargez depuis [tesseract‑ocr.org](https://github.com/tesseract-ocr/tesseract))
- Un fichier image volumineux que vous souhaitez traiter (`large_image.png` dans ce guide)

Aucun framework supplémentaire, pas d'async/await — juste le classique `threading` et un callback.

## Étape 1 : Importer le module threading (nécessaire pour l'exécution en arrière‑plan)

La première chose que nous faisons est d’importer le module `threading`. Il nous fournit la classe `Thread`, qui nous permet d’exécuter n’importe quelle fonction dans un thread OS séparé.

```python
import threading
```

*Pourquoi c’est important* : Si vous exécutez l’OCR sur le thread principal, votre programme (en particulier une interface graphique) se bloquera jusqu’à ce que l’OCR se termine. En déléguant le travail à un thread d’arrière‑plan, le thread principal reste libre pour mettre à jour l’UI, gérer les entrées utilisateur ou lancer d’autres tâches.

## Étape 2 : Définir un callback qui sera invoqué lorsque l'OCR est terminé

Un callback est simplement une fonction qu’un autre morceau de code appelle lorsqu’il a fini. Ici, nous afficherons le texte reconnu, mais vous pourriez le stocker, l’envoyer sur le réseau ou mettre à jour un widget UI.

```python
def ocr_done(result_text: str) -> None:
    """Called when the OCR thread finishes."""
    print("\n--- Async OCR finished ---")
    print(result_text)   # Display the recognized text
```

*Astuce pro* : Gardez le callback léger. Un traitement lourd à l’intérieur du callback annule l’intérêt du threading car il bloquera toujours le thread qui l’a appelé (souvent le thread principal).

## Étape 3 : Charger l'image que vous voulez traiter

Charger l'image est une préoccupation distincte de l’OCR, mais cela fait toujours partie du flux de travail global. Utiliser Pillow rend cela trivial.

```python
from PIL import Image

def load_image(path: str) -> Image.Image:
    """Loads an image from disk and returns a Pillow Image object."""
    try:
        img = Image.open(path)
        print(f"Image '{path}' loaded – size: {img.size}")
        return img
    except Exception as exc:
        raise RuntimeError(f"Failed to load image: {exc}") from exc
```

*Pourquoi nous le faisons ici* : Si l’image est énorme, la charger sur le thread principal peut déjà provoquer un ralentissement. Dans de nombreuses applications réelles, vous déchargeriez également le chargement vers un thread, mais pour plus de clarté nous le gardons synchrone.

## Étape 4 : Créer un petit wrapper d'engin OCR

Le fragment original utilisait `engine.process_async`. Nous allons imiter cela avec une petite classe qui démarre un thread en interne et appelle le callback fourni lorsqu’elle a terminé.

```python
import pytesseract

class SimpleOcrEngine:
    """A minimal OCR engine that runs pytesseract in a background thread."""

    def __init__(self, image: Image.Image):
        self.image = image

    def _run_ocr(self, callback):
        """Internal method executed in the worker thread."""
        try:
            # pytesseract returns the recognized text as a plain string
            text = pytesseract.image_to_string(self.image)
            callback(text)
        except Exception as exc:
            callback(f"OCR failed: {exc}")

    def process_async(self, callback):
        """Public method to start OCR on a new thread."""
        worker = threading.Thread(target=self._run_ocr, args=(callback,))
        worker.daemon = True          # Daemon so it won’t block program exit
        worker.start()
        print("OCR thread started…")
```

*Explication* :  
- `_run_ocr` effectue le travail lourd.  
- `process_async` crée un objet `Thread`, le marque comme daemon (afin que l’interpréteur puisse quitter même si le thread tourne encore), puis le démarre.  
- Le callback reçoit soit le texte OCR, soit un message d’erreur.

## Étape 5 : Assembler le tout et faire d'autres tâches pendant que l'OCR s'exécute

Nous orchestrons maintenant le flux complet : charger l’image, instancier le moteur, lancer l’OCR asynchrone, et garder le thread principal occupé avec autre chose (ici nous affichons simplement un message).

```python
if __name__ == "__main__":
    # 1️⃣ Load the image you want to OCR
    img_path = "YOUR_DIRECTORY/large_image.png"
    image = load_image(img_path)

    # 2️⃣ Create the OCR engine instance
    engine = SimpleOcrEngine(image)

    # 3️⃣ Start OCR on a background thread, passing our callback
    engine.process_async(callback=ocr_done)

    # 4️⃣ Do other work while OCR runs (simulated with a loop)
    for i in range(5):
        print(f"Main thread doing other work… ({i+1}/5)")
        # In a real app you might update a progress bar, handle UI events, etc.
        threading.Event().wait(0.5)  # Sleep 0.5 s without blocking the OS thread

    # Give the OCR thread a moment to finish before the script exits
    threading.Event().wait(2)
    print("Script finished.")
```

**Sortie attendue (troncature pour la brièveté)** :

```
Image 'YOUR_DIRECTORY/large_image.png' loaded – size: (3840, 2160)
OCR thread started…
Main thread doing other work… (1/5)
Main thread doing other work… (2/5)
...
--- Async OCR finished ---
The quick brown fox jumps over the lazy dog.
Script finished.
```

Si l’OCR échoue, le callback affichera un message d’erreur à la place du texte.

---

## Pourquoi cette approche fonctionne mieux qu'une simple boucle

- **Réactivité** : Le thread principal ne se bloque jamais sur l’appel OCR, qui peut prendre plusieurs secondes pour de grandes images.  
- **Scalabilité** : Vous pouvez lancer plusieurs instances de `SimpleOcrEngine`, chacune sur son propre thread, pour traiter un lot d’images en parallèle.  
- **Séparation des responsabilités** : Le chargement, le traitement et la gestion du résultat sont clairement séparés, ce qui rend le code plus facile à tester et à maintenir.

## Pièges courants et comment les éviter

| Piège | Ce qui se passe | Solution |
|-------|----------------|----------|
| Oublier de marquer le thread comme *daemon* | Le script reste bloqué après la fin du travail principal parce que le thread OCR est encore actif. | Définissez `worker.daemon = True` **ou** appelez `join()` sur le thread avant de quitter. |
| Utiliser une variable globale pour le résultat sans verrous | Des conditions de concurrence peuvent corrompre les données lorsque plusieurs threads écrivent simultanément. | Passez le résultat via un callback (comme nous le faisons) ou utilisez des conteneurs thread‑safe comme `queue.Queue`. |
| Charger une image massive sur le thread principal | L’UI se fige avant même que l’OCR en arrière‑plan ne démarre. | Déchargez également le chargement d’image vers un thread, ou utilisez des techniques de chargement paresseux. |
| Ne pas gérer les exceptions à l’intérieur du thread de travail | Des exceptions non capturées tuent silencieusement le thread, vous laissant sans résultat. | Enveloppez la logique OCR dans `try/except` et transmettez l’erreur au callback. |

## Étendre ce modèle

- **Rapport de progression** : Utilisez un `queue.Queue` partagé pour pousser les pourcentages de progression intermédiaires du thread OCR vers le thread principal.  
- **Pool de threads** : Pour le traitement par lots, remplacez les objets `Thread` individuels par un `concurrent.futures.ThreadPoolExecutor`.  
- **Intégration UI** : Dans une application Tkinter ou PyQt, planifiez le callback avec `after()` (Tkinter) ou `QTimer.singleShot` (Qt) afin de garantir que les mises à jour UI s’effectuent sur le thread principal.

## Exemple complet fonctionnel (prêt à copier‑coller)

```python
import threading
from PIL import Image
import pytesseract

def ocr_done(result_text: str) -> None:
    """Callback invoked when OCR finishes."""
    print("\n--- Async OCR finished ---")
    print(result_text)

def load_image(path: str) -> Image.Image:
    """Load an image and report its size."""
    try:
        img = Image.open(path)
        print(f"Image '{path}' loaded – size: {img.size}")
        return img

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}