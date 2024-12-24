# projek-basis-data

create database Pendataan_Apotek_13020230039;
use Pendataan_Apotek_13020230039;
drop database Pendataan_Apotek_13020230039;


-- Tabel Petugas
create table Petugas (
    id_Petugas int primary key, 
    Nama_Petugas varchar(100), 
    Jabatan enum('Kepala Apoteker', 'Apoteker', 'Asisten Apoteker', 'Staff Administrasi')
);

-- Tabel ObatMasuk
create table ObatMasuk (
    id_ObatM int primary key, 
    id_Petugas int, 
    Nama_Obat varchar(50), 
    Bentuk_Obat enum('Tablet', 'Sirup', 'Pil'), 
    Suhu_Penyimpanan varchar(30), 
    Tanggal_Masuk date, 
    Tanggal_Kadaluarsa date, 
    Kategori enum('Racikan', 'Non-Racikan'), 
    Harga_Obat int, 
    Dosis_Obat varchar(45), 
    Jumlah_Masuk int,
    foreign key (id_Petugas) references Petugas(id_Petugas)
);

-- Tabel ObatKeluar
create table ObatKeluar (
    id_ObatK int primary key, 
    id_ObatM int, 
    Keterangan enum('Transaksi', 'Kadaluarsa'), 
    Jumlah_Keluar int, 
    foreign key (id_ObatM) references ObatMasuk(id_ObatM)
);

-- Tabel Notifikasi
create table Notifikasi (
    id_Notifikasi int primary key, 
    id_ObatK int, 
    Tanggal_Notifikasi datetime, 
    Jenis_Notifikasi varchar(30), 
    foreign key (id_ObatK) references ObatKeluar(id_ObatK)
);

-- Tabel Transaksi
create table Transaksi (
    id_Transaksi int primary key, 
    id_Petugas int, 
    id_ObatK int, 
    Tanggal_Transaksi datetime, 
    Tipe_Transaksi varchar(100), 
    Jumlah_Transaksi int, 
    foreign key (id_ObatK) references ObatKeluar(id_ObatK), 
    foreign key (id_Petugas) references Petugas(id_Petugas)
);

-- Tabel Laporan
create table Laporan (
    id_Laporan int primary key, 
    id_Petugas int, 
    id_Transaksi int, 
    Tanggal_Laporan date, 
    foreign key (id_Transaksi) references Transaksi(id_Transaksi), 
    foreign key (id_Petugas) references Petugas(id_Petugas)
);



-- Insert data ke tabel Petugas
insert into Petugas (id_Petugas, Nama_Petugas, Jabatan) values
(1, 'Andi Pratama', 'Kepala Apoteker'),
(2, 'Budi Santoso', 'Apoteker'),
(3, 'Citra Dewi', 'Apoteker'),
(4, 'Dian Purnama', 'Asisten Apoteker'),
(5, 'Eka Wibowo', 'Asisten Apoteker'),
(6, 'Fajar Hidayat', 'Staff Administrasi'),
(7, 'Gita Permata', 'Staff Administrasi'),
(8, 'Hadi Saputra', 'Kepala Apoteker'),
(9, 'Indah Lestari', 'Apoteker'),
(10, 'Joko Riyadi', 'Asisten Apoteker');


-- Insert data ke tabel obatMasuk
insert into ObatMasuk (id_ObatM, id_Petugas, Nama_Obat, Bentuk_Obat, Suhu_Penyimpanan, Tanggal_Masuk, Tanggal_Kadaluarsa, Kategori, Harga_Obat, Dosis_Obat, Jumlah_Masuk) values
(1, 1, 'Paracetamol', 'Tablet', 'Suhu Ruangan', '2024-01-01', '2025-01-01', 'Non-Racikan', 5000, '500 mg', 100),
(2, 2, 'Amoxicillin', 'Sirup', '2-8°C', '2024-02-01', '2025-02-01', 'Non-Racikan', 15000, '250 mg', 50),
(3, 3, 'Ibuprofen', 'Tablet', 'Suhu Ruangan', '2024-03-01', '2025-03-01', 'Non-Racikan', 8000, '400 mg', 200),
(4, 4, 'Vitamin C', 'Tablet', 'Suhu Ruangan', '2024-04-01', '2025-04-01', 'Non-Racikan', 3000, '1000 mg', 150),
(5, 5, 'Antasida', 'Pil', 'Suhu Ruangan', '2024-05-01', '2025-05-01', 'Non-Racikan', 2000, '10 mg', 100),
(6, 6, 'Salbutamol', 'Sirup', '2-8°C', '2024-06-01', '2025-06-01', 'Non-Racikan', 12000, '2 mg', 80),
(7, 7, 'Metformin', 'Tablet', 'Suhu Ruangan', '2024-07-01', '2025-07-01', 'Non-Racikan', 10000, '500 mg', 120),
(8, 8, 'Captopril', 'Tablet', 'Suhu Ruangan', '2024-08-01', '2025-08-01', 'Non-Racikan', 6000, '50 mg', 100),
(9, 9, 'Ranitidine', 'Sirup', '2-8°C', '2024-09-01', '2025-09-01', 'Non-Racikan', 11000, '150 mg', 90),
(10, 10, 'Loperamide', 'Tablet', 'Suhu Ruangan', '2024-10-01', '2025-10-01', 'Non-Racikan', 4000, '2 mg', 200);


