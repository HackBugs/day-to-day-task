> ## **JBoss** application server ko RHEL (Red Hat Enterprise Linux) par install aur configure karne ke liye niche diye gaye steps ko follow karein:

---

### **Step 1: Prerequisites Check Karein**
1. **Java Install Karein**:
   JBoss ko chalane ke liye Java Development Kit (JDK) ka installed aur configured hona zaroori hai. 

   ```bash
   sudo yum install java-11-openjdk-devel
   ```

   Java version confirm karein:
   ```bash
   java -version
   ```

2. **Firewall and Ports Configuration**:
   JBoss default ports (8080, 9990) ko firewall me allow karein:
   ```bash
   sudo firewall-cmd --add-port=8080/tcp --permanent
   sudo firewall-cmd --add-port=9990/tcp --permanent
   sudo firewall-cmd --reload
   ```

---

### **Step 2: JBoss ZIP File Extract Karein**
1. **Download Location Par Navigate Karein**:
   JBoss ZIP file jis folder me downloaded hai, wahan jaayein:
   ```bash
   cd /path/to/downloaded/zip
   ```

2. **Extract ZIP File**:
   ZIP file ko extract karein:
   ```bash
   unzip jboss-eap-*.zip -d /opt/
   ```

   Agar `unzip` command nahi hai, to install karein:
   ```bash
   sudo yum install unzip
   ```

3. **JBoss Folder Rename Karein (Optional)**:
   Extracted folder ko rename karein:
   ```bash
   sudo mv /opt/jboss-eap-* /opt/jboss
   ```

---

### **Step 3: Environment Variable Set Karein**
1. **Java Path Ko Environment Variable Me Add Karein**:
   `/etc/profile` file me edit karein:
   ```bash
   sudo nano /etc/profile
   ```

   Niche lines add karein:
   ```bash
   export JAVA_HOME=/usr/lib/jvm/java-11-openjdk
   export PATH=$JAVA_HOME/bin:$PATH
   ```

2. **JBoss Path Ko Environment Variable Me Add Karein**:
   Us file me ye line bhi add karein:
   ```bash
   export JBOSS_HOME=/opt/jboss
   export PATH=$JBOSS_HOME/bin:$PATH
   ```

3. **Changes Apply Karein**:
   ```bash
   source /etc/profile
   ```

---

### **Step 4: JBoss Start Karein**
1. **Standalone Mode Me Start Karna**:
   Standalone mode ke liye:
   ```bash
   /opt/jboss/bin/standalone.sh
   ```

2. **Domain Mode Me Start Karna**:
   Agar domain mode chahiye:
   ```bash
   /opt/jboss/bin/domain.sh
   ```

3. **JBoss Admin Console Check Karein**:
   - Browser me open karein: `http://<your-server-ip>:9990`.
   - Default admin console available hoga.

---

### **Step 5: User Account Setup Karein (Admin Console Ke Liye)**
1. Admin user create karein:
   ```bash
   /opt/jboss/bin/add-user.sh
   ```

2. Instructions follow karein:
   - User type: `Management User`.
   - Username aur password set karein.
   - Configuration complete hone ke baad, ye admin console ke liye use hoga.

---

### **Step 6: JBoss Ko Background Me Run Karein (Optional)**
1. **SystemD Service Create Karein**:
   Service file banayein:
   ```bash
   sudo nano /etc/systemd/system/jboss.service
   ```

2. Content Add Karein:
   ```bash
   [Unit]
   Description=JBoss Application Server
   After=network.target

   [Service]
   User=root
   ExecStart=/opt/jboss/bin/standalone.sh
   ExecStop=/bin/kill -15 $MAINPID
   Restart=always

   [Install]
   WantedBy=multi-user.target
   ```

3. **Service Enable Aur Start Karein**:
   ```bash
   sudo systemctl daemon-reload
   sudo systemctl enable jboss
   sudo systemctl start jboss
   ```

4. **Status Check Karein**:
   ```bash
   sudo systemctl status jboss
   ```

---

### **Step 7: Verify Installation**
- Check karein ki JBoss sahi se chal raha hai:
  ```bash
  curl http://localhost:8080
  ```

- Agar response mile to iska matlab setup successful hai.

---

- [Doc Jboss Installtion](https://docs.redhat.com/en/documentation/red_hat_jboss_enterprise_application_platform/6.4/html/getting_started_guide/sect-download_and_install_jboss_eap_using_the_graphical_installation_program#Run_the_JBoss_EAP_Installation_Program)
- 
