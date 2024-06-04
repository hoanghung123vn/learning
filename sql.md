# MySQL Cheat Sheet

## Tạo mới bảng

```sql
CREATE TABLE hoc_sinh(
id INT AUTO_INCREMENT,
   ho VARCHAR(100),
   ten VARCHAR(100),
   tuoi INT,
   PRIMARY KEY(id)
);
```

```sql
CREATE TABLE diem_cuoi_ky(
id INT AUTO_INCREMENT,
   mon_hoc VARCHAR(100),
   diem FLOAT,
   hoc_sinh_id INT,
   PRIMARY KEY(id)
);
```

## Thêm dữ liệu cho bảng

```sql
INSERT INTO hoc_sinh (ho, ten, tuoi) values
('Tong', 'Anh Thu', 18),
('Hoang', 'Van Hung', 28);
```

```sql
INSERT INTO diem_cuoi_ky (mon_hoc, diem, hoc_sinh_id) values
('Toan', 10, 1),
('Ly', 9, 1),
('Hoa', 9, 1),
('Toan', 10, 2),
('Ly', 9, 2),
('Hoa', 8, 2);
```

## Update dữ liệu

```sql
UPDATE hoc_sinh SET ho = 'Tong', ten = 'Anh Thu' WHERE id = 1;
```

## Lấy dữ liệu từ bảng

```sql
SELECT * FROM hoc_sinh;
SELECT ho, ten, tuoi FROM hoc_sinh;
```

## Từ khoá WHERE

```sql
SELECT * FROM hoc_sinh WHERE ho = 'Tong';
SELECT * FROM hoc_sinh WHERE tuoi > 10;
```

## Từ khoá BETWEEN

```sql
SELECT * FROM hoc_sinh WHERE tuoi BETWEEN 10 AND 30;
```

## Từ khoá ORDER BY: sắp xếp dữ liệu

```sql
SELECT * FROM hoc_sinh WHERE tuoi BETWEEN 10 AND 30 ORDER BY tuoi DESC;
```

## Từ khoá DISTINCT: lấy dữ liệu không bị trùng

```sql
SELECT DISTINCT ten FROM hoc_sinh;
```

## Từ khoá LIKE: tìm kiếm dữ liệu

```sql
SELECT * FROM hoc_sinh WHERE ten LIKE '%Anh Thu%;
```

## Từ khoá AND: tất cả các điều kiện đều phải thoả mãn

```sql
SELECT * FROM hoc_sinh WHERE ten = 'Anh Thu' AND tuoi = 18;
```

## Từ khoá OR: một trong các điều kiện thoả mãn là được

```sql
SELECT * FROM hoc_sinh WHERE ten = 'Anh Thu' OR ten = 'Van Hung';
```

## Từ khoá IN: công dụng tương tự từ khoá OR

```sql
SELECT * FROM hoc_sinh WHERE ten IN ('Anh Thu', 'Van Hung');
```

## JOIN: kết hợp dữ liệu từ nhiều bảng

```sql
SELECT * from hoc_sinh, diem_cuoi_ky WHERE hoc_sinh.id = diem_cuoi_ky.hoc_sinh_id;
SELECT * from hoc_sinh H, diem_cuoi_ky D WHERE H.id = D.hoc_sinh_id;
SELECT * from hoc_sinh H INNER JOIN diem_cuoi_ky D ON H.id = D.hoc_sinh_id;
```

## Các hàm tổng hợp

```sql
SELECT COUNT(id) FROM hoc_sinh;
SELECT COUNT(1) FROM hoc_sinh;
SELECT COUNT(*) FROM hoc_sinh;

SELECT MAX(tuoi) FROM hoc_sinh;
SELECT MIN(tuoi) FROM hoc_sinh;
SELECT SUM(tuoi) FROM hoc_sinh;

SELECT UCASE(ho), LCASE(ten) FROM hoc_sinh;
```

## Từ khoá GROUP BY: dùng để nhóm các dữ liệu theo một tiêu chí

```sql
# Đếm số lượng học sinh nhóm theo độ tuổi
SELECT tuoi, COUNT(1) as so_luong FROM hoc_sinh GROUP BY tuoi;
SELECT tuoi, COUNT(1) as so_luong FROM hoc_sinh GROUP BY tuoi ORDER BY tuoi ASC;
# Lấy ra điểm trung bình của các bạn học sinh theo tên, sắp xếp theo điểm trung bình tăng dần
SELECT H.ten, AVG(D.diem) as diem_trung_binh FROM hoc_sinh H INNER JOIN diem_cuoi_ky D ON H.id = D.hoc_sinh_id GROUP BY H.ten ORDER BY diem_trung_binh ASC;
# Lấy ra điểm trung bình trên 9 của các bạn học sinh theo tên, sắp xếp theo điểm trung bình tăng dần
SELECT H.ten, AVG(D.diem) as diem_trung_binh FROM hoc_sinh H INNER JOIN diem_cuoi_ky D ON H.id = D.hoc_sinh_id
GROUP BY H.ten HAVING diem_trung_binh > 9 ORDER BY diem_trung_binh ASC;
```
