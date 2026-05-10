# [libtorch](https://github.com/pytorch) v2.11 – Haswell-optimized build

This repository provides a precompiled **LibTorch v2.11** (C++ PyTorch distribution) built specifically for **Intel Haswell** microarchitecture (`-march=haswell -mtune=haswell`) with optimized math libraries (MKL, MKLDNN, OpenMP).  
CUDA, ROCm, and distributed training are disabled – this is a pure CPU build tailored for high‑performance inference and training on Haswell‑class CPUs.

## 🔧 Build configuration

| Option | Value |
|--------|-------|
| PyTorch version | 2.11 |
| CMake generator | Ninja |
| Build type | Release |
| Install prefix | `$HOME/libtorch-haswell` |
| CPU architecture | `haswell` (`-march=haswell -mtune=haswell`) |
| Optimization flags | `-O3 -ffast-math` |
| BLAS | Intel MKL |
| MKLDNN | ON (with CBLAS) |
| OpenMP | ON |
| LAPACK | ON |
| Shared libraries | ON |
| CUDA / ROCm / NCCL | OFF |
| Distributed / MPI | OFF |
| Tests | OFF |

Full CMake command:
```bash
cmake .. \
  -GNinja \
  -DCMAKE_BUILD_TYPE=Release \
  -DCMAKE_INSTALL_PREFIX=$HOME/libtorch-haswell \
  -DUSE_CUDA=OFF \
  -DUSE_CUDNN=OFF \
  -DUSE_ROCM=OFF \
  -DUSE_NCCL=OFF \
  -DUSE_FBGEMM=OFF \
  -DUSE_OPENMP=ON \
  -DUSE_MKLDNN=ON \
  -DUSE_MKLDNN_CBLAS=ON \
  -DUSE_BLAS=MKL \
  -DUSE_LAPACK=ON \
  -DUSE_DISTRIBUTED=OFF \
  -DUSE_MPI=OFF \
  -DBUILD_TEST=OFF \
  -DBUILD_CAFFE2=ON \
  -DBUILD_SHARED_LIBS=ON \
  -DCMAKE_C_FLAGS="-march=haswell -mtune=haswell -O3 -ffast-math" \
  -DCMAKE_CXX_FLAGS="-march=haswell -mtune=haswell -O3 -ffast-math" \
  -DCMAKE_EXE_LINKER_FLAGS="-Wl,-rpath,\$ORIGIN"
```

## License
This repository only redistributes LibTorch, which is subject to the [BSD‑3 license](https://github.com/pytorch/pytorch/blob/v2.11.0/LICENSE).
The precompiled binaries are provided as‑is, without any warranty.
