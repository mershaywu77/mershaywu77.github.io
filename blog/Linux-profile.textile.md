http://gernotklingler.com/blog/gprof-valgrind-gperftools-evaluation-tools-application-level-cpu-profiling-linux/
http://www.pixelbeat.org/programming/profiling/



Specialised profiling
system entry points
	• strace -c $cmd
	• ltrace -c $cmd
heap memory
	• google perftools (does CPU profiling too)
	• go perftools
	• valgrind massif
	• glib mem tracing with systemtap
I/O
	• I/O profiling with systemtap
	• process I/O profiling with ioprofile (uses strace & lsof)
	• process I/O profiling with iogrind
GCC
	• gprof sampling
	• -finstrument-functions and_cyg_profile_func_enter
	• instrument functions and display with graphvis
misc
	• systemd, startup profiling
	• bootchart, startup profiling
	• latencytop
	• Online Web page profiler
	• Google Wide Profiling
	• gotchas with gprof and kcachegrind
	• viewing profiling data with flame graphs

From <http://www.pixelbeat.org/programming/profiling/> 