<p align="center"><a href="https://laravel.com" target="_blank"><img src="https://raw.githubusercontent.com/laravel/art/master/logo-lockup/5%20SVG/2%20CMYK/1%20Full%20Color/laravel-logolockup-cmyk-red.svg" width="400" alt="Laravel Logo"></a></p>

## Requirement

- [Docker](https://www.docker.com/)

## Service

- Nginx
- PHP 8.3
- MySQL
- Mailpit
- Redis
- Soketi
  
## Installation

1. Inisialisasi Projek

Buka Terminal (Jika menggunakan git)
```bash
git clone https://github.com/yogameleniawan/laravel-docker.git
```
Extract file `laravel-docker-main.zip` (Jika menggunakan .zip)

2. Buka folder hasil clone
```bash
cd laravel-docker
```
3. Jalankan perintah untuk copy .env
```bash
cp .env.example .env
```
4. Jalankan Docker Compose
```bash
docker compose up -d
``` 
5. Jalankan perintah untuk masuk ke container php
```bash
docker compose exec php bash
```
6. Jalankan perintah untuk melakukan instalasi dependency composer
```bash
composer install
```
7. Jalankan perintah untuk melakukan instalasi dependency node modules
```bash
npm install
```
8. Jalankan perintah untuk membuat key baru
```bash
php artisan key:generate
```
9. Jalankan perintah untuk mengeksekusi file migration
```bash
php artisan migrate
```
10. Untuk development bisa jalankan perintah berikut
```bash
npm run dev
```
11. Silahkan buka [localhost](http://localhost/) Jika berhasil maka hasilnya seperti ini

![image](https://github.com/user-attachments/assets/b62ff6ac-acc5-47e8-82ee-1d6f8d2b5e09)


