title: Windows 10 WSL - Corporate self-signed certificates and other fun
date: 29 April 2021
modified: 2021-04-30 15:15
category: Work
tags: windows10, wsl, corporate
author: John Howard
status: draft

# Working behind a corporate firewall can be painful.

Windows and development languages and tooling (python, javascript, docker, virtual env management, etc.) in a corporate network do not make happy bed fellows. The combination of locked down machines and proxy servers causes me pain daily. Simple stuff is just so hard.

I'd given up trying in the Windows environment, and then started trying the Windows Subsystem for Linux (WSL); and I'm making far more progress.

# Certificates

More precisely, corporate self-signed certificates. These seem to break most attempts to secure package managers. They are not signed by Certificate Authorities and so poor old pip and other folk throw up their hands with 'install fails with “connection error: [SSL: CERTIFICATE_VERIFY_FAILED] certificate verify failed (_ssl.c:598)”' or similar.

So pip can't verify the proxy server certificate. I'm running Ubuntu 18 WSL, so lets fix this. Firstly grab the certificate from the proxy. Firefox lets you download the intermediate certificate - double click on the padlock > Show connection details > More information > View Certificate. Make sure you're looking at the proxy certificate and save the PEM (cert) file. Copy the downloaded PEM file to /etc/ssl/certs and update the certificates using sudo update-ca-certificates. pip will thank you and install stuff happily.
