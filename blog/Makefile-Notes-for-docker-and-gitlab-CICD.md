#  1. To use docker for full build and incremental build.


`build:`

`mkdir -p build && docker run --platform i386 -i --rm -v$(CURDIR):/source $(COMPILER_IMAGE) /bin/bash -c "cd /source/build && cmake -DCMAKE_TOOLCHAIN_FILE=/opt/toolchain.cmake -DCMAKE_BUILD_TYPE=Debug .. && make -j"`

	

`inc_build:`

	`mkdir -p build && docker run --platform i386 -i --rm -v$(CURDIR):/source $(COMPILER_IMAGE) /bin/bash -c "cd /source/build && make -j"`


# 2.To avoid permission issue for CICD pipeline by using the same userid:groupid to run the pipeline

`mkdir -p build && docker run --platform i386 -u $(shell id -u):$(shell id -g) -i --rm -v$(CURDIR):/source $(COMPILER_IMAGE) /bin/bash -c "cd /source/build && cmake -DCMAKE_TOOLCHAIN_FILE=/opt/toolchain.cmake -DCMAKE_BUILD_TYPE=Debug .. && make -j"`