Making your own install packages for the client softwares
***********************************************************

You can make your own packages for our client programs that are NxClient, NxUpdate, NxMapper, NxLogon, NxBlock, NxRelay.
For NxLogon, since it is a simple Windows console application without installer you just need to replace several files from the original zip file and make your own zip file including them. You can change its name as well. When you change its name you also need to change the contents of the included batch files but these are all straight forward.
However it is a bit different for NxClient and NxUpdate, NxMapper as these softwares require you to make your own installers for Windows and Mac OS.
Making your own Windows installer
In our case, we use Inno Setup from http://www.jrsoftware.org to build the Windows installers. When you install NxClient, NxUpdate and NxMapper, they will create their own directories inside 'C:\Program Files (x86)' and register them as a Windows service. For example, when you run NxClient installer we copy all the required files into 'C:/Program Files (x86)/nxclient' and then we run 'bin/instsvc.bat' under the installation directory to register it as a Windows service and then we run 'bin/setup.bat' at the end of the installation process to run its setup program.
* We can provide our Inno Setup script of each client when you become one of our business partners.
* The zip files we use to build our installer packages are on our older package download page.
* When you uninstall it, we run 'bin/unstsvc.bat' to unregister it from Windows service list.
Making your own Mac OS installer
We use 'Packages' from http://s.sudre.free.fr for building our Mac OS installer. When you run our installer it will create its own directory under '/Library' and copy a 'conf/plist.default' file into '/Library/LaunchDaemons' with a new name like 'org.nxfilter.nxclient.plist' to run it as a daemon. and then it runs 'setup-mac.sh' inside its installation directory to launch its setup program. When you uninstall it, you need to run 'uninstall-mac.sh' inside the installation directory manually.
* We can provide our Packages script of each client when you become one of our business partners.
* The zip files we use to build our installer packages are on our older package download page.
Changing application name
When you customize our agents, one of the things you want to do might be changing the names of our agents. We have 'conf/appname' file for that under the installation directory. When you change the name inside the file, your own program name will be appeared on the setup program of our agents.
Replacing icon file and default setup value
When you want to use your own icon, the icon file is 'nxd.ico' inside the installation directory and it is a merged icon file for 16x16 and 32x32 and 48x48 icons. At the moment it is only for Windows Installer and setup program.
* For Java version NxClient and NxUpdate you need to add one more icon file which is 'nxd16.png'. It's 16x16 PNG file for its setup GUI.
One of the other things you might want to do is to change the default connection values to the server. You can change the default values for 'Server IP' and 'Login Token' on the setup program by modifying 'conf/cfg.default' file.
* 'conf/cfg.default' file will be copied into 'conf/cfg.properties' file when you run a setup program first time or during the installation process.
Writing your own setup program or GUI
If you can build your own package, to build and include your own setup program is also a possible option. On our setup programs there are some input controls and buttons. For input controls, we read the values from 'conf/cfg.properties' file.

And when you click the buttons that are 'SAVE', 'TEST', 'START', 'STOP' we do some action with the updated config values. With 'SAVE' button we save the config values into 'conf/cfg.properties' file. For 'START' and 'STOP' buttons, if it is on Windows we use 'net start' and 'net stop' commands as we install our agent as a service. On Mac OS, we use '/bin/launchstl' command with the Plist file we copied into '/Library/LaunchDaemons' directory.
So when you make a setup program for NxClient on Windows, you need to run these commands with 'START' and 'STOP' buttons,
net start NxClient
net stop NxClient
If it is on Mac OS,
/bin/launchctl load -w /Library/LaunchDaemons/org.nxfilter.nxclient.plist
/bin/launchctl unload -w /Library/LaunchDaemons/org.nxfilter.nxclient.plist
For 'TEST' button, you can run 'bin/test.bat' or 'bin/test.sh' script. Before you run the test script you have to save the config values first.
After you run the test script you can get some messages with the following exit codes.
0 = Success
-1 = Invalid config values
-2 = Connection error
-3 = Login error
* For NxMapper, we have 'test.exe' instead of 'bin/test.bat'.
* For NxMapper, we don't have the login error code as there is no login process.

Customization of NxBlock
--------------------------

NxBlock is an open source software. You can download its source code from our download page.
Customization of NxRelay
We don't provide an installer or a setup program for NxRelay as we don't think it is for an ordinary Windows user. But its structure is almost same as NxFilter. You have enough knowledge to make an installer package for it, if you already read the previous part of this tutorial.

Limitation
--------------

Building your own installers and changing the names of the client softwares will do what you want to do mostly. But there is something you can't touch or change. We have some internal code having 'nxfilter' signature. This is important as we need to have a unique signature to diffrentiate signals from our agents.
And you don't remove our license or any third party license from the package otherwise that is a license violation. You can have your own license file but you need to keep our license somewhere. All in all it is our software and you just customize it, so it is inevitable to have some limitation.