-- Insert data ke tabel obatKeluar
insert into ObatKeluar (id_ObatK, id_ObatM, Keterangan, Jumlah_Keluar) values
(1, 1, 'Transaksi', 10),
(2, 2, 'Transaksi', 5),
(3, 3, 'Kadaluarsa', 20),
(4, 4, 'Transaksi', 15),
(5, 5, 'Kadaluarsa', 10),
(6, 6, 'Transaksi', 8),
(7, 7, 'Kadaluarsa', 12),
(8, 8, 'Transaksi', 18),
(9, 9, 'Transaksi', 10),
(10, 10, 'Kadaluarsa', 25);


-- Insert data ke tabel Notifikasi
insert into Notifikasi (id_Notifikasi, id_ObatK, Tanggal_Notifikasi, Jenis_Notifikasi) values
(1, 3, '2024-11-01 08:00:00', 'Kadaluarsa'),
(2, 5, '2024-11-02 09:00:00', 'Kadaluarsa'),
(3, 7, '2024-11-03 10:00:00', 'Kadaluarsa'),
(4, 10, '2024-11-04 11:00:00', 'Kadaluarsa'),
(5, 1, '2024-11-05 12:00:00', 'Transaksi'),
(6, 2, '2024-11-06 13:00:00', 'Transaksi'),
(7, 4, '2024-11-07 14:00:00', 'Transaksi'),
(8, 6, '2024-11-08 15:00:00', 'Transaksi'),
(9, 8, '2024-11-09 16:00:00', 'Transaksi'),
(10, 9, '2024-11-10 17:00:00', 'Transaksi');


-- Insert data ke tabel Transaksi
insert into Transaksi (id_Transaksi, id_Petugas, id_ObatK, Tanggal_Transaksi, Tipe_Transaksi, Jumlah_Transaksi) values
(1, 1, 1, '2024-11-01 08:00:00', 'Tunai', 10),
(2, 2, 2, '2024-11-02 09:00:00', 'Transfer', 5),
(3, 3, 4, '2024-11-03 10:00:00', 'Tunai', 15),
(4, 4, 6, '2024-11-04 11:00:00', 'Transfer', 8),
(5, 5, 8, '2024-11-05 12:00:00', 'Tunai', 18),
(6, 6, 9, '2024-11-06 13:00:00', 'Transfer', 10),
(7, 7, 3, '2024-11-07 14:00:00', 'Tunai', 20),
(8, 8, 5, '2024-11-08 15:00:00', 'Tunai', 10),
(9, 9, 7, '2024-11-09 16:00:00', 'Tranfer', 12),
(10, 10, 10, '2024-11-10 17:00:00', 'Tunai', 25);


-- Insert data ke tabel Laporan
insert into Laporan (id_Laporan, id_Petugas, id_Transaksi, Tanggal_Laporan) values
(1, 1, 1, '2024-11-11'),
(2, 2, 2, '2024-11-12'),
(3, 3, 3, '2024-11-13'),
(4, 4, 4, '2024-11-14'),
(5, 5, 5, '2024-11-15'),
(6, 6, 6, '2024-11-16'),
(7, 7, 7, '2024-11-17'),
(8, 8, 8, '2024-11-18'),
(9, 9, 9, '2024-11-19'),
(10, 10, 10, '2024-11-20');


