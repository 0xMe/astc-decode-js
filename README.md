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
   


## Resources
- [ASTC-Encoder on GitHub](https://github.com/ARM-software/astc-encoder)
- [Basis Universal WASM Decoder](https://github.com/BinomialLLC/basis_universal)
- [Emscripten Documentation](https://emscripten.org/)