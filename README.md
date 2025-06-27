## ✅ **Outcome Report: Nessus Essentials Vulnerability Scanner Setup**

### 🧩 **Task Objective:**

To install and use **Nessus Essentials** (v10.8.4) to perform a **basic vulnerability scan** on the local system and understand how vulnerabilities are identified in real-world environments.

---

### ⚙️ **Process Overview:**

#### 📥 1. **Download & Install**

* Downloaded Nessus `.deb` package using `curl`:

  ```bash
  curl -O 'https://www.tenable.com/downloads/api/v2/pages/nessus/files/Nessus-10.8.4-ubuntu1604_amd64.deb'
  ```
* Installed Nessus:

  ```bash
  sudo dpkg -i Nessus-10.8.4-ubuntu1604_amd64.deb
  sudo apt --fix-broken install
  ```

#### 🔄 2. **Service Configuration**

* Started and enabled Nessus service:

  ```bash
  sudo systemctl start nessusd
  sudo systemctl enable nessusd
  ```

#### 🌐 3. **Web Interface Access**

* Opened Nessus in browser at `https://localhost:8834`
* Attempted initial setup and activation using Nessus Essentials license

---

### ❌ **Issue Encountered: Plugin Download Failure**

* **Error Message:**

  ```
  [error] Nessus Plugins: Did not get a 200 OK response from the server: HTTP/1.1 400 Bad Request
  ```
* Cause:

  * Plugin feed request rejected
  * Possibly due to:

    * Invalid/expired activation key
    * Network/firewall restrictions
    * Corrupt or stale plugin cache

---

### 🛠️ **Troubleshooting Steps Performed**

1. **Unregistered Nessus and removed cached data:**

   ```bash
   sudo /opt/nessus/sbin/nessuscli fetch --unregister
   sudo rm -rf /opt/nessus/var/nessus/*
   ```

2. **Re-attempted registration with correct OS info:**

   ```bash
   sudo /opt/nessus/sbin/nessuscli fetch --register <ACTIVATION-CODE> --os ubuntu1604 --accept-eula
   ```

3. **Validated connectivity to plugin servers:**

   ```bash
   curl -I https://plugins.nessus.org
   ```

---

### ✅ **Current Status:**

* Nessus is installed and service is running
* Plugins failed to download due to HTTP 400 error
* Awaiting successful registration and plugin download to begin scan
