
## 📘 Setup Guide for Symfony, PHP, MySQL, AWS CLI, Python, Node, and Composer

### 🔧 Prerequisites
Ensure you have the necessary permissions and a stable internet connection before beginning this setup.

### 🧰 Update System Packages
```bash
sudo apt update && sudo apt upgrade -y
```

### 🌐 Install Google Chrome
```bash
wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
sudo dpkg -i google-chrome-stable_current_amd64.deb
google-chrome
```

### 📦 Install PHP and Required Extensions
```bash
sudo apt install software-properties-common
sudo add-apt-repository ppa:ondrej/php
sudo apt update
sudo apt install php8.2-fpm
php -v
sudo apt install php8.2-common php8.2-mysql php8.2-xml php8.2-xmlrpc php8.2-curl php8.2-gd php8.2-cli php8.2-dev php8.2-imap php8.2-mbstring php8.2-opcache php8.2-soap php8.2-zip php8.2-redis php8.2-intl -y
sudo nano /etc/php/8.2/fpm/php.ini
sudo service php8.2-fpm restart
sudo nano /etc/php/8.2/fpm/pool.d/www.conf
sudo service php8.2-fpm restart
php-fpm8.2 -v
```

### 🐬 Install MySQL
```bash
sudo apt install mysql-server
sudo systemctl start mysql.service
sudo mysql
```

### 🌍 Install Nginx and Configure
```bash
sudo apt install nginx
sudo nano /etc/nginx/sites-available/socialverse
```
```bash
server {
    listen 80;
    listen [::]:80;

    server_name SachinKinha; # replace with your hostname
    root /home/alpha/Desktop/socialverse-backend/public; # replace with your path
    index index.php;
    client_max_body_size 100m;

    location / {
        try_files $uri $uri/ /index.php$is_args$args;
    }

    location ~ \.php {
        try_files $uri /index.php =404;
        fastcgi_pass unix:/var/run/php/php8.2-fpm.sock;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        fastcgi_param SCRIPT_NAME $fastcgi_script_name;
        fastcgi_split_path_info ^(.+\.php)(/.+)$;
        fastcgi_index index.php;
        include fastcgi_params;
      }

    location ~ /\.(?:ht|git|svn) {
        deny all;
    }
}
```
```bash
sudo ln -s /etc/nginx/sites-available/socialverse /etc/nginx/sites-enabled/
sudo nginx -t
sudo systemctl restart nginx
sudo systemctl status nginx
sudo ufw allow 8000
sudo chown -R alpha:alpha /home/alpha/Desktop/socialverse-backend/public
sudo chmod -R 755 /home/alpha/Desktop/socialverse-backend/public
sudo systemctl restart nginx
sudo ufw status
```

### 🚀 Install Symfony CLI
```bash
curl -1sLf 'https://dl.cloudsmith.io/public/symfony/stable/setup.deb.sh' | sudo -E bash
sudo apt install symfony-cli
wget https://get.symfony.com/cli/installer -O - | bash
mv /home/alpha/.symfony5/bin/symfony /usr/local/bin/symfony
sudo mv /home/alpha/.symfony5/bin/symfony /usr/local/bin/symfony
```

### 🛠️ Install Composer
```bash
php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
php -r "if (hash_file('sha384', 'composer-setup.php') === 'dac665fdc30fdd8ec78b38b9800061b4150413ff2e3b6f88543c636f7cd84f6db9189d43a81e5503cda447da73c7e5b6') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
php composer-setup.php
php -r "unlink('composer-setup.php');"
sudo mv composer.phar /usr/local/bin/composer
composer update
```

### 🐍 Install Python and AWS CLI
```bash
sudo apt install python3
python3 --version
sudo apt install python3-venv
python3 -m venv myenv
source myenv/bin/activate
python3 -m pip install --upgrade pip
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install
aws --version
aws configure
```

### 🌳 Install Node.js and NPM
```bash
sudo apt install nodejs
node -v
sudo apt install npm
```

### 📦 Install VS Code
```bash
wget https://go.microsoft.com/fwlink/?LinkID=760868 -O code.deb
sudo dpkg -i code.deb
sudo apt --fix-broken install
code --version
```

### 🎉 Final Setup Steps
```bash
sudo systemctl restart nginx
symfony serve
```
