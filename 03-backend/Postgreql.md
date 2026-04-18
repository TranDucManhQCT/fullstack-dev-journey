# PostgreSQL - Huong Dan Chi Tiet

## 1. PostgreSQL La Gi?

PostgreSQL la he quan tri co so du lieu quan he mo nguon (RDBMS) manh me, ho tro SQL tieu chuan va nhieu tinh nang nang cao. No duoc su dung rong rai trong cac ung dung web, data warehouse va phan tich du lieu.

---

## 2. Cai Dat PostgreSQL

### Windows
1. Tai installer tai: https://www.postgresql.org/download/windows/
2. Chay file `.exe`, chon thu muc cai dat
3. Dat mat khau cho user `postgres`
4. Chon port (mac dinh: `5432`)
5. Hoan tat cai dat

### Mac (dung Homebrew)
```bash
brew install postgresql
brew services start postgresql
```

### Linux (Ubuntu/Debian)
```bash
sudo apt update
sudo apt install postgresql postgresql-contrib
sudo systemctl start postgresql
sudo systemctl enable postgresql
```

---

## 3. Ket Noi Vao PostgreSQL

### Dung psql (terminal)
```bash
psql -U postgres
```

### Ket noi den database cu the
```bash
psql -U postgres -d ten_database
```

### Thoat psql
```sql
\q
```

---

## 4. Cac Lenh psql Hay Dung

| Lenh | Chuc nang |
|------|-----------|
| `\l` | Liet ke tat ca database |
| `\c ten_db` | Chuyen sang database khac |
| `\dt` | Liet ke tat ca bang trong DB hien tai |
| `\d ten_bang` | Xem cau truc cua bang |
| `\du` | Liet ke tat ca user |
| `\?` | Xem tro giup |
| `\q` | Thoat psql |

---

## 5. Quan Ly Database

### Tao database
```sql
CREATE DATABASE ten_database;
```

### Xoa database
```sql
DROP DATABASE ten_database;
```

### Chon database de lam viec
```bash
\c ten_database
```

---

## 6. Quan Ly Bang (Table)

### Tao bang
```sql
CREATE TABLE nguoi_dung (
    id SERIAL PRIMARY KEY,
    ten VARCHAR(100) NOT NULL,
    email VARCHAR(150) UNIQUE NOT NULL,
    tuoi INT CHECK (tuoi >= 0),
    ngay_tao TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

### Xem cau truc bang
```sql
\d nguoi_dung
```

### Xoa bang
```sql
DROP TABLE nguoi_dung;
```

### Them cot vao bang
```sql
ALTER TABLE nguoi_dung ADD COLUMN dia_chi TEXT;
```

### Xoa cot khoi bang
```sql
ALTER TABLE nguoi_dung DROP COLUMN dia_chi;
```

### Doi ten cot
```sql
ALTER TABLE nguoi_dung RENAME COLUMN ten TO ho_ten;
```

---

## 7. Cac Kieu Du Lieu Thuong Gap

| Kieu du lieu | Mo ta |
|--------------|-------|
| `INT` | So nguyen |
| `SERIAL` | So nguyen tu tang (dung cho ID) |
| `VARCHAR(n)` | Chuoi ky tu co gioi han |
| `TEXT` | Chuoi ky tu khong gioi han |
| `BOOLEAN` | Dung / Sai (true/false) |
| `FLOAT` | So thap phan |
| `NUMERIC(p,s)` | So chinh xac cao |
| `DATE` | Ngay (yyyy-mm-dd) |
| `TIMESTAMP` | Ngay gio |
| `JSON` / `JSONB` | Du lieu JSON |

---

## 8. Thao Tac Du Lieu (CRUD)

### Them du lieu (INSERT)
```sql
INSERT INTO nguoi_dung (ten, email, tuoi)
VALUES ('Nguyen Van A', 'a@gmail.com', 25);
```

### Them nhieu dong cung luc
```sql
INSERT INTO nguoi_dung (ten, email, tuoi) VALUES
    ('Tran Thi B', 'b@gmail.com', 30),
    ('Le Van C', 'c@gmail.com', 22);
```

### Xem du lieu (SELECT)
```sql
-- Xem tat ca
SELECT * FROM nguoi_dung;

-- Xem cac cot cu the
SELECT ten, email FROM nguoi_dung;

-- Co dieu kien
SELECT * FROM nguoi_dung WHERE tuoi > 20;

-- Sap xep
SELECT * FROM nguoi_dung ORDER BY tuoi DESC;

-- Gioi han so luong
SELECT * FROM nguoi_dung LIMIT 5;

-- Bo qua so hang dau
SELECT * FROM nguoi_dung OFFSET 10;
```

### Cap nhat du lieu (UPDATE)
```sql
UPDATE nguoi_dung
SET tuoi = 26
WHERE id = 1;
```

### Xoa du lieu (DELETE)
```sql
DELETE FROM nguoi_dung WHERE id = 1;

