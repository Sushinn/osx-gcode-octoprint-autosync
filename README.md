# OSX g-code Octoprint autosync
This scripts auto syncs a gcode folder from my mac to my raspberry pi running octopi through ssh. I think it may work with linux too.

You'll need fswatch ( https://github.com/emcrisostomo/fswatch ) to listen for changes in the origin folder (on mac just run " brew install fswatch ").

On OS X I've made a .plist file (included) to use on launchclt, so the script runs automaticly on boot.
Also you want to put you ssh key on the rasp, so you can login without password. As well as defining a alias on ~/.ssh/config, as so:

```
host octopi
        HostName my-ddns-address.ddns.net
        Port 222
        User pi
        ForwardX11Trusted yes
        ForwardX11 yes
```

Just change the HostName to the IP of your raspberry, as the Port.

**What you need to edit:**

* listenFolder.sh: The path to **syncToOctopi.sh** and the **folder to be watch**
* syncToOctopi.sh: The path to the **origin folder**, the ssh part (mine is defined on ~/.ssh/config) and the path to the **destination folder (probably ~/.octoprint/uploads/)**
* com.granzotto.syncfolder.plist: If you want to use OS X's launchctl, change the **WorkingDirectory** to your **~/** and the path to listenFolder.sh (in **ProgramArguments**)
* delete-all-gcodes: This will delete all local and remote g-codes, you just need to change both paths

Then just run listenFolder.sh and when you save a new .gcode file in the folder, it will appear on your octoprint uploads (may need to reload the page to see the new g-code)
