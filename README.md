# Taskflow Raytracer

A simple, multithreaded adaptation of Peter Shirley's [*Ray Tracing in One Weekend*](https://raytracing.github.io/) using the [Taskflow](https://taskflow.github.io/) concurrency library.

I modified `color.h` and `camera.h` to use Taskflow's `for_each_index` algorithm.

## Dependencies
* C++20 compatible compiler
* CMake
* Taskflow
* (Optional) Nix package manager, if you want to use the `flake.nix`

## Building and Running

To build the multithreaded version:
```bash
cmake -B build -DUSE_TASKFLOW=ON
cmake --build build
./build/raytracer > image.ppm
```

For the sequential version:
```bash
cmake -B build -DUSE_TASKFLOW=OFF
cmake --build build
./build/raytracer > image.ppm
```
