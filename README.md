<div align="center">
  <a href="https://laravel.com" target="_blank">
    <img src="https://raw.githubusercontent.com/laravel/art/master/logo-lockup/5%20SVG/2%20CMYK/1%20Full%20Color/laravel-logolockup-cmyk-red.svg" width="400" alt="Laravel Logo">
  </a>
</div>

<h1 align="center">Laravel Docker Boilerplate</h1>

<p align="center">
  A simple boilerplate for running Laravel applications with Docker, configured for both development and production environments.
</p>

---

## 🇮🇩 Versi Bahasa Indonesia

### 📋 Persyaratan

-   [Docker](https://www.docker.com/)

### 🛠️ Layanan

-   **Web Server**: Nginx
-   **Backend**: PHP 8.3
-   **Database**: MySQL
-   **Mail Server**: Mailpit
-   **Caching**: Redis
-   **WebSockets**: Soketi

### ⚙️ Instalasi Awal

Langkah-langkah ini hanya perlu dijalankan sekali saat pertama kali menyiapkan proyek.

1.  **Inisialisasi Proyek**
    -   Via Git:
        ```bash
        git clone [https://github.com/yogameleniawan/laravel-docker.git](https://github.com/yogameleniawan/laravel-docker.git)
        ```
    -   Via `.zip`: Ekstrak file `laravel-docker-main.zip`.

2.  **Masuk ke Direktori Proyek**
    ```bash
    cd laravel-docker
    ```

3.  **Salin File Environment**
    ```bash
    cp .env.example .env
    ```

### 🚀 Menjalankan Aplikasi

Pilih lingkungan yang ingin Anda jalankan.

#### Mode Development (Pengembangan) 🛠️

Mode ini menggunakan file `docker-compose.yml` dan cocok untuk pengembangan lokal.

1.  **Jalankan Docker Compose**
    ```bash
    docker compose up -d
    ```

2.  **Masuk ke Container & Instalasi Dependensi**
    ```bash
    # Masuk ke container PHP
    docker compose exec php bash

    # Instal dependensi PHP & JS
    composer install
    npm install

    # Generate key & jalankan migrasi
    php artisan key:generate
    php artisan migrate

    # Keluar dari container
    exit
    ```

3.  **Jalankan Vite Development Server**
    ```bash
    npm run dev
    ```

4.  **Selesai!** Buka [http://localhost](http://localhost) di browser Anda.

#### Mode Production (Produksi) 🚀

Mode ini menggunakan file `docker-compose.prod.yml` yang dioptimalkan untuk produksi.

1.  **Konfigurasi Environment Produksi**
    Buka file `.env` dan tambahkan atau sesuaikan variabel berikut, terutama jika Anda menggunakan **nginx-proxy** dengan **letsencrypt-nginx-proxy-companion**:
    ```ini
    # Sesuaikan dengan domain Anda
    VIRTUAL_HOST=domain-anda.com
    LETSENCRYPT_HOST=domain-anda.com
    LETSENCRYPT_EMAIL=email-anda@domain-anda.com
    ```
    Pastikan juga untuk mengatur `APP_URL` dan `DB_CONNECTION` sesuai dengan lingkungan produksi Anda.

2.  **Jalankan Docker Compose untuk Produksi**
    Gunakan flag `-f` untuk menunjuk file konfigurasi produksi.
    ```bash
    docker compose -f docker-compose.prod.yml up -d
    ```

3.  **Masuk ke Container & Persiapan Produksi**
    ```bash
    # Masuk ke container PHP
    docker compose -f docker-compose.prod.yml exec php bash

    # Instal dependensi (tanpa dev dependencies)
    composer install --no-dev --optimize-autoloader
    npm install

    # Build asset untuk produksi
    npm run build

    # Generate key, jalankan migrasi, dan optimalkan
    php artisan key:generate
    php artisan migrate --force # Gunakan --force untuk lingkungan non-lokal
    php artisan config:cache
    php artisan route:cache
    php artisan view:cache

    # Keluar dari container
    exit
    ```

4.  **Selesai!** Aplikasi Anda sekarang berjalan dalam mode produksi dan dapat diakses melalui domain yang telah Anda konfigurasikan.

![image](https://github.com/user-attachments/assets/b62ff6ac-acc5-47e8-82ee-1d6f8d2b5e09)

---

## 🇬🇧 English Version

### 📋 Requirements

-   [Docker](https://www.docker.com/)

### 🛠️ Services

-   **Web Server**: Nginx
-   **Backend**: PHP 8.3
-   **Database**: MySQL
-   **Mail Server**: Mailpit
-   **Caching**: Redis
-   **WebSockets**: Soketi

### ⚙️ Initial Setup

These steps only need to be run once when setting up the project for the first time.

1.  **Initialize The Project**
    -   Via Git:
        ```bash
        git clone [https://github.com/yogameleniawan/laravel-docker.git](https://github.com/yogameleniawan/laravel-docker.git)
        ```
    -   Via `.zip`: Extract the `laravel-docker-main.zip` file.

2.  **Navigate to The Project Directory**
    ```bash
    cd laravel-docker
    ```

3.  **Copy The Environment File**
    ```bash
    cp .env.example .env
    ```

### 🚀 Running the Application

Choose the environment you want to run.

#### Development Mode 🛠️

This mode uses the `docker-compose.yml` file and is ideal for local development.

1.  **Run Docker Compose**
    ```bash
    docker compose up -d
    ```

2.  **Enter Container & Install Dependencies**
    ```bash
    # Enter the PHP container
    docker compose exec php bash

    # Install PHP & JS dependencies
    composer install
    npm install

    # Generate key & run migrations
    php artisan key:generate
    php artisan migrate

    # Exit the container
    exit
    ```

3.  **Run the Vite Development Server**
    ```bash
    npm run dev
    ```

4.  **Done!** Open [http://localhost](http://localhost) in your browser.

#### Production Mode 🚀

This mode uses a `docker-compose.prod.yml` file optimized for production.

1.  **Configure Production Environment**
    Open your `.env` file and add or adjust the following variables, especially if you are using **nginx-proxy** with **letsencrypt-nginx-proxy-companion**:
    ```ini
    # Set this to your domain
    VIRTUAL_HOST=your-domain.com
    LETSENCRYPT_HOST=your-domain.com
    LETSENCRYPT_EMAIL=your-email@your-domain.com
    ```
    Also, ensure `APP_URL` and `DB_CONNECTION` are set correctly for your production environment.

2.  **Run Docker Compose for Production**
    Use the `-f` flag to specify the production configuration file.
    ```bash
    docker compose -f docker-compose.prod.yml up -d
    ```

3.  **Enter Container & Prepare for Production**
    ```bash
    # Enter the PHP container
    docker compose -f docker-compose.prod.yml exec php bash

    # Install dependencies (without dev dependencies)
    composer install --no-dev --optimize-autoloader
    npm install

    # Build assets for production
    npm run build

    # Generate key, run migrations, and optimize
    php artisan key:generate
    php artisan migrate --force # Use --force for non-local environments
    php artisan config:cache
    php artisan route:cache
    php artisan view:cache

    # Exit the container
    exit
    ```

4.  **Done!** Your application is now running in production mode and accessible via the domain you configured.

![image](https://github.com/user-attachments/assets/b62ff6ac-acc5-47e8-82ee-1d6f8d2b5e09)