DELIMITER //
CREATE FUNCTION HitungStokObat(id_Obat INT)
RETURNS INT
BEGIN
    DECLARE jumlahMasuk INT DEFAULT 0;
    DECLARE jumlahKeluar INT DEFAULT 0;

  SELECT SUM(Jumlah_Masuk) INTO jumlahMasuk
  FROM ObatMasuk
  WHERE id_ObatM = id_Obat;

  SELECT SUM(jumlah_Keluar) INTO jumlahKeluar
  FROM ObatKeluar
  WHERE id_ObatK = id_Obat;

  RETURN jumlahMasuk - jumlahKeluar;
END //
DELIMITER ;
SELECT 
    OM.id_ObatM,
    OM.Nama_Obat,
    OM.Bentuk_Obat,
    OM.Suhu_Penyimpanan,
    OM.Tanggal_Masuk,
    OM.Tanggal_Kadaluarsa,
    OM.Kategori,
    OM.Harga_Obat,
    OM.Dosis_Obat,
    OM.Jumlah_Masuk,
    HitungStokObat(OM.id_ObatM) AS Total_Stok
FROM 
    ObatMasuk OM;
desc obatmasuk;

DELIMITER //
CREATE PROCEDURE tambahstokobat(
    IN p_id_Obat INT,
    IN p_id_Petugas INT,
    IN p_Nama_Obat VARCHAR(50),
    IN p_Bentuk_Obat ENUM('Tablet', 'Sirup', 'Pil'),
    IN p_Suhu_Penyimpanan VARCHAR(30),
    IN p_Tanggal_Masuk DATE,
    IN p_Tanggal_Kadaluarsa DATE,
    IN p_Kategori ENUM('Racikan', 'Non-Racikan'),
    IN p_Harga_Obat INT,
    IN p_Dosis_Obat VARCHAR(45),
    IN p_Jumlah_Masuk INT
)
BEGIN
    INSERT INTO ObatMasuk (
        id_ObatM, id_Petugas, Nama_Obat, 
        Bentuk_Obat, Suhu_Penyimpanan, Tanggal_Masuk, 
        Tanggal_Kadaluarsa, Kategori, Harga_Obat, 
        Dosis_Obat, Jumlah_Masuk
    ) VALUES (
        p_id_Obat, p_id_Petugas, p_Nama_Obat, 
        p_Bentuk_Obat, p_Suhu_Penyimpanan, p_Tanggal_Masuk, 
        p_Tanggal_Kadaluarsa, p_Kategori, p_Harga_Obat, 
        p_Dosis_Obat, p_Jumlah_Masuk
    );
END //
DELIMITER ;
drop procedure tambahstokobat;
    call tambahstokobat(12, 10, 'Salbutamol', 'Sirup', '2-8°C', '2024-05-03', '2025-06-01', 'Racikan', 12000, '2 mg', 80);
   
    
  create view laporan_obat as select a.id_obatm, a. Nama_Obat, b.id_petugas, b.Nama_Petugas, c.tanggal_transaksi, c.jumlah_transaksi,
  d.tanggal_laporan from obatmasuk a join petugas b on a.id_petugas = b.id_petugas join transaksi c on c.id_petugas=b.id_Petugas
  join laporan d on c.id_transaksi = d.id_transaksi;
  select * from laporan_obat;
    
    
delimiter $$
create trigger mengurangi_stok_obat
after insert on transaksi
for each row
begin
	update obatmasuk
    set jumlah_masuk = jumlah_masuk - new.jumlah_transaksi
    where id_obatm = new.id_obatk;
end $$
delimiter ;

insert into Transaksi (id_Transaksi, id_Petugas, id_ObatK, Tanggal_Transaksi, Tipe_Transaksi, Jumlah_Transaksi) values
(15, 4, 1, '2024-11-01 08:00:00', 'Penjualan', 12);
select * from obatmasuk;
drop trigger mengurangi_stok_obat;




















create database Pendataan_Apotek_13020230039;
use Pendataan_Apotek_13020230039;
drop database Pendataan_Apotek_13020230039;


-- Tabel Petugas
create table Petugas (
    id_Petugas int primary key, 
    Nama_Petugas varchar(100), 
    Jabatan enum('Kepala Apoteker', 'Apoteker', 'Asisten Apoteker', 'Staff Administrasi')
);

-- Tabel ObatMasuk
create table ObatMasuk (
    id_ObatM int primary key, 
    id_Petugas int, 
    Nama_Obat varchar(50), 
    Bentuk_Obat enum('Tablet', 'Sirup', 'Pil'), 
    Suhu_Penyimpanan varchar(30), 
    Tanggal_Masuk date, 
    Tanggal_Kadaluarsa date, 
    Kategori enum('Racikan', 'Non-Racikan'), 
    Harga_Obat int, 
    Dosis_Obat varchar(45), 
    Jumlah_Masuk int,
    foreign key (id_Petugas) references Petugas(id_Petugas)
);

