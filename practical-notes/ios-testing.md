# iOS Application Testing

Jailbreak Tools:

Linux Jailbreak Software Checkra1n\
\
Windows version of Checkra1n - iRa1in \
3utools.com - iOS device management tool

Testing Tools:\
OpenSSH\
BurpPro mobile assistant\
\
Application Testing setup:

1. Install iproxy `npm install iproxy` and BurpSuite application proxy on host
2. Start Burp suite and add a listener on port 8082 for all interfaces
3. Go to iPhone settings, set a manual proxy using the the Burp Suite host's IP and port 8082
4.  Connect host PC to mobile device using SSH through iproxy using&#x20;

    a. `iproxy 2222 22 & ssh -R 8082:localhost:8082 root@localhost -p 2222`
5. Visit http://burpsuite to verify connectivity and download Burp CA certificate
6. Go to iPhone settings in the "profile downloaded" section and install certificate
7. Go Settings >General >About > Certificate Trust Settings and activate toggle switch&#x20;
