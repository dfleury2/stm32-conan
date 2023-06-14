# stm32-conan
Using Conan/CMake for STM32 baremetal

# How to fix the conan install ???

When conan (1.59) tries to compile bzip2 for the provided profile, using CC and CXX compiler.
(arm STM32 compiler), CMake can not generate an executable.

The CMake way could be to used CMAKE_C(XX)_COMPILER_WORKS, but I do know how to pass this info
to conan for building the dependencies.

ARM compiler can be found here :
https://developer.arm.com/downloads/-/arm-gnu-toolchain-downloads
(https://developer.arm.com/-/media/Files/downloads/gnu/12.2.mpacbti-rel1/binrel/arm-gnu-toolchain-12.2.mpacbti-rel1-x86_64-arm-none-eabi.tar.xz?rev=71e595a1f2b6457bab9242bc4a40db90&hash=41B9EE53CF6E77F7F0647767EC481951)

And under Linux, installed in /opt/.... folder.


In a shell :
```shell
export CC=/opt/arm-gnu-toolchain-12.2.mpacbti-rel1-x86_64-arm-none-eabi/bin/arm-none-eabi-gcc
export CXX=/opt/arm-gnu-toolchain-12.2.mpacbti-rel1-x86_64-arm-none-eabi/bin/arm-none-eabi-g++
mkdir build 
cd build
conan install .. -pr:b ../arm.profile -pr:h ../arm.profile -b missing
```

```
-- Using Conan toolchain: /home/dfl/.conan/data/bzip2/1.0.8/_/_/build/dea81dd9e18130ba26360cb803738b075abc9ba9/build/Debug/generators/conan_toolchain.cmake
-- Conan toolchain: Setting CMAKE_POSITION_INDEPENDENT_CODE=ON (options.fPIC)
-- Conan toolchain: Setting BUILD_SHARED_LIBS = OFF
-- The C compiler identification is GNU 12.2.1
-- Detecting C compiler ABI info
-- Detecting C compiler ABI info - failed
-- Check for working C compiler: /opt/arm-gnu-toolchain-12.2.mpacbti-rel1-x86_64-arm-none-eabi/bin/arm-none-eabi-gcc
-- Check for working C compiler: /opt/arm-gnu-toolchain-12.2.mpacbti-rel1-x86_64-arm-none-eabi/bin/arm-none-eabi-gcc - broken
CMake Error at /home/dfl/Tools/cmake-3.26.3-linux-x86_64/share/cmake-3.26/Modules/CMakeTestCCompiler.cmake:67 (message):
  The C compiler

    "/opt/arm-gnu-toolchain-12.2.mpacbti-rel1-x86_64-arm-none-eabi/bin/arm-none-eabi-gcc"

  is not able to compile a simple test program.

  It fails with the following output:

    Change Dir: /home/dfl/.conan/data/bzip2/1.0.8/_/_/build/dea81dd9e18130ba26360cb803738b075abc9ba9/build/Debug/CMakeFiles/CMakeScratch/TryCompile-GhXnLD
    
    Run Build Command(s):/home/dfl/Tools/cmake-3.26.3-linux-x86_64/bin/cmake -E env VERBOSE=1 /usr/bin/gmake -f Makefile cmTC_91e4c/fast && /usr/bin/gmake  -f CMakeFiles/cmTC_91e4c.dir/build.make CMakeFiles/cmTC_91e4c.dir/build
    gmake[1]: Entering directory '/home/dfl/.conan/data/bzip2/1.0.8/_/_/build/dea81dd9e18130ba26360cb803738b075abc9ba9/build/Debug/CMakeFiles/CMakeScratch/TryCompile-GhXnLD'
    Building C object CMakeFiles/cmTC_91e4c.dir/testCCompiler.c.o
    /opt/arm-gnu-toolchain-12.2.mpacbti-rel1-x86_64-arm-none-eabi/bin/arm-none-eabi-gcc   -fPIE -o CMakeFiles/cmTC_91e4c.dir/testCCompiler.c.o -c /home/dfl/.conan/data/bzip2/1.0.8/_/_/build/dea81dd9e18130ba26360cb803738b075abc9ba9/build/Debug/CMakeFiles/CMakeScratch/TryCompile-GhXnLD/testCCompiler.c
    Linking C executable cmTC_91e4c
    /home/dfl/Tools/cmake-3.26.3-linux-x86_64/bin/cmake -E cmake_link_script CMakeFiles/cmTC_91e4c.dir/link.txt --verbose=1
    /opt/arm-gnu-toolchain-12.2.mpacbti-rel1-x86_64-arm-none-eabi/bin/arm-none-eabi-gcc CMakeFiles/cmTC_91e4c.dir/testCCompiler.c.o -o cmTC_91e4c 
    /opt/arm-gnu-toolchain-12.2.mpacbti-rel1-x86_64-arm-none-eabi/bin/../lib/gcc/arm-none-eabi/12.2.1/../../../../arm-none-eabi/bin/ld: /opt/arm-gnu-toolchain-12.2.mpacbti-rel1-x86_64-arm-none-eabi/bin/../lib/gcc/arm-none-eabi/12.2.1/../../../../arm-none-eabi/lib/libc.a(libc_a-exit.o): in function `exit':
    exit.c:(.text.exit+0x28): undefined reference to `_exit'
    /opt/arm-gnu-toolchain-12.2.mpacbti-rel1-x86_64-arm-none-eabi/bin/../lib/gcc/arm-none-eabi/12.2.1/../../../../arm-none-eabi/bin/ld: /opt/arm-gnu-toolchain-12.2.mpacbti-rel1-x86_64-arm-none-eabi/bin/../lib/gcc/arm-none-eabi/12.2.1/../../../../arm-none-eabi/lib/libc.a(libc_a-writer.o): in function `_write_r':
    writer.c:(.text._write_r+0x24): undefined reference to `_write'
    /opt/arm-gnu-toolchain-12.2.mpacbti-rel1-x86_64-arm-none-eabi/bin/../lib/gcc/arm-none-eabi/12.2.1/../../../../arm-none-eabi/bin/ld: /opt/arm-gnu-toolchain-12.2.mpacbti-rel1-x86_64-arm-none-eabi/bin/../lib/gcc/arm-none-eabi/12.2.1/../../../../arm-none-eabi/lib/libc.a(libc_a-closer.o): in function `_close_r':
    closer.c:(.text._close_r+0x18): undefined reference to `_close'
    /opt/arm-gnu-toolchain-12.2.mpacbti-rel1-x86_64-arm-none-eabi/bin/../lib/gcc/arm-none-eabi/12.2.1/../../../../arm-none-eabi/bin/ld: /opt/arm-gnu-toolchain-12.2.mpacbti-rel1-x86_64-arm-none-eabi/bin/../lib/gcc/arm-none-eabi/12.2.1/../../../../arm-none-eabi/lib/libc.a(libc_a-lseekr.o): in function `_lseek_r':
    lseekr.c:(.text._lseek_r+0x24): undefined reference to `_lseek'
    /opt/arm-gnu-toolchain-12.2.mpacbti-rel1-x86_64-arm-none-eabi/bin/../lib/gcc/arm-none-eabi/12.2.1/../../../../arm-none-eabi/bin/ld: /opt/arm-gnu-toolchain-12.2.mpacbti-rel1-x86_64-arm-none-eabi/bin/../lib/gcc/arm-none-eabi/12.2.1/../../../../arm-none-eabi/lib/libc.a(libc_a-readr.o): in function `_read_r':
    readr.c:(.text._read_r+0x24): undefined reference to `_read'
    /opt/arm-gnu-toolchain-12.2.mpacbti-rel1-x86_64-arm-none-eabi/bin/../lib/gcc/arm-none-eabi/12.2.1/../../../../arm-none-eabi/bin/ld: /opt/arm-gnu-toolchain-12.2.mpacbti-rel1-x86_64-arm-none-eabi/bin/../lib/gcc/arm-none-eabi/12.2.1/../../../../arm-none-eabi/lib/libc.a(libc_a-sbrkr.o): in function `_sbrk_r':
    sbrkr.c:(.text._sbrk_r+0x18): undefined reference to `_sbrk'
    collect2: error: ld returned 1 exit status
    gmake[1]: *** [CMakeFiles/cmTC_91e4c.dir/build.make:99: cmTC_91e4c] Error 1
    gmake[1]: Leaving directory '/home/dfl/.conan/data/bzip2/1.0.8/_/_/build/dea81dd9e18130ba26360cb803738b075abc9ba9/build/Debug/CMakeFiles/CMakeScratch/TryCompile-GhXnLD'
    gmake: *** [Makefile:127: cmTC_91e4c/fast] Error 2
```
