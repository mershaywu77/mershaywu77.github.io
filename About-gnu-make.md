Manual: https://www.gnu.org/software/make/manual

Best Practice for Make http://make.mad-scientist.net/papers/rules-of-makefiles/#rule1

Gnu Make Auto Dependency http://make.mad-scientist.net/papers/advanced-auto-dependency-generation/

Different from clearmake, which do the automatic dependency (.c depend on .h they include) for us. See https://www.ibm.com/support/knowledgecenter/en/SSSH27_7.1.2/com.ibm.rational.clearcase.cc_ref.doc/topics/clearmake.htm

clearmake features a number of ClearCase extensions:

Configuration lookup. A build-avoidance scheme that is more sophisticated than the standard scheme, which uses time stamps of built objects. Configuration lookup also includes automatic dependency detection. For example, this guarantees correct build behavior as C-language header files change, even if the header files are not listed as dependencies in the makefile.   
Derived object sharing. Developers working in different views can share the files created by clearmake builds.   
Creation of configuration records. Software bill-of-materials records that fully document a build and support the ability to rebuild.   

![image](https://user-images.githubusercontent.com/17861461/158143792-02fd2937-0b9e-4cae-a5c1-911f45accfc9.png)
