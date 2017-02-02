# Connecting to your server

##### Port forwarding:

OT servers use port 7171 and 7172, which players use to connect to your server as long as they're open. Port 7171 is for logging in, and 7172 is the game port. Another port that we will be using is port 80, which allows access to websites, which we will be setting up soon.

To port forward \(aka open these ports\), you need admin access to your router or modem. Log in to your router and find "Port Forward" or "Virtual Servers" \(or something along the lines of those\), port forwarding options are usually found under the firewall tab in your router/modem's settings. 

If your router/modem gives you text boxes straight forward or gives you an "add" button, this should be the same. Set one of the boxes descriptions as whatever name you choose. After that, enter 7171/7171 for inbound/local ports. Click TCP/UDP for the type \(if you do not have a TCP/UDP option, forward it twice, once with TCP and another with UDP\). 

Once this is done, it's time to find your IPv4 address, open command prompt and type in **ipconfig**, it should give you a list of a bunch of different things, but for now we only need the IPv4 address, which should be in the format of 192.168.x.xxxx. Once you have your IPv4 address, go back to your router/modem and enter your IPv4 address as the "Private IP Address", this should be the final box you need to fill out. Do the same process but with port 7172 and port 80.

Your ports should now be forwarded, to test if your ports are open, you can use this [port checker](http://halfaway.net/portchecker.php).

We're not fully done yet, we still need to edit the hosts file. \(if you're using Linux, ignore this part\)

To access your hosts file, open Sublime Text \(which you should have previously installed\) in administrator mode first. Once you have Sublime Text open, go to **file-&gt;open file** and redirect your path at the top to **C:\Windows\System32\Drivers\etc**, open the "hosts" file by double clicking it. Now that we have the hosts file open, all you have to do at the bottom is add:

```
127.0.0.1    Your IP here
```

Of course, you will have to change "Your IP here" to what your actual IP address is \(you can find your IP address by going to [ipchicken](http://www.ipchicken.com)\)

After that, save the file and close it, we should be done with port forwarding now.



##### Website



##### Connecting

Finally, to connect to your server, you will need [OTLand IP Changer](https://otland.net/threads/otland-ip-changer.134369/), which lets you set the IP to connect to in the Tibia client and launch it, after which you can use your account/password to log in.



##### OTClient



