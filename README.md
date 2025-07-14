# 🗄️ `warp-cli` — Command-line Interface for Cloudflare WARP

`warp-cli` є офіційним інструментом командного рядка для керування сервісом Cloudflare WARP, що дозволяє легко підключатися до мережі Cloudflare для підвищення конфіденційності та безпеки.

-----

## ✅ Features

  - Легке підключення/відключення до Cloudflare WARP
  - Підтримка режимів WARP, WARP+ та DNS over HTTPS (DoH)
  - Керування ліцензійними ключами WARP+
  - Перевірка стану з'єднання та інформації про IP-адресу
  - Можливість увімкнення "завжди увімкнено" (always-on) режиму
  - Автоматичний запуск сервісу WARP при завантаженні системи

-----

## 🔧 Installation

### On Arch Linux (Recommended via AUR):

```bash
# Встановлення AUR-хелпера (якщо у вас його немає, наприклад, yay)
sudo pacman -S git base-devel
git clone https://aur.archlinux.org/yay.git
cd yay
makepkg -si
cd ..
rm -rf yay

# Встановлення warp-cli
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

Після встановлення необхідно запустити сервіс `warp-svc` та дозволити йому автоматично запускатися при завантаженні системи:

```bash
sudo systemctl start warp-svc
sudo systemctl enable warp-svc
```

-----

## 🚀 Basic Usage

### Реєстрація нового клієнта:

```bash
warp-cli registration new
```

### Підключення до WARP:

```bash
warp-cli connect
```

### Відключення від WARP:

```bash
warp-cli disconnect
```

### Перевірка статусу підключення:

```bash
warp-cli status
```

-----

## ⌨️ Essential Commands

| Command             | Action                                      |
|---------------------|---------------------------------------------|
| `warp-cli status`   | Показати поточний статус WARP               |
| `warp-cli connect`  | Підключитися до сервісу WARP                |
| `warp-cli disconnect`| Відключитися від сервісу WARP               |
| `warp-cli registration new`| Зареєструвати новий пристрій           |
| `warp-cli registration license <KEY>`| Встановити ліцензійний ключ WARP+ |
| `warp-cli enable-always-on`| Увімкнути режим "завжди увімкнено"     |
| `warp-cli disable-always-on`| Вимкнути режим "завжди увімкнено"     |
| `warp-cli mode warp`| Переключити в режим WARP                  |
| `warp-cli mode doh` | Переключити в режим DNS over HTTPS         |
| `warp-cli mode warp+doh`| Переключити в режим WARP з DoH           |
| `warp-cli help`     | Показати довідку по командах                |

-----

## 🧰 Configuration

### Встановлення ліцензійного ключа WARP+:

Якщо у вас є ліцензійний ключ WARP+, ви можете додати його для доступу до додаткових переваг:

```bash
warp-cli registration license YOUR_LICENSE_KEY_HERE
```

### Перемикання режимів:

Ви можете налаштувати режим роботи WARP відповідно до ваших потреб:

```bash
# Тільки WARP (стандартний режим)
warp-cli mode warp

# Тільки DNS over HTTPS (безпечні DNS-запити без повного тунелювання)
warp-cli mode doh

# WARP з DNS over HTTPS
warp-cli mode warp+doh
```

-----

## 🎯 Advanced Tips

  - **Перевірка зовнішньої IP-адреси:** Щоб перевірити, чи WARP працює і змінює вашу IP-адресу, використовуйте:

    ```bash
    curl https://www.cloudflare.com/cdn-cgi/trace/
    ```

    У виводі ви повинні побачити `warp=on` та `loc=` (розташування сервера Cloudflare).

  - **Налаштування через системні сервіси:**
    Якщо вам потрібно детальніше контролювати `warp-svc`, використовуйте `systemctl`:

    ```bash
    sudo systemctl status warp-svc # Перевірка статусу сервісу
    sudo systemctl restart warp-svc # Перезапуск сервісу
    ```

-----

## 📚 More Info

  - Cloudflare WARP Website: [https://cloudflarewarp.com/](https://cloudflarewarp.com/)
  - Cloudflare WARP Documentation: [https://developers.cloudflare.com/warp/](https://www.google.com/search?q=https://developers.cloudflare.com/warp/)
  - `warp-cli` Help: `warp-cli help`
