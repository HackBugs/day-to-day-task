> # Aapko RHEL ke liye `x64` architecture ke liye suitable package download karna hoga, kyunki RHEL (Red Hat Enterprise Linux) x64 architecture pe kaafi commonly chalti hai. Yaha options ke basis pe:

### **Recommended Download Options:**

1. **Compressed Archive (Manual Installation):**  
   Agar aap zip file se manually install karna chahte hain, to ye download karein:
   - **File:** `jdk-23_linux-x64_bin.tar.gz`  
   - **Link:** [Download Compressed Archive](https://download.oracle.com/java/23/latest/jdk-23_linux-x64_bin.tar.gz)  

2. **RPM Package (Simpler Installation):**  
   Agar aap RPM package prefer karte hain (jo ki RHEL aur CentOS ke liye asaan hai), to ye download karein:
   - **File:** `jdk-23_linux-x64_bin.rpm`  
   - **Link:** [Download RPM Package](https://download.oracle.com/java/23/latest/jdk-23_linux-x64_bin.rpm)

---

### **Kya Choose Karein?**
- **Compressed Archive (`tar.gz`)**: Agar aap manually Java ko `/opt/` folder me install aur configure karna chahte hain.
- **RPM Package:** Agar aap chahte hain ki Java automated tarike se install ho jaye (zyada commands ki zarurat nahi). RPM package ko `sudo rpm` ya `sudo dnf install` ke through install karte hain.

---

### **Installation Steps (After Download)**

#### **1. Compressed Archive (`tar.gz`) Installation**
1. File ko download karein aur `/opt/` directory me move karein:
   ```bash
   sudo mv jdk-23_linux-x64_bin.tar.gz /opt/
   ```
2. Extract karein:
   ```bash
   cd /opt/
   sudo tar -xvzf jdk-23_linux-x64_bin.tar.gz
   ```
3. Environment variables set karein:
   ```bash
   echo "export JAVA_HOME=/opt/jdk-23" | sudo tee -a /etc/profile
   echo "export PATH=$JAVA_HOME/bin:$PATH" | sudo tee -a /etc/profile
   source /etc/profile
   ```
4. Verify installation:
   ```bash
   java -version
   ```

---

#### **2. RPM Package Installation**
1. File ko download karein aur install karein:
   ```bash
   sudo dnf install ./jdk-23_linux-x64_bin.rpm
   ```
2. Verify installation:
   ```bash
   java -version
   ```

<hr>

> # JBoss (ab WildFly ke naam se jaana jata hai) ko manually zip file se install karne ya RPM package se configure karne ke liye aap niche diye gaye steps follow kar sakte hain. Pehle aapko JBoss ka compatible version download karna hoga.  

---

### **JBoss (WildFly) Download Options**
WildFly ka latest stable version download karna recommended hai.  
1. **Compressed Archive (Manual Installation)**:  
   - **File:** `wildfly-<version>.Final.zip`  
   - **Link:** [Download WildFly (JBoss) Compressed Archive](https://www.wildfly.org/downloads/)  

2. **RPM Package (Simpler Installation)**:  
   Agar aapko compressed archive chhodkar RPM prefer karna hai, to `jboss.org` ka RPM repository configure karke RPM package install kar sakte hain.

---

### **JBoss Installation Steps**

#### **1. Compressed Archive (`.zip`) Installation**
1. File ko download karein aur `/opt/` me move karein:  
   ```bash
   sudo mv wildfly-<version>.Final.zip /opt/
   ```
2. Extract karein:  
   ```bash
   cd /opt/
   sudo unzip wildfly-<version>.Final.zip
   ```
3. Directory rename karein for simplicity:
   ```bash
   sudo mv wildfly-<version>.Final wildfly
   ```

4. WildFly ko start karne ke liye `standalone.sh` script chalayein:
   ```bash
   /opt/wildfly/bin/standalone.sh
   ```
   Ye script JBoss ko default HTTP port `8080` par start karegi.

5. Web browser me access karein:
   - URL: `http://<your-server-ip>:8080`

6. Environment variables set karein (optional):
   ```bash
   echo "export JBOSS_HOME=/opt/wildfly" | sudo tee -a /etc/profile
   echo "export PATH=$JBOSS_HOME/bin:$PATH" | sudo tee -a /etc/profile
   source /etc/profile
   ```

---

#### **2. RPM Package Installation**
1. JBoss ke official RPM repository ko configure karein:
   ```bash
   sudo curl -o /etc/yum.repos.d/jboss.repo https://www.jboss.org/downloads/jboss.repo
   ```

2. WildFly install karein:
   ```bash
   sudo dnf install wildfly
   ```

3. WildFly service start karein:
   ```bash
   sudo systemctl start wildfly
   ```

4. WildFly ko browser me access karein:
   - URL: `http://<your-server-ip>:8080`

---

### **Important Notes**
1. **Default Ports**:  
   WildFly default ports HTTP ke liye `8080` aur management console ke liye `9990` use karta hai.
   
2. **Admin User Setup**:  
   Agar aapko admin user add karna hai, to ye command use karein:  
   ```bash
   /opt/wildfly/bin/add-user.sh
   ```

3. **Service Enable Karna (Systemd)**:
   Agar aap chahte hain ki WildFly boot ke time automatically start ho:
   ```bash
   sudo systemctl enable wildfly
   ```

---