-- Tabel ObatKeluar
create table ObatKeluar (
    id_ObatK int primary key, 
    id_ObatM int, 
    Keterangan enum('Transaksi', 'Kadaluarsa'), 
    Jumlah_Keluar int, 
    foreign key (id_ObatM) references ObatMasuk(id_ObatM)
);

-- Tabel Notifikasi
create table Notifikasi (
    id_Notifikasi int primary key, 
    id_ObatK int, 
    Tanggal_Notifikasi datetime, 
    Jenis_Notifikasi varchar(30), 
    foreign key (id_ObatK) references ObatKeluar(id_ObatK)
);

-- Tabel Transaksi
create table Transaksi (
    id_Transaksi int primary key, 
    id_Petugas int, 
    id_ObatK int, 
    Tanggal_Transaksi datetime, 
    Tipe_Transaksi varchar(100), 
    Jumlah_Transaksi int, 
    foreign key (id_ObatK) references ObatKeluar(id_ObatK), 
    foreign key (id_Petugas) references Petugas(id_Petugas)
);

-- Tabel Laporan
create table Laporan (
    id_Laporan int primary key, 
    id_Petugas int, 
    id_Transaksi int, 
    Tanggal_Laporan date, 
    foreign key (id_Transaksi) references Transaksi(id_Transaksi), 
    foreign key (id_Petugas) references Petugas(id_Petugas)
);



-- Insert data ke tabel Petugas
insert into Petugas (id_Petugas, Nama_Petugas, Jabatan) values
(1, 'Andi Pratama', 'Kepala Apoteker'),
(2, 'Budi Santoso', 'Apoteker'),
(3, 'Citra Dewi', 'Apoteker'),
(4, 'Dian Purnama', 'Asisten Apoteker'),
(5, 'Eka Wibowo', 'Asisten Apoteker'),
(6, 'Fajar Hidayat', 'Staff Administrasi'),
(7, 'Gita Permata', 'Staff Administrasi'),
(8, 'Hadi Saputra', 'Kepala Apoteker'),
(9, 'Indah Lestari', 'Apoteker'),
(10, 'Joko Riyadi', 'Asisten Apoteker');


-- Insert data ke tabel obatMasuk
insert into ObatMasuk (id_ObatM, id_Petugas, Nama_Obat, Bentuk_Obat, Suhu_Penyimpanan, Tanggal_Masuk, Tanggal_Kadaluarsa, Kategori, Harga_Obat, Dosis_Obat, Jumlah_Masuk) values
(1, 1, 'Paracetamol', 'Tablet', 'Suhu Ruangan', '2024-01-01', '2025-01-01', 'Non-Racikan', 5000, '500 mg', 100),
(2, 2, 'Amoxicillin', 'Sirup', '2-8°C', '2024-02-01', '2025-02-01', 'Non-Racikan', 15000, '250 mg', 50),
(3, 3, 'Ibuprofen', 'Tablet', 'Suhu Ruangan', '2024-03-01', '2025-03-01', 'Non-Racikan', 8000, '400 mg', 200),
(4, 4, 'Vitamin C', 'Tablet', 'Suhu Ruangan', '2024-04-01', '2025-04-01', 'Non-Racikan', 3000, '1000 mg', 150),
(5, 5, 'Antasida', 'Pil', 'Suhu Ruangan', '2024-05-01', '2025-05-01', 'Non-Racikan', 2000, '10 mg', 100),
(6, 6, 'Salbutamol', 'Sirup', '2-8°C', '2024-06-01', '2025-06-01', 'Non-Racikan', 12000, '2 mg', 80),
(7, 7, 'Metformin', 'Tablet', 'Suhu Ruangan', '2024-07-01', '2025-07-01', 'Non-Racikan', 10000, '500 mg', 120),
(8, 8, 'Captopril', 'Tablet', 'Suhu Ruangan', '2024-08-01', '2025-08-01', 'Non-Racikan', 6000, '50 mg', 100),
(9, 9, 'Ranitidine', 'Sirup', '2-8°C', '2024-09-01', '2025-09-01', 'Non-Racikan', 11000, '150 mg', 90),
(10, 10, 'Loperamide', 'Tablet', 'Suhu Ruangan', '2024-10-01', '2025-10-01', 'Non-Racikan', 4000, '2 mg', 200);


