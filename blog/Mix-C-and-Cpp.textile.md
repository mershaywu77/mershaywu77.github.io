How can I call a non-system C function f(int,char,float) from my C++ code?  
If you have an individual C function that you want to call, and for some reason you don’t have or don’t want to #include a C header file in which that function is declared, you can declare the individual C function in your C++ code using the extern "C" syntax. Naturally you need to use the full function prototype:

	1. extern "C" void f(int i, char c, float x);
A block of several C functions can be grouped via braces:

	1. extern "C" {
	2. void   f(int i, char c, float x);
	3. int    g(char* s, const char* s2);
	4. double sqrtOfSumOfSquares(double a, double b);
	5. }
After this you simply call the function just as if it were a C++ function:

	1. int main()
	2. {
	3. f(7, 'x', 3.14);   // Note: nothing unusual in the call
	4. // ...
	5. }
