# Sistem Informasi Manajemen Karyawan

Sistem ini merupakan implementasi basis data untuk manajemen karyawan, departemen, dan proyek dalam sebuah perusahaan. Tujuan dari sistem ini adalah untuk mempermudah pengelolaan data karyawan, alokasi proyek, dan supervisi karyawan.

## Struktur Basis Data

Basis data ini terdiri dari lima tabel utama:

1. `perusahaan`
2. `departemen`
3. `karyawan`
4. `project`
5. `project_detail`

### ER Diagram

![ER Diagram](https://path_to_your_image.jpg)

## Instalasi

Untuk menggunakan basis data ini, Anda dapat mengikuti langkah-langkah berikut:

1. **Clone repositori ini:**

    ```sh
    git clone https://github.com/username/repository-name.git
    cd repository-name
    ```

2. **Jalankan skrip SQL untuk membuat tabel dan mengisi data awal:**

    Buka file `database_setup.sql` dan jalankan perintah-perintah SQL di dalamnya pada database SQL Anda.

    ```sql
    -- Table for Perusahaan (Company)
    CREATE TABLE perusahaan (
        id_perusahaan VARCHAR(10) PRIMARY KEY,
        nama VARCHAR(100) NOT NULL,
        alamat VARCHAR(255) NOT NULL
    );

    -- Table for Departemen (Department)
    CREATE TABLE departemen (
        id_departemen VARCHAR(10) PRIMARY KEY,
        nama VARCHAR(100) NOT NULL,
        id_perusahaan VARCHAR(10) NOT NULL,
        nama_manager VARCHAR(100),
        FOREIGN KEY (id_perusahaan) REFERENCES perusahaan(id_perusahaan)
    );

    -- Table for Karyawan (Employee)
    CREATE TABLE karyawan (
        id_karyawan VARCHAR(10) PRIMARY KEY,
        nama VARCHAR(100) NOT NULL,
        id_departemen VARCHAR(10),
        id_supervisor VARCHAR(10),
        FOREIGN KEY (id_departemen) REFERENCES departemen(id_departemen),
        FOREIGN KEY (id_supervisor) REFERENCES karyawan(id_karyawan)
    );

    -- Table for Project
    CREATE TABLE project (
        id_project VARCHAR(10) PRIMARY KEY,
        nama VARCHAR(100) NOT NULL,
        tgl_mulai DATETIME NOT NULL,
        tgl_selesai DATETIME NOT NULL,
        status TINYINT(1) NOT NULL
    );

    -- Table for Project_Detail (Employee-Project Relationship)
    CREATE TABLE project_detail (
        id_project_detail VARCHAR(10) PRIMARY KEY,
        id_project VARCHAR(10) NOT NULL,
        id_karyawan VARCHAR(10) NOT NULL,
        FOREIGN KEY (id_project) REFERENCES project(id_project),
        FOREIGN KEY (id_karyawan) REFERENCES karyawan(id_karyawan)
    );

    -- Insert data into the tables
    -- Menambahkan data ke dalam tabel Perusahaan
    INSERT INTO perusahaan (id_perusahaan, nama, alamat) VALUES
    ('P001', 'Perusahaan ABC', 'Jl. Mawar No. 1'),
    ('P002', 'Perusahaan XYZ', 'Jl. Melati No. 2');

    -- Menambahkan data ke dalam tabel Departemen
    INSERT INTO departemen (id_departemen, nama, id_perusahaan, nama_manager) VALUES
    ('D001', 'Departemen IT', 'P001', 'Budi Santoso'),
    ('D002', 'Departemen HR', 'P001', 'Siti Aminah'),
    ('D003', 'Departemen Marketing', 'P002', 'Agus Salim');

    -- Menambahkan data ke dalam tabel Karyawan
    INSERT INTO karyawan (id_karyawan, nama, id_departemen, id_supervisor) VALUES
    ('K001', 'Ahmad Zaki', 'D001', NULL),
    ('K002', 'Rina Setiawan', 'D001', 'K001'),
    ('K003', 'Dewi Lestari', 'D002', NULL),
    ('K004', 'Joko Susanto', 'D003', 'K003'),
    ('K005', 'Fajar Nugroho', 'D003', 'K004');

    -- Menambahkan data ke dalam tabel Project
    INSERT INTO project (id_project, nama, tgl_mulai, tgl_selesai, status) VALUES
    ('PR001', 'Project Alpha', '2024-01-01 09:00:00', '2024-06-01 17:00:00', 1),
    ('PR002', 'Project Beta', '2024-02-01 09:00:00', '2024-07-01 17:00:00', 1);

    -- Menambahkan data ke dalam tabel Project_Detail
    INSERT INTO project_detail (id_project_detail, id_project, id_karyawan) VALUES
    ('PD001', 'PR001', 'K001'),
    ('PD002', 'PR001', 'K002'),
    ('PD003', 'PR002', 'K003'),
    ('PD004', 'PR002', 'K004'),
    ('PD005', 'PR002', 'K005');
    ```

3. **Verifikasi tabel dan data:**

    Pastikan tabel-tabel dan data telah ditambahkan dengan benar ke dalam basis data Anda.

## Lisensi
