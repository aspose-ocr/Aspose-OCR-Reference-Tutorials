---
category: general
date: 2026-06-03
description: Tutoriel OCR de sous-titres vidéo montrant comment extraire des images
  d’une vidéo et lire le texte des fichiers vidéo tels que MP4 en utilisant Aspose.OCR.
draft: false
keywords:
- video subtitle ocr
- extract frames from video
- read text from video
- extract text from mp4
language: fr
og_description: Apprenez la reconnaissance OCR des sous-titres vidéo avec Aspose.OCR.
  Extrayez des images d’une vidéo, lisez le texte d’une vidéo et extrayez le texte
  d’un MP4 en quelques minutes.
og_title: OCR de sous-titres vidéo en C# – Guide étape par étape
schemas:
- author: Aspose
  dateModified: '2026-06-03'
  description: Video subtitle OCR tutorial showing how to extract frames from video
    and read text from video files like MP4 using Aspose.OCR.
  headline: Video Subtitle OCR in C# – Complete Guide
  type: TechArticle
- description: Video subtitle OCR tutorial showing how to extract frames from video
    and read text from video files like MP4 using Aspose.OCR.
  name: Video Subtitle OCR in C# – Complete Guide
  steps:
  - name: Decodes an MP4 (or any supported format) into individual `Bitmap` frames.
    text: Decodes an MP4 (or any supported format) into individual `Bitmap` frames.
  - name: Limits the OCR region to the subtitle band so the engine isn’t distracted
      by the whole picture.
    text: Limits the OCR region to the subtitle band so the engine isn’t distracted
      by the whole picture.
  - name: Processes each frame with Aspose’s `VideoOcrProcessor`.
    text: Processes each frame with Aspose’s `VideoOcrProcessor`.
  - name: Prints the recognized subtitle text to the console.
    text: Prints the recognized subtitle text to the console.
  type: HowTo
tags:
- C#
- Aspose.OCR
- video-processing
title: OCR de sous-titres vidéo en C# – Guide complet
url: /fr/net/text-recognition/video-subtitle-ocr-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR de sous-titres vidéo en C# – Guide complet

Vous avez déjà eu besoin de **video subtitle ocr** mais vous ne saviez pas par où commencer ? Vous n'êtes pas seul. Que vous numérisiez des enregistrements de cours, extrayiez les sous-titres de vidéos de formation, ou soyez simplement curieux de lire du texte à partir d’une vidéo, ce tutoriel vous montre exactement comment le faire avec C# et Aspose.OCR.  

Dans les prochaines minutes, nous extrairons des images d’une vidéo, exécuterons l’OCR sur ces images, et enfin afficherons le texte des sous-titres image par image. À la fin, vous pourrez **lire du texte à partir d’une vidéo** – y compris les fichiers MP4 – sans chercher d’outils tiers.

## Ce que vous allez créer

Nous créerons une petite application console qui :

1. Décode un MP4 (ou tout format supporté) en images `Bitmap` individuelles.  
2. Limite la région OCR à la bande de sous-titres afin que le moteur ne soit pas distrait par l’image entière.  
3. Traite chaque image avec le `VideoOcrProcessor` d’Aspose.  
4. Affiche le texte des sous-titres reconnu dans la console.

Pas de fioritures, juste un exemple complet fonctionnel que vous pouvez intégrer dans un projet réel.

## Prérequis

- **.NET 6.0** ou ultérieur (le code fonctionne également sur .NET Framework 4.7+).  
- **Aspose.OCR for .NET** – installez via NuGet : `Install-Package Aspose.OCR`.  
- Un fichier vidéo (MP4 fonctionne très bien).  
- Un moyen de décoder les images vidéo – la démo utilise une méthode factice, mais vous pouvez brancher FFmpeg, OpenCV, ou toute bibliothèque qui renvoie des objets `Bitmap`.  

> Conseil pro : Si vous êtes sous Windows, le package `System.Drawing.Common` fonctionne bien pour les `Bitmap`. Sous Linux/macOS, vous aurez besoin de la dépendance native `libgdiplus`.

## Étape 1 – Extraire des images d’une vidéo

Le premier obstacle consiste à transformer une image animée en images fixes. La méthode `GetVideoFrames` ci‑dessous est délibérément laissée vide ; remplacez‑la par votre décodeur préféré. Voici un rapide croquis utilisant FFmpeg‑Core (juste pour illustrer la forme des données) :

