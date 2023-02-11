+++
author = "Nitish Kumar"
categories = ["Hack"]
date = 2021-09-17T12:22:00Z
description = ""
draft = false
image = "https://images.unsplash.com/photo-1610664921890-ebad05086414?crop=entropy&cs=tinysrgb&fit=max&fm=jpg&ixid=MnwxMTc3M3wwfDF8c2VhcmNofDM3fHxtb2JpbGV8ZW58MHx8fHwxNjMxNjQxMzU3&ixlib=rb-1.2.1&q=80&w=2000"
slug = "wireless-data-transfer-from-computer"
tags = ["Hack"]
title = "Wireless Data transfer from Computer"

+++


If you use apps like "ShareIt" and "AirDroid" to transfer data from computer to mobile, then you must have noticed that the Transfer Speed is very low. So I found a way to transfer a large amount of data wirelessly by using an open-source tool call NodeJs. This method gives you a high-speed wireless data transfer experience.

Not feeling like reading this? then, [here](https://www.youtube.com/watch?v=pO5tvTusUn4) is the YouTube video tutorial in which I have shown how you can transfer files wirelessly.

Follow these steps:

1. [Download](https://nodejs.org/en/download/) the latest version of NodeJs and install it.

2. To check whether Node is installed properly or not. Go to "Terminal" or ("Command prompt" for windows) and type `node -v` It will show the version of node js installed like `v6.10.0` If you get this then move to step 3. If you get any error the uninstall NodeJs and reinstall it. If still not working the leave a comment on this article. I will help you.

3. Then type, for Linux and Mac you may have to type sudo `npm install -g http-server` , this will install a small HTTP Server on your computer.

4. Then from your terminal go to the directory from where you want to transfer data, using `cd directoryPath`.

5. Then type `http-server` in that folder. It will start a local server on port 8080. It will also show your local ip address like

`[http://192.168.0.14:8080](http://192.168.0.14:8080/)`

Your IP may be different. But similar to the one above. And the cool this about this is you can access this IP on your mobile phone too.

Note: Make sure that your laptop and your mobile phone must be running on the same wifi.

6. Just type `[http://192.168.0.14:8080](http://192.168.0.14:8080/)` on your mobile phone browser (like chrome app) and it will show you the files and folder present in that folder.

7. To download on mobile: Just click on any file it will automatically start downloading. Or you make have too long press on the file to get more options like "download" on your smartphone.

If you open the IP address on another computer then to download the file, you have right-clicked on the file select an option called "save link as.." the save the file.

Also, [Here](https://www.youtube.com/watch?v=pO5tvTusUn4) is the youtube video tutorial for all the above steps.

You can even use this trick to transfer data from one computer to another computer. Just you have to take care of one thing your laptop and your mobile should be running on the same WiFi. And if you don't have wifi at your home you can start a hotspot in your mobile phone and connect the laptop with the same hotspot wifi, then this trick will work fine.

Try this cool trick and let me know how does it work for you by leaving a comment on this article.

