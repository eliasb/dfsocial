# **How To Drupal 8 Open Social Distribution**

**Description**
-------------

This is a Drupal 8 Development Environment using only the Official Docker Images. This Docker-Compose Project includes **Drupal 8**, **Drupal Console**, **Composer**, **Drush**, and **PHPMyAdmin**. It will also have Volumes configured in a way that will allow you to use your favorite IDE such as **Eclipse PDT**. The HTML files as well as the database are backed up in the folder that you will create for each of your clients.

----------

## **1. Install Docker Toolbox**

If you don't have Docker installed in your computer yet, I'd recommend that you start with Docker Toolbox. This is a set of tools that includes a tool called Kitematic which will make your first experience with Docker much easier. Docker Toolbox is available for Windows or Mac and it will create a small VirtualBox VM that will allow Docker to run in your computer without much hassle.

My first experience with Kitematic was a little disappointing. I felt a little like I was riding a bicycle with soldered training wheels. I was mistaken. Once I got a little more experienced with Docker I realized that I could access the back-end of Kitematic with a Terminal window and use Kitematic in combination with it.

[https://www.docker.com/products/docker-toolbox](https://www.docker.com/products/docker-toolbox)

You will also have to create a Docker account in order to be able to download images from their repository.

[https://cloud.docker.com](https://cloud.docker.com)

## **2. Creating A Workflow**

You can use this Docker project in any way you see fit. However, I have created this project to be a complement to my personal workflow. For this reason, I will explain here how I use this Docker project in my work routine.

The first thing that I did after installing Kitematic was to go to my **"C:\\\Users\\[My User Name]"** folder and create a folder called **"D"** for **"Docker"**. This folder will be the storage place for all my clients. 

Whenever I get a new client, I go the **"D"** folder and create a new folder for that client. I use my client's domain name as the name of that folder. If, for example, my client has a domain name **"example.com"**, I call this client's folder as **"example"**. I could use **".com"** as part of the folder's name but I try to keep this folder name as small as possible. The folder name will be used by Docker when creating the Containers so, keeping this name short will make the container names much more readable. There is also another reason. Windows has a limitation for the length of file paths. The file path cannot be longer than **"256 characters"**. For this reason, keeping the base folder names small should always be at the top of our priorities.

    C:\\Users\[My User Name]\D\example

Now that I have this folder created for my client, I go to the next phase which will be to clone this Docker project with **"Git"**.

## **3. Use Git To Clone This Repo**

First of all, you will have to create an account in GitHub if you don't already have one:

[https://github.com/join?source=header-home](https://github.com/join?source=header-home)

I am coming from the premise that you have installed Docker Toolbox. To clone this repository you should double-click on the **"Docker Quickstart Terminal"** shortcut that should be on your desktop. This will open a Linux like terminal in your Windows or Mac. The terminal window will open up at your home folder. To see in what folder you are located, do the following in the terminal window:

    $ pwd

After typing the above command you should see the following:

     /c/Users/[My User Name]

This just means that you are currently located on your **"C:"** drive and you are inside the folder **"Users/My User Name"** where the **"My User Name"** part should be replaced with the user name you have in your operating system.

If you have been following this tutorial from the beginning, you have created the folder **"D"** in your **"/c/Users/[My User Name]"** folder. So, in order to clone this repository, you will first have to enter into this folder:

    $ cd D

Now, you should be able to see the folder that you have created for your client. You can list the contents of a folder by doing the following:

    $ ls -al

The above command should output the following:

    drwxr-xr-x 1 User Name 197121 0 Jun 21 11:24 ./
    drwxr-xr-x 1 User Name 197121 0 Jul  8 03:30 ../
    drwxr-xr-x 1 User Name 197121 0 Jun 20 16:46 example/

At the end you should see the folder you have created for your client. To enter into this folder you will have to do the following:

    $ cd example

Of course, you should replace the word **"example"** with the name of the folder you created for your own client. Now, just to make sure, we should check where we are to see if we are actually on the right folder:

    $ pwd

The above command should output the following:

    /c/Users/[My User Name]/D/example

Now that we are sure to be in the right location we can finally clone this repository like so:

    $ git clone https://github.com/eliasb/dfdocker.git ./

After issuing the above command you may be prompted to login to your GitHub account. The above command will simply download all the necessary files and folder structure into your client's folder.

Now is time to execute the **docker-compose.yml** file.

## **4. Start The Containers With Docker-Compose**

Now that you have downloaded this repository, you will need to use a tool called **"Docker-Compose"**. This tool will read the **"docker-compose.yml"** file that you just downloaded and it will create all the necessary Docker Containers:

    $ docker-compose up -d

The above command will initiate a long process that should take about 5 minutes to complete on the first time you run it. Just be patient. The above command will execute the following tasks:

 1. Download all the Docker Images necessary
 2. Make a copy of the **"Drupal"** and the **"MariaDB"** images
 3. Install **"Composer"**, **"Drupal Console"**, **"Drush"**, **"Cron"**, and **"RSYNC"** in the new **"Drupal"** image
 4. Install **"Cron"**, and **"RSYNC"** in the new **"MariaDB"** image
 5. Start all containers

## **5. Start Cron**

**"Cron"** is a little program that I installed inside the  **"Drupal"** and the **"MariaDB"** containers. This little program will run a backup of your website and your database. This backup will be located inside your client's folder.

You should always start **"Cron"** every time you start **"Kitematic"**. This will assure that you will have an up to date backup of your website & database. If, God forbid, you accidentally delete the containers, you can always recreate them with "Docker-Compose" but your client's files will be protected.

To run **"Cron"** inside your two containers you should first know the name of these two containers. Docker will issue a name to each container that is composed by the name of your client's folder and the name of the image associated with this container. To find out the name of each of your containers you can simply look at the **"Kitematic"** window. As an alternative you can issue the following command in the terminal window:

    $ docker ps

The above command will output something like the following:

    CONTAINER ID IMAGE     COMMAND    CREATED   STATUS    PORTS    NAMES
    bbcc3039375f drupal... "apache... 2 days... Up Abo... 0.0.0... example_drupal_1
    23ee726d813a phpmya... "/run.s... 2 days... Up Abo... 0.0.0... example_phpmyadmin_1
    08d1192caec0 busybo... "sh"       2 days... Up Abo...          example_data_1
    176b2d5475d4 mariad... "docker... 2 days... Up Abo... 0.0.0... example_mariadb_1

The name of your containers should be at the last column. In my case the **"Drupal"** container was called **"example_drupal_1"** because **"example"** is the name of my client's folder. Consequently, my **"MariaDB"** container is called **"example_mariadb_1"**.

Now that we know the name of your two containers, we can issue the following two commands in order to run **"Cron"** and start the backups.

    $ docker exec -it example_drupal_1 bash /usr/sbin/service cron start
    $ docker exec -it example_mariadb_1 bash /usr/sbin/service cron start

## **6. Installing Drupal 8 From Within Kitematic**

Now you are done with the terminal commands. It is time to switch to the **"Kitematic"** interface.

1. From there you will see on the left-hand-side a list of your running containers. You should click on the container for **"Drupal"** which should have a name similar to **"example_drupal_1"**. You will see a bunch of stuff on the middle window. There is nothing for you to worry about. 
2. Look to the right-hand-side and you will be able to see a small window with a familiar appearance. There should be a small screenshot of a Drupal 8 Installation screen. Click on that small screenshot. This will bring up your default Browser with the first screen for the Drupal 8 installation. 
3. Follow the Standard installation and, when prompted for the Database information you should use the following credentials: 
	- Database Name: **drupal**
	- User Name: **drupal**
	- Password: **drupal**
4.  You should expand the "Advanced" option at the bottom and type the Database Server and Port number. To find out this information you should go back to the **"Kitematic"** interface
5. Click on the **"example_mariadb_1"** container
6. Click on the **"Settings"** tab that should be on the top right-hand-side
7. Now click on the **"Ports"** sub-tab. There you will be able to see the Database **"IP Number"** and the Port Number
8. Copy the **"IP Number"** into the Database Server field and the **"Ports"** number into the database port number
9. Proceed with the rest of the installation as normal

## **7. How To Use Drush, Composer, And Drupal Console**

I am starting from the premise that you have the **"Drupal"** container up and running. You could issue a **"Drush"** or a **"Composer"** command from outside of the container. However, I find that the most convenient way to execute these commands is by entering into the **"Drupal"** container inside a bash terminal. To do that you execute the following command:

    $ docker exec -i -t example_drupal_1 bash

Of course, you should replace the word **"example"** with the correct name of your **"Drupal"** container as I describe on step **"5. Start Cron"**!

## **8. How To Use PHPMyAdmin Within Kitematic**

Using **"PHPMyAdmin"** is very simple. Just follow these steps:

1. Switch to the **"Kitematic"** interface and click on the **"example_phpmyadmin_1"** container.
2. Look to the right-hand-side and you will be able to see a window with a small screenshot of a **"PHPMyAdmin"** login screen. Click on that small screenshot. This will bring up your default Browser with the **"PHPMyAdmin"** login page.
3. Following are the credentials you should supply in order to be able to login to **"PHPMyAdmin"**: 
	- Server: **example_mariadb_1**
	- Username: **root**
	- Password: **root**
4. Now you should have full access to your Databases. Your website database, as you know, will be called **"drupal"**

## **9. How To Create A New Client**

Great! You have your first client set up. But, now, you want to set up a second client. How hard is it?

When you are creating a new client in your computer, you can simply follow all the above steps and everything should work just fine. However, you will have to stop the previously running containers from your clients. There is a simple command that you can execute to stop all the running containers. You will have to execute the following command inside the **"Docker Quickstart Terminal"**:

    docker stop $(docker ps -a -q)

There is only one potential problem. If you plan on running the containers from both clients at the same time, you will not be able to follow exactly the same steps again. Your new client's containers will end up having a conflict with the **Port Numbers**. 

You will have to make a few small changes on the **docker-compose.yml** file. You will have to change the ports for 3 of the containers in order to be able to create your new client's containers. It is very simple, though! Just redo the step **"3. Use Git To Clone This Repo"** inside of your new client's folder. Once you have downloaded this Repository, edit the file **docker-compose.yml** with your favorite text editor.

First you should change the **Port Number** for the **"Drupal"** container. Go to line 19 where you should see the following:

      - "8081:80"

You should replace the number **"8081"** with another number. It can be the next number as long as it doesn't conflict with the port number of any other container. This line should, then, look like the following:

      - "8082:80"
 
Now is time to do the same for the **"MariaDB"** container. Go to line 29 and you will see something like the following:

      - '3307:3306'

Replace the number **"3307"** with another number. This line should, then, look like the following:

      - '3308:3306'

Finally, do the same for the **"PHPMyAdmin"** container. Go to line 45 and you will see something like the following:

      - '8091:80'

Replace the number **"8091"** with another number. This line should, then, look like the following:

      - '8092:80'

Now you can save your changes and continue with step **"4. Start The Containers With Docker-Compose"**. This time around, everything should go much faster. It should take just a couple of seconds for you to have the new containers up and running.

## **10. How To Use Eclipse PDT With This**

Eclipse is an amazing Open Source IDE (Integrated Development Environment). You can install Eclipse PDT by Googling for it and downloading the latest version. It can be a little confusing to figure out which version of Eclipse is the latest. The Eclipse community has the habit of giving names to each new major version instead of numbers. They also tend to develop each one in parallel. In my experience, the best way to know which one is the latest is not by going to their official website. You should, as I suggested, search on Google.

Just remember that there is an Eclipse version for each computer language. The Eclipse PDT is the one for PHP and JavaScript development.

I got the link to the most recent download page. I will not guarantee that this link will be working for very long because this address tends to change with an annoying frequency.

[https://eclipse.org/pdt/#download](https://eclipse.org/pdt/#download)

Once you have Eclipse PDT installed you can create a new project and you should import the files for this project from the folder associated with your client. Select the folder **"doc/html"** inside your client's folder.