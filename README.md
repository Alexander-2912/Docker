# Docker

## Project Objective & Background
Background dari projek ini adalah melakukan deployment terhadap sebuah aplikasi website yang sudah dibuat sebelumnya. Website yang telah dibuat sebelumnya akan dideploy menggunakan docker sebagai tools utama. Dalam pengerjaannya, akan terdapat fitur-fitur dan batasan yang perlu diikuti. Dalam pengerjaan projek ini, hasil/objektif akhir yang diharapkan adalah terbuatnya dua buah image (flask dan postgresql) dan docker compose yang akan membangun kedua image tersebut.

##  Create Dockerfile to Build Flask App Images
### Langkah Pertama
Membuat file didalam direktori flask. Dockerfile ini akan berisi serangkaian perintah yang diperlukan untuk membangun image.

![image](https://github.com/Alexander-2912/Docker/assets/118685091/2acf0ff5-120f-42bb-bdcf-d917289d6363)

### Langkah Kedua
Melakukan pull image. Image yang akan digunakan akan dipilih dan diambil dari registry Docker Hub. Projek ini menggunakan image versi 3.10.12-bullseye

![image](https://github.com/Alexander-2912/Docker/assets/118685091/6252b75e-99a1-4d2f-9cef-9a5393064029)

### Langkah Ketiga
Melakukan copy data. Projek ini melakukan copy data dari './app' sehingga 'COPY . /app' akan menyalin semua file dan direktori yang ada dalam direktori saat ini (di mana Dockerfile berada) ke direktori /app di dalam container. 

![image](https://github.com/Alexander-2912/Docker/assets/118685091/9c96eea5-5ccf-41e8-b00e-6eae59cd2c24)

### Langkah Keempat
Menginstall requirements. Projek ini akan menginstall requirements yang terdaftar dalam 'requirements.txt'.

![image](https://github.com/Alexander-2912/Docker/assets/118685091/70943b3e-edc0-4334-a309-d7ddf0ffc6a1)
![image](https://github.com/Alexander-2912/Docker/assets/118685091/787a0988-445a-4ec6-b1e3-b699108d6e5d)

Berikut adalah penjelasan code pada gambar diatas: 
1. 'python -m' pip menjalankan perintah pip menggunakan interpreter Python yang terpasang di dalam container.
2. 'install' adalah perintah yang diberikan kepada pip untuk memulai proses instalasi.
3. '-r requirements.txt' memberikan argumen kepada pip untuk menginstal semua dependensi yang terdaftar dalam file requirements.txt. -r menunjukkan bahwa dependensi diambil dari file requirements.

### Langkah Kelima
Menyiapkan Command. 
