# Sistem-Manajemen-Daftar-Film-V2


Nama : Ahmad Fajar Novia

Kelas : B

NIM : 2509116041

Sistem ini adalah aplikasi sederhana CRUD Film
Bisa lihat, tambah, update, dan hapus film.
Menggunakan Dictionary, Looping, Functions, Error Handling.
Sistem login dengan role (admin dan manusia)
========================================================
- Sistem login dengan dua role pengguna: admin dan manusia.
- Admin: dapat melakukan CRUD lengkap (lihat, tambah, update, hapus).
- User: hanya dapat melihat daftar film.
- Data film disimpan dalam dictionary.
- Tampilan daftar film menggunakan PrettyTable agar rapi.
- Program dilengkapi error handling untuk inputan yang salah

---

FLOWCHART

<img width="1626" height="2712" alt="Diagram Tanpa Judul drawio (3)" src="https://github.com/user-attachments/assets/641a12fb-c2be-4046-bcde-9bdb9f4a20cc" />


---

Dalam sistem ini terdapat **4 menu utama**, yaitu:

1. **Lihat Film**
2. **Tambah Film**
3. **Hapus Film**
4. **Keluar**

---

Menu 1 yaitu Lihat Film

* Input **1** untuk masuk ke menu **Lihat Film**.
* Sistem akan menampilkan daftar film yang tersedia.
* Jika ingin melihat detail film, ketik judul film yang sudah ada dalam list.
* Jika terjadi salah ketik atau film tidak ada, sistem akan menampilkan:
  ```
  Film tidak ditemukan
  ```
* Setelah itu, sistem kembali ke menu utama.

---

Menu 2 yaitu Tambah Film

* Input **2** untuk masuk ke menu **Tambah Film**.
* Sistem akan meminta input data film secara berurutan:

  * Judul
  * Genre
  * Pembuat
  * Sinopsis
  * Tanggal Rilis
  * Pemeran
* Setelah semua data diisi, sistem menambahkan film ke list dan menampilkan:

  ```
  Film berhasil ditambahkan
  ```
* Untuk mengecek apakah film berhasil ditambahkan, masuk ke **Menu Lihat Film**.

---

Menu 3 yaitu Hapus Film

* Input **3** untuk masuk ke menu **Hapus Film**.
* Sistem akan menampilkan daftar film terlebih dahulu.
* Masukkan **judul film** yang ingin dihapus.
* Jika judul tepat sesuai list, film akan dihapus dan menampilkan:

  ```
  Film berhasil dihapus!
  ```
* Jika salah ketik atau film tidak ada, sistem menampilkan:

  ```
  Film tidak ditemukan!
  ```
* Setelah itu, sistem kembali ke menu utama.

---

Menu 4 yaitu Keluar

* Input **4** untuk keluar dari program.
* Sistem akan menampilkan:

  ```
  Program selesai
  ```
* Program berhenti.

---

Input Tidak Valid

* Jika pengguna memasukkan angka selain 1-4, sistem akan menampilkan:

  ```
  Pilihan tidak valid!
  ```
* Sistem akan kembali ke menu utama.

---

