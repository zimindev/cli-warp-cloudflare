# 🗄️ `warp-cli` — Command-line Interface for Cloudflare WARP

`warp-cli` is the official command-line tool for managing the Cloudflare WARP service, allowing you to easily connect to the Cloudflare network for enhanced privacy and security.

-----

## ✅ Features

  - Easy connection and disconnection to Cloudflare WARP
  - Supports WARP, WARP+, and DNS over HTTPS (DoH) modes
  - Management of WARP+ license keys
  - Checking connection status and IP address information
  - Ability to enable "always-on" mode
  - Automatic startup of the WARP service upon system boot

-----

## 🔧 Installation

### On Arch Linux (Recommended via AUR):

```bash
# Install an AUR helper (e.g., yay), if you don't have one
sudo pacman -S git base-devel
git clone https://aur.archlinux.org/yay.git
cd yay
makepkg -si
cd ..
rm -rf yay

# Install warp-cli
yay -S cloudflare-warp-bin
```

### On Debian/Ubuntu:

```bash
curl https://pkg.cloudflareclient.com/pubkey.gpg | sudo gpg --dearmor -o /usr/share/keyrings/cloudflare-warp-archive-keyring.gpg
echo "deb [arch=amd64 signed-by=/usr/share/keyrings/cloudflare-warp-archive-keyring.gpg] https://pkg.cloudflareclient.com/ $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/cloudflare-client.list
sudo apt update
sudo apt install cloudflare-warp
```

### Starting the WARP Service:

After installation, you need to start the `warp-svc` service and enable it to run automatically on system startup:

```bash
sudo systemctl start warp-svc
sudo systemctl enable warp-svc
```

-----

## 🚀 Basic Usage

### Register a new client:

```bash
warp-cli registration new
```

### Connect to WARP:

```bash
warp-cli connect
```

### Disconnect from WARP:

```bash
warp-cli disconnect
```

### Check connection status:

```bash
warp-cli status
```

-----

## ⌨️ Essential Commands

| Command                     | Action                                        |
|-----------------------------|-----------------------------------------------|
| `warp-cli status`           | Show current WARP status                      |
| `warp-cli connect`          | Connect to the WARP service                   |
| `warp-cli disconnect`       | Disconnect from the WARP service              |
| `warp-cli registration new` | Register a new device                         |
| `warp-cli registration license <KEY>`| Set WARP+ license key                   |
| `warp-cli enable-always-on` | Enable "always-on" mode                       |
| `warp-cli disable-always-on`| Disable "always-on" mode                      |
| `warp-cli mode warp`        | Switch to WARP mode                           |
| `warp-cli mode doh`         | Switch to DNS over HTTPS mode                 |
| `warp-cli mode warp+doh`    | Switch to WARP with DoH mode                  |
| `warp-cli help`             | Show help for commands                        |

-----

## 🧰 Configuration

### Setting a WARP+ License Key:

If you have a WARP+ license key, you can add it to access additional benefits:

```bash
warp-cli registration license YOUR_LICENSE_KEY_HERE
```

### Switching Modes:

You can configure the WARP operating mode according to your needs:

```bash
# WARP only (standard mode)
warp-cli mode warp

# DNS over HTTPS only (secure DNS queries without full tunneling)
warp-cli mode doh

# WARP with DNS over HTTPS
warp-cli mode warp+doh
```

-----

## 🎯 Advanced Tips

  - **Checking your external IP address:** To verify if WARP is working and changing your IP, use:

    ```bash
    curl https://www.cloudflare.com/cdn-cgi/trace/
    ```

    In the output, you should see `warp=on` and `loc=` (Cloudflare server location).

  - **Managing via system services:**
    If you need more detailed control over `warp-svc`, use `systemctl`:

    ```bash
    sudo systemctl status warp-svc  # Check service status
    sudo systemctl restart warp-svc # Restart the service
    ```

-----

## 📚 More Info

  - Cloudflare WARP Website: [https://cloudflarewarp.com/](https://cloudflarewarp.com/)
  - Cloudflare WARP Documentation: [https://developers.cloudflare.com/warp/](https://www.google.com/search?q=https://developers.cloudflare.com/warp/)
  - `warp-cli` Help: `warp-cli help`
