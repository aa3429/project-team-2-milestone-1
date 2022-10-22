# project-team-2-milestone-1 readme file
Installation Instructions

Installation Guide
A CVAT installation guide for different operating systems.
Quick installation guide
Before you can use CVAT, you’ll need to get it installed. The document below contains instructions for the most popular operating systems. If your system is not covered by the document it should be relatively straight forward to adapt the instructions below for other systems.

Probably you need to modify the instructions below in case you are behind a proxy server. Proxy is an advanced topic and it is not covered by the guide.

For access from China, read sources for users from China section.

Ubuntu 18.04 (x86_64/amd64)

Open a terminal window. If you don’t know how to open a terminal window on Ubuntu please read the answer.

Type commands below into the terminal window to install docker. More instructions can be found here.

sudo apt-get update
sudo apt-get --no-install-recommends install -y \
  apt-transport-https \
  ca-certificates \
  curl \
  gnupg-agent \
  software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository \
  "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) \
  stable"
sudo apt-get update
sudo apt-get --no-install-recommends install -y docker-ce docker-ce-cli containerd.io
Copy
Perform post-installation steps to run docker without root permissions.

sudo groupadd docker
sudo usermod -aG docker $USER
Copy
Log out and log back in (or reboot) so that your group membership is re-evaluated. You can type groups command in a terminal window after that and check if docker group is in its output.

Install docker-compose (1.19.0 or newer). Compose is a tool for defining and running multi-container docker applications.

sudo apt-get --no-install-recommends install -y python3-pip python3-setuptools
sudo python3 -m pip install setuptools docker-compose
Copy
Clone CVAT source code from the GitHub repository with Git.

Following command will clone latest develop branch:

git clone https://github.com/opencv/cvat
cd cvat
Copy
See alternatives if you want to download one of the release versions or use the wget or curl tools.

To access CVAT over a network or through a different system, export CVAT_HOST environment variable

export CVAT_HOST=your-ip-address
Copy
Run docker containers. It will take some time to download the latest CVAT release and other required images like postgres, redis, etc. from DockerHub and create containers.

docker-compose up -d
Copy
(Optional) Use CVAT_VERSION environment variable to specify the version of CVAT you want to install specific version (e.g v2.1.0, dev). Default behavior: dev images will be pulled for develop branch, and corresponding release images for release versions.

CVAT_VERSION=dev docker-compose up -d
Copy
Alternative: if you want to build the images locally with unreleased changes see How to pull/build/update CVAT images section

You can register a user but by default it will not have rights even to view list of tasks. Thus you should create a superuser. A superuser can use an admin panel to assign correct groups to the user. Please use the command below:

docker exec -it cvat_server bash -ic 'python3 ~/manage.py createsuperuser'
Copy
Choose a username and a password for your admin account. For more information please read Django documentation.

Google Chrome is the only browser which is supported by CVAT. You need to install it as well. Type commands below in a terminal window:

curl https://dl-ssl.google.com/linux/linux_signing_key.pub | sudo apt-key add -
sudo sh -c 'echo "deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google-chrome.list'
sudo apt-get update
sudo apt-get --no-install-recommends install -y google-chrome-stable
Copy
Open the installed Google Chrome browser and go to localhost:8080. Type your login/password for the superuser on the login page and press the Login button. Now you should be able to create a new annotation task. Please read the CVAT manual for more details.

Windows 10

Install WSL2 (Windows subsystem for Linux) refer to this official guide. WSL2 requires Windows 10, version 2004 or higher. Note: You may not have to install a Linux distribution unless needed.

Download and install Docker Desktop for Windows. Double-click Docker for Windows Installer to run the installer. More instructions can be found here. Official guide for docker WSL2 backend can be found here. Note: Check that you are specifically using WSL2 backend for Docker.

Download and install Git for Windows. When installing the package please keep all options by default. More information about the package can be found here.

Download and install Google Chrome. It is the only browser which is supported by CVAT.

Go to windows menu, find Git Bash application and run it. You should see a terminal window.

Clone CVAT source code from the GitHub repository.

The following command will clone the latest develop branch:

git clone https://github.com/opencv/cvat
cd cvat
Copy
See alternatives if you want to download one of the release versions.

Run docker containers. It will take some time to download the latest CVAT release and other required images like postgres, redis, etc. from DockerHub and create containers.

docker-compose up -d
Copy
(Optional) Use CVAT_VERSION environment variable to specify the version of CVAT you want to install specific version (e.g v2.1.0, dev). Default behavior: dev images will be pulled for develop branch, and corresponding release images for release versions.

CVAT_VERSION=dev docker-compose up -d
Copy
Alternative: if you want to build the images locally with unreleased changes see How to pull/build/update CVAT images section

You can register a user but by default it will not have rights even to view list of tasks. Thus you should create a superuser. A superuser can use an admin panel to assign correct groups to other users. Please use the command below:

winpty docker exec -it cvat_server bash -ic 'python3 ~/manage.py createsuperuser'
Copy
If you don’t have winpty installed or the above command does not work, you may also try the following:

# enter docker image first
docker exec -it cvat_server /bin/bash
# then run
python3 ~/manage.py createsuperuser
Copy
Choose a username and a password for your admin account. For more information please read Django documentation.

Open the installed Google Chrome browser and go to localhost:8080. Type your login/password for the superuser on the login page and press the Login button. Now you should be able to create a new annotation task. Please read the CVAT manual for more details.

Mac OS Mojave

Download Docker for Mac. Double-click Docker.dmg to open the installer, then drag Moby the whale to the Applications folder. Double-click Docker.app in the Applications folder to start Docker. More instructions can be found here.

There are several ways to install Git on a Mac. The easiest is probably to install the Xcode Command Line Tools. On Mavericks (10.9) or above you can do this simply by trying to run git from the Terminal the very first time.

git --version
Copy
If you don’t have it installed already, it will prompt you to install it. More instructions can be found here.

Download and install Google Chrome. It is the only browser which is supported by CVAT.

Open a terminal window. The terminal app is in the Utilities folder in Applications. To open it, either open your Applications folder, then open Utilities and double-click on Terminal, or press Command - spacebar to launch Spotlight and type “Terminal,” then double-click the search result.

Clone CVAT source code from the GitHub repository with Git.

The following command will clone the latest develop branch:

git clone https://github.com/opencv/cvat
cd cvat
Copy
See alternatives if you want to download one of the release versions or use the wget or curl tools.

Run docker containers. It will take some time to download the latest CVAT release and other required images like postgres, redis, etc. from DockerHub and create containers.

docker-compose up -d
Copy
(Optional) Use CVAT_VERSION environment variable to specify the version of CVAT you want to install specific version (e.g v2.1.0, dev). Default behavior: dev images will be pulled for develop branch, and corresponding release images for release versions.

CVAT_VERSION=dev docker-compose up -d
Copy
Alternative: if you want to build the images locally with unreleased changes see How to pull/build/update CVAT images section

You can register a user but by default it will not have rights even to view list of tasks. Thus you should create a superuser. A superuser can use an admin panel to assign correct groups to other users. Please use the command below:

docker exec -it cvat_server bash -ic 'python3 ~/manage.py createsuperuser'
Copy
Choose a username and a password for your admin account. For more information please read Django documentation.

Open the installed Google Chrome browser and go to localhost:8080. Type your login/password for the superuser on the login page and press the Login button. Now you should be able to create a new annotation task. Please read the CVAT manual for more details.

