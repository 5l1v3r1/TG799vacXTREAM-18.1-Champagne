# TG799vacXTREAM-18.1-Champagne

On my new blog you might find other things for my projects as well in future: 

	https://nr1.nu

This wiki wont be as big as the one from Telia but I just got one of those (actually i wanted a telia one) but yeah, there is not much info 
about this router online I figured out and after few hours of playing around there is some stuff that I want to share.
The router seems to be more secured then telias but I doubt, they store passwords in plaintext aswell. 

There is horrible stuff about Telenors as well and this repo will be updated now and then.


# First out, Telenors password is also stored in plaintext, 

![Screenshot](.previews/telenors-password.txt)

Default Login: Kundservice 
Default Password: F0rth4stargran3n

How come nobody else have found this earlier or leaked this? The Router has been used since 2015, noob ISP. 

# Logviewer

How to get logviewer showing up

![Screenshot](.previews/logviewer_telenor.gif)

Screenshot 

![Screenshot](.previews/telenor_plasmo-password.png)

First thing that might help anyone that does know how to get logviewer shown up, passwords are stored here also for variuos features :) 

# Tcpdump 

![Screenshot](.previews/tcpdump_telenor.gif)

Login and rightclick on any other modal in upper right corner and just change the data-modal below:

	modals/diagnostics-tcpdump-modal.lp

It also works for: 

# Export config

Via developer console on prefered browser

Via developer console

    $.post('modals/gateway-modal.lp',{ action: "export_config",CSRFtoken: $("meta[name=CSRFtoken]").attr("content") },wait_for_webserver_down,"json");

![Screenshot](.previews/export_config.gif)

Via curl command for Linux

    #!/bin/bash

    CSFRTOKEN=$(curl -sL --insecure 'https://192.168.10.1/login.lp?action=getcsrf)
    SESSIONID=$(curl -sL --insecure 'https://192.168.10.1/login.lp?action=getcsrf -v 2>&1|grep -E 'sessionID'|cut -d'=' -f2|cut -d';' -f1)

	curl -sL --insecure 'https://192.168.10.1/modals/gateway-modal.lp' \  
	-H 'Cookie: sessionID=4b33240b9ba8641e3c0bf0ffeb32cb17eac8393556aa1c0fc832c5ee28e2fc6d; fileDownload=true' \
	-H 'Sec-Fetch-Dest: empty' \
 	-H 'Sec-Fetch-Mode: cors' \ 
	-H 'Sec-Fetch-Site: same-origin' \
	-H 'Pragma: no-cache' \
	-H 'Cache-Control: no-cache' \
	-H "Cookie: sessionID=$SESSIONID fileDownload=true" \
	--data-raw "action=export_config&CSRFtoken=$CSFRTOKEN" --insecure

