# Setting up your first server

When setting up your first server, things may seem quite tedious to look at, but it will certainly get easier as we go.



##### Installing a text editor

When editing code, programmers tend to use certain text editors that have colors, features, and design that they like. The most popular text editors are [Sublime Text](https://www.sublimetext.com/3) and [Notepad++](https://notepad-plus-plus.org/download). Install whichever one appeals to you more, we will be using a text editor later on.



##### Database

For storing information on your server, you will need a database, which will contain your account, players, among other things. You will need [Uniform Server Zero](http://www.uniformserver.com) to use MySQL and phpMyAdmin. 

After downloading Uniform Server, open "unicontroller.exe" and click the two buttons at the top right \(Start Apache, Start MySQL\). You will see two windows pop up in your default browser, close them. Click back on the unicontroller and click the button that says "phpMyAdmin". There will be another window now that should pop up in your default browser, keep this open.

The screen you're looking at will be a bit confusing due to all of the buttons, but we only need a few to set up our database. Follow these steps:

1. On the left sidebar, click "New"
2. Select your database name and click "Create"
3. You should have that database created now, and should have automatically opened it for you
4. At the top, click the button that says "Import"
5. Click "Choose File" next to "Browse your computer" and locate the "schema.sql" file you extracted
6. Scroll down and click "Go"

Now we have a database that our server will be able to store information in.



##### Server files

You will need a set of files to start off with so you can run your server, you can download the files [here](https://github.com/otland/forgottenserver/releases/tag/v1.2), after downloading, extract the zip.





##### DLL Files \(maybe include this as a part of TFS?\)



