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
Menyiapkan Command. CMD ["python", "run.py"] adalah perintah default dalam Dockerfile yang akan dijalankan saat container Docker berjalan. Perintah ini akan menjalankan skrip run.py menggunakan interpreter Python di dalam container.

![image](https://github.com/Alexander-2912/Docker/assets/118685091/42998db8-e39c-40a9-b510-821aeb4bac00)

Skrip run.py kemudian akan menjalankan aplikasi Flask dengan mengatur host menjadi '0.0.0.0' agar dapat diakses secara eksternal.

![image](https://github.com/Alexander-2912/Docker/assets/118685091/109fe350-5786-4743-9396-8cc405cdd393)

Pada baris pertama, 'from app import create_app' mengimport fungsi create_app dari modul app. Fungsi ini bertanggung jawab untuk membuat dan mengkonfigurasi objek Flask yang mewakili aplikasi.

Pada baris kedua, 'if __name__ == "__main__":' adalah kondisi yang mengecek apakah skrip ini dijalankan langsung sebagai program utama. Ini berarti kode di dalam blok kondisi ini hanya akan dieksekusi jika skrip ini dijalankan secara langsung, bukan diimpor oleh skrip lain.

Pada baris ketiga, 'app = create_app()' memanggil fungsi create_app() untuk membuat objek Flask dan menyimpannya dalam variabel app. Fungsi create_app() biasanya berisi konfigurasi aplikasi Flask, seperti mengatur rute, menginisialisasi ekstensi, dan pengaturan lainnya.

Pada baris keempat, 'app.run(host='0.0.0.0')' memulai server Flask dan menjalankan aplikasi dengan mengikatnya ke host '0.0.0.0'. Dengan pengaturan host ini, aplikasi Flask akan dapat diakses dari semua alamat IP yang terhubung ke container.

## Langkah Keenam
Membangun image. 
```
docker build -t flask:0.0.6 .
```
Command diatas digunakan untuk membangun (build) sebuah gambar Docker dengan nama flask:0.0.6. Opsi -t digunakan untuk memberikan tag pada gambar yang dibangun sehingga dapat diidentifikasi dan digunakan saat membuat container. Titik (.) pada akhir perintah menunjukkan bahwa Dockerfile yang digunakan untuk membangun gambar berada dalam direktori saat ini.

## Langkah ketuju
Membuat container.
```
docker create -p 5000:5000 --name flask-container flask:0.0.6
```
Command diatas digunakan untuk membuat sebuah container dengan nama flask-container menggunakan gambar Docker yang telah dibangun sebelumnya dengan tag flask:0.0.6. Opsi -p 5000:5000 mengarahkan port 5000 di host ke port 5000 di dalam container, sehingga aplikasi Flask yang berjalan di dalam container dapat diakses melalui port 5000 pada host.
