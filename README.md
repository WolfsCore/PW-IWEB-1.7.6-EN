# iWeb Backend Setup Guide

This guide explains how to set up the backend environment for the iWeb application, including Java installation, database setup, configuration, and deployment.

---

## Step 1: Install JDK 1.8

1. Copy `jdk1.8.0_301.tar.gz` to the `/usr/java` directory (create it if it doesn’t exist):

   ```bash
   mkdir -p /usr/java
   cp jdk1.8.0_301.tar.gz /usr/java
   cd /usr/java
   tar -xvf jdk1.8.0_301.tar.gz
   ```

2. Edit `/etc/profile` and add the following lines:

   ```bash
   sudo nano /etc/profile
   ```

   ```bash
   JAVA_HOME=/usr/java/jdk1.8.0_301
   JRE_HOME=$JAVA_HOME/jre
   CLASS_PATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar:$JRE_HOME/lib
   PATH=$PATH:$JAVA_HOME/bin:$JRE_HOME/bin
   export JAVA_HOME JRE_HOME CLASS_PATH PATH
   ```

3. Apply the changes:

   ```bash
   source /etc/profile
   ```

4. Verify installation:

   ```bash
   java -version
   ```

---

## Step 2: Import the Database

1. Use a database tool like **Navicat** to import the `wm.sql` file into your MySQL server.
2. The `adminuser` table contains admin login information.

---

## Step 3: Configure Application

1. Open `iweb176.jar` with **WinRAR** (do not extract it).
2. Navigate to: `BOOT-INF\classespplication.yml`.
3. Edit the database and SSH configuration:

   ```yaml
   datasource:
     username: root
     password: 123456
     url: jdbc:mysql://127.0.0.1:3306/wm?useUnicode=true&characterEncoding=utf-8&useSSL=false&serverTimezone=UTC
     driver-class-name: com.mysql.jdbc.Driver

   ssh_host: 127.0.0.1
   ssh_username: root
   ssh_password: P88T8J73ms7kfL3b@
   ssh_port: 22
   db_user: root
   db_password: 123456
   db_database: wm
   ```

4. Save the file. Confirm the update in WinRAR when prompted.

---

## Step 4: Deploy Backend

1. Create a deployment folder and upload the required files:

   ```bash
   mkdir -p /home/iweb
   # Upload start.sh, iweb176.jar, and the elconfigs folder
   ```

2. Set permissions:

   ```bash
   chmod -R 777 /home/iweb
   ```

3. Start the backend:

   ```bash
   ./start.sh start
   ```

4. Stop the backend:

   ```bash
   ./start.sh stop
   ```

---

## Access Backend

- URL: [http://127.0.0.1:9898](http://127.0.0.1:9898)
- Default admin credentials:
  - **Username:** `admin`
  - **Password:** `123123`

---

## Notes

- SSH credentials are necessary if remote access is required for features like map integration.
- Ensure the configuration reflects your actual database and server settings.

---

## License

This project is intended for internal use or educational purposes. Contact the maintainer for licensing options.
