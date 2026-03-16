# Headtracking-on-Linux
A short meta explanation on how to use Opentracker to achieve headtracking with Games running on Proton

The current headtracking situation (early 2026) on Linux is confusing, use this write-up to get Opentrack headtracking in hopefully most games running under Steams Proton.


Get https://github.com/markx86/opentrack-launcher and follow the instructions. 

This tool launches a windows Opentrack portable executable via Proton. (tested with Proton 10.0)
After the installation process is complete, the launch of Opentrack will fail. This is expected since there is a dependency issue with different Qt6 .dlls in the most current Version of Opentrack (.

Make sure ~./local/share/opentrack-launcher/scripts exist, this indicates the installation was successful. This process can take a couple of minutes, even after the launch crashed.
Now delete the contents of ~./local/share/opentrack-launcher/install

Download the 32-bit portable opentrack 2024.1.1 from https://github.com/opentrack/opentrack/releases/tag/opentrack-2024.1.1

Extract the portable opentrack version to ~./local/share/opentrack-launcher/install

The launch should be successful now, Opentrack.exe and your game both start. 

Now you need to install the native Linux Opentrack. You may find an appimage or compile from source. To compile from source (recommended) follow the instructions on https://github.com/opentrack/opentrack/wiki/Building-on-Linux

After the installation/compilation was successful, launch your game from Steam with the provided parameters to also launch the portable Opentrack.exe via opentrack-launcher. Start your Linux native Opentrack. 
Use the following settings:

NATIVE LINUX OPENTRACK SETTINGS: 

Input: NeuralNet Tracker (or any solution that works for you)

Output: UDP over network, 127.0.0.1 Port 4242 (Also allow this port on your ufw or other firewall, just make sure you open it for localhost only)

PORTABLE OPENTRACK.exe: 

Input: UDP over network, 127.0.0.1 Port 4242 (Don't forget to open this port.)

Output: Freetracker 2.0 Enhanced (make sure to select the correct interface option for your game if the headtracking input is buggy)

Press Start on both running Opentrack GUIs, use your head to look around. Hopefully.


Other options: Your game might support UDP over network and you don't have to go through all of this, the native Opentrack will work just fine.


This write-up is based on the experience of: https://github.com/opentrack/opentrack/issues/2109#issuecomment-3962445706
