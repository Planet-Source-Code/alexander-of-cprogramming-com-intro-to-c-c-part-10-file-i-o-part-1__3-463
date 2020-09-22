<div align="center">

## Intro to C/C\+\+ Part 10: File I/O \(part 1\)


</div>

### Description

This is a slightly more advanced topic than what I have covered so far, but I think that it is useful, and I think it will be useful to many people. File i/o is basically reading, and writing files. This lesson will only cover text files, that is, files that are readable through a text editor, as opposed to binary files(exes for example). It will not cover a great deal, for example, this lesson will not deal with searching files or reading specific data from files. It will merely be concerned with opening, writing, and reading text files. Don't worry though, lesson 11 will cover much more on this topic.
 
### More Info
 


<span>             |<span>
---                |---
**Submitted On**   |
**By**             |[Alexander of CProgramming\.com](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByAuthor/alexander-of-cprogramming-com.md)
**Level**          |Intermediate
**User Rating**    |4.8 (72 globes from 15 users)
**Compatibility**  |C\+\+ \(general\)
**Category**       |[Files](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByCategory/files__3-2.md)
**World**          |[C / C\+\+](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByWorld/c-c.md)
**Archive File**   |[](https://github.com/Planet-Source-Code/alexander-of-cprogramming-com-intro-to-c-c-part-10-file-i-o-part-1__3-463/archive/master.zip)





### Source Code

<font size="2">
<p>&nbsp;</p>
<p><font face="Verdana">&nbsp;&nbsp;&nbsp;&nbsp; Well, how does it all start
anyway? Files have their own specific functions to use, as&nbsp;well as their
own data-type, called a FILE(There is more to this, but right not it is not
important, and it will be explained later, when it is useful). The way to use
the FILE type is the same way as using an integer, or a float, or a char:</font></p>
<p><font face="Verdana">FILE *newfile; //Creates a FILE called newfile(don't
forget that it is a pointer)</font></p>
<p><font face="Verdana">Now, we can't use this unless there is a way to give the
FILE(*newfile) a file to point to.&nbsp;&nbsp; The way this works is that it is
what is called a stream. That means that it is where the output will go to. To
direct *newfile to a file the command to use is<br>
FILE *fopen(const char *filename, const char *mode), found in stdio.h. It simply
returns a pointer to a FILE, but it is easy enough to use. For example:</font></p>
<p><font face="Verdana">FILE *newfile: //Creates a FILE called newfile</font></p>
<p><font face="Verdana">newfile=fopen(&quot;c:\AUTOEXEC.BAT&quot;,
&quot;r&quot;);//open up for reading your autoexec.bat file, and assign</font></p>
<p><font face="Verdana">//it to newfile</font></p>
<p><font face="Verdana">&nbsp;&nbsp;&nbsp;&nbsp; Basically, fopen accepts two
strings. One of them is the file name, including the path, and the other is what
the file will be used for(the mode). In this case, the r designates the file
will only be opened for reading. Therefore, the file cannot be modified while it
is open. That is probably a good idea, because editing your autoexec.bat file
with giberish is not a good idea!</font></p>
<p><font face="Verdana"><br>
&nbsp;&nbsp;&nbsp;&nbsp; For a reference here is a chart listing the different
ways you open a file:</font></p>
<p><font face="Verdana">r Open for reading only.<br>
w Creates a file for writing. If a file by that name already exists, it will be
overwritten.<br>
a Append; open for writing at the end of the file, or create the file if it does
not exist.<br>
r+ Open an existing file for reading and writing.<br>
w+ Create a new file for reading and writing. If a file by that name already
exists, it will be overwritten.<br>
a+ Open for append; open (or create if the file does not exist) for update at
the end of the file.</font></p>
<p><font face="Verdana">&nbsp;&nbsp;&nbsp;&nbsp; Keep in mind that each of these
has a different use, and that you should choose the one most appropriate for you
task. For now however, lets concentrate on reading a file.</font></p>
<p><font face="Verdana">&nbsp;&nbsp;&nbsp;&nbsp; Now, let's say you want to
print the contents of autoexec.bat to your screen. Assuming you&nbsp;want to
make a program to do this you would need a function for reading from a file.
There are numerous useful ones, but for now we will use int fgetc(FILE
*stream)(Note that it returns an int, but the range will still be printable(so
it is the same as a char), defined in iostream.h. Basically, fgetc will get the
next character from a file you give it(that is, the stream you give it). An
example would be the following code to display the first few characters of your
autoexec.bat file:</font></p>
<p>&nbsp;</p>
<p><font face="Verdana">#include &lt;iostream.h&gt; //For cout<br>
#include &lt;stdio.h&gt; //For all file i/o functions<br>
void main()<br>
{<br>
int count=0; //Just a variable to keep from reading the file forever.<br>
FILE *afile; //We need a FILE to point to the stream to allow access to the fil<br>
afile=fopen(&quot;c:/AUTOEXEC.BAT&quot;, &quot;r&quot;); //Open up the
autoexec.bat file for reading</font></p>
<p><font face="Verdana">//No, I do not know why it must be a forward slash.<br>
while(count&lt;10)<br>
{<br>
cout&lt;&lt;(char)fgetc(afile); //Notice that fgetc returns an int, which can be
printed.</font></p>
<p><font face="Verdana">//Please note the use of (char) to 'typecast' the
returned integer. That means that it makes<br>
//it into a printable character from the number. There is more on this in lesson
11, which<br>
//I suggest you read.(Note that chars basically convert their ASCII numbers into
the<br>
//appropriate printable characters. 65= 'A' for example.</font></p>
<p><font face="Verdana">count++; //I don't think it should read forever, right?</font></p>
<p><font face="Verdana">}</font></p>
<p><font face="Verdana">fclose(afile); //A surprise(don't worry, just use it to
close a file when done).</font></p>
<p><font face="Verdana">//Just put in the pointer to the stream(the FILE thingy)</font></p>
<p><font face="Verdana">}</font></p>
<p><font face="Verdana">&nbsp;&nbsp;&nbsp;&nbsp; This program is fairly simple,
and it does not take advantage of many of C's more useful&nbsp;file operations.
Note though, that it is going to print out only a few characters. What if you
wanted to print the entire file out, though? Well, that is where a thing called
the EOF(end-of-file) comes into play. It is essentially a null that will signal
the end of the file has been reached.</font></p>
<p><font face="Verdana">&nbsp;&nbsp;&nbsp;&nbsp; So, how would you make a
program to use this? Well, fgetc retrieves a character from the&nbsp;file, and
it will return the EOF when it reaches the end of the file. Now, it is possible
to use a loop that will check to see if the last character is equal to the EOF.
For example, CHARACTERREAD!= EOF. This would return true if the CHARACTERREAD is
not the EOF.</font></p>
<p><font face="Verdana">Here's how I would do it:</font></p>
<p><font face="Verdana">#include &lt;iostream.h&gt; //For cout</font></p>
<p><font face="Verdana">#include &lt;stdio.h&gt; //For all file i/o functions</font></p>
<p><font face="Verdana">void main()</font></p>
<p><font face="Verdana">{</font></p>
<p><font face="Verdana">FILE *afile; //We need to define a FILE type to open a
file<br>
afile=fopen(&quot;c:/AUTOEXEC.BAT&quot;, &quot;r&quot;); //Opens autoexec.bat,
only to read, not write it. afile<br>
//is now the stream pointing to the file autoexec.bat,<br>
//and is used to do operations with autoexec.bat<br>
char c; //Without a character to store the information the program won't work<br>
while(c!=EOF) //Checking to see if the character just read is the end of the
file</font></p>
<p><font face="Verdana">{<br>
c=fgetc(afile); //This reads in the character<br>
//Note that it is not necessary to typecast the fgetc return, as it is
automatically turned<br>
//into a printable character when char c is a character.<br>
<br>
cout&lt;&lt;c; //The prints out the character(as you SHOULD know!)</font></p>
<p><font face="Verdana">}</font></p>
<p><font face="Verdana">fclose(afile); //Just to be safe, close the file!</font></p>
<p><font face="Verdana">}</font></p>
<p><font face="Verdana">&nbsp;&nbsp;&nbsp;&nbsp; Ok, so you finally got it to
print out! Well, what is the next thing to do? Why not have a program to make a
backup of autoexec.bat? There is a new function that you will need to add to
your repetoire before this can be done. The new function is fputc, defined in
stdio.h. int futc(int c, FILE *filethinghere);. Basically, it will return the
character given to it, or it will return an EOF. It accepts a character as the
first argument, and a pointer to a stream(the FILE thing) as the second
argument. Here is an example of how to use it:</font></p>
<p><font face="Verdana">fputc('A', newfile); //Writes the character 'A' to the
file pointed to by newfile</font></p>
<p><font face="Verdana">&nbsp;&nbsp;&nbsp;&nbsp; However, don't forget that this
does not always work. The file the stream points to has to have been opened for
writing, not just reading. Usually you will want to append to a file, but in the
case of our next example we want to create a new file, and overwrite an old one.</font></p>
<p><font face="Verdana">&nbsp;&nbsp;&nbsp;&nbsp; Now that we have a function to
print to a file, why not finish up with one program to&nbsp;backup autoexec.bat.
Basically, we will use the same loop as in the first function, that is, checking
to see if the end of the file is reached, otherwise it will continue to print
out characters. This time however, it will not print the characters to the
screen. Instead, it will print the characters to another file(In the example,
backup.aut).</font></p>
<p><font face="Verdana">-----------------------------------------------------------------------------------------------</font></p>
<p><font face="Verdana">WARNING: If you currently have a file called backup.aut
you will have it overwritten! DO NOT run the example program if you have the
file backup.aut in the directory with your compiler! Otherwise, you will hae it
overwritten.</font></p>
<p><font face="Verdana">-----------------------------------------------------------------------------------------------</font></p>
<p><font face="Verdana">#include &lt;stdio.h&gt; //Needed for file i/o
functions(including fopen!)</font></p>
<p><font face="Verdana">void main()</font></p>
<p><font face="Verdana">{</font></p>
<p><font face="Verdana">FILE *autoexec, *backup; //There are two files this
time, the AUTOEXEC.BAT and the backup</font></p>
<p><font face="Verdana">// file</font></p>
<p><font face="Verdana">autoexec=fopen(&quot;c:\AUTOEXEC.BAT&quot;,
&quot;r&quot;);//Open autoexec.bat to read the file</font></p>
<p><font face="Verdana">backup=fopen(&quot;backup.aut&quot;, &quot;w&quot;);
//Create(or overwrite)backup.aut for writing</font></p>
<p><font face="Verdana">char c; //We need a buffer for reading in the charactesr</font></p>
<p><font face="Verdana">while(c!=EOF) //Just checking to see if it's the end of
the file</font></p>
<p><font face="Verdana">{</font></p>
<p><font face="Verdana">c=fgetc(autoexec); //Reading in a character from
autoexec.bat</font></p>
<p><font face="Verdana">fputc(c, backup); //Writing a character to the backup
file!</font></p>
<p><font face="Verdana">}</font></p>
<p><font face="Verdana">fclose(autoexec);</font></p>
<p><font face="Verdana">fclose(backup); //Closing the files to finish it all up!</font></p>
<p><font face="Verdana">}</font></p>
<p><font face="Verdana">Wow! It's a program that could be useful. Feel free to
use it anytime you like. Just remember how it works. Don't think this is the end
of the file i/o information. There is more, but for now this should be enough to
whet your appetite. Oh, and you case use fputc to write user input to a file
also! I think you can figure it out!</font></font></p>

