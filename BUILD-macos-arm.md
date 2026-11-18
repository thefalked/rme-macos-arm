# Build Remere's Map Editor on macOS Apple Silicon (arm64)

This tree patches RME for modern Homebrew on Apple Silicon:

- `ASIO_STANDALONE` with Asio `io_context` (`io_service` alias)
- Updated Asio resolver / connect APIs
- `fmt/format.h` include
- Drop obsolete `AGL/agl.h` include on macOS
- Extra `data/clients.xml` hash for OTClientV8 8.60 assets

Upstream project: [hjnilsson/rme](https://github.com/hjnilsson/rme).

## License note

Upstream ships `LICENSE.rtf`, a freeware EULA that describes distribution of
**unmodified** copies. This repository is a **modified** source tree for macOS
ARM builds. Keep the license file with any redistribution. Prefer contributing
compatible fixes upstream when possible.

## Homebrew dependencies

```bash
brew install cmake ninja wxwidgets asio fmt nlohmann-json zlib freeimage boost pkg-config
```

Exact package names can vary by Homebrew revision. If CMake cannot find a
library, pass `-DCMAKE_PREFIX_PATH="$(brew --prefix)"`.

## Build

```bash
mkdir -p build && cd build
cmake .. -DCMAKE_BUILD_TYPE=Release -DCMAKE_PREFIX_PATH="$(brew --prefix)"
cmake --build . -j"$(sysctl -n hw.ncpu)"
```

Output binary: `build/rme` (Mach-O arm64).

## Run

Point RME at your own client data directory (`.dat` / `.spr`). Those assets are
not shipped here.
