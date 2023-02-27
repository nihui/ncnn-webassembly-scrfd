# ncnn-webassembly-scrfd

open https://nihui.github.io/ncnn-webassembly-scrfd and enjoy


# build and deploy

1. Install emscripten
```shell
git clone https://github.com/emscripten-core/emsdk.git
cd emsdk
./emsdk install 3.1.28
./emsdk activate 3.1.28

source emsdk/emsdk_env.sh
```

2. Download and extract ncnn webassembly package
```shell
wget https://github.com/Tencent/ncnn/releases/download/20230223/ncnn-20230223-webassembly.zip
unzip ncnn-20230223-webassembly.zip
```

3. Build four WASM feature variants
```shell
mkdir build
cd build
cmake -DCMAKE_TOOLCHAIN_FILE=$EMSDK/upstream/emscripten/cmake/Modules/Platform/Emscripten.cmake -DWASM_FEATURE=basic ..
make -j4
cmake -DCMAKE_TOOLCHAIN_FILE=$EMSDK/upstream/emscripten/cmake/Modules/Platform/Emscripten.cmake -DWASM_FEATURE=simd ..
make -j4
cmake -DCMAKE_TOOLCHAIN_FILE=$EMSDK/upstream/emscripten/cmake/Modules/Platform/Emscripten.cmake -DWASM_FEATURE=threads ..
make -j4
cmake -DCMAKE_TOOLCHAIN_FILE=$EMSDK/upstream/emscripten/cmake/Modules/Platform/Emscripten.cmake -DWASM_FEATURE=simd-threads ..
make -j4
```

4. Deploy the *.data *.js *.wasm and *.html files to your web server
