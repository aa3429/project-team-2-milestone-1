# project-team-2-milestone-1 readme file

# Installation Instructions (Windows and MacOS)

# Windows 10:

1) Install WSL2 (Windows subsystem for Linux) refer to this official guide: "https://docs.microsoft.com/windows/wsl/install-win10". WSL2 requires Windows 10, version 2004 or higher. Note: You may not have to install a Linux distribution unless needed.

2) Download and install Docker Desktop for Windows:"https://download.docker.com/win/stable/Docker%20Desktop%20Installer.exe". Double-click Docker for Windows Installer to run the installer. More instructions can be found here:"https://docs.docker.com/docker-for-windows/install/". Official guide for docker WSL2 backend can be found here:"https://docs.docker.com/docker-for-windows/wsl/". Note: Check that you are specifically using WSL2 backend for Docker.

3) Download and install Git for Windows:"https://github.com/git-for-windows/git/releases/download/v2.21.0.windows.1/Git-2.21.0-64-bit.exe". When installing the package please keep all options by default. More information about the package can be found here:"https://gitforwindows.org/".

4) Download and install Google Chrome:"https://www.google.com/chrome/". It is the only browser which is supported by CVAT.

5) Go to windows menu, find Git Bash application and run it. You should see a terminal window.

6) Clone CVAT source code from the GitHub repository:"https://github.com/opencv/cvat".

7) The following command will clone the latest develop branch:

git clone https://github.com/opencv/cvat
cd cvat

See alternatives:"https://opencv.github.io/cvat/docs/administration/basics/installation/#how-to-get-cvat-source-code" if you want to download one of the release versions.

8) Run docker containers. It will take some time to download the latest CVAT release and other required images like postgres, redis, etc. from DockerHub and create containers.

docker-compose up -d

(Optional) Use CVAT_VERSION environment variable to specify the version of CVAT you want to install specific version (e.g v2.1.0, dev). Default behavior: dev images will be pulled for develop branch, and corresponding release images for release versions.

9) CVAT_VERSION=dev docker-compose up -d

Alternative: if you want to build the images locally with unreleased changes see How to pull/build/update CVAT images section:"https://opencv.github.io/cvat/docs/administration/basics/installation/#how-to-pullbuildupdate-cvat-images"

You can register a user but by default it will not have rights even to view list of tasks. Thus you should create a superuser. A superuser can use an admin panel to assign correct groups to other users. Please use the command below:

10) winpty docker exec -it cvat_server bash -ic 'python3 ~/manage.py createsuperuser'

11) If you don’t have winpty installed or the above command does not work, you may also try the following:

enter docker image first
docker exec -it cvat_server /bin/bash
then run
python3 ~/manage.py createsuperuser

Choose a username and a password for your admin account. For more information please read Django documentation:"https://docs.djangoproject.com/en/2.2/ref/django-admin/#createsuperuser".

12) Open the installed Google Chrome browser and go to localhost:8080 "http://localhost:8080/". Type your login/password for the superuser on the login page and press the Login button. Now you should be able to create a new annotation task. Please read the CVAT manual:"https://opencv.github.io/cvat/docs/manual/" for more details.


# Mac OS Mojave

1) Download Docker for Mac:"https://download.docker.com/mac/stable/Docker.dmg". Double-click Docker.dmg to open the installer, then drag Moby the whale to the Applications folder. Double-click Docker.app in the Applications folder to start Docker. More instructions can be found here:"https://docs.docker.com/v17.12/docker-for-mac/install/#install-and-run-docker-for-mac".

2) There are several ways to install Git on a Mac. The easiest is probably to install the Xcode Command Line Tools. On Mavericks (10.9) or above you can do this simply by trying to run git from the Terminal the very first time.

3) git --version

If you don’t have it installed already, it will prompt you to install it. More instructions can be found here:"https://git-scm.com/book/en/v2/Getting-Started-Installing-Git".

Download and install Google Chrome:"https://www.google.com/chrome/". It is the only browser which is supported by CVAT.

4) Open a terminal window. The terminal app is in the Utilities folder in Applications. To open it, either open your Applications folder, then open Utilities and double-click on Terminal, or press Command - spacebar to launch Spotlight and type “Terminal,” then double-click the search result.

5) Clone CVAT source code from the GitHub repository:"https://github.com/opencv/cvat" with Git.

The following command will clone the latest develop branch:

git clone https://github.com/opencv/cvat
cd cvat

See alternatives:"https://opencv.github.io/cvat/docs/administration/basics/installation/#how-to-get-cvat-source-code" if you want to download one of the release versions or use the wget or curl tools.

6) Run docker containers. It will take some time to download the latest CVAT release and other required images like postgres, redis, etc. from DockerHub and create containers.

7) docker-compose up -d

(Optional) Use CVAT_VERSION environment variable to specify the version of CVAT you want to install specific version (e.g v2.1.0, dev). Default behavior: dev images will be pulled for develop branch, and corresponding release images for release versions.

8) CVAT_VERSION=dev docker-compose up -d

Alternative: if you want to build the images locally with unreleased changes see How to pull/build/update CVAT images section:"https://opencv.github.io/cvat/docs/administration/basics/installation/#how-to-pullbuildupdate-cvat-images"

You can register a user but by default it will not have rights even to view list of tasks. Thus you should create a superuser. A superuser can use an admin panel to assign correct groups to other users. Please use the command below:

9) docker exec -it cvat_server bash -ic 'python3 ~/manage.py createsuperuser'

Choose a username and a password for your admin account. For more information please read Django documentation:"https://docs.djangoproject.com/en/2.2/ref/django-admin/#createsuperuser".

10) Open the installed Google Chrome browser and go to localhost:8080 ("http://localhost:8080/"). Type your login/password for the superuser on the login page and press the Login button. Now you should be able to create a new annotation task. Please read the CVAT manual:"https://opencv.github.io/cvat/docs/manual/" for more details.
