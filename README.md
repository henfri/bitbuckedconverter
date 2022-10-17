Process:

-Run rfraw 177 in your SonOff console
-Push all your remote (each Button 2-3 times)

-Save everything from the console that happened after rfraw 177 to a file, e.g. console.txt

remove everything before the 'RfRaw' command

so each line looks similiar to this: 

{"RfRaw":{"Data":"AA B1 04 0123 0456 0789 ABCD 01010101010101010101010101010101010101010101010101 55"}}

a) Run bitbuckedconverter.py -f console.txt 

b) Run bitbuckedconverter.py -f console.txt -e &lt;IP of your Bridge&gt;

In case of a) each line of console.txt will be converted into a B0 string and displayed

In case of b) each line of console.txt will be converted into a B0 string and send to the Bridge. Then:

-if the device reacted as expeced, you can enter a name of the button (e.g. "light")

-else enter nothing to try the next

-repeat this until all lines have been tried

-The tool will create a list of buttons -and their B0 codes- that have worked (i.e. for which you have specified a name)

-In the end you can test all of these codes

