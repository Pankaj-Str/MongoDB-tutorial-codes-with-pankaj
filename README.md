# MongoDB Getting Started

## Getting Started with MongoDB

### Introduction

MongoDB is a popular NoSQL database known for its flexibility and scalability. In this tutorial, we will guide you through the installation and setup process of MongoDB on your machine.

### Prerequisites

* A computer running Windows, macOS, or Linux.
* Administrative privileges to install software.

### Step 1: Download MongoDB

1. **Visit the MongoDB Download Page:**
   * Go to the official MongoDB website: [MongoDB Download Center](https://www.mongodb.com/try/download/community).
2. **Select the Version:**
   * Choose the latest version of MongoDB Community Server. It is recommended to select the version compatible with your operating system.
3. **Choose the Package:**
   * Select the appropriate package for your operating system:
     * **Windows:** MSI package.
     * **macOS:** DMG package.
     * **Linux:** Tarball or DEB/RPM package, depending on your distribution.
4. **Download the Installer:**
   * Click on the "Download" button to start downloading the installer.

### Step 2: Install MongoDB

#### For Windows:

1. **Run the Installer:**
   * Locate the downloaded `.msi` file and double-click to run it.
2. **Choose Setup Type:**
   * Select “Complete” for a full installation.
3. **Service Configuration:**
   * Choose to run MongoDB as a Service. Leave the default settings to start MongoDB automatically.
4. **Install:**
   * Click on the “Install” button to proceed. Once installed, click “Finish.”
5. **Add MongoDB to the PATH:**
   * Open the command prompt and type `mongo --version` to check if MongoDB is in your PATH. If it isn’t, add it manually.

#### For macOS:

1. **Run the Installer:**
   * Locate the downloaded `.dmg` file and double-click to mount it.
2. **Drag and Drop:**
   * Drag the MongoDB icon to the Applications folder.
3. **Create Data Directory:**
   *   Open the terminal and create a data directory for MongoDB:

       ```bash
       mkdir -p /data/db
       ```
4. **Set Permissions:**
   *   Set permissions for the data directory:

       ```bash
       sudo chown -R `id -u` /data/db
       ```
5. **Start MongoDB:**
   *   In the terminal, start MongoDB with the following command:

       ```bash
       mongod
       ```

#### For Linux:

1.  **Import the Public Key:**

    ```bash
    wget -qO - https://www.mongodb.org/static/pgp/server-<version>.asc | sudo apt-key add -
    ```
2.  **Create the `/etc/apt/sources.list.d/mongodb-org-<version>.list` File:**

    ```bash
    echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu focal/mongodb-org/<version>/multiverse amd64 Packages" | sudo tee /etc/apt/sources.list.d/mongodb-org-<version>.list
    ```
3.  **Update the Package Database:**

    ```bash
    sudo apt-get update
    ```
4.  **Install MongoDB:**

    ```bash
    sudo apt-get install -y mongodb-org
    ```
5.  **Start MongoDB:**

    ```bash
    sudo systemctl start mongod
    ```
6.  **Enable MongoDB on Boot:**

    ```bash
    sudo systemctl enable mongod
    ```

### Step 3: Verify Installation

1. **Open a New Terminal/Command Prompt:**
   *   Type the following command to start the MongoDB shell:

       ```bash
       mongo
       ```
2. **Check MongoDB Version:**
   * You should see the MongoDB shell starting with version information. If you see this, MongoDB is successfully installed!

### Step 4: Basic MongoDB Commands

Now that MongoDB is installed, you can start using it with some basic commands:

*   **Show Databases:**

    ```javascript
    show dbs
    ```
*   **Create a Database:**

    ```javascript
    use myDatabase
    ```
*   **Insert Data:**

    ```javascript
    db.myCollection.insert({ name: "Pankaj", age: 25 })
    ```
*   **Find Data:**

    ```javascript
    db.myCollection.find()
    ```

### Conclusion

Congratulations! You have successfully installed MongoDB on your system and are ready to start building applications. In future tutorials, we will explore MongoDB features, including CRUD operations and advanced querying.

Feel free to reach out with any questions or for further guidance!

***