```csharp
using System.Collections.Generic;
using System.Drawing;
using System.Diagnostics;
using System.IO;

/// <summary>
/// Extracts every frame from the supplied video file and yields it as a Bitmap.
/// You can swap this implementation for OpenCV, MediaToolkit, etc.
/// </summary>
static IEnumerable<Bitmap> GetVideoFrames(string videoPath)
{
    // Create a temporary folder for the extracted PNGs
    string tempDir = Path.Combine(Path.GetTempPath(), Guid.NewGuid().ToString());
    Directory.CreateDirectory(tempDir);

    // FFmpeg command: -i input -vf fps=1 output_%04d.png (1 fps for demo)
    var startInfo = new ProcessStartInfo
    {
        FileName = "ffmpeg",
        Arguments = $"-i \"{videoPath}\" -vf fps=1 \"{tempDir}\\frame_%04d.png\" -hide_banner -loglevel error",
        RedirectStandardOutput = true,
        UseShellExecute = false,
        CreateNoWindow = true
    };
    Process ffmpeg = Process.Start(startInfo);
    ffmpeg.WaitForExit();

    foreach (var file in Directory.GetFiles(tempDir, "frame_*.png"))
    {
        using var bmp = new Bitmap(file);
        // Clone the bitmap so the file can be deleted later
        yield return new Bitmap(bmp);
    }

    // Clean up
    Directory.Delete(tempDir, true);
}
```

> **Pourquoi c’est important :** Extraire des images fournit à l’engin OCR une image statique avec laquelle travailler, ce qui améliore considérablement la précision comparé à la lecture directe d’un flux vidéo.

## Étape 2 – Configurer le VideoOcrProcessor

Maintenant que nous disposons d’une séquence d’objets `Bitmap`, nous pouvons les transmettre à Aspose.OCR. Le `VideoOcrProcessor` nous permet de définir une **Region of Interest (ROI)** – idéal pour les sous-titres qui se trouvent généralement en haut ou en bas de l’image.

```csharp
using Aspose.OCR.Video;
using System.Drawing;

// Create the processor and focus on the top 200 pixels (typical subtitle band)
var ocrProcessor = new VideoOcrProcessor
{
    // ROI = new Rectangle(x, y, width, height)
    Roi = new Rectangle(0, 0, 1920, 200)   // adjust width/height to your video resolution
};
```

> **Pourquoi limiter la ROI ?** En ignorant le reste de l’image, nous réduisons le bruit, diminuons le temps de traitement et évitons les faux positifs provenant des graphiques d’arrière‑plan.

## Étape 3 – Exécuter l’OCR sur la séquence d’images

Avec le processeur prêt, alimenter les images se fait en une seule ligne. La méthode `Process` renvoie un enumerable d’objets `OcrResult`, chacun contenant le texte reconnu pour l’image correspondante.

```csharp
IEnumerable<Bitmap> videoFrames = GetVideoFrames(@"C:\Videos\lecture.mp4");

// Execute OCR on every extracted frame
IEnumerable<OcrResult> ocrResults = ocrProcessor.Process(videoFrames);
```

> **Que se passe-t-il en coulisses ?** Aspose.OCR normalise en interne chaque bitmap, exécute un reconnaisseur basé sur un réseau de neurones, puis post‑traite la sortie pour améliorer la ponctuation et les sauts de ligne.

## Étape 4 – Afficher le texte extrait

Enfin, nous parcourons les résultats et affichons chaque ligne de sous-titre. Vous pourriez également les écrire dans un fichier SRT, une base de données, ou les transmettre à un service de traduction.

```csharp
int frameIndex = 0;
foreach (var result in ocrResults)
{
    // result.Text contains the plain‑text subtitle for this frame
    Console.WriteLine($"Frame {frameIndex++}: {result.Text}");
}
```

### Exemple complet fonctionnel

Assembler le tout donne un programme console autonome :

