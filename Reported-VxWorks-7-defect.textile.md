# V7COR-1142 : Lazy binding in shared libraries is currently disabled
Defect #:	V7COR-1142
Severity:	Standard
Status:	Acknowledged
Created Date:	05/15/2014
Component/s :	core_ldso
Description
Symbol references in VxWorks 7 shared libraries are currently immediately bound, ie upon load. Neither the LD_BIND_NOW environment variable nor any  compiler option that controls the generation of the DT_BIND_NOW dynamic tag have any effect.

Pasted from <https://knowledge.windriver.com/en-us/000_Products/000/020/000/020/020/000_V7COR-1142_%3A_Lazy_binding_in_shared_libraries_is_currently_disabled> 

# V7COR-3071 : Shared library search order does not match the documentation
Defect #:	V7COR-3071
Found In Version	1.0.3.1
Fix Version	1.0.4.2
Severity:	Standard
Status:	Fixed
Created Date:	06/16/2015
Component/s :	libc-usr
Description
The VxWorks Application Programmer's Guide, 7.0 indicates that shared libraries will be searched for at run time in the following order:
1. The VxWorks environment variable "LD_LIBRARY_PATH";
2. The configuration file "ld.so.conf";
3. The ELF RPATH record in the application's executable (created with the -rpath compiler option);
4. The same directory as the one in which the application file is located.
The actual order appears to be 4,1,2,3.
Steps to Reproduce
1. Create a simple "hello world" application that links several libraries;
2. Place the libraries in the same directory as the application and different folders;
3. Launch with the RTP command as described in the programmer's guide section "Setting LD_LIBRARY_PATH From the Shell"; You will see that the application loaded the libraries from the application directory rather than the directory specified in the LD_LIBRARY_PATH by using the "shl" command.

Pasted from <https://knowledge.windriver.com/en-us/000_Products/000/020/000/020/020/000_V7COR-3071_%3A_Shared_library_search_order_does_not_match_the_documentation> 

# V7COR-2678 : use of C++ in RTP shared libraries causes failures
Defect #:	V7COR-2678
Found In Version	1.0.9.1
Severity:	Standard
Status:	Acknowledged
Created Date:	03/11/2015
Component/s :	core_ldso
Description
Assertion failures or crashes can occur in dynamic RTPs when both the executable and a shared library are linked against a static standard C++ library such as libstlstd.  The failures include segmentation violations and memory corruption errors such as:
 
 memPartFree: invalid block 0x9d9dac in partition 0x9cef6c
 
The problems are at least partly caused by executing destructors twice for the same object -- once in the custom C++ shared library and once in the executable.
Workaround
The best solution to this problem is to create standard C++ shared libraries (libstlstd.so for Diab, libstdc++.so for GCC) and link both C++ executables and custom C++ shared libraries against these standard shared libraries.
 
Until such standard C++ shared libraries are available in a VxWorks release, you can create your own standard C++ shared libraries.  The following Makefile creates a Diab library named libstldotso.so that can be used in place of a libstlstd.so:
 
  LIB_BASE_NAME = stldotso
  OBJS = dummy.o
  # libc.so is in $(LIB_ROOT)/$(LIBDIRBASE), not $(LIB_ROOT)/$(LIBDIRBASE)/PIC.
  ADDED_SHARED_LD_FLAGS = -Wl,-A,$(LIB_ROOT)/$(LIBDIRBASE)/PIC/libstlstd.a \
    -L$(LIB_ROOT)/$(LIBDIRBASE) -lc
  LIB_FORMAT = shared
  LAYER_FORMAT = shared
 
  include $(WIND_USR_MK)/rules.library.mk
 
You can use the following contents for dummy.cpp:
 
  int __libstlstd_dummy = 0;
 
When linking custom C++ shared libraries, add the following to your Makefiles:
 
  ADDED_SHARED_LD_FLAGS = -L$(LIB_ROOT)/$(LIBDIRBASE) -lstldotso -lc
 
When linking dynamic RTP executables, add the following to your Makefiles:
 
  ADDED_LIBS += [... custom libraries ...] -lstldotso
 
Similarly, the following Makefile creates a GNU library named libstdcdotso.so that can be used in place of a libstdc++.so:
 
  LIB_BASE_NAME = stdcdotso
  OBJS = dummy.o
  # libc.so is in $(LIB_ROOT)/$(LIBDIRBASE), not $(LIB_ROOT)/$(LIBDIRBASE)/PIC.
  ADDED_SHARED_LD_FLAGS = -Wl,-Bstatic -Wl,-whole-archive -lstdc++ \
    -Wl,-no-whole-archive -Wl,-Bdynamic -L$(LIB_ROOT)/$(LIBDIRBASE) -lc
  LIB_FORMAT = shared
  LAYER_FORMAT = shared
 
  include $(WIND_USR_MK)/rules.library.mk
 
You can use the following contents for dummy.cpp:
 
  int __libstdcstd_dummy = 0;
 
When linking custom C++ shared libraries, add the following to your Makefiles:
 
  ADDED_SHARED_LD_FLAGS = -L$(LIB_ROOT)/$(LIBDIRBASE) -lstdcdotso -lc
 
When linking dynamic RTP executables, add the following to your Makefiles:
 
  ADDED_LIBS += [... custom libraries ...] -lstdcdotso
 
It is VERY important that the standard C++ library always comes AFTER any custom C++ shared libraries in the link.
 
WARNING:  Workbench-generated Makefiles for custom C++ shared libraries will contain code that links the custom libraries against the static standard C++ shared libraries (-lstlstd / libstlstd.a, -lstdc++ / libstdc++.a).  This is incorrect -- you must remove the -lstlstd / -lstdc++ flags manually, and replace them with -lstldotso / -lstdcdotso.
 
CAVEAT:  The workaround has not been extensively tested.  WR is still verifying that it solves the problem.
 
BIG CAVEAT:  This workaround is known to have problems with Diab versions that are older than 5.9.4.6.  No reliable workaround is currently available for older versions of Diab.
Steps to Reproduce
The attached zip files, c++-so-diab.rtp.zip and c++-so-gnu.rtp.zip, provide examples of using the workaround.  When you build the examples (with Diab and Gnu, respectively) and run the RTPs, the RTPs should print messages from the custom C++ shared libraries.
