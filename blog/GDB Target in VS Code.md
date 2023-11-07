This page is done base on chatGPT + manual tweak to make it work.

Debugging an embedded application over GDB Server in Visual Studio Code (VS Code) involves setting up the necessary configurations and using the GDB extension for VS Code. Here's an example of how to debug an embedded application using VS Code and GDB Server:

# Prerequisites:

An embedded target device connected to your development machine.

By Yocto, you can include GDB server by update /poky/build/conf/local.conf ”EXTRA_IMAGE_FEATURES ?= "debug-tweaks tools-profile tools-debug"”

VS Code installed in host (mine is Ubuntu 22.04 WSL2)

In host  install the cross compiler for ARM. ( Follow [Sam9x60CuriosityMainPage < Linux4SAM < TWiki,](https://www.linux4sam.org/bin/view/Linux4SAM/Sam9x60CuriosityMainPage#Setup_ARM_Cross_Compiler) neither approach will give you an workable gdb); I am using 11.3 Rel1 in  Arm GNU Toolchain Downloads – Arm Developer because the dependency can be managed, and it is very close to our toolchain in docker (11.2)



## download the toolchain
`wget -c https://developer.arm.com/-/media/Files/downloads/gnu/11.3.rel1/binrel/arm-gnu-toolchain-11.3.rel1-x86_64-arm-none-linux-gnueabihf.tar.xz?rev=65520e9cdf324eca9c02f5302c904fa4`

## rename the downloaded file and extract it
```
mv ‘arm-gnu-toolchain-11.3.rel1-x86_64-arm-none-linux-gnueabihf.tar.xz?rev=65520e9cdf324eca9c02f5302c904fa4’  arm-gnu-toolchain-11.3.rel1-x86_64-arm-none-linux-gnueabihf.tar.xz
tar -xf  arm-gnu-toolchain-11.3.rel1-x86_64-arm-none-linux-gnueabihf.tar.xz
```

## set env and save it to ./bashrc
```
echo 'export PATH="~/arm-gnu-toolchain-11.3.rel1-x86_64-arm-none-linux-gnueabihf/bin:$PATH"' >>~/.bashrc
echo 'export CROSS_COMPILE=~/arm-gnu-toolchain-11.3.rel1-x86_64-arm-none-linux-gnueabihf/bin/arm-none-linux-gnueabihf-' >>~/.bashrc
```

## install dependency libncursesw5
```
sudo apt install libncursesw5
```

## install dependency python3.8
```
sudo apt update
sudo apt upgrade
sudo add-apt-repository ppa:deadsnakes/ppa -y
sudo apt update
sudo apt install python3.8
# Verify Python 3.8 Installation 
python3.8 --version
```

# Step 1: Install GDB Debug Extension in VS Code


Open VS Code.

Go to the Extensions view by clicking on the square icon in the left sidebar or using the shortcut Ctrl+Shift+X.

Search for the "C/C++" extension by Microsoft, which includes GDB support. Install it.

# Step 2: Open Your Project in VS Code

Make sure your project path align with the build version (in case you code is built in docker with different path or mapped to different drive)


# Step 3: Configure Launch Settings

Create a .vscode folder in your project directory if it doesn't already exist.

Inside the .vscode folder, create a launch.json file to configure your debugging settings. Here's an example of a launch.json file:
```
{
  "version": "0.2.0",
  "configurations": [
    {
      "type": "gdb",
      "request": "attach",
      "name": "Attach to gdbserver",
      "executable": "/source/build/OSImage/home/509plus/main509plus", //your local path to the binary
      "target": "10.0.0.4:9999", //your target's IP and port
      "remote": true,
      "gdbpath": "/home/jun/arm-gnu-toolchain-11.3.rel1-x86_64-arm-none-linux-gnueabihf/bin/arm-none-linux-gnueabihf-gdb", //path to cross-compiler gdb
      "cwd": "${workspaceFolder}",
      //"preLaunchTask": "startGDBServer", 
      "postDebugTask": "stopGDBServer",
      "valuesFormatting": "parseText",
      "showDevDebugOutput": true
    }
  ]
}
```
Make sure to replace "your local path to the binary" with the path to your compiled embedded application and "path to cross-compiler gdb" with the path to your GDB executable. You should also replace "target's IP and port" with the appropriate GDB Server host and port information.

# Step 4: Configure a Debug Task

Create a tasks.json file in the .vscode folder of your project. This file will define a task to start the GDB Server. Here's an example tasks.json file:


```
{
	"version": "2.0.0",
	"tasks": [
		{
			"label": "transferToTarget",
			"type": "shell",
			"command": "scp",
			"args": [
				"/source/build/OSImage/home/509plus/main509plus", // Local path to your binary
				"root@10.0.0.4:/home/509plus/main509plus" // Remote path on the target
			],
			"group": {
				"kind": "build",
				"isDefault": true
			},
			"isBackground": true
		},
		{
			"label": "startGDBServer",
			"type": "shell",
			"command": "ssh",
			"args": [
				"-o StrictHostKeychecking=no", //it's convenient for this example beause my target will generate a new key every time it boots, comment out when it is a security concern
				"root@10.0.0.4", //replace with your target's IP
				"gdbserver",
				":9999", //replace with your target's port
				"/home/509plus/main509plus"
			], //replace with your target's (not in host) path to the executable
			"group": {
				"kind": "build",
				"isDefault": true
			},
			"dependsOn": "transferToTarget", // Optionally, specify a build task to ensure the binary is up to date	
			"isBackground": true	
		},
		{
			"label": "stopGDBServer",
			"type": "shell",
			"command": "ssh", // Use a suitable command for your platform
			"args": [
				"-o StrictHostKeychecking=no", //it's convenient for this example beause my target will generate a new key every time it boots, comment out when it is a security concern
				"root@10.0.0.4", //replace with your target's IP
				"pkill",
				"-f",
				"gdbserver"
			], // Modify the process name if needed
			"group": {
				"kind": "build",
				"isDefault": true
			}
		}
	]
}
```
You can manually run the tasks by

Terminal - > Run Task… ->

transferToTarget: copy your img to target

startGDBServer: start gdb server on target with your application

stopGDBServer: stop gdb server after debug

# Step 5: Debug Your Application

Set breakpoints in your code where you want to start debugging.

Terminal - > Run Task… → stopGDBServer if you have already a debug session.

Terminal - > Run Task… → transferToTarget if your application has been updated in host

Terminal - > Run Task… → startGDBServer

Click the Run “Start Debugging" icon in the left sidebar or use the shortcut F5.

Select the "Attach to gdbserver" configuration from the dropdown.

Click the green play button to start debugging.

VS Code will connect to the GDB Server, load your application, and stop at breakpoints, allowing you to inspect variables, step through code, and debug your embedded application.

Remember to customize the configurations and paths according to your specific setup and hardware.



 
