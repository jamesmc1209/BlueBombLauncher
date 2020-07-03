# BlueBombLauncher
An extension of bluebomb-helper.sh that creates a desktop launcher for thr exploit.

## Installation:

Press<code>CTRL + ALT + T</code> to open terminal window and enter:

      wget https://github.com/mcneproj/BlueBombLauncher/releases/download/0.1/bluebomb-helper.sh

After it downloads the file enter:
    
      chmod +x bluebomb-helper.sh

Then:
    
      ./bluebomb-helper.sh

Now all the required dependencies will be downloaded.
After the download has finished you will now see the Bluebomb Launcher on your desktop.

## Using the Bluemomb Exploit
First you will need to download the hack-mii installer from https://bootmii.org/download/
Once downloaded place the <code>boot.elf</code> file in the root of your SD card and insert it into the Wii Console.
<i>The Wii Mini lacks a SD card slot so you will have to place the <code>boot.elf</code> into the root of a FAT32 formatted Flash Drive or External Harddrive.</i>


After bluebomb has downloaded and unpacked run it via the bluebomb launcher on your desktop.
Bluebomb will launch in a terminal window.

Now you will see options to select your will console. select <b>1</b> for Original Wii console or select <b>2</b> for Wii Mini console.
Next it will ask you for your system menu version. If exploiting a Wii Mini select US or PAL depending on the consoles region. If exploiting an original Wii you will need to enter your system menu version. To find this navigate to your setting menu on your wii. In the top right corner there should be a version code that looks like<code>4.3U</code>.
After selecting your version type <code> Y </code> and press enter. If you see <code> Waiting to Accept...</code> then begin clicking the Wii's sync button until the exploit is loaded.

<b>For more detailed information about this exploit and wii softmodding in general please visit:</b> https://wii.guide/bluebomb



To download and use the launcher with an existing bluebomb exploit:

Delete existing bluebomb folder from /home/ directory.
Open bluebomb-helper.sh with gEdit.
Navigate to the function that says download() and replace it with this:
      
      download() {
    sc 1 "Prerequisites"
    [[ -e ./bluebomb/bluebomb-$arch ]] && printf "BlueBomb executable exists. Not downloading.\n" && cd bluebomb && return || true
    printf "* Downloading BlueBomb... "
    task="Download and extract BlueBomb"
    ## download zip from github
    mkdir -p bluebomb && cd bluebomb || false
    wget -q --secure-protocol=TLSv1_2 "https://github.com/Fullmetal5/bluebomb/releases/download/1.5/bluebomb1.5.zip" -O bluebomb.zip
    printf "Success!\n\n* Unpacking BlueBomb... "
    unzip -q bluebomb.zip
    rm bluebomb.zip
    wget -q --secure-protocol=TLSv1_2 "https://wii.guide/images/bluebomb.png"
    cd ~/Desktop    
    wget -q --secure-protocol=TLSv1_2 "https://github.com/mcneproj/BlueBombLauncher/releases/download/0.1/bluebomb.desktop"
    chmod +x bluebomb.desktop
    sudo cp $HOME/bluebomb/bluebomb.png /usr/share/icons/default
    cd $HOME/bluebomb    
    printf "Success!\n\n"
    }
Save the file and press <code>ctrl + alt + t</code> to open the terminal.
Type

      <code>./bluebomb-helper.sh</code>

and press enter.

Now bluebomb will be redownloaded and the bluebomb launcher will be added to the desktop.


_______________________________________________________________________________________________________________________________________
I modified the bluebomb-helper.sh from wii.guide to download the bluebomb icon from wii.guide as well as the bluebomb.desktop file from this repo.

It adds a desktop launcher that just opens the .sh file in terminal.

I needed this when my wii mini wasnt wanting to connect to my pc or raspi running the exploit. And I had to keep retrying the exploit.

Also probably should specify that Im using Ubuntu 16.04.
Note: I did not create the <code>bluebomb-helper.sh</code> that credit goes to urmum_69 & twosecslater. 
I only injected a few lines of code that downloads and enables the launcher. 
Also the bluebomb.png will be downloaded to the <code>/home/bluebomb/</code> folder then copied to <code>/usr/share/icons/default/</code> directory. 
I did this because the ICON directory requires an absolute path, using $USER or $HOME did not find the icon file.