-- Insert data ke tabel obatKeluar
insert into ObatKeluar (id_ObatK, id_ObatM, Keterangan, Jumlah_Keluar) values
(1, 1, 'Transaksi', 10),
(2, 2, 'Transaksi', 5),
(3, 3, 'Kadaluarsa', 20),
(4, 4, 'Transaksi', 15),
(5, 5, 'Kadaluarsa', 10),
(6, 6, 'Transaksi', 8),
(7, 7, 'Kadaluarsa', 12),
(8, 8, 'Transaksi', 18),
(9, 9, 'Transaksi', 10),
(10, 10, 'Kadaluarsa', 25);


-- Insert data ke tabel Notifikasi
insert into Notifikasi (id_Notifikasi, id_ObatK, Tanggal_Notifikasi, Jenis_Notifikasi) values
(1, 3, '2024-11-01 08:00:00', 'Kadaluarsa'),
(2, 5, '2024-11-02 09:00:00', 'Kadaluarsa'),
(3, 7, '2024-11-03 10:00:00', 'Kadaluarsa'),
(4, 10, '2024-11-04 11:00:00', 'Kadaluarsa'),
(5, 1, '2024-11-05 12:00:00', 'Transaksi'),
(6, 2, '2024-11-06 13:00:00', 'Transaksi'),
(7, 4, '2024-11-07 14:00:00', 'Transaksi'),
(8, 6, '2024-11-08 15:00:00', 'Transaksi'),
(9, 8, '2024-11-09 16:00:00', 'Transaksi'),
(10, 9, '2024-11-10 17:00:00', 'Transaksi');


-- Insert data ke tabel Transaksi
insert into Transaksi (id_Transaksi, id_Petugas, id_ObatK, Tanggal_Transaksi, Tipe_Transaksi, Jumlah_Transaksi) values
(1, 1, 1, '2024-11-01 08:00:00', 'Penjualan', 10),
(2, 2, 2, '2024-11-02 09:00:00', 'Penjualan', 5),
(3, 3, 4, '2024-11-03 10:00:00', 'Penjualan', 15),
(4, 4, 6, '2024-11-04 11:00:00', 'Penjualan', 8),
(5, 5, 8, '2024-11-05 12:00:00', 'Penjualan', 18),
(6, 6, 9, '2024-11-06 13:00:00', 'Penjualan', 10),
(7, 7, 3, '2024-11-07 14:00:00', 'Kadaluarsa', 20),
(8, 8, 5, '2024-11-08 15:00:00', 'Kadaluarsa', 10),
(9, 9, 7, '2024-11-09 16:00:00', 'Kadaluarsa', 12),
(10, 10, 10, '2024-11-10 17:00:00', 'Kadaluarsa', 25);


-- Insert data ke tabel Laporan
insert into Laporan (id_Laporan, id_Petugas, id_Transaksi, Tanggal_Laporan) values
(1, 1, 1, '2024-11-11'),
(2, 2, 2, '2024-11-12'),
(3, 3, 3, '2024-11-13'),
(4, 4, 4, '2024-11-14'),
(5, 5, 5, '2024-11-15'),
(6, 6, 6, '2024-11-16'),
(7, 7, 7, '2024-11-17'),
(8, 8, 8, '2024-11-18'),
(9, 9, 9, '2024-11-19'),
(10, 10, 10, '2024-11-20');


DELIMITER //
CREATE FUNCTION HitungStokObat(id_Obat INT)
RETURNS INT
BEGIN
    DECLARE jumlahMasuk INT DEFAULT 0;
    DECLARE jumlahKeluar INT DEFAULT 0;
    DECLARE stokObat INT;

    -- Menghitung total jumlah obat masuk berdasarkan id_Obat
    SELECT SUM(Jumlah_Masuk) INTO jumlahMasuk
    FROM ObatMasuk
    WHERE id_ObatM = id_Obat;

    -- Menghitung total jumlah obat keluar berdasarkan id_Obat
    SELECT SUM(jumlah_Keluar) INTO jumlahKeluar
    FROM ObatKeluar
    WHERE id_ObatK = id_Obat;

    -- Menghitung stok
    SET stokObat = IFNULL(jumlahMasuk, 0) - IFNULL(jumlahKeluar, 0);

    RETURN stokObat;
