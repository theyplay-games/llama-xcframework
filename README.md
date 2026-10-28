# llama.xcframework with iOS Simulator support

The official [llama.cpp](https://github.com/ggml-org/llama.cpp) releases ship an xcframework for iOS devices and macOS
only, so any app that links it can't run in the iOS Simulator. This is the same release, **b11887**, built with
llama.cpp's own `build-xcframework.sh` for three platforms:

| Slice | |
|---|---|
| `ios-arm64` | iPhone and iPad |
| `ios-arm64_x86_64-simulator` | iOS Simulator (Apple silicon and Intel Macs) |
| `macos-arm64_x86_64` | Mac |

Nothing in the source was changed. Built with:

```sh
git clone --depth 1 --branch b11887 https://github.com/ggml-org/llama.cpp
cd llama.cpp && ./build-xcframework.sh ios-sim ios-device macos
```

## Swift Package Manager

```swift
.binaryTarget(
    name: "llama",
    url: "https://github.com/theyplay-games/llama-xcframework/releases/download/b11887/llama-b11887-ondevice.xcframework.zip",
    checksum: "aef22cd0310a0e5204d89c0f3f02b1d6a20ac44dc543ccd93bb205b5cd3d6207"
)
```

Then `import llama` in your target.

**Simulator tip:** the Simulator's Metal lacks most of llama.cpp's GPU kernels and ends up slower than the CPU.
Load models there with `n_gpu_layers = 0`. On real devices, keep `99`.

## License

llama.cpp is MIT licensed (see `LICENSE`, copyright the ggml authors). This repository only redistributes the build.

Used by [OnDevice Kit](https://theyplay.games/ondevice) and [swift-gbnf](https://github.com/theyplaygames/swift-gbnf).
Made by [theyplay.games](https://theyplay.games).
