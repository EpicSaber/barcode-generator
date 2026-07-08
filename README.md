[Barcode Generator](https://apify.com/zsoftware/barcode-generator?fpr=data)

# 📦 Barcode Generator

This Apify actor generates barcode images from a list of input texts.

Each barcode is saved as an individual PNG file, and all images are also bundled into a downloadable ZIP file.

## 🛠 Features

- Supports multiple barcode types (e.g., **Code128**, **EAN13**)
- Saves individual barcode images to the Key-Value Store
- Packages all barcode images into a single ZIP file
- Outputs structured dataset records (text, barcode type, filename, image URL)

Supported barcode types include: `code128`, `ean13`, `ean8`, `upca`, `isbn13`, `issn`, etc.

## 📥 Input Fields

| Field | Type | Required | Default | Description |
| --- | --- | --- | --- | --- |
| `texts` | Array of strings | Yes | — | List of texts to generate barcodes from. |
| `barcodeType` | String | No | `code128` | Barcode format to use for generation. |

> ℹ️ **Note**: Some barcode types (e.g., `ean13`, `ean8`) require the text to be numeric and of specific lengths.

## 📤 Output

- Each generated barcode is saved as a **PNG** image file in the default Key-Value Store.
- All images are also bundled together into a single **ZIP** file (`barcodes.zip`).
- A dataset entry is created for each barcode, including:

- The original text
- The filename
- A public URL to access the barcode image

Example of a dataset record:

```
{
  "text": "123456789012",
  "filename": "barcode_1.png",
  "image_url": "https://api.apify.com/v2/key-value-stores/{STORE_ID}/records/barcode_1.png"
}
```

## ⚙️ How It Works

1. **Input Processing**

The actor reads the list of `texts` provided in the input and the selected `barcodeType`.
2. **Barcode Generation**

For each text:

- A barcode image is generated based on the specified barcode type.
- The barcode is saved as a PNG image into the Key-Value Store.
3. **Dataset Entry Creation**

Alongside each generated barcode:

- A dataset record is created containing the original text, the image filename, and a direct image URL.
4. **ZIP File Creation**

After all barcodes are generated:

- All barcode images are bundled together into a `barcodes.zip` file and saved to the Key-Value Store for easy downloading.
5. **Final Output**

Users can:

- Download individual barcode images.
- Download the entire collection as a single ZIP file.
- Access a structured dataset with links to each barcode image.