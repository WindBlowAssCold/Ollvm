# ollvm for windows
ollvm based on llvm_15.0.1, Hikari-ollvm, Armariris.

https://llvm.org  
https://github.com/61bcdefg/Hikari-LLVM15  
https://github.com/GoSSIP-SJTU/Armariris  

# Build

**Compile**

1. ninja build

```bash
cmake -S llvm -B build -G Ninja -DLLVM_ENABLE_PROJECTS="clang" -DCMAKE_BUILD_TYPE=Release -DLLVM_INCLUDE_TESTS=OFF 

#  vscmd-x86 for llvm-x86
#  vscmd-x64 for llvm-x64

#  llvm < 15 , use following flags: 
# -DLLVM_ENABLE_NEW_PASS_MANAGER=OFF
# -DLLVM_TARGETS_TO_BUILD=X86
# -DBUILD_SHARED_LIBS=On

cmake --build build -j16
```

2. vs build

```bash
mkdir build
cd build
cmake -DLLVM_ENABLE_PROJECTS=clang -G "Visual Studio 15 2017" -A x64 -Thost=x64 ..\llvm -DLLVM_TARGETS_TO_BUILD=X86
```


## Usage

```bash
The following flags are supported

# Enable Bogus Control Flow
-mllvm -enable-bcf (√)

# Enable Control Flow Flattening
-mllvm -enable-fla (√)

#Enable Basic Block Spliting
-mllvm -enable-split (√)

#Enable Instruction Substitution
-mllvm -enable-sub (√)

#Enable Register-Based Indirect Branching
-mllvm -enable-indibran (√)

#Enable String Encryption
-mllvm -enable-sobf (√)

#Enable Constant Encryption
-mllvm -enable-constenc (√)
```

## Advance

### BogusControlFlow

```bash

-bcf_onlyjunkasm
# only insert junk code in blocks.

-bcf_junkasm
# Default off.

-bcf_junkasm_minnum
# Default 2.

-bcf_junkasm_maxnum
# Default 4.

-bcf_createfunc
# Default off.

```

### ConstantEncryption

```bash
# https://iosre.com/t/llvm-llvm/11132

-enable-constenc
# Default off.

-constenc_times
# Default 1.

-constenc_prob
# Default 50.

-constenc_togv
# Default off.

-constenc_subxor
# xor the result of constant encryption. 
```

### StringEncryption

```bash

-strcry_prob
# Default 100%.

```

### IndirectBranch

```bash
-indibran-use-stack
# Default off.

-indibran-enc-jump-target
# Default off.

```
