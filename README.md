

---

# 🚀 Google Cloud Shell Virtual Machine — Full Setup Guide

### (VNC + XFCE Desktop + NoVNC + Firefox)

---

## **1. Open Cloud Shell & Update System**

1. Open Google Cloud Shell (**>_ icon**).
2. Run:

```bash
sudo apt update
```

---

## **2. Install Required Software**

Run:

```bash
sudo apt install -y xfce4 xfce4-goodies tigervnc-standalone-server novnc websockify dbus-x11 software-properties-common
```

---

## **3. Set VNC Password**

1. Start VNC:

```bash
vncserver
```

2. Enter password: **bel@123**

   * Max 8 characters
3. Say **N** for view-only mode.
4. When it finishes, kill the default session:

```bash
vncserver -kill :1
```

---

## **4. Configure VNC Startup File**

Edit the xstartup file:

```bash
nano ~/.vnc/xstartup
```

### Delete everything inside and paste:

```bash
#!/bin/bash
dbus-launch --exit-with-session startxfce4
```

Save & exit:

* **Ctrl + O**, Enter
* **Ctrl + X**

Make it executable:

```bash
chmod +x ~/.vnc/xstartup
```

---

## **5. Start VNC Server**

Run:

```bash
vncserver -localhost no -geometry 1280x800 :1
```

---

## **6. Start NoVNC Web Proxy**

Run:

```bash
websockify --web /usr/share/novnc/ 6080 localhost:5901
```

👉 **Keep this terminal running**

---

## **7. Connect Using Browser**

1. In Cloud Shell, click **Web Preview → Change port**
2. Enter **6080**
3. Click **Change and Preview**
4. In NoVNC page → Click **Connect**
5. Enter VNC password: **bel@123**

---

## **8. Install Firefox (Inside VNC Terminal)**

Open terminal inside XFCE desktop, run:

### Add Mozilla Team PPA

```bash
sudo add-apt-repository ppa:mozillateam/ppa
```

### Create preference file

```bash
echo 'Package: *
Pin: release o=LP-PPA-mozillateam
Pin-Priority: 1001' | sudo tee /etc/apt/preferences.d/mozilla-firefox
```

### Update & Install Firefox ESR

```bash
sudo apt update
sudo apt install -y firefox-esr
```

---

## **9. Launch Firefox (Inside VNC Desktop)**

```bash
firefox-esr
```

---

### ✅ **Your Google Cloud Shell GUI Desktop is Ready!**

Use Firefox, terminal, full Linux environment inside Cloud Shell.

If you want, I can also prepare:
✔ A downloadable PDF
✔ A one-page cheat sheet
✔ A script that automates everything

Just tell me!