```csharp
using Aspose.OCR.Video;
using System;
using System.Collections.Generic;
using System.Drawing;
using System.Diagnostics;
using System.IO;

class VideoSubtitleOcrDemo
{
    static void Main()
    {
        // 1️⃣ Extract frames from the MP4 (replace with your own decoder)
        IEnumerable<Bitmap> videoFrames = GetVideoFrames(@"C:\Videos\lecture.mp4");

        // 2️⃣ Configure OCR – focus on the subtitle band
        var ocrProcessor = new VideoOcrProcessor
        {
            Roi = new Rectangle(0, 0, 1920, 200) // tweak for your video size
        };

        // 3️⃣ Run OCR across all frames
        IEnumerable<OcrResult> ocrResults = ocrProcessor.Process(videoFrames);

        // 4️⃣ Output the recognized subtitle text
        int frameIndex = 0;
        foreach (var result in ocrResults)
        {
            Console.WriteLine($"Frame {frameIndex++}: {result.Text}");
        }
    }

    // --------------------------------------------------------------------
    // Helper: extract one‑frame‑per‑second PNGs using FFmpeg.
    // Replace this with any library that can return Bitmap objects.
    // --------------------------------------------------------------------
    static IEnumerable<Bitmap> GetVideoFrames(string videoPath)
    {
        string tempDir = Path.Combine(Path.GetTempPath(), Guid.NewGuid().ToString());
        Directory.CreateDirectory(tempDir);

        var startInfo = new ProcessStartInfo
        {
            FileName = "ffmpeg",
            Arguments = $"-i \"{videoPath}\" -vf fps=1 \"{tempDir}\\frame_%04d.png\" -hide_banner -loglevel error",
            RedirectStandardOutput = true,
            UseShellExecute = false,
            CreateNoWindow = true
        };
        using var ffmpeg = Process.Start(startInfo);
        ffmpeg.WaitForExit();

        foreach (var file in Directory.GetFiles(tempDir, "frame_*.png"))
        {
            using var bmp = new Bitmap(file);
            yield return new Bitmap(bmp);
        }

        Directory.Delete(tempDir, true);
    }
}
```

**Sortie attendue (exemple)**  

```
Frame 0: Welcome to the Introduction to Machine Learning.
Frame 1: In this lecture we will cover...
Frame 2: ...
```

Si l’OCR a du mal avec une image particulière, vous verrez une chaîne vide – c’est le signal pour ajuster la ROI ou augmenter le taux d’extraction d’images.

## Problèmes courants & comment les résoudre

| Problème | Pourquoi cela se produit | Solution |
|----------|--------------------------|----------|
| **Caractères indésirables** | Images à basse résolution ou forte compression | Extrayez les images à un débit binaire plus élevé, ou agrandissez le bitmap avant l’OCR (`Bitmap.Clone(new Size(...), ...)`). |
| **Aucun texte retourné** | La ROI ne couvre pas réellement la bande de sous-titres | Vérifiez les coordonnées du rectangle (utilisez un outil de capture d’écran pour mesurer). |
| **Goulot d’étranglement de performance** | Traiter chaque image à 30 fps est excessif | Sous‑échantillonnez à 1‑2 fps pour la plupart des flux de sous-titres ; vous pouvez toujours capturer chaque changement de sous-titre. |
| **FFmpeg introuvable** | `ffmpeg.exe` n’est pas dans le `PATH` | Fournissez le chemin complet dans `ProcessStartInfo.FileName` ou installez FFmpeg globalement. |

## Étendre la solution

- **Export to SRT** – concaténez les horodatages avec le texte OCR et écrivez un fichier SubRip.  
- **Multi‑language support** – définissez `ocrProcessor.Language = OcrLanguage.Spanish` (ou toute langue supportée).  
- **Real‑time processing** – transmettez les images directement depuis un flux en direct au lieu de les lire depuis le disque.  

Toutes ces variantes tournent toujours autour des idées principales d’**extraction d’images d’une vidéo**, **lecture de texte à partir d’une vidéo**, et **extraction de texte d’un mp4**.

## Conclusion

Nous venons de parcourir un flux de travail complet d’**video subtitle ocr** en C#. En extrayant des images d’une vidéo, en concentrant l’OCR sur la bande de sous-titres, et en itérant sur les résultats, vous pouvez de manière fiable **read text from video** des fichiers tels que MP4. Le code est prêt à être copié‑collé, et la conception modulaire vous permet de remplacer n’importe quel décodeur d’images que vous préférez.

Prochaines étapes ? Essayez d’exporter les résultats vers un fichier SRT, expérimentez différentes tailles de ROI, ou alimentez les sous-titres dans une API de traduction pour des légendes multilingues. Le ciel est la limite une fois que vous avez maîtrisé les bases de l’extraction de texte à partir d’une vidéo.

Bon codage, et que vos sous-titres soient toujours d’une clarté cristalline !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités d’API supplémentaires et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Extract Text from Image Using Aspose.OCR .NET](/ocr/english/net/image-and-drawing-recognition/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}