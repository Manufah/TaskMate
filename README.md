# TaskMate
Simple CLI To-Do List manager built with Python

# Gambaran Project
Sebuah sistem interaktif CLI sederhana untuk mengelola daftar tugas kuliah, mencatat deadline, melihat urutan tugas, menandai tugas selesai, dan menghapus tugas

## Computational Thinking

### 1. Dekomposisi
* **Lihat Tugas**: Menampilkan daftar tugas beserta ID/nomor tugas
* **Tambah Tugas**: Menerima input nama mata kuliah, nama tugas, dan deadline
* **Tandai Selesai**: Mengubah status tugas dari "Belum" menjadi "Selesai" berdasarkan ID
* **Hapus Tugas**: Menghapus tugas dari daftar berdasarkan ID setelah konfirmasi
* **Penyimpanan Data**: Membaca data saat aplikasi dibuka dan menyimpan pembaruan ke file
* **Keluar**: Menampilkan pesan perpisahan dan menghentikan perulangan program

### 2. Pengenalan Pola
* Setiap entitas tugas memiliki struktur data yang konsisten (ID, nama matkul, nama tugas, deadline, status)
* Modul Tambah, Tandai Selesai, dan Hapus memiliki alur serupa: Minta Input -> Olah Data di Memori -> Simpan

### 3. Abstraksi
* **Data Diproses**: Nama mata kuliah, nama tugas, deadline, status
* **Data Diabaikan**: Nama dosen, lokasi kelas, bobot SKS

### 4. Algoritma
1. Memuat data tugas dari file ke memori
2. Masuk ke perulangan utama (main loop) menu 1–5
3. Memproses opsi pilihan pengguna (Lihat, Tambah, Tandai, Hapus, Keluar)
4. Menyimpan data ke file JSON saat pengguna memilih keluar

---

## Pseudo Code
```
FUNCTION lihat_tugas(list_tugas)
	IF list_tugas KOSONG THEN
		OUTPUT "Belum ada tugas yang tersimpan."
	ELSE
		OUTPUT list_tugas
	END IF
END FUNCTION

FUNCTION tambah_tugas(list_tugas)
	INPUT nama_tugas, nama_matkul, deadline
	BUAT data_baru (id, nama_tugas, nama_matkul, deadline, status="Belum")
	APPEND data_baru TO list_tugas
	OUTPUT "Tugas berhasil ditambahkan!"
END FUNCTION

FUNCTION tandai_selesai(list_tugas)
	INPUT id_tugas
	ditemukan = False
	FOR EACH tugas IN list_tugas
		IF tugas.id == id_tugas THEN
			tugas.status = "Selesai"
			ditemukan = True
			OUTPUT "Status tugas berhasil diubah menjadi Selesai!"
			BREAK
		END IF
	END FOR
	IF ditemukan == False THEN
		OUTPUT "ID tugas tidak ditemukan!"
	END IF
END FUNCTION

FUNCTION hapus_tugas(list_tugas)
	INPUT id_tugas
	ditemukan = False
	FOR EACH tugas IN list_tugas
		IF tugas.id == id_tugas THEN
			ditemukan = True
			INPUT "Yakin ingin menghapus? (Ya/Tidak)" TO konfirmasi
			IF konfirmasi == "Ya" THEN
				HAPUS tugas FROM list_tugas
				OUTPUT "Tugas berhasil dihapus!"
			ELSE
				OUTPUT "Penghapusan dibatalkan."
			END IF
			BREAK
		END IF
	END FOR
	IF ditemukan == False THEN
		OUTPUT "ID tugas tidak ditemukan!"
	END IF
END FUNCTION


BEGIN
	list_tugas = []
	pilihan = 0
	WHILE pilihan != 5
		OUTPUT "Pilih aktivitas (1. Lihat, 2. Tambah, 3. Tandai, 4. Hapus, 5. Keluar)"
		INPUT pilihan
		IF pilihan == 1 THEN
			lihat_tugas(list_tugas)
		ELIF pilihan == 2 THEN
			tambah_tugas(list_tugas)
		ELIF pilihan == 3 THEN
			tandai_selesai(list_tugas)
		ELIF pilihan == 4 THEN
			hapus_tugas(list_tugas)
		ELIF pilihan == 5 THEN
			SIMPAN list_tugas TO "data_tugas.json"
			OUTPUT "Thank you for using TaskMate. Have a good day :)"
			BREAK
		ELSE
			OUTPUT "Pilihan tidak valid! Pilih dari 1-5"
		END IF
	END WHILE
END PROGRAM