-- Xoa tat ca (can than!)
DELETE FROM nguoi_dung;
```

---

## 9. Dieu Kien Loc (WHERE)

```sql
-- Ket hop dieu kien
SELECT * FROM nguoi_dung WHERE tuoi > 18 AND ten = 'Nguyen Van A';

-- Hoac
SELECT * FROM nguoi_dung WHERE tuoi < 18 OR tuoi > 60;

-- Pham vi
SELECT * FROM nguoi_dung WHERE tuoi BETWEEN 20 AND 30;

-- Trong danh sach
SELECT * FROM nguoi_dung WHERE tuoi IN (18, 21, 25);

-- Tim kiem chuoi (LIKE)
SELECT * FROM nguoi_dung WHERE ten LIKE 'Nguyen%';

-- Khong phan biet hoa thuong (ILIKE)
SELECT * FROM nguoi_dung WHERE ten ILIKE 'nguyen%';

-- Kiem tra NULL
SELECT * FROM nguoi_dung WHERE dia_chi IS NULL;
SELECT * FROM nguoi_dung WHERE dia_chi IS NOT NULL;
```

---

## 10. Ham Tong Hop (Aggregate Functions)

```sql
-- Dem so hang
SELECT COUNT(*) FROM nguoi_dung;

-- Tinh trung binh
SELECT AVG(tuoi) FROM nguoi_dung;

-- Gia tri lon nhat / nho nhat
SELECT MAX(tuoi), MIN(tuoi) FROM nguoi_dung;

-- Tong
SELECT SUM(tuoi) FROM nguoi_dung;

-- Nhom du lieu (GROUP BY)
SELECT tuoi, COUNT(*) AS so_nguoi
FROM nguoi_dung
GROUP BY tuoi;

-- Loc nhom (HAVING)
SELECT tuoi, COUNT(*) AS so_nguoi
FROM nguoi_dung
GROUP BY tuoi
HAVING COUNT(*) > 1;
```

---

## 11. Ket Hop Bang (JOIN)

Gia su co 2 bang: `nguoi_dung` va `don_hang`

```sql
-- INNER JOIN: chi lay hang co lien ket 2 phia
SELECT nd.ten, dh.san_pham
FROM nguoi_dung nd
INNER JOIN don_hang dh ON nd.id = dh.nguoi_dung_id;

-- LEFT JOIN: lay tat ca nguoi dung, ke ca chua co don hang
SELECT nd.ten, dh.san_pham
FROM nguoi_dung nd
LEFT JOIN don_hang dh ON nd.id = dh.nguoi_dung_id;

-- RIGHT JOIN: lay tat ca don hang, ke ca khong co nguoi dung
SELECT nd.ten, dh.san_pham
FROM nguoi_dung nd
RIGHT JOIN don_hang dh ON nd.id = dh.nguoi_dung_id;
```

---

## 12. Rang Buoc (Constraints)

```sql
CREATE TABLE san_pham (
    id SERIAL PRIMARY KEY,           -- Khoa chinh
    ten VARCHAR(100) NOT NULL,       -- Khong duoc de trong
    gia NUMERIC(10,2) CHECK (gia > 0), -- Gia phai > 0
    ma_sp VARCHAR(50) UNIQUE,        -- Khong trung lap
    danh_muc_id INT REFERENCES danh_muc(id) -- Khoa ngoai
);
```

---

## 13. Index (Chi Muc)

Index giup tang toc do truy van, nhung ton them bo nho.

```sql
-- Tao index
CREATE INDEX idx_nguoi_dung_email ON nguoi_dung(email);

-- Tao unique index
CREATE UNIQUE INDEX idx_nguoi_dung_email_unique ON nguoi_dung(email);

-- Xoa index
DROP INDEX idx_nguoi_dung_email;

-- Xem cac index trong bang
\d nguoi_dung
```

---

## 14. View (Bang Ao)

View la truy van duoc luu lai de tai su dung.

```sql
-- Tao view
CREATE VIEW nguoi_dung_tre AS
SELECT * FROM nguoi_dung WHERE tuoi < 30;

-- Dung view nhu bang binh thuong
SELECT * FROM nguoi_dung_tre;

-- Xoa view
DROP VIEW nguoi_dung_tre;
```

---

## 15. Transaction (Giao Dich)

Transaction dam bao nhieu lenh SQL thuc hien thanh cong cung hoac that bai cung.

```sql
BEGIN;

UPDATE tai_khoan SET so_du = so_du - 100 WHERE id = 1;
UPDATE tai_khoan SET so_du = so_du + 100 WHERE id = 2;

-- Neu khong co loi, luu lai
COMMIT;

-- Neu co loi, hoan tac
ROLLBACK;
```

---

## 16. Stored Procedure va Function

### Tao function
```sql
CREATE OR REPLACE FUNCTION tinh_tuoi(nam_sinh INT)
RETURNS INT AS $$
BEGIN
    RETURN EXTRACT(YEAR FROM CURRENT_DATE) - nam_sinh;
