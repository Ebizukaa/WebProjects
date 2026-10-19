ssh root@IP_VPS_KAMU
apt update && apt upgrade -y
apt install git curl nginx ufw -y

# Install Node.js LTS
curl -fsSL https://deb.nodesource.com/setup_22.x | bash -
apt install nodejs -y
node -v && npm -v

# Install PM2 (agar app tetap jalan meski SSH ditutup / VPS restart)
npm install -g pm2

cd /var/www
git clone https://Ebizukaa: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@github.com/Ebizukaa/WebProjects.git webprojects
cd webprojects

npm install
# Cek dulu isi package.json bagian "scripts" dan port di server.js (mis. 3000)
npm start          # coba manual dulu, kalau muncul berarti OK, stop dengan Ctrl+C

pm2 start server.js --name webprojects   # atau: pm2 start npm --name webprojects -- start
pm2 save
pm2 startup        # ikuti perintah yang muncul agar auto-start saat reboot
pm2 logs webprojects   # cek log kalau error

nano /etc/nginx/sites-available/ngga.cloud
server {
    server_name ngga.cloud www.ngga.cloud;

    location / {
        proxy_pass http://127.0.0.1:<portmu>;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_cache_bypass $http_upgrade;
    }
}

ln -s /etc/nginx/sites-available/ngga.cloud /etc/nginx/sites-enabled/
nginx -t
systemctl reload nginx

apt install certbot python3-certbot-nginx -y
certbot --nginx -d ngga.cloud -d www.ngga.cloud

ufw allow OpenSSH
ufw allow 'Nginx Full'
ufw enable

# Kalau ada Update di Repository
cd /var/www/webprojects
git pull
npm install          # kalau dependency berubah
pm2 restart webprojects

# My Face If i See this Repository
<img width="1920" height="1080" alt="Screenshot" src="https://github.com/user-attachments/assets/b81493ec-43da-4fda-a4a3-62a16ebc08c5" />
