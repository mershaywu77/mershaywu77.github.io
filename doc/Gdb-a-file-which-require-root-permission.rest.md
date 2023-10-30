As a workaround, you can decorate existing gdb binary with a bash script and then use it.
Steps are,
	• cd /usr/bin
	• sudo mv gdb gdborig
Now you need to create a bash script named gdb with following content.
	• sudo vim gdb
Content of the bash is;
#!/bin/sh
sudo gdborig $@
Finally, make the script runnable.
sudo chmod 0755 gdb
Then you should be OK.