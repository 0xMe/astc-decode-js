## What is ASTC?
ASTC is a texture compression format used primarily in graphics (especially mobile and web), offering good quality at various bitrates.

## Decoding ASTC in the Web
Decoding ASTC on the web typically means:
- Using JavaScript or WebAssembly (WASM) to decode `.astc` files to raw RGBA pixel buffers.
- Displaying the result on a `<canvas>` or using in WebGL.

### Options

1. **Use WebAssembly ASTC Decoder**
   - There are open-source ASTC decoders (C/C++) you can compile to WASM:
     - [ARM’s astc-encoder/decoder](https://github.com/ARM-software/astc-encoder)
   - Compile the decoder to WASM (via Emscripten), then call from JS.

2. **JavaScript Libraries**
   - There aren’t many pure JS ASTC decoders (due to performance), so WASM is preferred.
   - Example: [Basis Universal](https://github.com/BinomialLLC/basis_universal) supports ASTC and offers WASM/JS bindings.

3. **Browser Support**
   - WebGL does not natively support ASTC textures everywhere; you must decode to RGBA for wide compatibility.
   
### Example


```html
<!DOCTYPE html>
<html>
<head>
    <title>ASTC Decoder Example</title>
      <script src="https://cdn.jsdelivr.net/gh/0xMe/astc-decode-js@main/astc-decode.js"></script>
</head>
<body>
    <canvas id="outputCanvas"></canvas>
    <script>
    async function DisplayASTC() {
        const canvas = document.getElementById('outputCanvas');
        const ctx = canvas.getContext('2d');
        try {
            // Wait for auto-initialization or manually initialize
            if (!wasm) {
                await initASTCDecoder();
            }
    
            const response = await fetch('https://dl-tata.freefireind.in/live/ABHotUpdates/IconCDN/android/906000076_rgb.astc');
            const astcData = new Uint8Array(await response.arrayBuffer());
            const decodedData = decodeASTCTexture(astcData);
            
            const header = parseASTCHeader(astcData);
            canvas.width = header.width;
            canvas.height = header.height;
            const success = drawToCanvas(ctx, decodedData, header.width, header.height);
            if (!success) {
                // use Default Icon
            } 
        } catch (error) {
            console.error('Decoding error:', error);
        }
    }
    // Start the process when page loads
    window.addEventListener('load', DisplayASTC);
    </script>
</body>
</html>
```

## Resources
- [ASTC-Encoder on GitHub](https://github.com/ARM-software/astc-encoder)
- [Basis Universal WASM Decoder](https://github.com/BinomialLLC/basis_universal)
- [Emscripten Documentation](https://emscripten.org/)
