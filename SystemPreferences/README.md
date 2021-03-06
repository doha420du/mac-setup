# System Preferences

First thing you need to do, on any OS actually, is update the system! For that: **Apple menu () > About This Mac > Software Update.**

Also upgrade your OS in case you want to work on the latest OS. Sierra is a free upgrade so please check that.

If this is a new computer, there are a couple tweaks you would like to make to the System Preferences. Feel free to follow these, or to ignore them, depending on your personal preferences.

### Users & Groups
- Login Options -> Change fast switching user menu to Icon
- Set up Password, Apple ID, Picture, etc.

### Trackpad
- Point & Click
    - Enable Tap to click with one finger
    - Change Secondary click to right corner
    - Uncheck three finger drag
- Scroll & Zoom
    - Uncheck all apart from Zoom in and out

### Dock
- Visual settings
    - Change position to left and make the size of Icons small
- Other settings
    - Remove workspace auto-switching
    
        ```
        $ defaults write com.apple.dock workspaces-auto-swoosh -bool NO
        $ killall Dock
        ```

### Finder
- Toolbar
    - Update to add path, new folder and delete
- Sidebar
    - Add home and code directory
    - Remove shared and tags
    - New finder window to open in the home directory

### Menubar
- Remove the display and Bluetooth icons
- Change battery to show percentage symbols

### Spotlight
- Uncheck fonts, images, files etc.
- Uncheck the keyboard shortcuts as we'll be replacing them with Alfred.

### Accounts
- Add an iCloud account and sync Calendar, Find my mac, Contacts etc.

### Write to NTFS on OSX Yosemite and El Capitan

#### Install Homebrew and Homebrew Cask
- Instructions [here](http://sourabhbajaj.com/mac-setup/Homebrew/README.html)!

#### Update Homebrew formulae:
```
    $ brew update
```
#### Install osxfuse
- If you are on OSX 10.11 (El Capitan), install the (3.x.x) from https://github.com/osxfuse/osxfuse/releases.
```
    $ brew cask install osxfuse
```   
#### Install ntfs-3g
```
    $ brew install ntfs-3g
```
#### If you are on OSX 10.11 (El Capitan), temporary disable System Integrity Protection.

 - **reboot** and hold CMD+R to get in recovery mode
 - Open the terminal and type
```
    $ csrutil disable
```  
 - **reboot** normally

#### Create a symlink for mount_ntfs
```
    $ sudo mv /sbin/mount_ntfs /sbin/mount_ntfs.original
    $ sudo ln -s /usr/local/sbin/mount_ntfs /sbin/mount_ntfs
```
#### If you are on OSX 10.11 (El Capitan), re-enable System Integrity Protection.
 - **reboot** and hold CMD+R to get in recovery mode
 - Open the terminal and type
```
    $ csrutil enable
```
 - **reboot** normally
 
 

# Set the Mac hostname or computer name from the terminal

Perform the following tasks to change the workstation hostname using the scutil command.

- Open a terminal.
- Type the following command to change the primary hostname of your Mac:
This is your fully qualified hostname, for example myMac.domain.com
```
    $ sudo scutil --set HostName <new host name>
```
so for example:
```
    $ sudo scutil --set HostName flame01.domain.com
```
- Type the following command to change the Bonjour hostname of your Mac:
This is the name usable on the local network, for example myMac.local.
```
    $ sudo scutil --set LocalHostName <new host name>
```
so for example:
```
    $ sudo scutil --set LocalHostName flame01.local
```
- Type the following command to change the computer name:
This is the user-friendly computer name you see in Finder, for example myMac.
```
    $ sudo scutil --set ComputerName <new name>
```
so for example:
```
    $ sudo scutil --set ComputerName flame01
```
- Flush the DNS cache by typing:
```
    $ dscacheutil -flushcache
```
- Restart your Mac.

## Additional Resources
Type scutil --help for the complete list of parameters.


# Change terminal display of computer name
You can define what you want to see before the $ in your terminal by modifying the file ~/.profile.

For example if you add to the file ~/.profile the following line:
```
    export PS1="\h:\w$ "
```
you will see the host name and the complete path of the current directory:
```
    host_name:current_directory_path$
```
You can also modify my example by using the following options in the export command:
```
    \d – Current date
    \t – Current time
    \h – Host name
    \# – Command number
    \u – User name
    \W – Current working directory (i.e: Desktop/)
    \w – Current working directory, full path (i.e: /Users/Admin/Desktop)
```
After that run the following command to make the change effective
```
    $ source ~/.profile
```
