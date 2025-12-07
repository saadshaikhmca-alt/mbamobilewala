# MBA MobileWala - Installation & Setup Guide

## System Requirements

### For Development
- **Flutter SDK**: 3.19.2+
- **Dart**: 3.3.0+
- **Android Studio** or **Xcode**
- **Node.js**: 18+ (optional, for build tools)
- **Git**: For version control

### For Backend
- **PHP**: 8.1+
- **MySQL**: 8.0+
- **Apache 2.4** or **Nginx**
- **Composer**: For dependency management
- **OpenSSL**: For SSL certificates

---

## Local Development Setup

### 1. Clone Repository

```bash
git clone https://github.com/saadshaikhmca-alt/mbamobilewala.git
cd mbamobilewala
```

### 2. Backend Setup (Bagisto)

```bash
# Clone Bagisto
git clone https://github.com/bagisto/bagisto.git backend
cd backend

# Install PHP dependencies
composer install

# Copy environment file
cp .env.example .env

# Generate key
php artisan key:generate

# Create database
mysql -u root -p -e "CREATE DATABASE mbamobilewala_db;"

# Run migrations
php artisan migrate:refresh --seed

# Link storage
php artisan storage:link

# Serve locally
php artisan serve
```

**Backend available at**: http://localhost:8000

### 3. Mobile App Setup (Flutter)

```bash
# Navigate to Flutter app directory
cd ../mobile-app

# Get dependencies
flutter pub get

# Generate build files
flutter pub run build_runner build --delete-conflicting-outputs

# Run on emulator/device
flutter run
```

---

## Docker Setup (Recommended)

For isolated development environment:

```bash
# Build Docker image
docker-compose build

# Start services
docker-compose up -d

# Run migrations
docker-compose exec app php artisan migrate:refresh --seed

# Access application
# Frontend: http://localhost
# API: http://localhost/api
# Admin: http://localhost/admin
```

---

## Deployment Options (FREE)

### Option 1: DigitalOcean (Recommended) - $0
**Using GitHub Student Pack $200 credit**

```bash
# 1. Create Droplet (Ubuntu 22.04, 2GB RAM)
# 2. SSH into droplet
ssh root@YOUR_DROPLET_IP

# 3. Update system
sudo apt update && sudo apt upgrade -y

# 4. Install dependencies
sudo apt install -y apache2 php php-mysql php-json php-curl php-zip mysql-server composer git

# 5. Clone repository
cd /var/www/html
sudo git clone https://github.com/saadshaikhmca-alt/mbamobilewala.git .

# 6. Setup backend
cd backend
composer install
cp .env.example .env
# Edit .env with your database credentials
php artisan key:generate
php artisan migrate:refresh --seed

# 7. Configure Apache
sudo nano /etc/apache2/sites-available/mbamobilewala.conf
# (Add configuration)

# 8. Enable site
sudo a2ensite mbamobilewala
sudo a2dissite 000-default
sudo systemctl restart apache2

# 9. Get SSL certificate
sudo apt install certbot python3-certbot-apache
sudo certbot --apache -d yourdomain.me
```

**Cost**: $0 with Student Pack credit ✅

---

### Option 2: Render.com - $0
**Free tier with limitations**

```bash
# 1. Push to GitHub
git push origin main

# 2. Connect to Render
# - Go to https://render.com
# - Connect GitHub
# - Create Web Service
# - Build command: ./build.sh
# - Start command: php artisan serve

# 3. Set environment variables in Render dashboard
DB_HOST=your_db_host
DB_NAME=mbamobilewala_db
DB_USER=root
DB_PASSWORD=your_password
APP_KEY=your_app_key
```

**Cost**: Free tier (500 hours/month) ✅

---

### Option 3: Railway.app - $0
**Free tier with $5 monthly credit**

```bash
# 1. Install Railway CLI
npm i -g @railway/cli

# 2. Login
railway login

# 3. Initialize project
railway init

# 4. Link to GitHub
railway link

# 5. Deploy
railway up
```

**Cost**: Free with $5 monthly credit ✅

---

## Database Setup

### Local MySQL

```bash
# Login to MySQL
mysql -u root -p

# Create database
CREATE DATABASE mbamobilewala_db;
CREATE USER 'mbawala'@'localhost' IDENTIFIED BY 'strong_password';
GRANT ALL PRIVILEGES ON mbamobilewala_db.* TO 'mbawala'@'localhost';
FLUSH PRIVILEGES;
EXIT;
```

### Remote Database (Render.com)

```bash
# Create PostgreSQL database on Render
# Use connection string in .env
DB_CONNECTION=pgsql
DB_HOST=your_db_host
DB_PORT=5432
DB_DATABASE=mbamobilewala_db
DB_USERNAME=render_user
DB_PASSWORD=your_password
```

