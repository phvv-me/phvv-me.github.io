---
header:
  overlay_image: assets/webp/mohammad-rahmani-code-editor.webp
  image_description: Open code editor in laptop screen
  caption: Photo by [**Mohammad Rahmani**](https://unsplash.com/ja/@afgprogrammer)
layout: single
tags:
    - vscode
title: How to fix inline LaTex equations with vscode regex find and replace
excerpt: Replace inline LaTex equation from `$...$` to `\\\(...\\\)` excluding `$ $...$ $` in VSCode
---

## TL;DR

- Find: `(?<!\$)\$(?!\$)(.*?)(?<!\$)\$(?!\$)`
- Replace: `\\\($1\\\)`

## Instructions

1. Open the Find and Replace panel in Visual Studio Code using `Ctrl + H` (Windows/Linux) or `Cmd + H` (Mac).
2. Make sure the regex mode is enabled by clicking on the `.*` button or pressing `Alt + R`.
3. In the Find input field, enter the following regex pattern: `(?<!\$)\$(?!\$)(.*?)(?<!\$)\$(?!\$)`.
   - Here, `(?<!\$)\$` matches a single `$` character that is not preceded by another `$`.
   - `(?!\$)\$` matches a single `$` character that is not followed by another `$`.
   - `(.*?)` captures the content between the dollar signs.
   - The negative 'lookarounds', `(?<!\$)` and `(?!\$)`, ensure that the `$...$` strings are not preceded or followed by another dollar sign, effectively excluding `$$...$$` strings.
4. In the Replace input field, enter: `\\\($1\\\)`.
   - Here, `\\\(` and `\\\)` represent the literal characters `\\(` and `\\)` in the replacement string.
   - `$1` refers to the captured group from the find pattern, which contains the content between the dollar signs.
5. Ensure that the "Match Case" and "Match Whole Word" options are unchecked unless you want to perform a case-sensitive or whole-word search.
6. Click on the Replace All button or use the Replace button to replace each occurrence individually.

Then, replacing `$...$` strings with `\(...\)` strings, excluding `$$...$$` strings in Visual Studio Code using regular expressions becomes possible.

### Attention

I replace using 3 backslashes, as Jekyll requires this to build the equations correctly.