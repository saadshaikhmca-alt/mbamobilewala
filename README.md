# Bagisto + Flutter Mobile Ecommerce Marketplace

**FREE Deployment Guide using GitHub Student Pack Benefits**

## Overview

A complete mobile ecommerce marketplace for buyers and sellers of mobile phones. Built with:
- **Backend**: Bagisto (Laravel) - Free & Open Source
- **Mobile App**: Flutter - Cross-platform (iOS & Android)
- **Hosting**: DigitalOcean (Free via Student Pack)
- **Domain**: Namecheap (Free via Student Pack)
- **CI/CD**: GitHub Actions & Pages (Free)

---

## GitHub Student Developer Pack Benefits

Your student account includes **$200+ worth of free services**:

| Service | Benefit | Duration |
|---------|---------|----------|
| **DigitalOcean** | $200 credit | 12 months |
| **Namecheap** | Free .ME domain + 50% off | 1 year |
| **GitHub Copilot Pro** | Free subscription | Duration of pack |
| **Heroku** | Free credits | Duration of pack |
| **JetBrains IDEs** | All IDEs free | Duration of pack |
| **Visual Studio** | Free professional license | Duration of pack |

---

## Part 1: Setup DigitalOcean Backend

### Step 1: Claim DigitalOcean Credit

1. Go to: https://education.github.com/pack
2. Find "DigitalOcean" section
3. Click "Get access"
4. Sign up with GitHub account
5. You'll receive **$200 credit** (12 months)

### Step 2: Create Droplet for Bagisto

1. Log into DigitalOcean
2. Click **Create** → **Droplets**
3. Choose Image: **Ubuntu 22.04 LTS**
4. Plan: **Basic** ($7/month = Free with $200 credit!)
5. Region: **Choose closest to India** (Bangalore or Singapore)
6. SSH Key: Add your GitHub SSH key
7. Hostname: `bagisto-backend`
8. Click **Create**

### Step 3: Install Dependencies

```bash
# SSH into your droplet
ssh root@your_droplet_ip

# Update system
sudo apt update && sudo apt upgrade -y

# Install LAMP Stack
sudo apt install -y apache2 php php-cli php-fpm php-mysql
sudo apt install -y php-json php-mbstring php-xml php-curl php-zip
sudo apt install -y mysql-server mysql-client
sudo apt install -y composer git

# Enable mod_rewrite
sudo a2enmod rewrite
sudo a2enmod headers
sudo systemctl restart apache2
```

### Step 4: Create MySQL Database

```bash
mysql -u root -p

CREATE DATABASE bagisto_db;
CREATE USER 'bagisto_user'@'localhost' IDENTIFIED BY 'strong_password';
GRANT ALL PRIVILEGES ON bagisto_db.* TO 'bagisto_user'@'localhost';
FLUSH PRIVILEGES;
EXIT;
```

### Step 5: Clone & Install Bagisto

```bash
cd /var/www/html
sudo rm -rf index.html

# Clone Bagisto
sudo git clone https://github.com/bagisto/bagisto.git .

# Set permissions
sudo chown -R www-data:www-data /var/www/html
sudo chmod -R 755 /var/www/html

# Install dependencies
cd /var/www/html
sudo -u www-data composer install
```

### Step 6: Configure Bagisto

```bash
# Create .env file
sudo -u www-data cp .env.example .env

# Edit .env with your database credentials
sudo nano .env
```

Update these fields:
```env
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=bagisto_db
DB_USERNAME=bagisto_user
DB_PASSWORD=strong_password
APP_URL=https://yourdomain.com
```

### Step 7: Run Installation

```bash
sudo -u www-data php artisan key:generate
sudo -u www-data php artisan migrate:refresh --seed
sudo -u www-data php artisan storage:link
```

### Step 8: Configure Apache Virtual Host

```bash
sudo nano /etc/apache2/sites-available/bagisto.conf
```

Paste:
```apache
<VirtualHost *:80>
    ServerName yourdomain.com
    ServerAlias www.yourdomain.com
    DocumentRoot /var/www/html/public
    
    <Directory /var/www/html/public>
        AllowOverride All
        Require all granted
    </Directory>
    
    ErrorLog ${APACHE_LOG_DIR}/bagisto-error.log
    CustomLog ${APACHE_LOG_DIR}/bagisto-access.log combined
</VirtualHost>
```

```bash
sudo a2ensite bagisto
sudo a2dissite 000-default
sudo systemctl restart apache2
```

### Step 9: Enable HTTPS with Let's Encrypt

```bash
sudo apt install -y certbot python3-certbot-apache
sudo certbot --apache -d yourdomain.com -d www.yourdomain.com
```

---

## Part 2: Setup Free Domain with Namecheap

### Step 1: Claim Namecheap Domain

1. Go to: https://education.github.com/pack
2. Find "Namecheap" section
3. Click **Get access**
4. Select: **.me domain (1 year free)**
5. Complete verification

### Step 2: Point Domain to DigitalOcean

1. In Namecheap Dashboard
2. Go to **Domain List** → **Manage**
3. Click **Advanced DNS**
4. Update **A Record**:
   ```
   Type: A
   Host: @
   Value: YOUR_DROPLET_IP
   TTL: 30 min
   ```
