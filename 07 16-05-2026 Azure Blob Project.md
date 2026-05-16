# Azure Blob Storage Static Website Demo with Azure VM (Linux)

This project demonstrates how to:

* Upload and maintain object storage using Microsoft Azure Blob Storage
* Configure public blob access
* Upload images to Blob Storage
* Host a simple HTML webpage on an Azure Linux VM
* Display images directly from Blob Storage inside a webpage

---

# 📌 Architecture Overview

```text
Azure Blob Storage  --->  Stores cat.jpg
        |
        v
Azure Linux VM (Apache Web Server)
        |
        v
Browser Access via Public IP
```

---

# 📌 Step 1 — Create Resource Group

Go to:

```text
Azure Portal → Resource Groups → Create
```

Example:

| Setting             | Value           |
| ------------------- | --------------- |
| Resource Group Name | rg-storage-demo |
| Region              | Central India   |

Click:

```text
Review + Create
```

---

# 📌 Step 2 — Create Storage Account

Go to:

```text
Azure Portal → Storage Accounts → Create
```

Example Configuration:

| Setting              | Value                 |
| -------------------- | --------------------- |
| Resource Group       | rg-storage-demo       |
| Storage Account Name | mystorageaccount98600 |
| Performance          | Standard              |
| Redundancy           | LRS                   |
| Primary Service      | Blob Storage          |
| Access Tier          | Hot                   |

Click:

```text
Review + Create
```

---

# 📌 Step 3 — Open Storage Browser

Navigate to:

```text
Storage Account → Storage Browser
```

---

# 📌 Step 4 — Create Blob Container

Go to:

```text
Blob Containers → + Container
```

Example:

| Setting             | Value       |
| ------------------- | ----------- |
| Container Name      | mycontainer |
| Public Access Level | Private     |

Click:

```text
Create
```

---

# 📌 Step 5 — Open Container

Click:

```text
mycontainer
```

---

# 📌 Step 6 — Upload Image

Upload:

```text
cat.jpg
```

---

# 📌 Step 7 — Copy Blob URL

After upload:

```text
Click File → Copy URL
```

Example URL:

```text
https://mystorageaccount98600.blob.core.windows.net/mycontainer/cat.jpg
```

---

# 📌 Step 8 — Test Blob URL

Paste the URL in browser:

```text
https://mystorageaccount98600.blob.core.windows.net/mycontainer/cat.jpg
```

Initially it may show:

```text
Public access is not permitted
```

---

# 📌 Step 9 — Enable Anonymous Blob Access

Go to:

```text
Storage Account → Settings → Configuration
```

Enable:

```text
Allow Blob Anonymous Access = Enabled
```

Save changes.

---

# 📌 Step 10 — Change Container Access Level

Go to:

```text
Container → Change Access Level
```

Change:

```text
Private  →  Blob
```

Now access the image again:

```text
https://mystorageaccount98600.blob.core.windows.net/mycontainer/cat.jpg
```

The image should load successfully.

---

# 📌 Step 11 — Launch Azure Linux VM

Go to:

```text
Azure Portal → Virtual Machines → Create
```

Example Configuration:

| Setting        | Value        |
| -------------- | ------------ |
| VM Name        | vm-web-demo  |
| OS             | Ubuntu Linux |
| Authentication | SSH Key      |
| Username       | atul         |

---

## 📌 NSG Rules

Allow:

| Port | Purpose |
| ---- | ------- |
| 22   | SSH     |
| 80   | HTTP    |
| 443  | HTTPS   |

---

# 📌 Step 12 — Connect to Azure VM

On Mac/Linux Terminal:

```bash
cd Downloads

chmod 400 key.pem

ssh -i key.pem atul@104.42.79.108
```

---

# 📌 Step 13 — Install Apache Web Server

Run:

```bash
sudo apt update -y

sudo apt install apache2 -y

sudo systemctl start apache2

sudo systemctl enable apache2
```

---

# 📌 Step 14 — Configure Web Directory

Run:

```bash
chmod 755 /var/www/html

cd /var/www/html

sudo rm index.html

sudo nano index.html

sudo touch index.html
```

---

# 📌 Step 15 — Add HTML Code

Paste the following content inside:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Azure Blob Image Demo</title>

    <style>
        body {
            margin: 0;
            padding: 0;
            font-family: Arial, sans-serif;
            background-color: #f4f6f9;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
        }

        .container {
            background: white;
            padding: 20px;
            border-radius: 12px;
            box-shadow: 0 4px 10px rgba(0,0,0,0.1);
            text-align: center;
            width: 500px;
        }

        h1 {
            color: #0078D4;
        }

        img {
            width: 100%;
            border-radius: 10px;
            margin-top: 15px;
        }

        p {
            color: #555;
        }
    </style>
</head>
<body>

    <div class="container">
        <h1>Azure Blob Storage Image</h1>

        <p>Image loaded from Azure Blob Storage</p>

        <img 
            src="https://mystorageaccount98600.blob.core.windows.net/mycontainer/cat.jpg" 
            alt="Cat Image"
        />
    </div>

</body>
</html>
```

Save file:

```text
CTRL + O → ENTER → CTRL + X
```

---

# 📌 Step 16 — Verify Apache Service

Check status:

```bash
sudo systemctl status apache2
```

---

# 📌 Step 17 — Check Azure VM Public IP

From Azure Portal:

```text
Virtual Machine → Overview → Public IP Address
```

Example:

```text
104.42.79.108
```

---

# 📌 Step 18 — Access Website

Open browser:

```text
http://104.42.79.108/
```

You should see:

* Azure Blob Storage Image Demo
* Image loaded directly from Blob Storage

---

# 📌 Final Outcome

Successfully completed:

✅ Azure Blob Storage setup
✅ Public Blob Access configuration
✅ Blob Container creation
✅ Image upload and management
✅ Azure Linux VM deployment
✅ Apache Web Server installation
✅ Static website hosting
✅ Blob image integration with HTML webpage

---

# 📌 Key Learning Concepts

* Object Storage using Azure Blob Storage
* Public vs Private Blob Access
* Storage Containers
* Azure VM Networking
* NSG Rules
* Linux VM Administration
* Apache Web Server Setup
* Static Website Hosting
* Integrating Cloud Storage with Web Applications
