# MBA MobileWala - Complete Deployment Checklist

**Deploy for FREE using GitHub Student Pack Benefits**

---

## 📋 Pre-Deployment Checklist

### GitHub Student Pack Setup
- [ ] Verify Student Pack is active at https://github.com/settings/education/benefits
- [ ] Check expiration date (should be 2027)
- [ ] Access all partner benefits

### Required Accounts
- [ ] GitHub account (free) ✅
- [ ] DigitalOcean account (with $200 credit)
- [ ] Namecheap account (for free domain)
- [ ] Google Play Developer account ($25, one-time)
- [ ] Firebase account (for notifications)

---

## 🚀 Phase 1: Claim Free Credits (5 minutes)

### DigitalOcean
- [ ] Go to https://education.github.com/pack
- [ ] Click on DigitalOcean section
- [ ] Click "Get access"
- [ ] Verify with GitHub
- [ ] Accept $200 credit
- [ ] Note credit code for later use

### Namecheap
- [ ] Go to https://education.github.com/pack
- [ ] Find Namecheap section
- [ ] Click "Get access"
- [ ] Claim free .ME domain
- [ ] Complete verification
- [ ] Domain is yours for 1 year free!

### GitHub Benefits
- [ ] GitHub Copilot Pro (AI coding)
- [ ] JetBrains IDEs (all products)
- [ ] GitHub Pages (free hosting)
- [ ] GitHub Actions (free CI/CD)

---

## 💻 Phase 2: Backend Deployment (20 minutes)

### Create DigitalOcean Droplet
- [ ] Log into DigitalOcean
- [ ] Click "Create" → "Droplets"
- [ ] Select: Ubuntu 22.04 LTS
- [ ] Plan: Basic ($7/month)
- [ ] Region: India (Bangalore or Singapore)
- [ ] Size: 2GB RAM, 1vCPU
- [ ] Add SSH key
- [ ] Create droplet
- [ ] Note droplet IP address

### Install Server Software
- [ ] SSH into droplet
- [ ] Update system: `apt update && apt upgrade`
- [ ] Install Apache: `apt install apache2`
- [ ] Install PHP: `apt install php php-mysql php-json php-curl php-zip`
- [ ] Install MySQL: `apt install mysql-server`
- [ ] Install Composer: `apt install composer`
- [ ] Install Git: `apt install git`
- [ ] Enable mod_rewrite: `a2enmod rewrite`
- [ ] Restart Apache: `systemctl restart apache2`

### Deploy Bagisto
- [ ] Clone Bagisto: `git clone https://github.com/bagisto/bagisto.git /var/www/html`
- [ ] Set permissions: `chown -R www-data:www-data /var/www/html`
- [ ] Install dependencies: `composer install`
- [ ] Create `.env` file
- [ ] Configure database credentials
- [ ] Run migrations: `php artisan migrate:refresh --seed`
- [ ] Create storage link: `php artisan storage:link`
- [ ] Test: Visit http://YOUR_IP in browser

### Secure with SSL
- [ ] Install Certbot: `apt install certbot python3-certbot-apache`
- [ ] Generate certificate: `certbot --apache -d yourdomain.me`
- [ ] Verify HTTPS works
- [ ] Set auto-renewal

---

## 🌍 Phase 3: Domain Setup (5 minutes)

### Point Domain to Server
- [ ] Log into Namecheap
- [ ] Go to Domain List
- [ ] Click "Manage"
- [ ] Go to "Advanced DNS"
- [ ] Add A Record:
  - Type: A
  - Host: @
  - Value: YOUR_DROPLET_IP
  - TTL: 30 min
- [ ] Add WWW Record:
  - Type: A
  - Host: www
  - Value: YOUR_DROPLET_IP
- [ ] Wait 15-30 minutes for DNS
- [ ] Test: `nslookup yourdomain.me`

### Update Bagisto Config
- [ ] SSH into server
- [ ] Edit .env: `APP_URL=https://yourdomain.me`
- [ ] Clear cache: `php artisan cache:clear`
- [ ] Restart Apache
- [ ] Visit https://yourdomain.me (should work!)

---

## 📱 Phase 4: Mobile App Configuration (15 minutes)

### Clone Flutter App
- [ ] Clone: `git clone https://github.com/bagisto/opensource-ecommerce-mobile-app.git mbamobilewala-app`
- [ ] Navigate: `cd mbamobilewala-app`
- [ ] Get dependencies: `flutter pub get`

### Configure App Branding
- [ ] Update app name to "MBA MobileWala"
- [ ] Change package name to `com.mbamobilewala.app`
- [ ] Update Android manifest
- [ ] Update iOS info.plist
- [ ] Add app icons
- [ ] Add splash screen

