Launch Sublime Text 2 or 3 from the Mac OSX Terminal
=============
As I’m working in the OSX Terminal more and more these days, I'm always on the lookout for time saving shortcuts.

A really useful tip that I picked up recently from Zander Martineau is how to open up Sublime Text straight from the Terminal. This is done by hooking into a CLI utility that Sublime provides called subl.

The following instructions are based largely on the original gist on Github by Artero, so credit for this solution should be directed to them and not myself.

It’s a slightly different installation depending on whether you’re using Sublime Text 2 or 3, so I’ll split the two out below in the installaton; simply refer to the instructions that are relevant to you.

#Installation

Assuming you installed Sublime in the Applications folder, the following command should open up the editor when you type it into the Terminal:

For Sublime Text 2:
open /Applications/Sublime\ Text\ 2.app/Contents/SharedSupport/bin/subl

For Sublime Text 3:
open /Applications/Sublime\ Text.app/Contents/SharedSupport/bin/subl

If that worked, you're good to go.

You now need to create a symlink called sublime which links the subl CLI to a folder where your system usually looks to execute these binaries. To do this, type in:

For Sublime Text 2:
ln -s /Applications/Sublime\ Text\ 2.app/Contents/SharedSupport/bin/subl /usr/local/bin/sublime

For Sublime Text 3:
ln -s "/Applications/Sublime Text.app/Contents/SharedSupport/bin/subl" /usr/local/bin/sublime

#Check your profile

The final thing you need to do, is to check that your system profile is looking in the right place to see the symlink you have just created.

Enter the following command into your Terminal:
```
open ~/.bash_profile
```
Note that in some cases the profile may be called ~/.profile.

This should open up your profile in a text editor. What you’re looking for is a line towards the top of the file that starts with export PATH=. Your PATH contains all the directories that will be checked for executable binaries when you type a command into your Terminal. Since we created a symlink in the /usr/local/bin folder, we want to make sure that that folder is being checked too.

Hopefully, you’ll be able to see something similar to this:
```
export PATH=/usr/local/bin:(...)
```
If not, simply add this folder to your PATH and save the file.

Note: The (...) in this example represents other folders that would be listed on the same line and separated by a colon.

If you don't already have a PATH set in your bash_profile you can type the following on a new line:
```
export PATH=/usr/local/bin:$PATH
```
Finally, if you did have to add /usr/local/bin to your PATH, run the following command before continuing:
```
source ~/.bash_profile
```
This will reload your .bash_profile with the newly added directory in your PATH.

#Test it works!

In your Terminal, the following commands should now work:

sublime . – opens the current directory in Sublime
sublime filename – opens a file where filename is the file to be opened
sublime foldername – opens a folder where foldername is the folder to be opened
And there you have it – you can now open any file or folder in Sublime straight from the Terminal.

Thanks and credit for this great solution again goes to Artero. If you have any problems getting it working, let me know and I’ll do my best to help you out.