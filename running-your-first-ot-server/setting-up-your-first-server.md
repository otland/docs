# Setting up your first server

When setting up your first server, things may seem quite tedious to look at, but it will certainly get easier as we go.

**Installing a text editor**

When editing code, programmers tend to use certain text editors they are most familiar with. This lets them program easierly thanks to features like highlighting, auto-complete, etc. The most popular text editors are [Notepad++](https://notepad-plus-plus.org/download) \(free\) and [Sublime Text](https://www.sublimetext.com/3) \(free trial\). You may install whichever one appeals more to you, as we will be using it later on.

**Database**

Open Tibia servers store information such as accounts, players, house items and many more things in a database. This database is a separate service from the Open Tibia server itself, but it is necessary for the server to work. This means you need to install a database service to run alongside the Open Tibia server. In this tutorial, we will be using [Uniform Server Zero](http://www.uniformserver.com/) \(stable version: [13\_3\_2\_ZeroXIII.exe](https://sourceforge.net/projects/miniserver/files/Uniform%20Server%20ZeroXIII/13_3_2_ZeroXIII/13_3_2_ZeroXIII.exe/download)\), a web server which includes a database service \(MySQL\) and a web based database management tool called phpMyAdmin, where you will be able to view and modify data such as player names, levels or other stored information.

After downloading Uniform Server Zero, extract it and open "unicontroller.exe". If you come across any errors, you may need to install [vc\_redist.x64.exe](https://aka.ms/vs/16/release/vc_redist.x64.exe). Otherwise, a prompt will ask you to change your MySQL root password. It is highly recommended to do so, as leaving the default password may be risky.

Now you can start Apache and MySQL by just clicking the buttons on the new window that will appear. Two webs will pop up, you may close them. It's time to open "phpMyAdmin" by clicking on the button. A new window should pop up in your default browser.

The website you're looking \(phpMyAdmin\) will allow you to modify the information in MySQL easily. First things first, we are going to create our databse and import our schema from TFS:

1. On the left sidebar, click "New".
2. Select your database name and click "Create".
3. Your database should be created now and selected.
4. At the top, click the "Import" button.
5. Click "Choose File" next to "Browse your computer" and locate the "schema.sql" file from TFS sources.
6. Scroll down and click "Go".

The database is ready to go! Our server will now be able to store and retrieve information from it.

**Server files**

You will need a set of files before you can run your server. The files can be found [here](https://github.com/otland/forgottenserver/releases/tag/v1.2). Once downloaded, extract the zip. You will also need another set of files which are required to run the server engine, you can find them [here](https://otland.net/threads/opentibia-dll-pack-v2-0.155310/). Extract them into the same folder as beore.

The folder should look like this now:

![](../.gitbook/assets/image%20%281%29.png)

Open config.lua with your preferred text editor and follow these steps:

1. Locate mysqlUser and change the value to "root", if necessary.
2. Locate mysqlPass and change the value to the one you selected earlier.
3. Locate mysqlDatabase and change the value to the one you chose in the second step of the previous section.

Once you are done, save and close the file.

Now it's time for you to open theforgottenserver.exe... Your server is now running!

**Website \(Znote AAC\)**

To create an account on your new server, we will need to set up a website. We will be using Znote AAC for this tutorial, which you can get [here](https://github.com/znote/znoteaac).

Extract the .zip file to your web directory \(for example, "C:\UniServZ\www"\), which should be empty. Enter the website \(if your web directory is UniServZ's, you can do this by clicking "View www" in unicontroller\) and wait for MySQL connection error. This will show you the rest of the instructions:

1. The first step is the one we already did when setting up the database.
2. The second step tells you to run the given SQL queries in your database via phpMyAdmin.
3. The third step asks you to modify config.php. Open it with your text editor and edit the following variables \(at least\):
   1. `$config['ServerEngine']` with the correct TFS version you are running \(`TFS_02`, `TFS_03` or `TFS_10`\).
   2. `$config['sqlUser']` with your MySQL user \(root\).
   3. `$config['sqlPassword']` with the MySQL password you chose.
   4. `$config['sqlDatabase']` with the database name you chose.

You should now be able to connect to your website by typing to 127.0.0.1, localhost or your IP in your browser. Go ahead and create your account and character!

**Website alternative \(Gesior AAC\)**

Download Gesior 2012 from GitHub: [https://github.com/gesior/Gesior2012/archive/TFS-1.0.zip](https://github.com/gesior/Gesior2012/archive/TFS-1.0.zip)

Extract the .zip file to your web directory \(for example, "C:\UniServZ\www"\), which should be empty. Enter the website \(if your web directory is UniServZ's, you can do this by clicking "View www" in unicontroller\) and follow the installation steps. In case you come across an error in step 2, add this line somewhere in your config.lua: `passwordType = "sha1"`.

You should now be able to connect to your website by typing to 127.0.0.1, localhost or your IP in your browser. Go ahead and create your account and character!

