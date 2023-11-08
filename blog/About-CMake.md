# Best practices for using CMake in OpenEmbedded/Yocto
http://bec-systems.com/site/1128/best-practices-for-using-cmake-in-openembeddedyocto   
https://www.slideshare.net/DanielPfeifer1/cmake-48475415   
http://fujii.github.io/2015/10/10/cmake-best-practice/   
https://archive.fosdem.org/2013/schedule/event/moderncmake/attachments/slides/258/export/events/attachments/moderncmake/slides/258/cmake_fosdem_2013.pdf   
https://crascit.com/2016/01/31/enhanced-source-file-handling-with-target_sources/   
https://softwareengineering.stackexchange.com/questions/289348/directory-organization-of-a-cmake-c-repository-containing-several-projects   

# SHARED vs MODULE
The difference is that you can link to a SHARED library with the linker, but you cannot link to a MODULE with the linker. On some platforms.    
So... to be fully cross-platform and work everywhere CMake works, you should never do this:    
## This is a big NO-NO:
```
add_library(mylib MODULE ${srcs})
target_link_libraries(myexe mylib)
```
To be fair, on Windows, they're both just dlls, and so this code might actually work. But when you take it to a platform where it's impossible to link to the MODULE, you'll encounter an error.        
Bottom line: if you need to link to the library, use SHARED. If you are guaranteed that the library will only be loaded dynamically, then it's safe to use a MODULE. (And perhaps even preferable to help detect if somebody does try to link to it...)

# Find pthread
`# link common libraries`    
`set(THREADS_PREFER_PTHREAD_FLAG ON)`    
`find_package(Threads REQUIRED)`    
`target_link_libraries(${EXECUTABLE_NAME} Threads::Threads)`    

# Use doxygen
````
MACRO(GENERATE_DOCUMENTATION DOXYGEN_CONFIG_FILE)
    FIND_PACKAGE(Doxygen)
    SET(DOXYFILE_FOUND false)
    IF(EXISTS ${PROJECT_SOURCE_DIR}/${DOXYGEN_CONFIG_FILE})
        SET(DOXYFILE_FOUND true)
    ENDIF(EXISTS ${PROJECT_SOURCE_DIR}/${DOXYGEN_CONFIG_FILE})

    IF( DOXYGEN_FOUND )
        IF( DOXYFILE_FOUND )
        # Add target
            ADD_CUSTOM_TARGET( doc ALL ${DOXYGEN_EXECUTABLE}  
    "${PROJECT_SOURCE_DIR}/${DOXYGEN_CONFIG_FILE}" )

        # Add .tag file and generated documentation to the list of files we  must erase when distcleaning

        # Read doxygen configuration file
        FILE( READ ${PROJECT_SOURCE_DIR}/${DOXYGEN_CONFIG_FILE} DOXYFILE_CONTENTS )
        STRING( REGEX REPLACE "\n" ";" DOXYFILE_LINES ${DOXYFILE_CONTENTS} )

        # Parse .tag filename and add to list of files to delete if it exists
        FOREACH( DOXYLINE ${DOXYFILE_CONTENTS} )
            STRING( REGEX REPLACE ".*GENERATE_TAGFILE *= *([^ ^\n]+).*"  
    "\\1" DOXYGEN_TAG_FILE ${DOXYLINE} )
        ENDFOREACH( DOXYLINE )
        ADD_TO_DISTCLEAN( ${PROJECT_BINARY_DIR}/${DOXYGEN_TAG_FILE} )

        # Parse doxygen output doc dir and add to list of files to delete if  
    it exists
        FOREACH( DOXYLINE ${DOXYFILE_CONTENTS} )
            STRING( REGEX REPLACE ".*OUTPUT_DIRECTORY *= *([^ ^\n]+).*" "\\1"  
    DOXYGEN_DOC_DIR ${DOXYLINE} )
        ENDFOREACH( DOXYLINE )
        ADD_TO_DISTCLEAN( ${PROJECT_BINARY_DIR}/${DOXYGEN_DOC_DIR} )
        ADD_TO_DISTCLEAN( ${PROJECT_BINARY_DIR}/${DOXYGEN_DOC_DIR}.dir )

        ELSE( DOXYFILE_FOUND )
        MESSAGE( STATUS "Doxygen configuration file not found - Documentation  
    will not be generated" )
        ENDIF( DOXYFILE_FOUND )
    ELSE(DOXYGEN_FOUND)
        MESSAGE(STATUS "Doxygen not found - Documentation will not be generated")
    ENDIF(DOXYGEN_FOUND)
ENDMACRO(GENERATE_DOCUMENTATION)
````

# Enable gprof
Compile your program to enable prof    
`cmake -DCMAKE_CXX_FLAGS=-pg -DCMAKE_EXE_LINKER_FLAGS=-pg -DCMAKE_SHARED_LINKER_FLAGS=-pg <SOURCE_DIR>`    
Make sure you program will return or exit (not abort)   
Run the application normal   
`gprof options executable-file gmon.out bb-data [yet-more-profile-data-files…] [> outfile]  `      

# Passing compiler options to cmake in command line
`cmake -D CMAKE_CXX_FLAGS="" your_path_of_cmake_file`    

e.g. preprocess only
`cmake -D CMAKE_CXX_FLAGS="-E" your_path_of_cmake_file`    
