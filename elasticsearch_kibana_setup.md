# 🛡️ Elasticsearch + Kibana Lab Setup Guide

This guide documents the step-by-step process to install, configure, and secure Elasticsearch and Kibana on an Ubuntu Server. Ideal for SOC lab setups and cybersecurity learning.

---

## 🔧 Step 1: Download Ubuntu Server

- **Link**: https://www.elastic.co/downloads/elasticsearch

---

## 🛠️ Step 2: Download Elasticsearch

**Link**: [https://www.elastic.co/downloads/kibana](https://www.elastic.co/downloads/kibana)
```bash
wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-9.1.0-amd64.deb
```

---

## 🛠️ Step 3: Install Elasticsearch

```bash
sudo dpkg -i elasticsearch-9.1.0-amd64.deb
```

---

## 🔒 Step 4: Save Security Autoconfiguration Output

After installation, Elasticsearch will display a message with a superuser password and configuration tips. **Copy and save** this entire message to a file (e.g., `elasticsearch_config.txt`).

---

## 📝 Step 5: Edit Elasticsearch Config

```bash
cd /etc/elasticsearch/
sudo nano elasticsearch.yml
```

- Uncomment and set `network.host` to your Ubuntu server IP
- Uncomment `http.port` and ensure it is `9200`

---

## ▶️ Step 6: Start and Enable Elasticsearch

```bash
sudo systemctl daemon-reload
sudo systemctl enable elasticsearch.service
sudo systemctl start elasticsearch.service
sudo systemctl status elasticsearch.service
```

---

## 🖥️ Step 7: Download Kibana

- **Link**: [https://www.elastic.co/downloads/kibana](https://www.elastic.co/downloads/kibana)

```bash
wget https://artifacts.elastic.co/downloads/kibana/kibana-9.1.0-amd64.deb
```

---

## 🛠️ Step 8: Install Kibana

```bash
sudo dpkg -i kibana-9.1.0-amd64.deb
```

---

## ⚙️ Step 9: Edit Kibana Config

```bash
sudo nano /etc/kibana/kibana.yml
```

- Uncomment and set `server.port: 5601`
- Uncomment and set `server.host: <your-ubuntu-server-ip>`

---

## ▶️ Step 10: Start and Enable Kibana

```bash
sudo systemctl daemon-reload
sudo systemctl enable kibana.service
sudo systemctl start kibana.service
sudo systemctl status kibana.service
```

---

## 🔐 Step 11: Generate Kibana Enrollment Token

```bash
cd /usr/share/elasticsearch/bin
./elasticsearch-create-enrollment-token --scope kibana
```

- Copy the token and save it in Notepad

---

## 🌐 Step 12: Access Kibana via Browser

- URL: `http://<your-server-ip>:5601`
- If connection fails, check:

```bash
sudo systemctl status kibana.service
sudo systemctl status elasticsearch.service
sudo ufw allow 5601
```

---

## 🧾 Step 13: Paste Enrollment Token

- Paste the token from earlier when prompted in browser

---

## 🔑 Step 14: Get Kibana Verification Code

```bash
cd /usr/share/kibana/bin
./kibana-verification-code
```

- Paste the code into the browser

---

## 🔓 Step 15: Login to Kibana Dashboard

- Username: `elastic`
- Password: from security autoconfiguration message
- If needed, reset password:

```bash
/usr/share/elasticsearch/bin/elasticsearch-reset-password -u elastic
```

- To regenerate token:

```bash
/usr/share/elasticsearch/bin/elasticsearch-create-enrollment-token -s kibana
```

---

## 📊 Step 16: Access Kibana Dashboard

- After login, you will see the full Kibana interface

---

## 🚨 Step 17: Check Alerts Section

- Go to **Security → Alerts**
- You will see: "API integration is required"

---

## 🔐 Step 18: Generate Kibana Encryption Keys

```bash
cd /usr/share/kibana/bin
./kibana-encryption-keys generate
```

- Copy all 3 keys and save them

---

## 🔑 Step 19: Add Keys to Kibana Keystore

```bash
cd /usr/share/kibana/bin
./kibana-keystore add <setting-name>
```

- Paste the value when prompted

---

## 🔁 Step 20: Restart Kibana and Verify

```bash
sudo systemctl restart kibana.service
```

- Refresh browser
- Alert warning should be gone

---

### ✅ Setup Completed by **Anith C** 🎯

