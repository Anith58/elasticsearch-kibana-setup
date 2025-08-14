# 🚀 Fleet Server Installation Guide (Ubuntu)

This guide walks you through installing and configuring **Fleet Server** on your Ubuntu Server, integrating with your existing Elasticsearch and Kibana setup.

---

## 📥 Step 1: Download Elastic Agent (with Fleet support)

```bash
wget https://artifacts.elastic.co/downloads/beats/elastic-agent/elastic-agent-9.1.0-amd64.deb
```

---

## 🛠️ Step 2: Install the Elastic Agent

```bash
sudo dpkg -i elastic-agent-9.1.0-amd64.deb
```

---

## 🔐 Step 3: Generate Fleet Enrollment Token from Kibana

1. Open **Kibana UI**.
2. Go to **Management → Fleet → Agents → Add Agent**.
3. Select **"Enroll in Fleet"**.
4. Click **"Generate enrollment token"**.
5. Copy the **Enrollment Token** and save it in Notepad.

---

## 🧾 Step 4: Copy the Fleet Server Command

Kibana will show a prebuilt command like this:

```bash
sudo ./elastic-agent install \
  --fleet-server-es=https://<your-elasticsearch-ip>:9200 \
  --fleet-server-service-token=<TOKEN> \
  --fleet-server-policy=<POLICY-ID> \
  --certificate-authorities=<path-to-ca.crt>
```

> ⚠️ **Important:** Adjust IPs, token, policy, and cert paths as needed.

---

## ▶️ Step 5: Run the Fleet Server Install Command

```bash
sudo ./elastic-agent install [options from step above]
```

- Agent will install and enroll with Kibana’s Fleet system.

---

## ✅ Step 6: Verify Agent Connection in Kibana

- Go to **Kibana → Fleet → Agents**.
- You should see the **Fleet Server** status as healthy.

---

### 🎯 Fleet Server Installed Successfully by **Anith C**

