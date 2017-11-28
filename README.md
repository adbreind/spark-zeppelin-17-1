# Spark with Zeppelin 

### Materials and setup instructions

1. Download Apache Zeppelin version 0.7 with "all" bundled interpreters. Although the following link looks like a direct link to the package, it actually opens the Apache download page, where you can choose a mirror: http://www.apache.org/dyn/closer.cgi/zeppelin/zeppelin-0.7.3/zeppelin-0.7.3-bin-all.tgz
2. Install ... which should be as simple as unzipping the archive you just downloaded. This version of Zeppelin includes an embedded install of Apache Spark 2.1, which is tested to work with the class notebooks.
3. Test it out! 
	* `cd` into the folder where you unpacked Zeppelin
	* If you run `ls` you should see the `bin` folder
	* on ~~MacOS/~~Linux, run `bin/zeppelin-daemon.sh start`
		* __UPDATE For MacOS USERS__:
			* There is a known bug that makes Zeppelin run extremely(!) slowly on MacOS (https://issues.apache.org/jira/browse/ZEPPELIN-2948) so, while it does work, I strongly recommend using Linux instead
		* __UPDATE FOR WINDOWS USERS__:
			* In theory, Zeppelin should run on Windows with minor changes (e.g., `zeppelin.cmd`), but your mileage may vary
			* Zeppelin claims support on Win 7 SP 1, but I have not tried that
			* I __did__ try it on Windows 10 (more or less latest Microsoft build) and it did *not* work out of the box
			* Of course, it's quite possible that with some monkeying around it can be made to work on Win 10
			* __HOWEVER__ my recommendation would be to install a Linux VM and run it there: free, easy, definitely works, and your "real" Spark work will almost certainly be on Linux anyway
			* Easiest path: Grab free VMWare or VirtualBox, install ubuntu-16.04.2-desktop-amd64, add a JRE with `sudo apt install openjdk-8-jre-headless` and then just unzip Zeppelin and you're all set.
				* Make sure you give this VM a good chunk of resources -- I'd recommend 8 GB RAM and 2 CPU cores if you have them
	* Point your browser to `localhost:8080` and you should see Zeppelin running!
		* occasionally it seems to require an extra few seconds, refreshes, or even clearing browser cache, moreso than other webapps, not sure why, but don't sweat it
	* Click "create new note" to start a new notebook
		* Give it a name (like "Test"); the default interpreter should say "Spark" and you can leave that as is, and click "Create Note"
	* In the first notebook cell, type in `1 + 1` and hit shift + enter
		* After a few seconds, you should see `res0: Int = 2` pop out
	* Just to make sure Spark can actually run a job, in the next cell, enter `sc.parallelize(1 to 100).sum` and hit shift + enter
		* You should see `res1: Double = 5050.0` pop out
	* Congrats, your Zeppelin + embedded Spark 2.1 is installed!
4. If you haven't yet cloned this github repo on your machine, go ahead and do that. If you really don't want to use git, you can just "Download as Zip" this whole repo and use that, and you'll be fine.
5. Move or copy the "data" folder from the repo into your Zeppelin folder. It should be at the same "level" as `bin`, `conf`, `interpreter`, etc. Why? This way, if you `cd` to the Zeppelin folder and start it with `bin/zeppelin-daemon.sh start`, inside the notebook environment, your data will be under `data/`.
	* This is for simplicity; of course you are welcome to `%sh cd ...` from inside Zeppelin, or hack the paths to the datasets, or anything else you wish -- I'm just trying to make it as simple and consistent for everyone as possible.
	* You can check if everything is in the right place by punching in `%sh ls data` from inside a notebook cell, and you should see the list of data files, with `amazon20k.parquet`, `diamonds.csv`, etc.
6. Make note (for yourself) of where you put the `notebooks` folder from this repo. You don't need to do anything with them yet, but in class, we will load notebooks into Zeppelin, so it will be handy to know where to find the files.
	* If you want, you can try it from the main Zeppelin page by clicking "Import Note" then "Choose a JSON here" and then using the file picker to find the notebook.
		* When long notebooks like these import, they will look weird at first -- like a bunch of blank cells. Just wait about 30 seconds for Zeppelin to catch up and render them, and you should be all set.


