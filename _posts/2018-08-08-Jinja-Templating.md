---
title: Jinja Templating To Make Change Management Easier
date: 2018-10-29 08:00:00 +0100
categories: [templates]
tags: [networking, jinja, scripting]
---




I’ve been looking at Change Management and Maintenance Windows and investigating ways of reducing human error when making planned changes to configuration. One way of doing this is by using configuration templates for repetitive tasks and by using a variable file, we can render router configuration. I’ll show an very basic example of how to generate configuration to change multiple interface descriptions at the same time.

We’ll be using:

Python2.7

Jinja2 – http://jinja.pocoo.org/

Jinja is the templating language. It is similar to python but can take a bit of getting used to, especially if you’re already trying to learn a programming language.

For our program, we’ll need three components:


1. A Template. We can create separate templates depending on the Change being performed.

2. a Variable file. With our template, we feed in variables.

3. a Python script to generate the template. We’ll output this to an output file.

We can feed the output file to the router in question and ‘push’ our new config.
Here is the template I wrote in Jinja2:

```vim tmpl.j1```
```jinja
1 configure terminal
2 {% for int in interface_list %}
3 interface fa{{ int }}
4 description {{ desc }}_{{tt}}
5 exit
6 {% endfor %}
7 exit
8 copy run start
```

lines:

2 & 6 are a for loop  
{{ int }} means that our variable ‘int’ will be put in it’s place in the final render.  
Here’s the variable file in YAML format:  

```vim var.yaml```

```yaml
1 ---
2 device_name: "R1"
3 interfaces: "0/0,0/1"
4 desc: "NY4 to FRA2- Circuit ID- NY_FRA_3517538413: Carrier XYZ NOC- 011-555-1234"
```

This should be self explanatory. We can put in other variables and change our template file to use them. ‘device_name’ isn’t used in our instance.
and here is our python script to generate the output file:
```bash
vim j1.py
```

```python
1 from jinja2 import Template
2 import yaml
3 from sys import argv
4 import time
5
6 script, CTT = argv
7
8 file = open ('tmpl.j1','r')
9 tmpl = file.read()
10
11 var_file = open("var.j1","r")
12 var = yaml.load(var_file.read())
13
14 device = var['device_name']
15 var_interfaces = var['interfaces']
16 interfaces = var_interfaces.split(",")
17 description = var['desc']
18
19 t = Template(tmpl)
20 output_render = t.render(interface_list = interfaces, dev = device, desc = description, tt = CTT)
21
22 print output_render
23
24 timestr = time.strftime('%Y%m%d-%H%M%S')
25 output_file_name = ('output-'+timestr+' '+CTT)
26 output_file = open (output_file_name , 'w')
27 output_file.write(output_render)
28 output_file.close()
```

lines  
1-4: Importing the various libraries.  
6: we must enter an argument when starting our python script. for me it’s the CM ticket number for reference. You;’ll see the TT is placed in the description in the template  
8-12 are for opening and reading the template and variable file
14-17 are searching within the variable file. We’re searching within the yaml format. Yaml is a great format for variables as it’s very readable.  
19-20 are used to generate our output file.  
22 prints it to the screen  
23-28 creates a timestamp, creates a file named output, appended with the timestamp and TT number. It writes our rendered config and closes the file afterwards.  
Once we run our script with the CTT number for, we get the following output:  
```bash
$ python j1.py CTT-0001
configure terminal
interface fa0/0
description NY4 to FRA2- Circuit ID- NY_FRA_3517538413: Carrier XYZ NOC- 011-555-1234_CTT-0001
exit
interface fa0/1
description NY4 to FRA2- Circuit ID- NY_FRA_3517538413: Carrier XYZ NOC- 011-555-1234_CTT-0001
exit
exit
copy run start
```

A crude (but effective) way to push this is to just copy and paste this into our router.
There are other methods we can use, like Paramiko. I’ll cover this in another post.


The important thing to take away from this is the philosophy at work. This is about making small but concrete steps to improve the safety of the network, not about fixing everything at once.  

Templates can be improved, more features added. Over time you can quickly built templates for every configuration scenario available, on all manner of devices. This also allows more controlled changes as you can store all the files on git or on a server somewhere, so that every change in the network is documented.


It’s part of the overall goal:  
Improve network safety.  
Reduce human error.  
Accelerate delivery of features.  
Enjoy!  