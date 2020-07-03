# BlueBombLauncher
An extension of bluebomb-helper.sh from wii.guide.

Installation:

Open Terminal and enter:

      wget https://github.com/mcneproj/BlueBombLauncher/releases/download/0.1/bluebomb-helper.sh

After it downloads the file enter:
    
      chmod +x bluebomb-helper.sh

Then:
    
      ./bluebomb-helper.sh

Now all the required dependencies will be downloaded.
After the download has finished you will now see the Bluebomb Launcher on your desktop.

I modified the bluebomb-helper.sh from wii.guide to download the bluebomb icon from wii.guide as well as the bluebomb.desktop file from this repo.
It adds a desktop launcher that just opens the .sh file in terminal.
I needed this when my wii mini wasnt wanting to connect to my pc or raspi running the exploit. And I had to keep retrying the exploit.

Also probably should specify that Im using Ubuntu 16.04.
Note: I did not create the bluebomb-helper.sh that credit goes to urmum_69 & twosecslater. I only injected a few lines of code that downloads and enables the launcher. When downloading the bluebomb.png will be downloaded to the /home/bluebomb/ folder then copied to /usr/share/icons/default/ directory. I did this because the ICON directory requires an absolute path, using $USER or $HOME did not find the icon file.

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
      ./bluebomb-helper.sh
and press enter.
bluebomb will be redownloaded and the bluebomb launcher will be added to the desktop.
