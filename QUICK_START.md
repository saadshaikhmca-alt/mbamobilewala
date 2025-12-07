# Quick Start Guide - 5 Minutes to Deploy

## ⚡ What You Have (FREE from GitHub Student Pack)

✅ **$200 DigitalOcean Credit** - Runs Bagisto backend (1 year free)  
✅ **Free .ME Domain** - From Namecheap (1 year)  
✅ **GitHub Copilot Pro** - AI-powered development  
✅ **JetBrains IDEs** - All professional IDEs free  

---

## 🚀 Step 1: Get DigitalOcean Credit (2 minutes)

```
1. Go to: https://education.github.com/pack
2. Scroll to DigitalOcean
3. Click "Get access"
4. Sign up with your GitHub account
5. Copy your $200 credit code
6. Go to DigitalOcean.com and apply credit
```

**You now have $200 to spend on servers! 🎉**

---

## 🌍 Step 2: Get Free Domain (2 minutes)

```
1. Go to: https://education.github.com/pack
2. Find Namecheap section
3. Click "Get access"
4. Claim your free .ME domain
5. Point it to your DigitalOcean droplet IP
```

---

## 🖥️ Step 3: Setup Server (Copy-Paste Commands)

### Create a DigitalOcean Droplet
```bash
# Select: Ubuntu 22.04 LTS
# Plan: $7/month Basic
# Region: India (Bangalore or Singapore)
# Size: 2GB RAM, 1vCPU
```

### Install Everything
```bash
# SSH into your droplet
ssh root@YOUR_DROPLET_IP

# Copy & Paste this:
sudo apt update && sudo apt install -y apache2 php php-cli php-mysql php-json php-mbstring php-xml php-curl php-zip mysql-server mysql-client composer git
sudo a2enmod rewrite headers
sudo systemctl restart apache2
```

---

## 📦 Step 4: Deploy Bagisto (5 minutes)

```bash
# Connect to MySQL
mysql -u root -p

# Create database
CREATE DATABASE bagisto_db;
CREATE USER 'bagisto_user'@'localhost' IDENTIFIED BY 'YourPassword';
GRANT ALL PRIVILEGES ON bagisto_db.* TO 'bagisto_user'@'localhost';
FLUSH PRIVILEGES;
EXIT;

# Clone Bagisto
cd /var/www/html
sudo rm -rf index.html
sudo git clone https://github.com/bagisto/bagisto.git .
sudo chown -R www-data:www-data /var/www/html
sudo -u www-data composer install

# Setup Bagisto
sudo -u www-data cp .env.example .env
sudo nano .env  # Edit database details
sudo -u www-data php artisan key:generate
sudo -u www-data php artisan migrate:refresh --seed
```

---

## 📱 Step 5: Deploy Flutter App (1 minute config)

```bash
# In your Flutter app project:
Edit: lib/utils/server_configuration.dart

Change:
static const String baseDomain = 'https://yourdomain.me/graphql';

# Build APK
flutter build apk --release

# Find it at:
build/app/outputs/apk/release/app-release.apk
```

---

## 🎯 What You Now Have

| Component | Status | Cost |
|-----------|--------|------|
| Bagisto Backend | ✅ Running | $0 |
| Domain | ✅ Active | $0 |
| Flutter App | ✅ Built | $0 |
| Database | ✅ MySQL | $0 |
| Multi-Vendor | ✅ Enabled | $0 |
| **TOTAL** | **✅ COMPLETE** | **$0** |

---

## 📊 Cost Breakdown

Without Student Pack:
- DigitalOcean: $7/month = **$84/year**
- Domain: $8.99/year = **$9/year**
- JetBrains IDEs: $200/year = **$200/year**
- GitHub Copilot: $20/month = **$240/year**
- **TOTAL: $533/year**

**With Student Pack: $0 for 3 years! 🎉**

---

## 🎓 You Save: $1,599+

---

## ⚠️ Important Notes

- Your $200 DigitalOcean credit is enough for:
  - 1 Droplet ($7/month) × 12 months = $84 (still $116 left!)
  - Database backups
  - Additional storage
  
- Student Pack lasts until Dec 4, 2027 ✅

- Free domain renewal:
  - First year: Free (.ME)
  - After 1 year: Renew or get another free one

---

## 🤔 Next Steps

1. Claim all benefits on GitHub Education pack
2. Test your app locally first
3. Upload APK to Google Play Store ($25 one-time)
4. Monitor your DigitalOcean usage
5. Scale up if needed (still have budget!)

---

## 📚 Full Documentation

See `README.md` for detailed setup instructions for each component.

---

**Happy Deploying! 🚀**
