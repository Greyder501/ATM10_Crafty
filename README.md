# How to install an ATM10 Server with Crafty Controller 
   ## This was done on Ubuntu Server 24.04 
   If you have any suggestions or additions to add for other platforms, let me know.
   ## Download Neoforge (Version 21.1.73 at the time of writing)
    https://projects.neoforged.net/neoforged/neoforge

   ## Create a server in the Craft Controller WebUI with these settings.
   ### Server Type `Minecraft Servers`
   ### Server Select `vanilla`
   ### Server Version `1.21.1` (At the time of writing)
   All other settings are up to you. 

# Script install
   1. Go to curse forge and search ATM10 and download the server pack
   2. Move into the server directory.
   ```
   cd /var/opt/minecraft/crafty/crafty-4/servers/XXXXXXXX-XXXX-XXXX-XXXXXXXXXXXX/
   ```
   3. Unzip the Server Pack to your server directory.
   ``` 
   sudo unzip -d . ~/Downloads/Server-Files-X.XX
   ```
   4. Move all the files that are now in `/var/opt/minecraft/crafty/crafty-4/servers/XXXXXXXX-XXXX-XXXX-XXXXXXXXXXXX/Server-Files-X.XX`
   ```
   sudo mv Server-Files-X.XX/* .
   ```
   5. Creat the `eula.txt` file
   ```
   echo "eula=True" | sudo tee eula.txt
   ```
   6. Run `startserver.sh`
   ```
   sudo chmod +x startserver.sh
   ```
   ```
   ./startserver.sh
   ```
   Let the server fully launch, you will see a line in the output that says something like `Dedicated server took XX.XXX seconds to load`

   Then stop the server with 
   ```
   stop
   ```     
   Once you stop getting output use Ctrl+C to exit the console.
  
   7. You now have all of the files and mods, next step it to set permissions.
   ```
   sudo chown crafty:crafty * -R
   ```
   ```
   sudo chmod 2775 * -R
   ```
# Manual install
##
Download `user_jvm_args.txt` from above.

## Install Neoforge in the server directory
1. Unzip Server-Files-X.XX.zip
```
unzip ~/Downloads/Server-Files-X.XX.zip
```
2. Move into the server directory.
```
cd /var/opt/minecraft/crafty/crafty-4/servers/XXXXXXXX-XXXX-XXXX-XXXXXXXXXXXX/
```
3. Move your `neoforge-21.1.73-installer.jar` to the server directory.
```
sudo mv ~/Downloads/neoforge-21.1.73-installer.jar /var/opt/minecraft/crafty/crafty-4/servers/XXXXXXXX-XXXX-XXXX-XXXXXXXXXXXX/
```
4. Install Neoforge
```
sudo java -jar neoforge-21.1.73-installer.jar --install-server
```
5. Move `user_jvm_args.txt` into the server directory
```
mv ~/Downloads/user_jvm_args.txt .
```
6. Copy the `mods` folder from Server-Files-X.XX.
```
sudo cp -r ~/Downloads/Server-Files-X.XX/mods .
```
7. Ensure permissons are correct
```
sudo chown crafty:crafty * -R
```
```
sudo chmod 2775 * -R
```
## Update Crafty Controller `Config` tab.
### Server Executable
```
neoforge-21.1.73-installer.jar
```
### Server Execution Command
```
java @user_jvm_args.txt @libraries/net/neoforged/neoforge/21.1.73/unix_args.txt libraries/net/neoforged/neoforge/21.1.73/neoforge-21.1.73-server.jar nogui

```
### Remove the Server Executable Update URL

Click the Save button at the bottom of the page. 

## You should now be able to start the server
