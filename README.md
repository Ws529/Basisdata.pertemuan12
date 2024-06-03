# TugasPraktikum5
# Tugas Praktikum { Pertemuan ke 12 } <img src=https://logos-download.com/wp-content/uploads/2016/05/MySQL_logo_logotype.png width="130px" >


|**Nama**|**NIM**|**Kelas**|**Matkul**|
|----|---|-----|------|
|Wawan Suwandi|312310457|TI.23.A.5|Basis Data|


# Soal Latihan Praktikum 

![alt text](Picture/1.PNG)

```
-- Membuat Tabel Mahasiswa
CREATE TABLE Mahasiswa (
    nim VARCHAR(10) PRIMARY KEY,
    nama VARCHAR(50),
    jk CHAR(1),
    tgl_lahir DATE,
    jalan VARCHAR(100),
    kota VARCHAR(50),
    kodepos VARCHAR(10),
    no_hp VARCHAR(15),
    kd_ds VARCHAR(5),
    FOREIGN KEY (kd_ds) REFERENCES Dosen(kd_ds)
);
```

![alt text](Picture/2.PNG)

```sql
-- Membuat Tabel Dosen
CREATE TABLE Dosen (
    kd_ds VARCHAR(5) PRIMARY KEY,
    nama VARCHAR(50)
);
```

![alt text](Picture/3.PNG)

```
-- Membuat Tabel MataKuliah
CREATE TABLE MataKuliah (
    kd_mk VARCHAR(5) PRIMARY KEY,
    nama VARCHAR(100),
    sks INT
);

```

![alt text](Picture/4.PNG)

```
-- Membuat Tabel Jadwal
CREATE TABLE Jadwal (
    kd_mk VARCHAR(5),
    kd_ds VARCHAR(5),
    hari VARCHAR(10),
    jam TIME,
    ruang VARCHAR(10),
    PRIMARY KEY (kd_mk, kd_ds, hari, jam),
    FOREIGN KEY (kd_mk) REFERENCES MataKuliah(kd_mk),
    FOREIGN KEY (kd_ds) REFERENCES Dosen(kd_ds)
);
```

![alt text](Picture/5.PNG)

```
-- Membuat Tabel KRS
CREATE TABLE KRS (
    nim VARCHAR(10),
    kd_mk VARCHAR(5),
    kd_ds VARCHAR(5),
    semester INT,
    nilai CHAR(2),
    PRIMARY KEY (nim, kd_mk),
    FOREIGN KEY (kd_mk) REFERENCES MataKuliah(kd_mk),
    FOREIGN KEY (kd_ds) REFERENCES Dosen(kd_ds)
);
```

## Latihan

- Lakukan JOIN table Mahasiswa dan Dosen.
- Lakukan JOIN tabel Matakuliah dan Dosen.
- Lakukan JOIN table JadwalMengajar, Dosen, dan Matakuliah.
- Lakukan JOIN tabel KrsMahasiswa, Mahasiswa, Matakuliah, dan Dosen.

## Buat Script SQL JOIN Table berdasarkan skema data diatas.

![alt text](Picture/SS1.png)
![alt text](Picture/SS2.png)

# Latihan
- JOIN table Mahasiswa dan Dosen
`````
SELECT Mahasiswa.nim, Mahasiswa.nama AS nama_mahasiswa, Mahasiswa.jk AS jenis_kelamin, Dosen.nama AS nama_dosen
FROM Mahasiswa
JOIN Dosen ON Mahasiswa.kd_ds = Dosen.kd_ds;

`````
Output :
![alt text](Picture/LL1.png)

- Lakukan JOIN tabel Matakuliah dan Dosen.
`````
SELECT MataKuliah.kd_mk, MataKuliah.nama AS nama_matakuliah, MataKuliah.sks, Dosen.nama AS nama_dosen
FROM MataKuliah
LEFT JOIN Jadwal ON MataKuliah.kd_mk = Jadwal.kd_mk
LEFT JOIN Dosen ON Jadwal.kd_ds = Dosen.kd_ds;
`````
Output:
![alt text](Picture/LL2.png)

- JOIN table JadwalMengajar, Dosen, dan Matakuliah
`````
SELECT Jadwal.kd_mk, MataKuliah.nama AS nama_matakuliah, Dosen.nama AS nama_dosen, Jadwal.hari, Jadwal.jam, Jadwal.ruang
FROM Jadwal
JOIN Dosen ON Jadwal.kd_ds = Dosen.kd_ds
JOIN MataKuliah ON Jadwal.kd_mk = MataKuliah.kd_mk;
`````
Output :
![alt text](Picture/LL3.png)

- JOIN tabel KRSMahasiswa, Mahasiswa, Matakuliah, dan Dosen
`````
SELECT KRS.nim, Mahasiswa.nama AS nama_mahasiswa, Mahasiswa.jk AS jenis_kelamin, Mahasiswa.tgl_lahir, MataKuliah.nama AS nama_matakuliah, Dosen.nama AS nama_dosen, KRS.semester, KRS.nilai
FROM KRS
JOIN Mahasiswa ON KRS.nim = Mahasiswa.nim
JOIN MataKuliah ON KRS.kd_mk = MataKuliah.kd_mk
JOIN Dosen ON KRS.kd_ds = Dosen.kd_ds;
`````
Output :
![alt text](Picture/LL4.png)

## SELESAI <img align="center" alt="Ikhsan-Python" height="40" width="45" src="https://em-content.zobj.net/source/microsoft-teams/337/student_1f9d1-200d-1f393.png"> <img align="center" alt="Ikhsan-Python" height="40" width="45" src="https://em-content.zobj.net/thumbs/160/twitter/348/flag-indonesia_1f1ee-1f1e9.png">
