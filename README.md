````md README.md
# sift-surf-webgpu

`sift-surf-webgpu` is a lightweight **WebGPU-based JavaScript library** that implements the classic SIFT (Scale-Invariant Feature Transform) and SURF (Speeded-Up Robust Features) algorithms for keypoint detection and descriptor matching — **directly in the browser**.

---

## ✨ Features

- 🔍 **SIFT + SURF** keypoint detection  
- 🎛️ **OpenCV-like API** (`detect`, `compute`, `detectAndCompute`)  
- ⚡ **Runs fully in WebGPU** (no WASM or native bindings)  
- 🖼️ Works with browser images (`<img>`, `ImageBitmap`, `OffscreenCanvas`)  
- 📦 Lightweight, focused: only SIFT + SURF, not a full CV framework  

---

## 🚀 Getting Started

### Clone the repository
```bash
git clone https://github.com/algorithmic-games/sift-surf-webgpu.git
cd sift-surf-webgpu
````

### Install dependencies

```bash
npm install
```

### Run demo

```bash
npm run dev
```

This will launch a Vite dev server and open a demo page showing SIFT/SURF keypoints overlaid on sample images.

---

## 📖 Usage

```js
import { SIFT, SURF } from "sift-surf-webgpu";

// Request WebGPU device
const adapter = await navigator.gpu.requestAdapter();
const device = await adapter.requestDevice();

// Initialize SIFT
const sift = new SIFT({ device });

// Detect + Compute
const { keypoints, descriptors } = await sift.detectAndCompute(img);

// Keypoints example
console.log(keypoints[0]);
// {
//   pt: [123.4, 87.6],
//   size: 4.5,
//   angle: 90.0,
//   response: 0.012,
//   octave: 2
// }

// Descriptors: Float32Array per keypoint
console.log(descriptors.length); // e.g. 128 per keypoint
```

---

## 📂 Project Structure

```
/src
  /api
    SIFT.js
    SURF.js
  /gpu
    context.js        # WebGPU setup
    bufferManager.js
    shaderManager.js
  /shaders
    grayscale.wgsl
    gaussian_blur.wgsl
    downsample.wgsl
    dog.wgsl
    extrema_detection.wgsl
    refine_keypoints.wgsl
    orientation_sift.wgsl
    descriptor_sift.wgsl
    integral_image.wgsl
    hessian_response.wgsl
    descriptor_surf.wgsl
  /utils
    imageLoader.js
    mathUtils.js

/tests
  test_sift.js
  test_surf.js

/docs
  ARCHITECTURE.md
```

---

## 📜 License

MIT © 2025 Algorithmic Games
Patents covering SIFT and SURF have expired, making open implementation permissible.

---

## 🤝 Contributing

Contributions are welcome!

* Open issues for bugs or feature requests.
* Submit PRs with improvements, optimizations, or fixes.

---

## 🧭 Roadmap

* [x] Project skeleton + API
* [ ] Gaussian pyramid (SIFT) / Integral image (SURF)
* [ ] DoG / Hessian response shaders
* [ ] Keypoint refinement
* [ ] Orientation assignment
* [ ] Descriptor extraction
* [ ] Matching API (`matchDescriptors`)
* [ ] Demo + Visualization tools

