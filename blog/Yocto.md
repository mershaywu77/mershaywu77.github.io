# This page include useful notes/tips of yocto  

[Config Yocto for Debug](https://developer.ridgerun.com/wiki/index.php?title=Preparing_Yocto_Development_Environment_for_Debugging#Valgrind)  
but valgrind is not supported on all platforms. especially in embedded processors. See comments from packagegroup-core-tools-profile.bb

```
# valgrind does not work on the following configurations/architectures

VALGRIND = "valgrind"
VALGRIND:libc-musl = ""
VALGRIND:mipsarch = ""
VALGRIND:nios2 = ""
VALGRIND:arc = ""
VALGRIND:armv4 = ""
VALGRIND:armv5 = ""
VALGRIND:armv6 = ""
VALGRIND:armeb = ""
VALGRIND:aarch64 = ""
VALGRIND:riscv64 = ""
VALGRIND:riscv32 = ""
VALGRIND:powerpc = "${@bb.utils.contains('TARGET_FPU', 'soft', '', 'valgrind', d)}"
VALGRIND:linux-gnux32 = ""
VALGRIND:linux-gnun32 = ""
```
