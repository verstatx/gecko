# Gecko Tools
## Purpose
I quickly put together this project to solve a problem I was having while developing codes for Super Smash Bros Melee. I was finding it really annoying, every time I made an ASM code change, having to copy my new code into CodeWrite, set the address, click the arrow, and then copy the contents and replace the correct portion of my composite code in GALE01r2.ini.

Composite codes (perhaps there's a better term) is a trend I've been seeing where Melee developers package multiple individual Gecko codes as one single code. The process I described earlier gets even more annoying when I make changes to say 3 asm files at once. I have to correctly compile and replace every single one. I wanted an easier, faster, and less error prone method.

Drawing inspiration from package managers such as npm, I thought it would be a good idea to just define what codes I wanted to compile and what addresses I wanted to inject at in a configuration file and just say "build". So that's what I did and currently that's the full scope of this simple project.
## Installation
1. Visit the [releases page](https://github.com/JLaferri/gecko/releases) to download the latest version
2. Extract the files to a directory such as `C:\gecko\bin`. The contents include:
	* **gecko.exe** - main program binary for running commands
	* **powerpc-gekko-as.exe** - helper binary for compiling code
	* **codes.json** - an example codes.json file used in my project
3. Add `C:\gecko\bin` (or whatever path you placed the files in) to your PATH environment variable.
4. Done!
## Usage
### build command
All you have to do to use the build command is write a `codes.json` file and put it in a directory which contains all of your files containing your assembly code, cd to that file from the command line, and type `gecko build`. This will create a text file with all of your compiled composite codes where you specified.
#### codes.json
I feel like it's easiest to lead by example. The `codes.json` file is relatively self explanatory. I'll show a very simple version here and then link to a more complex solution in my project to show off all the possibilities.

```
{
  "outputFile": "CodeList.txt",
  "codes": [
    {
      "name": "My Composite Code",
      "authors": [
        "Fizzi",
        "Melee Modding Community"
      ],
      "description": [
        "My super awesome code",
        "description line 2"
      ],
      "build": [
        {
          "type": "replace",
          "address": "801A4000",
          "value": "38600036",
          "annotation": "Example replace (04) [Fizzi]"
        },
        {
          "type": "inject",
          "address": "8006B0DC",
          "sourceFile": "InjectCode.asm",
          "annotation": "Example inject (C2) [Fizzi]"
        }
      ]
    }
  ]
}
```
#### Real example
For a more complex example view the [codes.json file](https://github.com/JLaferri/project-slippi/blob/master/Gecko%20Codes/codes.json) in my project and the resulting [CodeList.txt file](https://github.com/JLaferri/project-slippi/blob/master/Gecko%20Codes/CodeList.txt)
#### Relative paths
I haven't tested this but it should be possible to define relative paths for `sourceFile` and `outputFile` if you have a nested directory structure.
#### File watchers
If you use a code editer that supports file watchers, you could consider hooking up the command to run automatically whenever you save one of your assembly code files. This strategy would save you the trouble of having to `gecko build` manually.
## Other Commands
If anyone has any ideas as to some other commands that might be useful I'm more than open to contributions. Please just fork my project and submit a pull request. I called this project Gecko Tool(s) for a reason. Hopefully there are more useful things that can be done with it.
