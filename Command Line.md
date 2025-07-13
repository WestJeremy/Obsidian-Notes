 
apt
	"advanced package tool" 
	use a command from the advanced package tools

cd
	"change Directory"
	cd ..
		backs out of directory
ls
	"list"
	list directories available in the working directory


mkdir
	"make directory"
pwd
	"print working directory"
	print where in the file system you are



sudo 
	"superuser do" 
	allow user access to privileged commands
	if in a venv it will install globally rather than on the venv
	  


source
	run the file at the end of path
	source myenv/bin/activate  //run activate






**Common Commands**

------
sudo apt update 
	update all the packages



sudo apt-get update



sudo apt upgrade
	download and upgrade system packages
	uses info from "sudo apt-get update"


sudo apt --fix-broken install
	if an install just failed download its dependencies and reinstall it
	

**PYTHON**
____________________
**Install python**
	sudo apt install python3.12  //for python3.12
	sudo apt install python3.12-venv

**Make a Virtual env with a specific python version**
	/usr/bin/python3.12 -m venv myenv3_12

**Install dev Tools C for Python**
sudo apt-get install python3.11-dev  //for python version 3.11


**Activate a VENV**
	source myenv/bin/activate
	python --version // to confirm

**Deactivate a VENV**
	deactivate



**GIT**


Clone repo at link
	git clone url/url/url


