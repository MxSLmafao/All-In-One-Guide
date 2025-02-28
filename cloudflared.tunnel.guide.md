#Cloudflare Ubuntu CLI Guide
This guide covers **all essential Cloudflared commands**, including creating, running, managing, and deleting tunnels.

---

## **📌 1. Install Cloudflared**
### **Ubuntu Installation**
```bash
curl -fsSL https://github.com/cloudflare/cloudflared/releases/latest/download/cloudflared-linux-amd64 -o /usr/local/bin/cloudflared
chmod +x /usr/local/bin/cloudflared
cloudflared --version  # Verify installation
```

---

## **📌 2. Authenticate with Cloudflare**
```bash
cloudflared tunnel login
```
- This opens a browser window where you **authorize Cloudflare access** to your account.

---

## **📌 3. Create a New Tunnel**
```bash
cloudflared tunnel create <TUNNEL_NAME>
```
Example:
```bash
cloudflared tunnel create my-tunnel
```
- This creates a tunnel and generates a **tunnel ID**.
- Credentials are saved in:
  ```plaintext
  ~/.cloudflared/<TUNNEL_ID>.json
  ```

---

## **📌 4. Configure the Tunnel**
### **Create/Edit Config File**
```bash
nano ~/.cloudflared/config.yml
```
#### **Example Configuration:**
```yaml
tunnel: <TUNNEL_ID>
credentials-file: /home/ubuntu/.cloudflared/<TUNNEL_ID>.json

ingress:
  - hostname: example.com
    service: http://localhost:8080
  - service: http_status:404
```
- Replace **example.com** with your actual domain.
- Replace **localhost:8080** with your service.

---

## **📌 5. Link a Domain to the Tunnel**
```bash
cloudflared tunnel route dns <TUNNEL_ID> <DOMAIN>
```
Example:
```bash
cloudflared tunnel route dns 7cfcfa33-e4c0-4377-9fcc-9c8cfc6db94f example.com
```

### **Verify the DNS Route**
```bash
cloudflared tunnel route dns
```

---

## **📌 6. Start the Tunnel**
### **Manually Run the Tunnel**
```bash
cloudflared tunnel run <TUNNEL_NAME>
```
OR with a specific **config file**:
```bash
cloudflared tunnel --config ~/.cloudflared/config.yml run <TUNNEL_NAME>
```

---

## **📌 7. Stop the Tunnel**
If running manually, use:
```bash
CTRL + C
```

If running as a system service:
```bash
sudo systemctl stop cloudflared
```

---

## **📌 8. Run the Tunnel as a Background System Service**
To make the tunnel start automatically at boot:
```bash
sudo cloudflared service install
sudo systemctl enable cloudflared
sudo systemctl start cloudflared
```

### **Check Service Status**
```bash
systemctl status cloudflared
```

### **Restart Service**
```bash
sudo systemctl restart cloudflared
```

### **View Logs**
```bash
journalctl -u cloudflared -f
```

---

## **📌 9. List Active Tunnels**
```bash
cloudflared tunnel list
```

---

## **📌 10. Remove a DNS Route**
```bash
cloudflared tunnel route dns delete <TUNNEL_ID> <DOMAIN>
```
Example:
```bash
cloudflared tunnel route dns delete 7cfcfa33-e4c0-4377-9fcc-9c8cfc6db94f example.com
```

---

## **📌 11. Delete a Tunnel**
### **Remove the Tunnel from Cloudflare**
```bash
cloudflared tunnel delete <TUNNEL_ID>
```
Example:
```bash
cloudflared tunnel delete 7cfcfa33-e4c0-4377-9fcc-9c8cfc6db94f
```

### **Remove Credentials**
```bash
rm ~/.cloudflared/<TUNNEL_ID>.json
```

### **Remove Systemd Service (If Used)**
```bash
sudo systemctl stop cloudflared
sudo systemctl disable cloudflared
sudo rm /etc/systemd/system/cloudflared.service
sudo systemctl daemon-reload
```

---

## **📌 12. Useful Debugging Commands**
### **Check Logs**
```bash
journalctl -u cloudflared -f
```
or
```bash
cloudflared tunnel log
```

### **Check Cloudflare Tunnel Connection**
```bash
cloudflared tunnel info <TUNNEL_ID>
```

### **Resolve DNS Issues**
```bash
dig example.com
```
or
```bash
nslookup example.com
```

---

## **📌 13. Advanced: Run Multiple Tunnels**
If you want to run multiple tunnels, **create separate config files**:
```bash
nano ~/.cloudflared/tunnel1.yml
nano ~/.cloudflared/tunnel2.yml
```
Then, start each one manually:
```bash
cloudflared tunnel --config ~/.cloudflared/tunnel1.yml run tunnel1 &
cloudflared tunnel --config ~/.cloudflared/tunnel2.yml run tunnel2 &
```
Or, set them as **systemd services**.

---

### **✅ Now You Know All Cloudflared Commands! 🚀**
This guide covers **installation, linking, running, stopping, deleting, debugging, and advanced setups**.
