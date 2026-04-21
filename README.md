# Taskflow Raytracer

A simple, multithreaded adaptation of Peter Shirley's [*Ray Tracing in One Weekend*](https://raytracing.github.io/) using the [Taskflow](https://taskflow.github.io/) concurrency library.

I modified `color.h` and `camera.h` to use Taskflow's `for_each_index` algorithm.

## Performance

I benchmarked the performance difference on my Apple Silicon M2 Macbook, using C++ `std::chrono` timers.

### Results
| Implementation | Workers | Execution Time | Speedup |
| :--- | :--- | :--- |:--- |
| **Sequential** | 1 | ~19.6s | 1.00x |
| **Taskflow** | 8* | ~4.5s | **4.35x** |

*\*Taskflow defaults to the number of available threads.*

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
