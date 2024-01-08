# Powershell Hash Script
 - The goal of this is to create a script that can analyze multiple hashes of multiple files and look for known malicious signatures.

## Checking Blank Directory
We first want to check our directories, to make sure it is blank before we start.

We will utilize the <b>ls</b> command for this.

![ls blank state](https://i.imgur.com/SF69sxJ.png)


## Creating our first directory
Directories are folders, and we don't need the GUI to create them. The <b>mkdir</b> command is what we will be using.

Lets run the command <b>mkdir somefolder</b>.

![mkdir somefolder](https://i.imgur.com/tbGyCJY.png)

Lets verify that the directory was created, again using the <b>ls</b> command.

![ls of somefolder](https://i.imgur.com/zOgimKI.png)


## Change Directories and Create Files
We can start moving through the directories by using the <b>cd</b> command. In this example it will be: <b>cd somefolder</b>. After that we will create 2 text documents named "Hello" and "Bye". The <b>echo</b> command is what we will use to place text inside a new text document.

![cd and echo](https://i.imgur.com/JtgLoqf.png)

Once the 2 files are created, lets view its contents by using the <b>type</b> command.

![type hello and bye](https://i.imgur.com/8V0IkW7.png)


## Get-ChildItem and Loops
We can view files inside directories by using the <b>Get-ChildItem</b> command specifying the path with <b>-Path</b>. 

![Get-ChildItem somefolder](https://i.imgur.com/x5OMOlP.png)

Next, we will introduce a pipe <b>|</b> and another command <b>Foreach-Object</b>. The pipe will take the output from the first portion of the command and use it as input for the next portion of the command. 

![Foreach-Object](https://i.imgur.com/E7u1PLE.png)


## Variables
In short, <b>variables</b> are a unit of memory. You can store values inside variables. Lets use the below examples.

To test, we will use the <b>Get-Item</b> command.

![Get-Item](https://i.imgur.com/dSZ3RlV.png)

Now, lets create a variable containing this value with <b>$myOwnVariable</b>. **NOTE: You can name your variable whatever you want. 

Once your variable is created, use the <b>type</b> command.

![variable1](https://i.imgur.com/lDMKKcN.png)

Now, lets use some of the following commands to get some values.

![variable2](https://i.imgur.com/tkYs1zv.png)

## Get-FileHash
When you want to view the SHA256 hash of a file, use the <b>Get-FileHash</b> command. 

Lets pull the hashes of our 2 text files. This will be very close to the loop we created before. 

![get hash](https://i.imgur.com/0l7Rgr1.png)

This looks good, but lets clean up the output a bit. 

![get hash2](https://i.imgur.com/mnvCa5V.png)

The <b>Select-Object</b> command is utilized and specified with <b>Hash,Path</b>. Basically we told it we only wanted those 2 values. 

Next, lets create another directory named <b>somehashes</b>, where we store our hashes. 

![somehashes](https://i.imgur.com/s62JabW.png)

## Sigcheck
Sysinternals is a fantastic suite of tools from Microsoft. <b>Sigcheck</b> is a tool that can pull various information from a file and is like <b>Get-FileHash</b> but on steroids. You will need to install Sigcheck and place the <b>.exe</b> inside its own directory, since we will be calling it.

![install](https://i.imgur.com/u8HwQ1m.png)

Once it is downloaded move the <b>sigcheck.exe</b> to its own directory inside the <b>C:</b> drive. I created a folder named <b>Utils</b> and placed it there. 

![utils](https://i.imgur.com/mIP4UI9.png)

Now, lets test sigcheck out. <b>cd</b> into the directory you placed sigcheck and run <b>.\sigcheck.exe</b>. This will display the help page with all the parameters.

![sigcheck0](https://i.imgur.com/YMXxulp.png)

The first parameter we will want to use is the <b>-h</b>, this will display the file hashes. 

![sigcheck1](https://i.imgur.com/BezJczy.png)

![sigcheck2](https://i.imgur.com/a344ATY.png)

We can see that it pulled the info from both text files Hello and Bye. This looks good so far, but we want to incorporate Virus Total using the <b>-v</b> **NOTE: when using the <b>-v</b> you will need to accept it, before being able to use it. 

![vt1](https://i.imgur.com/5WNWqQr.png)

![vt2](https://i.imgur.com/XtRW3oF.png)

With using the <b>-v</b> parameter, we can see the Virus Total information is displayed. This information looks good but lets clean it up some more. 

## Cleaning up the output 
The next command we are going to add to our loop is <b>Select-String</b>. This will select values specified from the output and display them. In this case, we only want the output to showcase the hashes and Virus Total information.

![clean output](https://i.imgur.com/enXaVlE.png)

This looks a lot better and very clean. Next, lets put this into its own directory, so we don't have to keep running it.

![hashes txt](https://i.imgur.com/sNERcnO.png)

Finally, lets use the <b>type</b> command one last time to verify the file contents.

![final contents](https://i.imgur.com/KQRy36C.png)
