---
category: general
date: 2026-05-28
description: How to perform OCR in ASP.NET Core—learn to upload image, extract text
  from image, and handle file upload efficiently.
draft: false
keywords:
- how to perform OCR
- extract text from image
- handle file upload
- how to upload file
- upload image OCR
language: en
og_description: How to perform OCR in ASP.NET Core. Learn step‑by‑step how to upload
  an image, extract text from image, and handle file upload with Aspose OCR.
og_title: How to Perform OCR in ASP.NET Core – Full Guide
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: How to perform OCR in ASP.NET Core—learn to upload image, extract text
    from image, and handle file upload efficiently.
  headline: How to Perform OCR in ASP.NET Core – Full Guide
  type: TechArticle
tags:
- OCR
- ASP.NET Core
- C#
- file upload
title: How to Perform OCR in ASP.NET Core – Full Guide
url: /net/text-recognition/how-to-perform-ocr-in-asp-net-core-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Perform OCR in ASP.NET Core – Full Guide

Ever wondered **how to perform OCR** inside a modern web API without pulling your hair out? You're not the only one. Developers constantly need to let users drop a picture—maybe a receipt, a passport scan, or a handwritten note—and get the raw text back in JSON.  

In this tutorial we’ll walk through a complete, production‑ready solution that shows **how to upload file**, validates it, runs Aspose OCR, and finally **extract text from image**. By the end you’ll have a ready‑to‑paste controller that you can drop into any ASP.NET Core project.

## What You’ll Build

- An `OcrController` that accepts multipart/form‑data uploads
- Validation that the file actually exists and isn’t empty
- Asynchronous OCR processing using the Aspose OCR engine
- A clean JSON response containing the recognized text

No external services, no hidden magic—just pure C# code you can run locally.

## Prerequisites (What You Need Before Starting)

| Requirement | Why It Matters |
|-------------|----------------|
| .NET 6 SDK or later | ASP.NET Core 6+ gives us minimal API features and async support. |
| Visual Studio 2022 (or VS Code) | IDE makes debugging easier, but any editor works. |
| Aspose.OCR NuGet package (`dotnet add package Aspose.OCR`) | The engine that actually performs the OCR work. |
| Basic knowledge of ASP.NET Core MVC | We’ll be using `ControllerBase` and routing attributes. |

If you’ve got those, great—let’s dive in.

## Step 1: Set Up the Project and Install Aspose OCR

Open a terminal and create a fresh web API project:

```bash
dotnet new webapi -n OcrDemo
cd OcrDemo
dotnet add package Aspose.OCR
```

That single command pulls in the OCR library and all its dependencies. Nothing else to configure; Aspose works out‑of‑the‑box for common image formats.

## Step 2: Add the OCR Controller (The Core of **how to perform OCR**)

Create a new file `Controllers/OcrController.cs` and paste the following code. It’s the full, runnable example—no missing pieces.

```csharp
using Aspose.OCR;
using Microsoft.AspNetCore.Mvc;
using System.Threading.Tasks;

namespace OcrDemo.Controllers
{
    [ApiController]
    [Route("[controller]")]
    public class OcrController : ControllerBase
    {
        // Step 1: Receive the uploaded file from the request
        [HttpPost("upload")]
        public async Task<IActionResult> Upload([FromForm] IFormFile uploadedFile)
        {
            // Step 2: Validate that a file was actually provided
            if (uploadedFile == null || uploadedFile.Length == 0)
                return BadRequest("No file supplied.");

            // Step 3: Open a read‑only stream for the file content
            await using var fileStream = uploadedFile.OpenReadStream();

            // Step 4: Create the OCR engine and load the image from the stream
            var ocrEngine = new OcrEngine();
            ocrEngine.Image = ImageStream.FromStream(fileStream);

            // Step 5: Perform asynchronous text recognition
            string extractedText = await ocrEngine.RecognizeAsync();

            // Step 6: Return the recognized text in the response
            return Ok(new { extractedText });
        }
    }
}
```

### Why This Works

- **`[FromForm] IFormFile`** tells ASP.NET Core to bind the multipart file part to `uploadedFile`. That’s the classic way to **handle file upload** in a web API.
- The `if` guard ensures we **handle file upload** errors gracefully, returning a 400 Bad Request if the client forgot to send a file.
- `using var fileStream = uploadedFile.OpenReadStream();` opens a *read‑only* stream, which is essential for large files—no need to load the whole image into memory at once.
- `ocrEngine.Image = ImageStream.FromStream(fileStream);` feeds the stream directly into Aspose OCR, keeping the pipeline lean.
- `await ocrEngine.RecognizeAsync();` runs the heavy lifting on a background thread, so our API stays responsive. This is the heart of **how to perform OCR** asynchronously.
- Finally, we wrap the result in a JSON object (`{ extractedText }`)—perfect for front‑end consumption.