---

## Configuration Files

### .env (Backend)

```env
APP_NAME="MBA MobileWala"
APP_ENV=production
APP_DEBUG=false
APP_URL=https://yourdomain.me

DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=mbamobilewala_db
DB_USERNAME=mbawala
DB_PASSWORD=strong_password

MAIL_MAILER=smtp
MAIL_HOST=smtp.mailtrap.io
MAIL_PORT=465
MAIL_USERNAME=your_email
MAIL_PASSWORD=your_password
MAIL_ENCRYPTION=ssl

AWS_ACCESS_KEY_ID=your_key
AWS_SECRET_ACCESS_KEY=your_secret
AWS_DEFAULT_REGION=ap-south-1
AWS_BUCKET=mbamobilewala

API_CORS_ENABLED=true
API_CORS_ALLOWED_ORIGINS=*
```

### pubspec.yaml (Flutter)

```yaml
name: mbamobilewala
description: "MBA MobileWala - Mobile marketplace for buying and selling phones"

environment:
  sdk: '>=3.0.0 <4.0.0'

dependencies:
  flutter:
    sdk: flutter
  http: ^1.0.0
  provider: ^6.0.0
  shared_preferences: ^2.1.0
  firebase_core: ^2.7.0
  firebase_messaging: ^14.2.0
  get: ^4.6.0

dev_dependencies:
  flutter_test:
    sdk: flutter
```

---

## First Run Checklist

- [ ] Install all dependencies
- [ ] Create database
- [ ] Configure .env file
- [ ] Run migrations
- [ ] Create admin user
- [ ] Test API endpoints
- [ ] Build Flutter app
- [ ] Test mobile app connections
- [ ] Enable SSL certificate
- [ ] Configure email service
- [ ] Setup payment gateway (optional)
- [ ] Configure cloud storage (optional)
- [ ] Create backup strategy
- [ ] Monitor application

---

## Troubleshooting

### PHP Extension Errors

```bash
# Install missing extensions
sudo apt install php-gd php-xml php-bcmath
sudo systemctl restart apache2
```

### Permission Denied

```bash
# Fix file permissions
chown -R www-data:www-data /var/www/html
chmod -R 755 /var/www/html
chmod -R 775 /var/www/html/storage
chmod -R 775 /var/www/html/bootstrap/cache
```

### Database Connection Failed

```bash
# Check MySQL status
sudo systemctl status mysql

# Restart MySQL
sudo systemctl restart mysql

# Test connection
mysql -h localhost -u mbawala -p mbamobilewala_db
```

### Flutter Build Errors

```bash
# Clean and rebuild
flutter clean
flutter pub get
flutter pub run build_runner clean
flutter pub run build_runner build --delete-conflicting-outputs
flutter build apk --release
```

---

## Production Deployment

### Pre-deployment Checklist

- [ ] Update .env to production settings
- [ ] Set APP_DEBUG=false
- [ ] Enable HTTPS/SSL
- [ ] Configure backup schedule
- [ ] Setup monitoring & logging
- [ ] Create database backups
- [ ] Test email notifications
- [ ] Configure payment processing
- [ ] Setup CDN for assets
- [ ] Enable caching
- [ ] Configure rate limiting
- [ ] Setup error logging (Sentry)
- [ ] Enable security headers
- [ ] Run security audit

### Deployment Steps

```bash
# 1. Pull latest code
git pull origin main

# 2. Install dependencies
composer install --no-dev --optimize-autoloader

# 3. Run migrations
php artisan migrate --force

# 4. Cache configuration
php artisan config:cache
php artisan route:cache
php artisan view:cache

# 5. Optimize application
php artisan optimize

# 6. Restart services
sudo systemctl restart apache2
sudo systemctl restart mysql
```

---

## Ongoing Maintenance

### Daily
- Monitor error logs
- Check disk space
- Verify backups completed

### Weekly
- Update packages
- Review user feedback
- Analyze performance metrics

### Monthly
- Update dependencies
- Security audit
- Database optimization
- Backup verification

---

## Support & Resources

- **Bagisto Docs**: https://bagisto.com/en/documentation/
- **Flutter Docs**: https://flutter.dev/docs
- **DigitalOcean Guides**: https://www.digitalocean.com/community/tutorials
- **Render Docs**: https://render.com/docs
- **GitHub Issues**: https://github.com/saadshaikhmca-alt/mbamobilewala/issues

---

**Installation Complete!** 🎉

Your MBA MobileWala application is now ready to use. Start with **QUICK_START.md** for fastest deployment!