CODE
  ```
from prettytable import PrettyTable
import getpass

# library
users = {
    "admin": {"password": "123", "role": "admin"},
    "fajar": {"password": "123", "role": "user"}
}

film_list = {
    1: {"judul": "Avengers Endgame", "genre": "Action", "pembuat": "Marvel Studio", "sinopsis": "Pertarungan melawan Thanos.", "tgl_rilis": "2019-04-26", "pemeran": "Robert Downey Jr, Chris Evans"},
    2: {"judul": "John Wick", "genre": "Action", "pembuat": "Lionsgate", "sinopsis": "Seorang mantan pembunuh bayaran membalas dendam.", "tgl_rilis": "2014-10-24", "pemeran": "Keanu Reeves"}
}

# fungsi sistem
def lihat_film():
    table = PrettyTable()
    table.field_names = ["ID", "Judul", "Genre", "Pembuat", "Tgl Rilis", "Pemeran"]
    for id_film, data in film_list.items():
        table.add_row([id_film, data["judul"], data["genre"], data["pembuat"], data["tgl_rilis"], data["pemeran"]])
    print(table)

def tambah_film():
    while True:
        try:
            id_film = int(input("Masukkan ID film baru: "))
            if id_film in film_list:
                print("Masukkan ID lain")
                continue
            judul = input("Masukkan judul: ")
            genre = input("Masukkan genre: ")
            pembuat = input("Masukkan pembuat: ")
            sinopsis = input("Masukkan sinopsis: ")
            tgl_rilis = input("Masukkan tanggal rilis: ")
            pemeran = input("Masukkan pemeran: ")
            film_list[id_film] = {
                "judul": judul,
                "genre": genre,
                "pembuat": pembuat,
                "sinopsis": sinopsis,
                "tgl_rilis": tgl_rilis,
                "pemeran": pemeran
            }
            print("Film berhasil ditambahkan!")
            break
        except ValueError:
            print("Tolong masukkan angka.")
        except KeyboardInterrupt:
            print("Kartu kuning")
            break
        except EOFError:
            print("Kartu merah")
            break

def update_film():
    while True:
        lihat_film()
        try:
            id_film = int(input("Masukkan ID film: "))
            if id_film in film_list:
                print("Kosongkan input jika tidak ingin mengubah.")
                judul = input(f"Judul ({film_list[id_film]['judul']}): ") or film_list[id_film]['judul']
                genre = input(f"Genre ({film_list[id_film]['genre']}): ") or film_list[id_film]['genre']
                pembuat = input(f"Pembuat ({film_list[id_film]['pembuat']}): ") or film_list[id_film]['pembuat']
                sinopsis = input(f"Sinopsis ({film_list[id_film]['sinopsis']}): ") or film_list[id_film]['sinopsis']
                tgl_rilis = input(f"Tgl Rilis ({film_list[id_film]['tgl_rilis']}): ") or film_list[id_film]['tgl_rilis']
                pemeran = input(f"Pemeran ({film_list[id_film]['pemeran']}): ") or film_list[id_film]['pemeran']
                film_list[id_film] = {
                    "judul": judul,
                    "genre": genre,
                    "pembuat": pembuat,
                    "sinopsis": sinopsis,
                    "tgl_rilis": tgl_rilis,
                    "pemeran": pemeran
                }
                print("Film berhasil diperbarui!")
                break
            else:
                print("ID film tidak ada")
        except ValueError:
            print("Tolong masukkan angka.")
        except KeyboardInterrupt:
            print("Kartu kuning")
            break
        except EOFError:
            print("Kartu merah")
            break

def hapus_film():
    while True:
        lihat_film()
        try:
            id_film = int(input("Masukkan ID film yang ingin dihapus: "))
            if id_film in film_list:
                del film_list[id_film]
                print("Film berhasil dihapus!")
                break
            else:
                print("ID film tidak ada")
        except ValueError:
            print("Tolong masukkan angka.")
        except KeyboardInterrupt:
            print("Kartu kuning")
            break
        except EOFError:
            print("Kartu merah")
            break

# menu login
try:
    print("=== Login ===")
    username = input("Username: ")
    password = getpass.getpass("Password: ")

    if username in users and users[username]["password"] == password:
        role = users[username]["role"]
        print(f"Login berhasil {username} ({role})")
    else:
        print("Login gagal!")
        exit()
except KeyboardInterrupt:
    print("Kartu kuning")
    exit()
except EOFError:
    print("Kartu merah")
    exit()

# menu admiin
if role == "admin":
    while True:
        try:
            print("\n===== Menu Admin =====")
            print("1. Lihat Film")
            print("2. Tambah Film")
            print("3. Update Film")
            print("4. Hapus Film")
            print("5. Keluar")
            pilihan = input("Masukkan pilihan: ")

            if pilihan == "1":
                lihat_film()
            elif pilihan == "2":
                tambah_film()
            elif pilihan == "3":
                update_film()
            elif pilihan == "4":
                hapus_film()
            elif pilihan == "5":
                print("Program selesai.")
                break
            else:
                print("Pilihan tidak ada")
        except ValueError:
            print("Tolong masukkan angka.")
        except KeyboardInterrupt:
            print("Kartu kuning")
        except EOFError:
            print("Kartu merah")

# Menu User
elif role == "user":
    while True:
        try:
            print("\n===== Menu User =====")
            print("1. Lihat Film")
            print("2. Keluar")
            pilihan = input("Masukkan pilihan: ")

            if pilihan == "1":
                lihat_film()
            elif pilihan == "2":
                print("Program selesai.")
                break
            else:
                print("Pilihan tidak ada")
        except ValueError:
            print("Tolong masukkan angka.")
        except KeyboardInterrupt:
            print("Kartu kuning")
        except EOFError:
            print("Kartu merah")
  ```
---

## 1. Sistem Login

<img width="181" height="70" alt="Screenshot 2025-09-28 120003" src="https://github.com/user-attachments/assets/eb77a798-14cb-4800-a6af-bcd01ae5e1fe" />


Sebelum mengakses menu utama, pengguna harus login:

* **Input:** Username dan Password.
* **Validasi:** Sistem memeriksa username dan password yang dimasukkan sesuai dengan database.
* **Role:** Sistem mengenali peran pengguna, yaitu `admin` atau `user`.
* **Login Gagal:** Jika data tidak sesuai, muncul pesan **"Login gagal!"** dan program berhenti.

**Error Handling saat Login:**

<img width="588" height="111" alt="1" src="https://github.com/user-attachments/assets/744fb17d-8cff-4e02-ab8f-6864b07166aa" />


* CTRL + C → muncul pesan **"Kartu kuning"**
* CTRL + Z → muncul pesan **"Kartu merah"**

