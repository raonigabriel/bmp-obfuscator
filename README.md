```markdown
# BMP Obfuscator

A free online tool to hide text inside a data-efficient **1-bit monochrome BMP image**, using a simple, reversible **bitwise NOT operation**.

➡️ [Live demo](https://raonigabriel.github.io/bmp-obfuscator/)

---

## 🧠 How It Works

This tool obfuscates your input text by flipping all bits of each 64-bit chunk using JavaScript's `DataView` and `BigInt64` APIs. The obfuscated binary is then embedded into a valid [BMP file format](https://en.wikipedia.org/wiki/BMP_file_format) using 1-bit-per-pixel encoding.

This approach is:

- **Symmetric**: the same operation is used to encode and decode.
- **Not encryption**: it simply flips bits; there's no cryptographic key.
- **Lossless**: original text is perfectly recoverable, byte-for-byte.

---

## 💡 Use Cases

This is **not** secure encryption, but it may be useful for:

- Educational purposes (bitwise ops, binary formats, image structure)
- Lightweight steganographic experiments
- Obfuscation in non-critical contexts (e.g., Easter eggs, demos)

---

## 🔍 Technical Details

- Format: 1-bit-per-pixel **monochrome BMP**
- Transformation: `~BigInt64` (bitwise NOT)
- Padding: BMP pixel data is padded to fit a square image (width × height), aligned to 32 pixels
- BMP headers manually created using `DataView`
- No external dependencies

The **encoded text** is converted to bytes using `TextEncoder`, padded to fit into the pixel buffer, and then each 64-bit block is flipped with:

```js
const original = dataView.getBigInt64(offset, true);
const obfuscated = ~original;
dataView.setBigInt64(offset, obfuscated, true);
```

To decode, the exact same operation is applied.

---

## 🧱 Why BMP?

We chose the BMP format because:

- It's **uncompressed** and well-documented
- Easy to manipulate at the byte level
- Supports 1-bit-per-pixel images (very compact)
- Does not require external encoders or decoders

See: [Wikipedia – BMP File Format](https://en.wikipedia.org/wiki/BMP_file_format)

BMP padding: Each row of pixels is padded to a multiple of **4 bytes**, which is handled internally in the layout.

---

## 📦 JavaScript APIs Used

- [`TextEncoder`](https://developer.mozilla.org/en-US/docs/Web/API/TextEncoder)
- [`TextDecoder`](https://developer.mozilla.org/en-US/docs/Web/API/TextDecoder)
- [`DataView`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/DataView)
- [`BigInt64`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/BigInt64Array)
- [`Blob`](https://developer.mozilla.org/en-US/docs/Web/API/Blob)
- File APIs: `FileReader`, `ArrayBuffer`, `Uint8Array`

---

## ⚠️ Disclaimer

> This is **not** encryption and should **not** be used for securing sensitive or private information.  
> It is a **simple obfuscation** mechanism based on bitwise inversion and offers no resistance against forensic analysis or reverse engineering.

---

## 📚 Related Concepts

- [Steganography](https://en.wikipedia.org/wiki/Steganography)
- [Obfuscation](https://en.wikipedia.org/wiki/Obfuscation_(software))
- [Bitwise **NOT** Operation](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Bitwise_NOT)
- [Involution](https://en.wikipedia.org/wiki/Involution_(mathematics)#Computer_science)
- [Monochrome Bitmap](https://en.wikipedia.org/wiki/Bitmap#Monochrome_bitmap)

---

## 👨‍💻 Author

Made with 💙 by [Raoni Gabriel](https://github.com/raonigabriel)  
🔗 [LinkedIn](https://www.linkedin.com/in/raonigabriel/)

---

## 📜 License

[Apache License, Version 2.0](https://www.apache.org/licenses/LICENSE-2.0)
```
