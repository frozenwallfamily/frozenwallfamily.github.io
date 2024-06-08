---
layout: post
title:  "Setting Up a Headless Raspberry Pi 4 Running WordPress"
date:   2024-06-09 14:54:55 +1200
categories: jekyll update
---

Sure, here's a detailed blog post on setting up a headless Raspberry Pi 4 running WordPress:

---

## Setting Up a Headless Raspberry Pi 4 Running WordPress

The Raspberry Pi 4 is a versatile single-board computer that can be used for a variety of projects, including running a WordPress website. Setting it up in headless mode means you can manage it without needing a direct monitor, keyboard, or mouse connection. Here's a step-by-step guide on how to do it.

### Prerequisites

1. **Raspberry Pi 4**
2. **microSD Card (16GB or larger)**
3. **Power Supply for Raspberry Pi 4**
4. **Ethernet Cable or Wi-Fi Connection**
5. **Computer with SD Card Reader**

### Step 1: Prepare the microSD Card

#### 1.1 Download Raspberry Pi OS

- Download the latest version of Raspberry Pi OS (formerly Raspbian) from the [official Raspberry Pi website](https://www.raspberrypi.org/software/operating-systems/).

#### 1.2 Flash the OS to the microSD Card

- Use a tool like [Balena Etcher](https://www.balena.io/etcher/) to flash the downloaded Raspberry Pi OS image onto your microSD card.

### Step 2: Configure the Raspberry Pi for Headless Operation

#### 2.1 Enable SSH

- After flashing the OS, create a file named `ssh` (without any extension) in the root directory of the microSD card. This enables SSH access.

#### 2.2 Configure Wi-Fi (if not using Ethernet)

- Create a file named `wpa_supplicant.conf` in the root directory of the microSD card with the following content:

  ```
  country=YOUR_COUNTRY_CODE
  ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
  update_config=1

  network={
      ssid="YOUR_SSID"
      psk="YOUR_PASSWORD"
  }
  ```

  Replace `YOUR_COUNTRY_CODE`, `YOUR_SSID`, and `YOUR_PASSWORD` with your Wi-Fi country code, network name, and password, respectively.

### Step 3: Initial Boot and Update

- Insert the microSD card into the Raspberry Pi and power it on.
- Find the Raspberry Pi's IP address using a network scanning tool or by checking your router’s connected devices list.
- Connect to the Raspberry Pi via SSH:
  
  ```sh
  ssh pi@<Raspberry_Pi_IP_Address>
  ```

  The default password is `raspberry`.

- Update the package list and upgrade all packages:

  ```sh
  sudo apt update
  sudo apt upgrade -y
  ```

### Step 4: Install the LAMP Stack

#### 4.1 Install Apache

  ```sh
  sudo apt install apache2 -y
  ```

  Verify Apache installation by visiting the Raspberry Pi’s IP address in a web browser. You should see the Apache2 default page.

#### 4.2 Install MySQL

  ```sh
  sudo apt install mariadb-server -y
  ```

  Secure the MySQL installation:

  ```sh
  sudo mysql_secure_installation
  ```

  Follow the prompts to set the root password and secure the installation.

#### 4.3 Install PHP

  ```sh
  sudo apt install php libapache2-mod-php php-mysql -y
  ```

### Step 5: Install WordPress

#### 5.1 Download and Extract WordPress

  ```sh
  cd /var/www/html
  sudo wget https://wordpress.org/latest.tar.gz
  sudo tar -xzvf latest.tar.gz
  sudo rm latest.tar.gz
  sudo mv wordpress/* .
  sudo rmdir wordpress
  ```

#### 5.2 Set Permissions

  ```sh
  sudo chown -R www-data:www-data /var/www/html
  sudo chmod -R 755 /var/www/html
  ```

#### 5.3 Configure WordPress

- Create a WordPress database:

  ```sh
  sudo mysql -u root -p
  ```

  Inside the MySQL shell, run:

  ```sql
  CREATE DATABASE wordpress;
  CREATE USER 'wp_user'@'localhost' IDENTIFIED BY 'password';
  GRANT ALL PRIVILEGES ON wordpress.* TO 'wp_user'@'localhost';
  FLUSH PRIVILEGES;
  EXIT;
  ```

- Rename the sample configuration file:

  ```sh
  cd /var/www/html
  sudo mv wp-config-sample.php wp-config.php
  ```

- Edit `wp-config.php` with your database information:

  ```sh
  sudo nano wp-config.php
  ```

  Update the following lines with your database name, user, and password:

  ```php
  define('DB_NAME', 'wordpress');
  define('DB_USER', 'wp_user');
  define('DB_PASSWORD', 'password');
  define('DB_HOST', 'localhost');
  ```

### Step 6: Finalize the Installation

- Open a web browser and navigate to `http://<Raspberry_Pi_IP_Address>`.
- Follow the on-screen instructions to complete the WordPress setup.

### Conclusion

You now have a headless Raspberry Pi 4 running a fully functional WordPress site. This setup is ideal for a small personal blog or a test environment. For a production site, consider additional security measures and regular backups.

Happy blogging!

---

Feel free to adjust any steps based on your specific needs or network configuration.