---

## 2. Menu Admin

Admin memiliki akses penuh dengan 5 menu utama:

1. **Lihat Film**
2. **Tambah Film**
3. **Update Film**
4. **Hapus Film**
5. **Keluar**

**Error Handling:**

<img width="526" height="834" alt="2" src="https://github.com/user-attachments/assets/e0b8617a-9d5a-441b-ae54-e07834150705" />

* CTRL + C → muncul pesan **"Kartu kuning"**
* CTRL + Z → muncul pesan **"Kartu merah"**

---
### Opsi 1 – Lihat Film

<img width="967" height="419" alt="login admin masukkan pilihan 1" src="https://github.com/user-attachments/assets/8f8c8f18-60ec-416b-8e12-8ff20577bdee" />

* Menampilkan daftar semua film dalam bentuk tabel dengan kolom:
  `ID`, `Judul`, `Genre`, `Pembuat`, `Tanggal Rilis`, `Pemeran`.
* Admin dapat melihat seluruh data film yang tersimpan.

---

### Opsi 2 – Tambah Film

<img width="599" height="444" alt="menu admin milih opsi 2 jika id film tidak ada akan ngulang terus dan jika id film ada tambahkan" src="https://github.com/user-attachments/assets/9682a576-1a76-4d30-988a-1fbe86895193" />

* Admin memasukkan **ID film baru** dan detail film (judul, genre, pembuat, sinopsis, tanggal rilis, pemeran).
* **Jika ID sudah ada:** muncul pesan **"Masukkan ID lain"**, sistem meminta admin memasukkan ID baru.
* **Jika ID valid:** film ditambahkan ke daftar, muncul pesan **"Film berhasil ditambahkan!"**

**Error Handling:**

<img width="540" height="392" alt="3" src="https://github.com/user-attachments/assets/8f0a3d5a-04b0-43ea-98b0-4cab3c25cef7" />


* Input ID harus angka → jika bukan angka → **"Tolong masukkan angka."**
* CTRL + C → muncul pesan **"Kartu kuning"**
* CTRL + Z → muncul pesan **"Kartu merah"**

---

### Opsi 3 – Update Film

<img width="952" height="726" alt="admin opsi 3" src="https://github.com/user-attachments/assets/84044354-fc30-40ad-ba09-3ea496f87dc2" />


* Admin memilih **ID film** yang ingin diubah.
* Jika ID ditemukan:

  * Sistem menampilkan data lama dari setiap kolom.
  * Admin bisa menekan **Enter** untuk tetap menggunakan data lama.
  * Setelah selesai, muncul pesan **"Film berhasil diperbarui!"**
* Jika ID tidak ditemukan → muncul pesan **"ID film tidak ada"**, admin diminta memasukkan ulang.

**Error Handling:**

<img width="962" height="669" alt="4" src="https://github.com/user-attachments/assets/afb96b58-92ed-4905-bf29-d9e6ca7ff125" />

* Input harus angka → jika tidak → **"Tolong masukkan angka."**
* CTRL + C → muncul pesan **"Kartu kuning"**
* CTRL + Z → muncul pesan **"Kartu merah"**

---

### Opsi 4 – Hapus Film

<img width="966" height="564" alt="admin menu 4" src="https://github.com/user-attachments/assets/9000f4ba-27b7-4fbc-b01b-ca2aaebc74f0" />


* Admin memasukkan **ID film** yang ingin dihapus.
* Jika ID valid → film dihapus, muncul pesan **"Film berhasil dihapus!"**
* Jika ID tidak ada → muncul pesan **"ID film tidak ada"**, kembali ke menu.

**Error Handling:**

<img width="937" height="527" alt="5" src="https://github.com/user-attachments/assets/09598c30-6c3c-41fb-92ff-a0fd2d2153e6" />

* Input harus angka → jika tidak → **"Tolong masukkan angka."**
* CTRL + C → muncul pesan **"Kartu kuning"**
* CTRL + Z → muncul pesan **"Kartu merah"**

---

### Opsi 5 – Keluar

<img width="670" height="199" alt="menu 5 keluar" src="https://github.com/user-attachments/assets/034f0b09-a60b-4bed-a134-448157cbc703" />


* Sistem menampilkan pesan **"Program selesai."**

---

## 3. Menu User

User hanya mempunyai 2 menu :

1. **Lihat Film**
2. **Keluar**

### Opsi 1 – Lihat Film

<img width="969" height="341" alt="login user pilih 1" src="https://github.com/user-attachments/assets/3deffa67-2bc1-43f6-acb8-6acf1d52bbec" />

* User dapat melihat seluruh daftar film dalam tabel sama seperti admin.

### Opsi 2 – Keluar

* User keluar dari program dengan pesan **"Program selesai."**

**Error Handling untuk User:**

* CTRL + C → muncul pesan **"Kartu kuning"**
* CTRL + Z → muncul pesan **"Kartu merah"**

---


