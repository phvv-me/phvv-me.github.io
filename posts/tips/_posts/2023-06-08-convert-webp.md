---
header:
  overlay_image: assets/webp/mohammad-rahmani-code-editor.webp
  image_description: Open code editor in laptop screen
  caption: Photo by [**Mohammad Rahmani**](https://unsplash.com/ja/@afgprogrammer)
layout: single
tags:
    - programming
title: How to Convert Images to WebP Format with Compression Using cwebp
excerpt: Learn how to use the cwebp command-line tool to convert images to WebP format with compression.
---

## Introduction

WebP is a modern image format that provides superior compression compared to JPEG and PNG formats. If you have a large collection of images that you want to convert to WebP format with compression, you can use the `cwebp` command-line tool. In this post, we'll show you how to use the `cwebp` tool to convert images to WebP format with compression.

## TL;DR

To convert all images in a folder to WebP format with compression and save them in a sibling folder named `webp`, run the following command in the Terminal:

```
for file in /path/to/folder/*.{jpg,jpeg,png}; do cwebp -q 80 "$file" -o "../webp/$(basename "$file" .jpg).webp"; done
```

## Instructions

1. Install the WebP image format library on your system. You can download the library from the [official website](https://developers.google.com/speed/webp/docs/precompiled).
2. Open the Terminal on your system.
3. Navigate to the folder containing the images you want to convert using the `cd` command.
4. Run the following command to convert all images in the folder to WebP format with compression and save them in the same folder:

   ```
   for file in *.{jpg,jpeg,png}; do cwebp -q 80 "$file" -o "${file%.*}.webp"; done
   ```

   This command uses a `for` loop to iterate over all files in the folder that have a `.jpg`, `.jpeg`, or `.png` extension. For each file, it runs the `cwebp` command with a quality setting of 80 and saves the output file with the same original filename but with a `.webp` extension.

   You can adjust the quality setting to a value between 0 and 100 to control the compression level. A higher quality setting results in a larger file size and better image quality.

5. If you want to save the converted files in a different sibling folder named `webp`, run the following command instead:

   ```
   for file in *.{jpg,jpeg,png}; do cwebp -q 80 "$file" -o "../webp/$(basename "$file" .jpg).webp"; done
   ```

   This command is similar to the previous command, but it saves the output files in a sibling folder named `webp` with the same original filename but with a `.webp` extension.

## Example

Suppose you have a folder named `images` that contains the following three image files:

```
images/
├── cat.jpg
├── dog.jpeg
└── bird.png
```

To convert all images in the folder to WebP format with compression and save them in the same folder, follow these steps:

1. Open the Terminal on your system.
2. Navigate to the `images` folder using the `cd` command.
3. Run the following command:

   ```
   for file in *.{jpg,jpeg,png}; do cwebp -q 80 "$file" -o "${file%.*}.webp"; done
   ```

After running the command, the `images` folder will contain the following six files:

```
images/
├── cat.jpg
├── cat.webp
├── dog.jpeg
├── dog.webp
├── bird.png
└── bird.webp
```

The original image files are still present, and the converted files have the same original filename but with a `.webp` extension.

## Conclusion

In this post, we showed you how to use the `cwebp` command-line tool to convert images to WebP format with compression. By using this technique, you can significantly reduce the file size of your images without sacrificing image quality.

| Original Image | Converted Image |
| --- | --- |
| ![Original JPEG Image](assets/images/../../../../../assets/images/two-woman-sitting-on-sofa-while-using-laptops.jpg) | ![Converted WebP Image](assets/images/../../../../../assets/webp/two-woman-sitting-on-sofa-while-using-laptops.webp) |
| --- | --- |