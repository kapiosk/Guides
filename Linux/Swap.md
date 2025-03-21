## Adding Swap Space on an Azure VM

### **1. Check if Swap Already Exists**
```bash
sudo swapon --show
free -h
```
If there is no output from `swapon --show`, then swap is not set up.

### **2. Create a Swap File**
Replace `2G` with the desired swap size.
```bash
sudo fallocate -l 2G /swapfile
```
If `fallocate` is not available, use:
```bash
sudo dd if=/dev/zero of=/swapfile bs=1M count=2048
```

### **3. Set Permissions**
```bash
sudo chmod 600 /swapfile
```

### **4. Format as Swap**
```bash
sudo mkswap /swapfile
```

### **5. Enable the Swap File**
```bash
sudo swapon /swapfile
```

### **6. Verify Swap is Active**
```bash
free -h
```

### **7. Make the Swap File Permanent**
Add the following line to `/etc/fstab`:
```bash
echo '/swapfile none swap sw 0 0' | sudo tee -a /etc/fstab
```
