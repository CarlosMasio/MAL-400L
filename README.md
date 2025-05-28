# MAL-400L

**MAL-400L** is a real-time, system-wide malware and payload monitoring tool built on top of [`malprotocol.py`](https://github.com/CarlosMasio/Mal-Protocol). It continuously scans for new files created anywhere on the system, analyzes them using pattern-matching and signature logic, and automatically deletes malicious files upon detection.

> Designed for ethical hacking, red teamers, malware analysts, and power users who want automated file-level protection in real-time.

---

## 🔧 Features

- 🛡️ Automatic detection & deletion of malicious files
- 🔍 Monitors the **entire filesystem**
- 🧠 Smart exclusions (system folders, symbolic links, unreadable files)
- ⚙️ Systemd service for background automation
- 🐍 Python-based, lightweight and fast

---

## 🛠️ Install Dependencies

```bash
sudo apt update
sudo apt install binwalk exiftool p7zip-full python3-requests -y
````

---

## 📥 Installation

```bash
git clone https://github.com/CarlosMasio/MAL-400L.git
cd MAL-400L
```

---

## 🐍 Python Setup (Virtual Environment Recommended)

```bash
python3 -m venv myenv
source myenv/bin/activate
pip3 install -r requirements.txt
```

> ✅ Ensure `malprotocol.py` is working and tested manually before using this tool.

---

## ⚙️ Configure File Path for `malprotocol.py`

Open the monitor script:

```bash
nano mal_monitor.py
```

Then **edit line 23** (or wherever defined) to set your path:

```python
MALPROTOCOL_PATH = "/file/path/to/MAL-400L/malprotocol.py"
```

Save and exit.

---

## 🔓 Make the Script Executable

```bash
chmod +x mal_monitor.py
```

---

## 🚀 Run Manually

```bash
python3 mal_monitor.py
```

---

## 🌀 Optional: Setup Systemd for Background Monitoring

### 1. Create a service file

```bash
sudo nano /etc/systemd/system/mal400l.service
```

### 2. Paste this content (replace paths accordingly)

```ini
[Unit]
Description=MalProtocol Background Monitor
After=network.target

[Service]
Type=simple
User=kali
WorkingDirectory=/your/path/to/MAL-400L
ExecStart=/usr/bin/python3 /your/path/to/MAL-400L/mal_monitor.py
Restart=always
RestartSec=5

[Install]
WantedBy=multi-user.target
```

### 3. Enable and start the service

```bash
sudo systemctl daemon-reload
sudo systemctl enable mal400l.service
sudo systemctl start mal400l.service
```

### 4. Check service status

```bash
sudo systemctl status mal400l.service
```

---

## 📁 Directory Structure

```
MAL-400L/
├── mal_monitor.py          # Main scanner script
├── requirements.txt        # Python dependencies (if any)
└── README.md               # This file
```

---

## 🧪 Testing

To verify that scanning works:

1. Drop a known malicious `.exe`, `.apk`, or `.zip` into any folder.
2. The script should automatically:

   * Detect the file
   * Scan it with `malprotocol.py`
   * Print its output
   * Delete if flagged

---

## 📢 Notes

* Make sure `malprotocol.py` has all its dependencies (including `yara-python`)
* Logs are printed to the terminal by default (you can redirect output to a file if needed)
* Best run on test machines or inside labs — deleting files is **automatic and irreversible**

---

## 📚 Credits

* [`Mal-Protocol`](https://github.com/CarlosMasio/Mal-Protocol) by CarlosMasio
* Maintained by: [CarlosMasio](https://github.com/CarlosMasio)

---

## 🛡️ Disclaimer

> This tool is for **educational and ethical** use only. The author is not responsible for any misuse or damage caused by this software.

