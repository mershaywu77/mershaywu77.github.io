Influence of unrelated interrupt handling 
• It’s effective to fix real-time tasks to cores which doesn’t handle unrelated IRQs 
• after setting IRQ affinity

Lock debugging features add much more latency 
• Disabling them is effective

Interrupt response time 
• Time period between expiry of a hardware timer and scheduling of a userspace task 
• measured by cyclictest (in rt-tests) 
• cyclictest -a 0 -p 99 -m -n -l 100000 -q -- histogram=500 
• -a: set CPU affinity to CPU0 
• -p 99: set priority to 99 • -m: use mlockall 
• -n: use clock_nanosleep to measure time 
• -l 100000: number of trials 
• -q: don’t print anything while testing 
• --histogram=50: print histogram 0-49us after the test