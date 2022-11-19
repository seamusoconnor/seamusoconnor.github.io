---
title: using PATH to run scripts from anywhere
date: 2018-01-26 00:00:00 +0100
categories: [bash]
tags: [scripts, mac, development]
---


## Background

I’ve been looking at setting up a tools folder on my computer so scripts within it can be run from anywhere.
Normally, you can only invoke a script like this from either within the folder it is placed, or by specifying the path in which the script resides.
To do this we can modify the .bash_profile file, depending on the shell you’re using.
For example:
Here is my current PATH:

```bash
/Library/Frameworks/Python.framework/Versions/3.4/bin:/Library/Frameworks/Python.framework/Versions/3.6/bin:/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin:/opt/X11/bin
```


I’ve created a simple script that echos Test to the terminal in:

```bash
/Users/Simac/Tools

Tools $ ls
time.sh
```




when I execute this in my home directory, it’s not recognised by the system as the above current PATH doesn’t include my script.
The system checks the PATH from left-to-right looking for the file to execute. Each directory is colon separated and if it finds the script in /usr/local/bin it won’t search any further. There is potential for danger here as if some malicious script is placed at the start of the PATH, then it will override a legitimate, similarly named script. For that reason, I’d recommend to place the new path at the end (far right of the full PATH).
I’m using bash as my shell, which can be checked with:

```bash
~ $ echo $0
-bash
```

so the directory is added in ```~/.bash_profile```  
Enter the below:
```bash
export PATH="$PATH:/Users/Simac/Tools"
```

open a new terminal session for the new PATH to take effect or use ```source ~/.bash_profile```


Now you can see the changes have taken effect:
```bash

~ $ echo $PATH
/Library/Frameworks/Python.framework/Versions/3.4/bin:/Library/Frameworks/Python.framework/Versions/3.6/bin:/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin:/opt/X11/bin:/Users/Simac/Tools
```

You can see that the new path has been appended to the full PATH.
If you wanted to prepend the path, enter the following command:
```bash
export PATH="/Users/Simac/Tools:$PATH"
```

Now we can test our script:
```bash
/Users/Simac
~ $ time.sh
Test
```


The script runs perfectly from our home directory (or anywhere else)
