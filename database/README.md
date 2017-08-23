**Database Folder**
===================
This folder was created to be a storage place for the database in your **Docker Development Environment**

----------

Description
-------------
When your website is created and all the scripts executed, the database in your **"MariaDB"** container will be synchronized with this folder by a **"cron"** job that will be running inside the container. This **"cron"** job will execute every minute. 

> **Note:**
> 
> If you have just made changes to your database, it would be advisable to wait for, at list, 2 minutes before stopping your container. This will give enough time for **"cron"** to synchronize your **"MariaDB"** Docker Container database with this backup folder.