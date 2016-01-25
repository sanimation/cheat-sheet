# Node.Js

## Get away from sudo: npm without root

Running everything as root is both tedious and not a good idea. So let's fix our npm installation so that we don't run things as root anymore:
1. Fire up your editor and open the file ".npmrc" in your home directory (note the leading dot).
2. Add this line, substituting the location of your home directory for mine, of course:
prefix = /Users/boutell/npm
3. Create that folder:
mkdir ~/npm
Now npm will install and look for things in ~/npm/bin (the ~ stands for your home directory) rather than in a global folder that only root can write to. You have your own personal npm, and you can run "npm link" without root privileges.
Just remember that any command line tools you install with "npm install -g", such as "forever," are going to wind up in ~/npm/bin. So let's fix that by adding a line to ~/.profile (or ~/.bashrc if that's your preference):
export PATH=~/npm/bin:$PATH
Start a new terminal window and you'll find that commands installed in ~/npm/bin can now be found.
4. One more catch: you probably have a folder called ~/.npm. And if you've been running npm commands with sudo (stop doing that! Never do it again!), you'll get errors when you try to use "npm link" because it can't overwrite what's already there.
It's easy to clean this up, because there is nothing in ~/.npm that can't be recreated by running npm commands again. But just to be on the safe side, let's move it aside:
mv ~/.npm ~/.npm-old-and-busted
Now "npm link" should work for you exactly as advertised. You can make changes "live" in src/appy and they will be immediately visible when "require"d by src/mysite. You can still run "npm publish" when you have a new stable release that's worth publishing to the rest of the world.