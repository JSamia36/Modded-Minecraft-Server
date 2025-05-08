# Intro
I recently setup an ATM10 Modded Minecraft server and wanted to make an easy guide similar to the PalWorld server for people to follow along with. In this example I will be setting up ATM10 on a debain VM. I'll be including tunneling, and some configurations I did to help make it easier and for my own documentation sake. The resources required will depend on the modpack you use as well as the amount of players that will be on at the same time. Unfortunately allocating too much RAM can also cause the server to lag.

# Setup
Assuming you have a fresh linux install, we will need Java 21 for this modpack. To install lets run a few commands:
```
sudo apt update
sudo apt install default-jdk
sudo apt install openjdk-21-jdk
java -version
```
Ideally you should now have java, unfortunately that may not work so instead I ran:
```
wget https://download.oracle.com/java/21/latest/jdk-21_linux-x64_bin.deb
sudo dpkg -i jdk-21_linux-x64_bin.deb
java -version
```
These commands can be found [here](https://www.tecmint.com/install-java-on-debian-12/).

Now with Java installed we need to do two different things. First to create a spot where we want to keep all of our files and second to download the appropriate modpack. I just create a simple folder with the server name usually in the home directory. As for downloading the modpack, on CurseForge there should be a small icon where you can download the Server Pack right next to the normal install. Please make sure to use the server pack and not the normal pack, this is very important. If you are using the web version of curseforge, the server files can be found on the right side if you scroll down. 

![image](https://github.com/user-attachments/assets/637ab932-ecd9-40a8-8d96-40a4e2181d0d)


Once that is done we should have a zip file in our downloads, we just want to unzip that to the folder we created. You can use '-d' to specify location when using unzip.
Now I usually add some server side mods to reduce potential lag such as ModernFix, if that is something you'd like to do as well I'll briefly touch on it. We just have to find the mod download page, then move it to the mods folder in our Server Folder. Now that we have that going I'll include some common configs I use below, otherwise we can run:
```
sudo bash startserver.sh
```
That will run, we will have to cancel it then modify the eula.txt to be TRUE, save that then run the command above again. Congrats you should have a server now!

# Networking setup
You could port forward and do all of that but I personally don't have option or like to expose my home IP address so instead I create a tunnel. Cloudflare is typically most common but won't work for a minecraft server so instead we have to use playit.gg. I used this for setting up my dedicated PalWorld server so just going to copy that part over here:
```
curl -SsL https://playit-cloud.github.io/ppa/key.gpg | gpg --dearmor | sudo tee /etc/apt/trusted.gpg.d/playit.gpg >/dev/null
echo "deb [signed-by=/etc/apt/trusted.gpg.d/playit.gpg] https://playit-cloud.github.io/ppa/data ./" | sudo tee /etc/apt/sources.list.d/playit-cloud.list
sudo apt update
sudo apt install playit
```
We can then go to /usr/local/bin and run play it with `./playit`

# Configs
These can vary so much depending on resources and needs for each server. For starters I recommend
- difficulty=normal
- max-players=40 (ONLY IF NEEDED)
- spawn-protection=0
- simulation-distance=6
- view-distance=6
- white-list=true

  
Again these are just personal settings I use on my most recent ATM10 server. There is so many other customizations I'll add as I modify including pregenerating chunks