END //
DELIMITER ;
SELECT Hitungstokobat() AS StokObat;
drop function Hitungstokobat;

DELIMITER //

CREATE FUNCTION HitungTotalStok()
RETURNS INT
DETERMINISTIC
BEGIN
    DECLARE totalStok INT DEFAULT 0;
    
    -- Menghitung total stok obat yang tersisa
    SELECT SUM(Jumlah_Masuk) - IFNULL((SELECT SUM(Jumlah_Keluar) 
	   FROM ObatKeluar
	   WHERE ObatKeluar.id_ObatM = ObatMasuk.id_ObatM), 0)
    INTO totalStok
    FROM ObatMasuk;
    
    RETURN totalStok;
END //
DELIMITER ;



DELIMITER //
CREATE PROCEDURE LihatObatKadaluarsa()
BEGIN
    SELECT 
        a.id_ObatM,
        P.Nama_Petugas,
        a.Nama_Obat,
        a.Tanggal_Kadaluarsa,
        a.Kategori,
        a.Bentuk_Obat,
        b.Keterangan
    FROM 
        ObatMasuk a JOIN 
        Petugas P ON a.id_Petugas = P.id_Petugas 
        join ObatKeluar b on a.id_ObatM = b.id_ObatM
    WHERE 
         b.Keterangan = 'Kadaluarsa'
	order by a.Tanggal_Kadaluarsa ASC;
END //
DELIMITER ;
CALL LihatObatKadaluarsa();
drop procedure LihatObatKadaluarsa;



DELIMITER //
CREATE TRIGGER KurangiStokObat
AFTER INSERT ON Transaksi
FOR EACH ROW
BEGIN
    -- Kurangi jumlah stok obat pada tabel ObatMasuk
    UPDATE ObatMasuk
    SET Jumlah_Masuk = Jumlah_Masuk - NEW.Jumlah_Transaksi
    WHERE id_ObatM = NEW.id_ObatK;
END //

DELIMITER ;
INSERT INTO Transaksi (id_Transaksi, id_Petugas, id_ObatK, Tanggal_Transaksi, Tipe_Transaksi, Jumlah_Transaksi)
VALUES (1, 1, 1, '2024-12-11', 'Penjualan', 10);



DELIMITER //
CREATE TRIGGER PindahkanObatKadaluarsa
AFTER UPDATE ON ObatMasuk
FOR EACH ROW
BEGIN
    -- Memeriksa apakah obat sudah kadaluarsa
    IF NEW.Tanggal_Kadaluarsa < CURDATE() THEN
        -- Memasukkan data obat kadaluarsa ke tabel ObatKeluar
        INSERT INTO ObatKeluar (id_ObatK, id_Petugas, Keterangan, Obat_Kadaluarsa)
        VALUES (NEW.id_ObatM, NULL, 'Kadaluarsa', NEW.Jumlah_Masuk);

        -- Mengatur stok obat kadaluarsa di tabel ObatMasuk menjadi 0
        UPDATE ObatMasuk
        SET Jumlah_Masuk = 0
        WHERE id_ObatM = NEW.id_ObatM;
    END IF;
END //
DELIMITER ;

UPDATE ObatMasuk
SET Tanggal_Kadaluarsa = '2023-11-30'
WHERE id_ObatM = 1;



DELIMITER //
CREATE TRIGGER SetelahObatMasuk
AFTER INSERT ON ObatMasuk
FOR EACH ROW
BEGIN
    -- Memeriksa jika jumlah obat yang dimasukkan lebih besar dari 0
    IF NEW.Jumlah_Masuk > 0 THEN
        -- Insert notifikasi ke tabel Notifikasi untuk setiap obat yang baru dimasukkan
        INSERT INTO Notifikasi (id_ObatK, Tanggal_Notifikasi, Jenis_Notifikasi)
        VALUES (NEW.id_ObatM, NOW(), 'Obat Masuk');
    END IF;
END //
DELIMITER ;
INSERT INTO ObatMasuk (id_ObatM, id_Petugas, Nama_Obat, Bentuk_Obat, Suhu_Penyimpanan, Tanggal_Masuk, Tanggal_Kadaluarsa, Kategori, Harga_Obat, Dosis_Obat, Jumlah_Masuk)
VALUES (11, 1, 'Metformin', 'Tablet', 'Suhu Ruangan', '2024-12-11', '2025-12-11', 'Non-Racikan', 10000, '500 mg', 50);
SELECT * FROM Notifikasi;