## Step 3: Configure the Request Size Limit (Optional but Handy)

If you expect high‑resolution scans, bump the default request size. Add this to `Program.cs`:

```csharp
builder.Services.Configure<FormOptions>(options =>
{
    options.MultipartBodyLengthLimit = 50 * 1024 * 1024; // 50 MB
});
```

Now the API won’t choke on a 10 MB receipt image. Adjust the limit based on your use case.

## Step 4: Test the Endpoint with cURL or Postman

Here’s a quick cURL command you can run from the terminal:

```bash
curl -X POST http://localhost:5000/ocr/upload \
  -F "uploadedFile=@/path/to/your/image.png"
```

You should see a JSON payload similar to:

```json
{
  "extractedText": "Sample text that was on the image."
}
```

If the image contains no recognizable characters, the string will be empty—nothing crashes, just an empty result. That’s a good edge case to keep in mind.

## Step 5: Visual Confirmation (Optional Image)

Below is a placeholder screenshot that demonstrates the JSON response you’ll receive after a successful OCR request.

![How to perform OCR result – screenshot of JSON response showing extracted text](/images/ocr-result.png)

*Alt text:* **how to perform OCR result screenshot showing extracted text from image**

## Common Pitfalls & Pro Tips

| Pitfall | Solution |
|---------|----------|
| **Unsupported image format** (e.g., TIFF with multiple pages) | Convert to PNG/JPEG first or use Aspose's `ImageConverter` before feeding it to `OcrEngine`. |
| **Large files cause memory pressure** | Stream the file as shown; avoid `IFormFile.CopyToAsync` into a `MemoryStream`. |
| **OCR returns garbled text** | Ensure the image is high‑contrast and properly oriented. Pre‑process with `ocrEngine.Preprocess()` if needed. |
| **Multiple concurrent requests** | Aspose OCR is thread‑safe, but you may want to limit concurrency with a semaphore if your server is memory‑constrained. |

## Extending the Example: Bulk Upload & Parallel Processing

If you need to **handle file upload** for several images at once, change the action signature to accept a list:

```csharp
[HttpPost("batch")]
public async Task<IActionResult> BatchUpload([FromForm] List<IFormFile> files)
{
    if (files == null || !files.Any())
        return BadRequest("No files supplied.");

    var results = new List<object>();

    foreach (var file in files)
    {
        await using var stream = file.OpenReadStream();
        var engine = new OcrEngine { Image = ImageStream.FromStream(stream) };
        var text = await engine.RecognizeAsync();
        results.Add(new { fileName = file.FileName, extractedText = text });
    }

    return Ok(results);
}
```

Now you can **upload image OCR** in bulk—great for scanning a folder of receipts in one go.

## Security Considerations

- **Validate file extensions** (`.png`, `.jpg`, `.jpeg`) before processing to avoid malicious uploads.
- **Scan for viruses** if your API is exposed to the internet; integrate with a service like ClamAV.
- **Rate‑limit** the endpoint to prevent denial‑of‑service attacks.

## Expected Output & How to Verify

When you hit the `/ocr/upload` endpoint with a clear image containing the word “Hello”, the response should be:

```json
{
  "extractedText": "Hello"
}
```

You can quickly verify by opening the browser’s developer tools → Network tab, or by inspecting the cURL output.

## Recap – What We Covered

- Set up an ASP.NET Core project and added the Aspose OCR NuGet package.
- Implemented a clean controller that shows **how to perform OCR**, **handle file upload**, and **extract text from image**.
- Discussed error handling, performance tweaks, and security best practices.
- Provided a ready‑to‑run code sample plus a bulk‑upload variant.

## What’s Next?

- **Add language support**: Aspose OCR can be configured for different languages (`ocrEngine.Language = Language.English;`).
- **Integrate with a database**: Store the extracted text alongside metadata for later searching.
- **Front‑end UI**: Build a simple React or Blazor page that lets users drag‑and‑drop images and see the OCR result instantly.

Feel free to experiment—swap out the OCR engine, try different image pre‑processing steps, or hook the result into a downstream AI model. The sky’s the limit when you know **how to perform OCR** in a modern .NET stack.

Happy coding, and may your text always be legible!


## Related Tutorials

- [How to OCR Image – Perform OCR on Image in OCR Image Recognition](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)
- [How to Use Aspose to Recognize Image from Stream in OCR Image Recognition](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)
- [How to Set Threshold Value in OCR Image Recognition](/ocr/english/net/ocr-settings/set-threshold-value/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}