5. Update **WWW Record**:
   ```
   Type: A
   Host: www
   Value: YOUR_DROPLET_IP
   TTL: 30 min
   ```
6. Wait 15-30 minutes for DNS propagation

### Step 3: Test Domain

```bash
nslookup yourdomain.me
# Should show your DigitalOcean IP
```

---

## Part 3: Deploy Flutter Mobile App

### Step 1: Clone Bagisto Mobile App

```bash
git clone https://github.com/bagisto/opensource-ecommerce-mobile-app.git
cd opensource-ecommerce-mobile-app
```

### Step 2: Configure API Connection

Edit: `lib/utils/server_configuration.dart`

```dart
static const String baseDomain = 'https://yourdomain.me/graphql';
```

### Step 3: Build for Android

```bash
flutter pub get
flutter build apk --release
# Output: build/app/outputs/apk/release/app-release.apk
```

### Step 4: Build for iOS (macOS only)

```bash
flutter build ios --release
# Use Xcode to create IPA file
```

### Step 5: Upload to Play Store

1. Create Google Play Developer Account ($25 one-time)
2. Create App Listing
3. Upload APK/AAB
4. Fill descriptions & screenshots
5. Submit for review (24-48 hours)

---

## Part 4: GitHub Pages Frontend (Optional)

### Step 1: Create GitHub Pages Repo

```bash
git clone https://github.com/yourusername/yourusername.github.io.git
```

### Step 2: Add Landing Page

Create `index.html`:
```html
<!DOCTYPE html>
<html>
<head>
    <title>MBA MobileWala - Mobile Marketplace</title>
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
</head>
<body>
    <h1>Download Our Mobile Marketplace App</h1>
    <a href="https://play.google.com/store/apps/details?id=com.yourdomain.app">
        Download Android
    </a>
</body>
</html>
```

### Step 3: Push to GitHub

```bash
git add .
git commit -m "Add landing page"
git push origin main
```

Your site is now at: `https://yourusername.github.io`

---

## Part 5: Multi-Vendor Marketplace Setup

### Enable Multi-Vendor in Bagisto

1. Admin Panel → Catalog → Sellers
2. Enable seller registration
3. Set commission rates (default 10%)
4. Approve seller accounts manually or auto

### Database Tables Created Automatically:
- `sellers` - Vendor information
- `seller_products` - Vendor products
- `seller_commissions` - Commission tracking
- `seller_payouts` - Payment history

---

## Part 6: GitHub Actions CI/CD

### Automated Tests on Push

Create: `.github/workflows/test.yml`

```yaml
name: Tests
on: [push, pull_request]
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - name: Run tests
        run: |
          cd backend
          composer install
          ./vendor/bin/phpunit
```

### Deploy on Release

Create: `.github/workflows/deploy.yml`

```yaml
name: Deploy to DigitalOcean
on:
  push:
    branches: [main]
jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - name: Deploy to server
        run: |
          mkdir -p ~/.ssh
          echo "${{ secrets.DEPLOY_KEY }}" > ~/.ssh/id_rsa
          chmod 600 ~/.ssh/id_rsa
          ssh-keyscan -H ${{ secrets.SERVER_IP }} >> ~/.ssh/known_hosts
          ssh root@${{ secrets.SERVER_IP }} 'cd /var/www/html && git pull'
```

---

## Troubleshooting

### Bagisto Not Loading

```bash
# Check Laravel logs
tail -f /var/www/html/storage/logs/laravel.log

# Clear cache
cd /var/www/html
sudo -u www-data php artisan cache:clear
sudo -u www-data php artisan config:clear
```

### Flutter App Can't Connect to API

1. Check API endpoint in `server_configuration.dart`
2. Ensure CORS is enabled in Bagisto `.env`:
   ```
   API_CORS_ENABLED=true
   ```
3. Test API with: `curl https://yourdomain.me/graphql`

### Database Connection Error

```bash
# Check MySQL is running
sudo systemctl status mysql

# Check database credentials
mysql -u bagisto_user -p bagisto_db
```

---

## Cost Breakdown

| Item | Regular Price | Student Price | Duration |
|------|-------------|----------|----------|
| DigitalOcean Droplet | $7/month | FREE | 12 months |
| Namecheap .me Domain | $8.99/year | FREE | 1 year |
| GitHub Copilot Pro | $20/month | FREE | Pack duration |
| JetBrains IDEs | $200/year | FREE | Pack duration |
| **TOTAL SAVINGS** | **$2,000+** | **$0** | **3 years** |

---

## Next Steps

1. ✅ Claim all GitHub Student Pack benefits
2. ✅ Setup DigitalOcean Droplet
3. ✅ Install Bagisto on server
4. ✅ Get free domain from Namecheap
5. ✅ Deploy Flutter app
6. ✅ Test multi-vendor functionality
7. ✅ Submit app to Play Store
8. ✅ Monitor with GitHub Actions

---

## Resources

- Bagisto Docs: https://bagisto.com/en/documentation/
- Flutter Docs: https://flutter.dev/docs
- DigitalOcean Tutorials: https://www.digitalocean.com/community/tutorials
- GitHub Education: https://education.github.com/

---

## License

MIT License - See LICENSE file

**Made with ❤️ for Indian Students & Entrepreneurs**