### Set API Endpoint
- [ ] Edit: `lib/utils/server_configuration.dart`
- [ ] Change: `baseDomain = 'https://yourdomain.me/graphql'`
- [ ] Save

### Build Release APK
- [ ] Run: `flutter build apk --release`
- [ ] Output: `build/app/outputs/apk/release/app-release.apk`
- [ ] File size: ~100MB

### Build App Bundle (Recommended)
- [ ] Run: `flutter build appbundle --release`
- [ ] Output: `build/app/outputs/bundle/release/app-release.aab`
- [ ] Use for Play Store

---

## 🎮 Phase 5: Google Play Store Deployment (varies)

### Create Developer Account
- [ ] Go to https://play.google.com/console
- [ ] Pay $25 registration (one-time)
- [ ] Complete identity verification
- [ ] Accept agreements

### Create App Listing
- [ ] Click "Create app"
- [ ] App name: "MBA MobileWala"
- [ ] Category: Shopping
- [ ] Content rating: Collect data
- [ ] Target audience: 13+

### Prepare Store Listing
- [ ] Add 2-4 screenshots (best practices: show features)
- [ ] Add feature graphic (1024x500px)
- [ ] Add short description (80 chars)
- [ ] Add full description
- [ ] Add privacy policy URL
- [ ] Add contact email

### Upload APK/AAB
- [ ] Go to "Release" → "Production"
- [ ] Upload `.aab` file
- [ ] Review and publish
- [ ] Google reviews (typically 24-48 hours)
- [ ] App goes live!

---

## ✅ Post-Deployment Verification

### Backend
- [ ] Bagisto admin accessible at `/admin`
- [ ] Database connected
- [ ] File uploads working
- [ ] Email configured (optional)
- [ ] Cron jobs set up (optional)

### Mobile App
- [ ] APK installs successfully
- [ ] App connects to backend API
- [ ] Login/registration works
- [ ] Product listing displays
- [ ] Cart functionality works
- [ ] Push notifications work (if enabled)

### Domain & Security
- [ ] Domain resolves (http and https)
- [ ] SSL certificate valid (no warnings)
- [ ] Admin panel accessible
- [ ] API endpoints responding

---

## 💰 Cost Verification

### What You Get for FREE
- DigitalOcean Droplet: $7/month × 12 months = **$84** ✅ FREE
- .ME Domain: **$9/year** ✅ FREE
- GitHub Copilot Pro: **$20/month** ✅ FREE
- JetBrains IDEs: **$200/year** ✅ FREE

### Total Savings
**$1,599+ in services FREE for 3 years!** 🎉

---

## 📊 Monitoring & Maintenance

### Daily
- [ ] Check DigitalOcean dashboard
- [ ] Monitor server performance
- [ ] Check disk space usage
- [ ] Review error logs

### Weekly
- [ ] Check database backups
- [ ] Review app analytics
- [ ] Check user feedback
- [ ] Update security patches

### Monthly
- [ ] Monitor credit usage
- [ ] Review billing
- [ ] Optimize database
- [ ] Analyze performance metrics

---

## 🆘 Troubleshooting Quick Links

- **Bagisto Won't Load**: See README.md → Troubleshooting
- **App Can't Connect**: See FLUTTER_APP_SETUP.md → API Connection Issues
- **Domain Issues**: See Part 2 in README.md → Setup Free Domain
- **Build Errors**: See FLUTTER_APP_SETUP.md → Troubleshooting

---

## 📚 Documentation Files

Refer to these guides during deployment:

1. **README.md** - Complete setup (6 parts)
2. **QUICK_START.md** - 5-minute guide
3. **FLUTTER_APP_SETUP.md** - App configuration
4. **DEPLOYMENT_CHECKLIST.md** - This file!

---

## 🎯 Success Criteria

✅ **Deployment Complete When:**
- Bagisto backend running on your domain
- Mobile app installed on device
- App connects to backend successfully
- Can browse products
- Can add to cart
- App listed on Play Store
- Zero out-of-pocket costs

---

## 📞 Support

**If you get stuck:**
1. Check the troubleshooting sections in README.md
2. Review the specific guide (Flutter/Backend/Domain)
3. Check Bagisto forums: https://forum.bagisto.com/
4. Check Flutter issues: https://github.com/flutter/flutter/issues
5. Check DigitalOcean tutorials

---

## 🎓 Final Steps

1. ✅ Mark all items complete in this checklist
2. ✅ Update the README with your domain
3. ✅ Share your app with friends and family
4. ✅ Get reviews on Play Store
5. ✅ Iterate and improve!

---

**Estimated Total Time: 1-2 hours for complete deployment** ⏱️

**Start with QUICK_START.md if you're in a hurry!** 🚀

**Made with 💜 for MBA MobileWala Entrepreneurs**
