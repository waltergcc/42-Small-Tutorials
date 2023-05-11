# Debug throught VSCode
It's possible to debug our code throught VSCode. Even our projects have many files. It's even possible to debug already sent the arguments to the program. To do this in your project, you need to follow the steps below.

## 1. Install C/C++ extension
Launch VS Code Quick Open (Ctrl+P), paste the following command, and press enter.
```
ext install ms-vscode.cpptools
```

## 2. Create a tasks.json file
In your project folder or parent folder create a folder called `.vscode` then create a file called `tasks.json`.
Then copy and paste the code into your tasks.json file according to the type of compilation of your project.

### Using Makefile
```json
{
	"tasks": [
		{
			"label": "build",
			"type": "shell",
			"command": "make -C your_project_folder_name/",
			"group": {
				"kind": "build",
				"isDefault": true
			}
		}
	],
	"version": "2.0.0"
}
```
Replace `your_project_folder_name` with your project folder name. If your workspace is your project folder, then you can remove the `your_project_folder_name/` part. 
```json
"command": "make -C",
```
After that, in your Makefile add the Flag `-g` in the CFLAGS variable.
```makefile 
CFLAGS = -Wall -Wextra -Werror -g
```

### Using cc Command Manually
```json
{
    "tasks": [
		{
            "label": "build",
            "type": "shell",
            "command": "cc",
			"args": [
				"-Wall",
				"-Wextra",
				"-Werror",
				"-g",
				"-I",
				"your_project_folder_name",
				"your_project_folder_name/your_file.c",
				"-o",
				"your_project_folder_name/your_executable_name"
			],
            "group": {
                "kind": "build",
                "isDefault": true,
				"problemMatcher": "$gcc"
            }
        }
	],
    "version": "2.0.0"
}
```
Replace `your_project_folder_name` with your project folder name. If your workspace is your project folder, then you can remove the `your_project_folder_name/` part. After -I flag, put a dot. 
```json
				"-I",
				".",
				"your_file.c",
				"-o",
				"your_executable_name"
```
## 3. Create a launch.json file
Create a file called `launch.json` in your `.vscode` folder. Then copy and paste this code into your launch.json file.
```json
{
	"version": "0.2.0",
	"configurations": [
		{
            "name": "(gdb) Launch",
            "type": "cppdbg",
            "request": "launch",
            "program": "${workspaceFolder}/your_project_folder_name/your_executable_name",
            "args": [
				
			],
            "stopAtEntry": false,
            "cwd": "${workspaceFolder}",
            "environment": [],
            "externalConsole": false,
            "MIMode": "gdb",
            "setupCommands": [
                {
                    "description": "Enable pretty-printing for gdb",
                    "text": "-enable-pretty-printing",
                    "ignoreFailures": true
                }
            ],
			"preLaunchTask": "build"
        }
	]
}
```
Replace `your_project_folder_name` with your project folder name. If your workspace is your project folder, then you can remove the `your_project_folder_name/` part. 

If you want to send arguments to your program, then you can add them in the args array.
```json
			"args": [
				"arg1", "arg2", "arg3..."
			],
```
### 4. Degub your code
Now you can mark Breakpoints in any file of your then press `F5`. It will start the debug and stop in the breakpoint that you set up.
If you want Debug to start at the beginning of the program, just change the `launch.json` file and put the value `true` on the `stopAtEntry`.
```json
			"stopAtEntry": true,
```
In this repository files I left the example of how my .vscode folder was in the push_Swap project.

It's all! :smile:
