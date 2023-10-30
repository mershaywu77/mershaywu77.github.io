
	1. For out-parameters
		a. Best case: no out-parameters, return a struct
		b. Use pointers to clear speak "we plan to change the parameter"
	2. Passing by const-ref vs. Passing by value
		○ If the type is bigger than 16 bytes, pass by const-ref.
		○ If the type has a non-trivial copy-constructor or a non-trivial destructor, pass by const-ref to avoid executing these methods.
		○ All other types should usually be passed by value.
	3. Avoiding virtual functions, keep virtual functions minimum.
	4. Constness
		a. Const functions that take input pointer arguments almost always take const pointer arguments.
		b. Return Non-class values
		c. Return const class type
		d. Return pointers instead of const pointers
		e. Return value instead of const reference (except only when speed is critical)
		f. Const vs the state of an object: do not have overloaded const/non-const versions of a function
	5. Beware of bool parameters, which often lead to unreadable code
	
	

4.1 Choose self-explanatory names and signatures
4.2 Choose unambiguous names for related things
4.3 Beware of false consistency
4.4 Avoid abbreviations
4.5 Prefer specific names to general names
4.6 Don’t be a slave of an underlying API’s naming practices (for legacy code or third part library)
4.7 Choose good defaults
4.8 Avoid making your APIs overly clever
4.9 Pay attention to edge cases
4.10 Be careful when defining virtual APIs
	In C++, this means making all virtual methods protected.
4.11 Strive for property-based APIs
	
Pimpl Idiom

The pimpl idiom (pointer to implementation) provides a great solution to this situation by using an opaque pointer to a class that’s defined in your .cpp file. This is also referred to as a d-pointer in some libraries, such as Qt and KDE.
.h file	.cpp file
	// implementation class
// public class	class AudioPlayer::Impl
class AudioPlayer	{
{	public:
public:	bool PlayLocal();
AudioPlayer();	bool PlayHttpStream();
~AudioPlayer();	
	std::string mUrl;
bool Play(const std::string &uri);	bool mIsPlaying;
bool IsPlaying() const;	};
	
private:	AudioPlayer::AudioPlayer() :
// Make noncopyable because of pointer	mImpl(new Impl)
AudioPlayer(const AudioPlayer &);	{
const AudioPlayer &operator =(const AudioPlayer &);	}
	
// Opaque pointer to implementation	AudioPlayer::~AudioPlayer()
class Impl;	{
Impl *mImpl;	delete mImpl;
};	}



