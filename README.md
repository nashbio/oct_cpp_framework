# oct_cpp_framework (Patched Fork)

> **This is a patched fork of [neurodial/oct_cpp_framework](https://github.com/neurodial/oct_cpp_framework).**
> Original author: Kay Gawlik / neurodial.

A C++ framework providing OpenCV Mat serialization, matrix compression, and ZIP archive handling. Used as a dependency by [LibOctData](https://github.com/neurodial/LibOctData) for reading OCT file formats.

## Modifications in This Fork

1. **OpenCV 4 header migration**: `opencv/cv.h` -> `opencv2/opencv.hpp`, `opencv2/cv.hpp` -> `opencv2/opencv.hpp`
2. **CMake subdirectory compatibility**:
   - `CMAKE_SOURCE_DIR` -> `CMAKE_CURRENT_SOURCE_DIR` so the library builds correctly as a subdirectory of a parent project
   - Generates an empty `oct_cpp_framework_export.h` for static builds (the upstream `install()` block references this file but no `GENERATE_EXPORT_HEADER` call creates it)

These changes allow the library to build with OpenCV 4.x and to be included via `add_subdirectory()` in a parent CMake project.

## Components

- **cvmat/** — OpenCV `cv::Mat` tree serialization to/from binary
- **matcompress/** — Matrix compression utilities
- **zip/** — C++ wrapper around minizip for ZIP archive creation/extraction
- **minizip/** — Bundled minizip library (zip/unzip C implementation)

## Dependencies

- **Boost** (filesystem, system)
- **OpenCV**
- **ZLIB** (optional, default ON)

## Build

Standalone:

```bash
mkdir build && cd build
cmake .. -DCMAKE_BUILD_TYPE=Release
make -j$(nproc)
```

Or as a subdirectory in a parent CMake project:

```cmake
add_subdirectory(extern/oct_cpp_framework)
# Target OctCppFramework::oct_cpp_framework is now available
```

## License

This project is licensed under the LGPL-3.0 License — see [licence.txt](licence.txt) for details.
