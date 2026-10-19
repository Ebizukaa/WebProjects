ssh root@IP_VPS_KAMU
apt update && apt upgrade -y
apt install git curl nginx ufw -y

# Install Node.js LTS
curl -fsSL https://deb.nodesource.com/setup_22.x | bash -
apt install nodejs -y
node -v && npm -v

# Install PM2 (agar app tetap jalan meski SSH ditutup / VPS restart)
npm install -g pm2
