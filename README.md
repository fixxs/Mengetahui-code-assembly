# Mengetahui-code-assembly

# Nama  :FIKRI RUSDINERZA
# Kelas  :SKU 2B
# MK      :Organisasi & Arsiitektur Komputer


![Screenshot 2025-04-14 150649](https://github.com/user-attachments/assets/0514c373-2755-4e5f-92ab-5f596d7d785b)




## 🔧 SECTION .data ##

![image](https://github.com/user-attachments/assets/afcd12a6-71cd-43e8-9564-b180bcda9a6d)

* db: define byte (mendeklarasikan string). 

* 10 = newline (ASCII untuk baris baru).

* 0 = null terminator (standar untuk string).

* noLen dan yesLen: menghitung panjang pesan secara otomatis (equ $ - label).

## 🔧 SECTION .text ##

![image](https://github.com/user-attachments/assets/95850885-1932-4bd0-9302-6c0320b6c070)

* Mendefinisikan titik masuk utama program (untuk Linux).

  ## ▶️ _start: ##

  ![image](https://github.com/user-attachments/assets/e6a45905-e6c4-4b26-9836-307887d8853b)

  * Kita langsung menggunakan angka tetap 100 dan simpan di rsi sebagai angka yang ingin dicek.
## ✅ Cek kondisi awal ##

![image](https://github.com/user-attachments/assets/da64856d-e8e5-450d-8cfb-abd5529455d6)

* Jika angka kurang dari 2 (misal: 0 atau 1), bukan prima.

## 🔁 Loop untuk cek prima ##

![image](https://github.com/user-attachments/assets/ac525f56-11d4-4363-b923-84fa800896d9)

* Mulai dari rcx = 2 (bilangan pembagi).

* div rcx: bagi rsi dengan rcx, hasil sisa disimpan di rdx.

* Kalau rdx == 0 → bisa dibagi tanpa sisa → bukan prima.

## 🔄 Naikkan pembagi dan lanjut loop ##

![image](https://github.com/user-attachments/assets/f25c39ff-a738-419d-aa7e-1be53d454fd0)

* Cek apakah kuadrat rcx (yaitu rcx * rcx) masih lebih kecil atau sama dengan angka (rsi).

* Jika masih, lanjut loop.

* Tujuannya: kita hanya perlu mengecek pembagi hingga √n, efisien secara matematis.

## 🎉 Jika lolos semua pengecekan → prima ##

![image](https://github.com/user-attachments/assets/7242bd02-3310-48d1-9614-4c0f5a109277)

* Ini akan ditrigger kalau nggak ketemu pembagi dari 2 sampai √n (alias angka tersebut cuma bisa dibagi 1 dan dirinya sendiri).

* Dia akan tampilkan string “Angka prima” ke layar pake syscall Linux write.


## ❌ Kalau ketemu pembagi → bukan prima ##


![image](https://github.com/user-attachments/assets/f39cedf3-a617-4783-9d7e-1a8ede2488c5)

# mov rax, 1 #
* syscall write rax digunakan untuk menyimpan nomor syscall di Linux.1 adalah syscall untuk write, artinya kita ingin menulis data ke file descriptor (biasanya terminal).

# mov rdi, 1 # 
* stdout Argumen pertama syscall write adalah file descriptor: 0 → stdin (input dari keyboard) 1 → stdout (keluar ke terminal) 2 → stderr (error output)Jadi rdi = 1 artinya kita mau menulis ke terminal (stdout).

# mov rsi, no #
* alamat string "Bukan angka prima" Argumen kedua syscall write adalah alamat dari data yang ingin ditulis.
* rsi diisi dengan alamat label no, yang isinya "Bukan angka prima".

# mov rdx, noLen #
* panjang string Argumen ketiga syscall write adalah panjang data yang ingin ditulis.
* rdx diisi dengan panjang dari string "Bukan angka prima" yang sudah dihitung sebelumnya: 10 di akhir string adalah newline (ASCII 10), biar hasilnya rapi pas tampil di terminal.

# syscall #
Ini instruksi untuk menjalankan syscall berdasarkan nilai register:

* rax = nomor syscall (1 → write)
* rdi = file descriptor (1 → stdout)
* rsi = alamat string
* rdx = panjang string



