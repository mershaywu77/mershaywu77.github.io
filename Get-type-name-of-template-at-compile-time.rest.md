__PRETTY_FUNCTION__ should solve your problem (at run time at least)
The output to the program below is:
asfdasdfasdf test<type>::test() [with type = int]
asfdasdfasdf test<type>::test() [with type = int]
asfdasdfasdf test<type>::test() [with type = int]
asfdasdfasdf test<type>::test() [with type = int]
asfdasdfasdf test<type>::test() [with type = int]
asfdasdfasdf test<type>::test() [with type = int]
asfdasdfasdf void tempFunction() [with type = bool]
asfdasdfasdf void tempFunction() [with type = bool]
asfdasdfasdf void tempFunction() [with type = bool]
asfdasdfasdf void tempFunction() [with type = bool]
asfdasdfasdf void tempFunction() [with type = bool]
asfdasdfasdf void tempFunction() [with type = bool]
!!!Hello World!!!
If you really, really, need the typename as a string, you could hack this (using snprintf instead of printf) and pull the substring after '=' and before ']'.
#include <iostream>
using namespace std;
template<typename type>
class test
{
public:
test()
{
    printf("asfdasdfasdf %s\n", __PRETTY_FUNCTION__);
    printf("asfdasdfasdf %s\n", __PRETTY_FUNCTION__);
    printf("asfdasdfasdf %s\n", __PRETTY_FUNCTION__);
    printf("asfdasdfasdf %s\n", __PRETTY_FUNCTION__);
    printf("asfdasdfasdf %s\n", __PRETTY_FUNCTION__);
    printf("asfdasdfasdf %s\n", __PRETTY_FUNCTION__);
}
};
template<typename type>
void tempFunction()
{
    printf("asfdasdfasdf %s\n", __PRETTY_FUNCTION__);
    printf("asfdasdfasdf %s\n", __PRETTY_FUNCTION__);
    printf("asfdasdfasdf %s\n", __PRETTY_FUNCTION__);
    printf("asfdasdfasdf %s\n", __PRETTY_FUNCTION__);
    printf("asfdasdfasdf %s\n", __PRETTY_FUNCTION__);
    printf("asfdasdfasdf %s\n", __PRETTY_FUNCTION__);
}
int main() {
    test<int> test;
tempFunction<bool>();
    cout << "!!!Hello World!!!" << endl; // prints !!!Hello World!!!
    return 0;
}
