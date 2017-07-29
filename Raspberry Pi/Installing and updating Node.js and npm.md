# Installing and updating Node.js and npm on a Raspberry Pi
This tutorial describes how you can easily install and update Node.js on a Raspberry Pi.
I'll be using the latest version of Raspbian, but the instructions will probably work just fine on other Linux distributions.

## Installing Node.js and npm
First of all, we'll need to figure out the CPU architecture of the Raspberry Pi.
All boards use ARM chips, but they don't all use the same CPU architecture.

SSH into your Pi and run `lscpu | grep 'Architecture'` to find out which architecture your Pi uses. You'll see something like 'armv6l' or 'armv7l'.

Once we know this piece of information, we're ready to download and install Node.js!

### Step 1: downloading the correct pre-built binary
The Node.js Foundation provides pre-built binaries for a lot of different CPU architectures.
There are two different versions of Node.js: a version containing the latest features and a long-term support version. Both versions can be installed using the same instructions in this tutorial.

On your computer, go to the Download page on Node.js' website:
https://nodejs.org/en/download/

Click on the version you'd like to install (either 'LTS' or 'Current').
On the right of 'Linux Binaries (ARM)', right-click on the CPU architecture that your Pi is running (e.g. 'ARMv6' if `lscpu` printed 'armv6l') and copy the link URL.

On your Pi, change directory to your home folder using `cd ~`.
Next, we'll use `wget` to download the Node.js binary. Simply type `wget` followed by the URL you copied and hit Return. This should look something like this:
`wget https://nodejs.org/dist/v8.2.1/node-v8.2.1-linux-armv6l.tar.xz`

Once the binary has been download, we'll untar it using the `tar` utility. Type `tar -x -f` followed by the name of the archive and hit Return. This should look something like this: `tar -x -f node-v8.2.1-linux-armv6l.tar.xz`

Once the archive has been extracted, we need to change directory into the extracted folder. Type `cd ` followed by the name of the archive without the `.tar.xz` extension and hit Return. This should look something like this: `cd node-v8.2.1-linux-armv6l`

### Step 2: installing the downloaded binary
The downloaded binary is now almost ready to be installed. First, which is as simple as copying all files from the extracted folder to the `/usr/local/` folder. We'll do this using the `cp` utility. Super-user privileges are required, so we'll need to use `sudo`.

Before we start copying all files, we need to remove some static files that don't have to be copied to the `/usr/local` folder. Type `rm -f CHANGELOG.md LICENSE README.md` and hit Return to do this.

We're now ready to install Node.js and npm. Type `sudo cp -R -f * /usr/local` and hit Return. Once this is done, Node.js and npm should be ready for use!

To cleanup your home folder, type `cd ..` and hit Return. Then type `rm -R -f` followed by the name of the archive, a whitespace and the extracted folder name and hit Return. This should look something like this: `rm -R -f node-v8.2.1-linux-armv6l.tar.xz node-v8.2.1-linux-armv6l`

All installation files are now removed from your home folder.
Node.js and npm should now be correctly installed and ready for use. Simply run `node -v` to see the version of the installed binary. Running `npm -v` prints the version of the installed `npm` binary.

## Updating Node.js and/or npm
To update Node.js, simply follow the above instructions again. The old version will be overwritten, so it's probably best to run `sudo reboot now` after you've followed the above instructions.

Updating `npm` is quite easy. Simply run `sudo npm install npm@latest -g` to install the latest version of npm. After running the command, type `npm -v` to see if the update went smoothly.