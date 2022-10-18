Prepare your **SonOff RF Bridge** https://tasmota.github.io/docs/devices/Sonoff-RF-Bridge-433/

## Install dependencies (Linux)
```
sudo apt update
sudo apt install python3-pip libcurl4-openssl-dev libssl-dev
pip install pycurl image
curl https://raw.githubusercontent.com/s0mm3rb/bitbuckedconverter/master/BitBucketConverter -o bitbucketconverter.py
chmod +x bitbucketconverter.py
```
## Prepare
1. Run `RfRaw 177` in your **SonOff RF Bridge** console
2. Push all your buttons on the remote (each Button 2-3 times)
3. Save everything from the console that happened after `RfRaw 177` to a file, e.g. `console.txt`

   remove everything before the `RfRaw` command  
   so each line looks similar to this:  
   `{"RfRaw":{"Data":"AA B1 04 0123 0456 0789 ABCD 01010101010101010101010101010101010101010101010101 55"}}`  

## Execute
either run: 
```
bitbuckedconverter.py -f console.txt 
```
each line of `console.txt` will be converted into a `B0 string` and displayed

or run: 
```
bitbuckedconverter.py -f console.txt -e <IP of your Bridge>
```
each line of `console.txt` will be converted into a `B0 string`, displayed and sent to the Bridge.  

Then:  
if the device reacted as expected, you can enter a name of the button (e.g. `lightOn`)  
or enter nothing to try the next line  
repeat this until all lines have been tried  
the tool will create a list of buttons (and their B0 codes) that have worked (i.e. for which you have specified a name)  
in the end the successfull commands will be displayed, like:  
```
Successful commands were: {'lightOn':  'AA B0 25 05 02 0123 0456 0789 ABCD 0EFG 2121212121212121212121212121212121212121212121 55'}
Successful commands were: {'lightOff': 'AA B0 25 05 02 ABCD 0987 6543 2100 0EFG 0121212121212121212121212121212121212121212120 55'}
Do you want to test these commands now? (y/n)
```
you can test these codes again or copy the raw value to use for MQTT or other tools  
you can also send the command directly in the RF Bridge console:  
```
RfRaw AA B0 25 05 02 0123 0456 0789 ABCD 0EFG 21212121212121212121212121212121212121212121212121 55
```