END;
$$ LANGUAGE plpgsql;

-- Goi function
SELECT tinh_tuoi(2000);
```

---

## 17. Quan Ly User va Quyen

```sql
-- Tao user
CREATE USER ten_user WITH PASSWORD 'mat_khau';

-- Cap quyen tren database
GRANT ALL PRIVILEGES ON DATABASE ten_db TO ten_user;

-- Cap quyen tren bang
GRANT SELECT, INSERT ON nguoi_dung TO ten_user;

-- Thu hoi quyen
REVOKE INSERT ON nguoi_dung FROM ten_user;

-- Xoa user
DROP USER ten_user;
```

---

## 18. Backup va Restore

### Backup
```bash
# Backup mot database
pg_dump -U postgres ten_database > backup.sql

# Backup toan bo server
pg_dumpall -U postgres > tat_ca.sql
```

### Restore
```bash
# Restore mot database
psql -U postgres ten_database < backup.sql

# Restore toan bo
psql -U postgres < tat_ca.sql
```

---

## 19. Mot So Ham Xu Ly Chuoi

```sql
-- Viet hoa
SELECT UPPER('hello');          -- HELLO
SELECT LOWER('HELLO');          -- hello

-- Do dai chuoi
SELECT LENGTH('hello');         -- 5

-- Ghep chuoi
SELECT CONCAT('Xin ', 'chao');  -- Xin chao
SELECT 'Xin ' || 'chao';        -- Xin chao

-- Cat chuoi
SELECT TRIM('  hello  ');       -- hello
SELECT SUBSTRING('hello' FROM 2 FOR 3); -- ell
```

---

## 20. Mot So Ham Xu Ly Ngay Gio

```sql
-- Ngay hien tai
SELECT CURRENT_DATE;

-- Gio hien tai
SELECT CURRENT_TIME;

-- Ngay gio hien tai
SELECT NOW();

-- Trich xuat nam, thang, ngay
SELECT EXTRACT(YEAR FROM NOW());
SELECT EXTRACT(MONTH FROM NOW());
SELECT EXTRACT(DAY FROM NOW());

-- Cong them khoang thoi gian
SELECT NOW() + INTERVAL '7 days';
SELECT NOW() - INTERVAL '1 month';
```

---

## 21. Ket Noi PostgreSQL Tu Node.js

### Cai dat thu vien
```bash
npm install pg
```

### Vi du ket noi
```javascript
const { Pool } = require('pg');

const pool = new Pool({
    user: 'postgres',
    host: 'localhost',
    database: 'ten_database',
    password: 'mat_khau',
    port: 5432,
});

// Truy van du lieu
async function layNguoiDung() {
    const result = await pool.query('SELECT * FROM nguoi_dung');
    console.log(result.rows);
}

layNguoiDung();
```

### Vi du voi tham so (tranh SQL injection)
```javascript
async function timNguoiDung(email) {
    const result = await pool.query(
        'SELECT * FROM nguoi_dung WHERE email = $1',
        [email]
    );
    return result.rows[0];
}
```

---

## 22. Ket Noi PostgreSQL Tu Python

### Cai dat thu vien
```bash
pip install psycopg2-binary
```

### Vi du ket noi
```python
import psycopg2

conn = psycopg2.connect(
    host="localhost",
    database="ten_database",
    user="postgres",
    password="mat_khau"
)

cur = conn.cursor()
cur.execute("SELECT * FROM nguoi_dung")
rows = cur.fetchall()

for row in rows:
    print(row)

cur.close()
conn.close()
```

---

## 23. Cac Loi Thuong Gap Va Cach Xu Ly

| Loi | Nguyen nhan | Giai phap |
|-----|-------------|-----------|
| `connection refused` | PostgreSQL chua chay | Khoi dong dich vu PostgreSQL |
| `permission denied` | User khong co quyen | Cap quyen cho user |
| `duplicate key` | Vi pham rang buoc UNIQUE | Kiem tra du lieu truoc khi them |
| `null value in column` | Them NULL vao cot NOT NULL | Dam bao du lieu day du |
| `relation does not exist` | Bang chua duoc tao | Kiem tra ten bang, tao bang truoc |

---

## 24. Meo Toi Uu Hieu Suat

1. **Them INDEX** cho cac cot thuong xuyen dung trong WHERE, JOIN, ORDER BY
2. **Dung EXPLAIN ANALYZE** de phan tich truy van cham
```sql
EXPLAIN ANALYZE SELECT * FROM nguoi_dung WHERE email = 'a@gmail.com';
```
3. **Tranh SELECT star** (`SELECT *`) khi khong can thiet, chi lay cot can dung
4. **Dung LIMIT** khi chi can mot so hang nhat dinh
5. **Dung connection pool** thay vi tao ket noi moi moi lan
6. **Chon kieu du lieu phu hop**: dung `INT` thay `TEXT` cho so, `BOOLEAN` thay `CHAR(1)`

