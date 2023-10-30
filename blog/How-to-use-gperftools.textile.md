There are several alternatives to actually turn on CPU profiling for a given run of an executable:
	1. Define the environment variable CPUPROFILE to the filename to dump the profile to. For instance, if you had a version of /bin/ls that had been linked against libprofiler, you could run:
% env CPUPROFILE=ls.prof /bin/ls
	 Not working for me
	2. In addition to defining the environment variable CPUPROFILE you can also define CPUPROFILESIGNAL. This allows profiling to be controlled via the signal number that you specify. The signal number must be unused by the program under normal operation. Internally it acts as a switch, triggered by the signal, which is off by default. For instance, if you had a copy of /bin/chrome that had been been linked against libprofiler, you could run:
% env CPUPROFILE=chrome.prof CPUPROFILESIGNAL=12 /bin/chrome &
You can then trigger profiling to start:
% killall -12 chrome
Then after a period of time you can tell it to stop which will generate the profile:
% killall -12 chrome
	Not Working for me
	3. In your code, bracket the code you want profiled in calls to ProfilerStart() and ProfilerStop(). (These functions are declared in <gperftools/profiler.h>.) ProfilerStart() will take the profile-filename as an argument.
	Segment Fault

From <https://gperftools.github.io/gperftools/cpuprofile.html> 


#install libunwind 1.01 ; I have problems with 0.99. It failed in its gperltool unit test
#Download from http://download.savannah.gnu.org/releases/libunwind/libunwind-1.0.1.tar.gz
#I
#Extract the files, then
CFLAGS=-U_FORTIFY_SOURCE ./configure
make
make install

#install gperftoos in ubuntu 16.04

sudo apt-get update
Sudo apt-get install git autoconf automake libtool

git clone https://github.com/gperftools/gperftools.git
 ./autogen.sh
 ./configure --prefix /usr
 make
 make check
 sudo make install

From <https://github.com/linux-on-ibm-z/docs/wiki/Building-gperftools> 

#use gperf cpu profiler
https://gperftools.github.io/gperftools/cpuprofile.html

Try very small test application, 3 works for me.

Here are some further information about it:
https://stackoverflow.com/questions/10874308/how-to-use-google-perf-tools

My host VM CONFIG_HZ = 250
