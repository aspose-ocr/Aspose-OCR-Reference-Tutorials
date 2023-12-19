---
title: Getting Rectangles with Text Areas in Aspose.OCR
linktitle: Getting Rectangles with Text Areas in Aspose.OCR
second_title: Aspose.OCR Java API
description: 
type: docs
weight: 12
url: /java/ocr-basics/get-rectangles-with-text-areas/
---

## Complete Source Code
```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AreasType;
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.examples.License.SetLicense;
import com.aspose.ocr.examples.Utils;

import java.awt.*;
import java.io.IOException;
import java.util.ArrayList;

public class GetRectanglesWithTextAreas {

	public static void main(String[] args) throws IOException {
		// ExStart:1
		// The path to the documents directory.
		String dataDir = "Your Document Directory";

		// The image path
		String imagePath = dataDir + "p3.png";

		//Create api instance
		AsposeOCR api = new AsposeOCR();

		// Recognize page by full path to file
		try {
			String result = api.RecognizePage(imagePath);
			System.out.println("Result: " + result);
		} catch (IOException e) {
			e.printStackTrace();
		}

		//Get rectangles with text areas in the image.
		ArrayList<Rectangle> rectResult = api.getTextAreas(imagePath, AreasType.PARAGRAPHS, true);
		for(Rectangle r : rectResult) {
			System.out.println("Text area:" + r);
		}
		// ExEnd:1
	}
}

```