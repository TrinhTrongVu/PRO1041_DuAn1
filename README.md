CREATE DATABASE QuanLyBanGiay_DA1_Nhom4
USE QuanLyBanGiay_DA1_Nhom4
GO
-- ChucVu
CREATE TABLE ChucVu(
Id UNIQUEIDENTIFIER PRIMARY KEY DEFAULT NEWID(),
Ma VARCHAR(20) UNIQUE,
Ten NVARCHAR(50) DEFAULT NULL
)
GO
-- NhanVien
CREATE TABLE NhanVien(
Id UNIQUEIDENTIFIER PRIMARY KEY DEFAULT NEWID(),
IdCV UNIQUEIDENTIFIER,
Ma VARCHAR(20) UNIQUE,
HoTen NVARCHAR(100),
TaiKhoan VARCHAR(MAX) DEFAULT NULL,
MatKhau VARCHAR(MAX) DEFAULT NULL,
Sdt VARCHAR(30) DEFAULT NULL,
Email  VARCHAR(100) DEFAULT NULL,
GioiTinh NVARCHAR(10) DEFAULT NULL,
NgaySinh DATE DEFAULT NULL,
DiaChi NVARCHAR(100) DEFAULT NULL
)
GO
-- KhachHang
CREATE TABLE KhachHang(
Id UNIQUEIDENTIFIER PRIMARY KEY DEFAULT NEWID(),
Ma VARCHAR(20) UNIQUE,
HoTen NVARCHAR(100),
Sdt VARCHAR(30),
NgaySinh DATE DEFAULT NULL,
DiaChi NVARCHAR(100) DEFAULT NULL,
)
GO
-- SanPham
CREATE TABLE SanPham(
Id UNIQUEIDENTIFIER PRIMARY KEY DEFAULT NEWID(),
Ma VARCHAR(20) UNIQUE,
Ten NVARCHAR(30)
)
GO
-- DeGiay
CREATE TABLE DeGiay(
Id UNIQUEIDENTIFIER PRIMARY KEY DEFAULT NEWID(),
Ma VARCHAR(20) UNIQUE,
Ten NVARCHAR(30)
)
GO
-- MauSac
CREATE TABLE MauSac(
Id UNIQUEIDENTIFIER PRIMARY KEY DEFAULT NEWID(),
Ma VARCHAR(20) UNIQUE,
Ten NVARCHAR(30)
)
GO
-- DongSP
CREATE TABLE DongSP(
Id UNIQUEIDENTIFIER PRIMARY KEY DEFAULT NEWID(),
Ma VARCHAR(20) UNIQUE,
Ten NVARCHAR(30)
)
GO
-- ChiTietSP
CREATE TABLE ChiTietSP(
Id UNIQUEIDENTIFIER PRIMARY KEY DEFAULT NEWID(),
IdSP UNIQUEIDENTIFIER,
IdDongSP UNIQUEIDENTIFIER,
IdDeGiay UNIQUEIDENTIFIER,
IdMauSac UNIQUEIDENTIFIER,
NgayNhapHang DATE DEFAULT NULL,
DonGia DECIMAL(20,0) DEFAULT 0,
SoLuong INT,
XuatXu NVARCHAR(50) DEFAULT NULL,
KichCo NVARCHAR(20),
TrangThai int DEFAULT 0
)
GO
--SanPhamLoi
CREATE TABLE DoiTra(
Id UNIQUEIDENTIFIER PRIMARY KEY DEFAULT NEWID(),
IdCTSP UNIQUEIDENTIFIER,
IdHD UNIQUEIDENTIFIER,
IdKH UNIQUEIDENTIFIER,
NgayDoi DATE DEFAULT NULL,
SoLuong INT,
LiDoDoi NVARCHAR(50) DEFAULT NULL,
GhiChu NVARCHAR(100) DEFAULT NULL
)
GO

--HoaDon
CREATE TABLE HoaDon(
Id UNIQUEIDENTIFIER PRIMARY KEY DEFAULT NEWID(),
IdKH UNIQUEIDENTIFIER,
IdNV UNIQUEIDENTIFIER,
IdVoucher UNIQUEIDENTIFIER,
Ma VARCHAR(20) UNIQUE,
NgayTao DATE DEFAULT NULL,
NgayThanhToan DATE DEFAULT NULL,
TongTien DECIMAL(20,0) DEFAULT 0,
TongSanPham INT,
TrangThai INT DEFAULT 0
)
GO

-- HoaDonChiTiet
CREATE TABLE HoaDonChiTiet(
Id UNIQUEIDENTIFIER PRIMARY KEY DEFAULT NEWID(),
IdHoaDon UNIQUEIDENTIFIER,
IdChiTietSP UNIQUEIDENTIFIER,
SoLuong INT,
DonGia DECIMAL(20,0) DEFAULT 0
)

-- Voucher
CREATE TABLE Voucher(
Id UNIQUEIDENTIFIER PRIMARY KEY DEFAULT NEWID(),
Ma VARCHAR(20) UNIQUE,
Ten NVARCHAR(100),
GiamGia FLOAT,
NgayBatDau DATE DEFAULT NULL,
NgayHetHan DATE DEFAULT NULL,
GhiChu Nvarchar(100) DEFAULT NULL,
TrangThai INT DEFAULT 0
)

GO
--T?O QUAN H? GI?A CÁC B?NG
--NhanVien - ChucVu
ALTER TABLE NhanVien ADD FOREIGN KEY (IdCV) REFERENCES ChucVu(Id)

-- ChiTietSP - SanPham
ALTER TABLE ChiTietSP ADD FOREIGN KEY(IdSP) REFERENCES SanPham(Id)
-- ChiTietSP - DongSP
ALTER TABLE ChiTietSP ADD FOREIGN KEY(IdDongSP) REFERENCES DongSP(Id)
-- ChiTietSP - DeGiay
ALTER TABLE ChiTietSP ADD FOREIGN KEY(IdDeGiay) REFERENCES DeGiay(Id)
-- ChiTietSP - MauSac
ALTER TABLE ChiTietSP ADD FOREIGN KEY(IdMauSac) REFERENCES MauSac(Id)
-- ChiTietSP - NhaCC

-- DoiTra - CTSanPham
ALTER TABLE DoiTra ADD FOREIGN KEY(IdCTSP) REFERENCES ChiTietSP(Id)
-- DoiTra - HoaDon
ALTER TABLE DoiTra ADD FOREIGN KEY(IdHD) REFERENCES HoaDon(Id)
-- DoiTra - KhachHang
ALTER TABLE DoiTra ADD FOREIGN KEY(IdKH) REFERENCES KhachHang(Id)


--HoaDonCT - ChiTietSP
ALTER TABLE HoaDonChiTiet ADD FOREIGN KEY(IdHoaDon) REFERENCES HoaDon(Id)
--HoaDonCT - ChiTietSP
ALTER TABLE HoaDonChiTiet ADD FOREIGN KEY(IdChiTietSP) REFERENCES ChiTietSP(Id)

-- HoaDon - KhachHang
ALTER TABLE HoaDon ADD FOREIGN KEY (IdKH) REFERENCES KhachHang(Id)
-- HoaDon - NhanVien
ALTER TABLE HoaDon ADD FOREIGN KEY (IdNV) REFERENCES NhanVien(Id)
-- HoaDon - Voucher
ALTER TABLE HoaDon ADD FOREIGN KEY (IdVoucher) REFERENCES Voucher(Id)




--**********************************************************************
-- PHẦN INSERT CHẠY RIÊNG NHÉ !!!
-- BẢNG NÀO KHÔNG CÓ KHÓA PHỤ THÌ CỨ THẾ MÀ BÔI ÐEN XONG EXECUTE
-- BẢNG NÀO CÓ KHÓA PHỤ THÌ SỬA PHẦN ID ÐỂ MAPPING VỚI BẢNG CÒN LẠI
--
--
--
--
--
--
--
--
--
--
--
--
--***********************************************************************
--Insert ChucVu
INSERT INTO ChucVu VALUES (NEWID(),'CV01',N'Quản lý')
INSERT INTO ChucVu VALUES (NEWID(),'CV02',N'Nhân viên')
Select * from ChucVu

--Insert NhanVien
Select * from NhanVien
INSERT INTO NhanVien VALUES(NEWID(),'532A3C16-B396-4148-A369-CFEA33B39A87','NV01',N'Tr?n Ð?c Bo','nhanvien01','nv01','0989031433','boductran1980@gmail.com',N'Nam','07-06-1999',N's? 3 ngõ 178 Lê Ð?c Th?, Hà N?i')
INSERT INTO NhanVien VALUES(NEWID(),'532A3C16-B396-4148-A369-CFEA33B39A87','NV02',N'Nguy?n Hoàng Ð?c','nhanvien02','nv02','0970987231','ducnguyenhoang1980@gmail.com',N'Nam','05-09-1980',N's? 20 ngõ 91 Ki?u Mai, Hà N?i')
INSERT INTO NhanVien VALUES(NEWID(),'101C5461-F391-44E6-8CC1-57AA16D50CF9','QL01',N'Nguy?n Thùy Linh','quanly01','ql01','0970987231','linhttnguyen19770@gmail.com',N'N?','04-11-1977',N's? 19 ngõ 20 H? Tùng M?u, B?c Ninh')

--Insert KhachHang
Select * from KhachHang
INSERT INTO KhachHang VALUES(NEWID(),'KH01',N'Nguy?n Công Phu?ng','0978031456',N's? 09 ngõ 77 Nh?n, Hà N?i')
INSERT INTO KhachHang VALUES(NEWID(),'KH02',N'Nguy?n Ti?n Linh','0989076890',N's? 29 ngõ 197 C?u Di?n, Thái Nguyên')
INSERT INTO KhachHang VALUES(NEWID(),'KH03',N'Ð?ng Van Lâm','0978031456',N's? 81 ngõ 104 Nguyên Xá, Hà N?i')
--Insert SanPham
Select * from SanPham
INSERT INTO SanPham VALUES (NEWID(),'SP01',N'Adidas Ultra Boost')
INSERT INTO SanPham VALUES (NEWID(),'SP02',N'Adidas Yeezy')
INSERT INTO SanPham VALUES (NEWID(),'SP03',N'Adidas Stan Smith')
INSERT INTO SanPham VALUES (NEWID(),'SP04',N'Adidas NMD')
INSERT INTO SanPham VALUES (NEWID(),'SP05',N'Nike Jordan')
INSERT INTO SanPham VALUES (NEWID(),'SP06',N'Nike Air')
INSERT INTO SanPham VALUES (NEWID(),'SP07',N'Nike Air Max')
INSERT INTO SanPham VALUES (NEWID(),'SP08',N'Nike Cortez')
INSERT INTO SanPham VALUES (NEWID(),'SP09',N'Nike Air Force 1')
INSERT INTO SanPham VALUES (NEWID(),'SP10',N'Converse Chuck Taylor')
INSERT INTO SanPham VALUES (NEWID(),'SP11',N'Converse Chuck Taylor 2')
INSERT INTO SanPham VALUES (NEWID(),'SP12',N'Converse 1970s')


--Insert DeGiay
Select * from DeGiay
INSERT INTO DeGiay VALUES (NEWID(),'DG01',N'Low – Top')
INSERT INTO DeGiay VALUES (NEWID(),'DG02',N'Mid – Top')
INSERT INTO DeGiay VALUES (NEWID(),'DG03',N'High – Top')

--Insert MauSac
Select * from MauSac
INSERT INTO MauSac VALUES (NEWID(),'MS01',N'Ðen')
INSERT INTO MauSac VALUES (NEWID(),'MS02',N'Tr?ng')
INSERT INTO MauSac VALUES (NEWID(),'MS03',N'Nâu')
INSERT INTO MauSac VALUES (NEWID(),'MS04',N'H?ng')
INSERT INTO MauSac VALUES (NEWID(),'MS05',N'Ð?')
INSERT INTO MauSac VALUES (NEWID(),'MS06',N'Xanh')
--Insert DongSanPham
Select * from DongSP
INSERT INTO DongSP VALUES (NEWID(),'DSP01',N'Adidas')
INSERT INTO DongSP VALUES (NEWID(),'DSP02',N'Nike')
INSERT INTO DongSP VALUES (NEWID(),'DSP03',N'Converse')


--Insert ChiTietSanPham
Select * from SanPham
Select * from DongSP
Select * from DeGiay
Select * from MauSac

select * from ChiTietSP

Insert into ChiTietSP values(NEWID(),'BC5D2E0A-F135-4219-9269-53C0A1DFA8A9','66D09DE6-7A7E-4352-8B74-95C3F427E338','820B3EB2-0360-493A-9F58-9DF0CF498C18','51FE82CD-A300-4D99-B880-6744C6D776E5','10-10-2022',250000,26,N'Vi?t Nam','40',0)
Insert into ChiTietSP values(NEWID(),'6279D366-E342-437F-9482-D1B1AAF64379','06F5A187-D52A-4F72-A1CE-5C591C430316','229EF8B2-576C-4657-8104-621A573D6D9C','F162B079-5B19-4BCA-86FF-75BD435E9B81','09-20-2022',240000,46,N'Trung Qu?c','39',0)
Insert into ChiTietSP values(NEWID(),'EFCC3FCC-1528-40AD-8AEF-30AB68A4E749','1259F3D0-3E4B-4647-B6DA-C1030FA51211','063EADAF-B64F-42A6-B995-1E95A5E37A04','B6D0EE89-E460-4DA3-AC85-6A242E29A86E','09-07-2022',290000,17,N'Vi?t Nam','38',0)
--Insert into ChiTietSP values(NEWID(),'','','','','','10-10-2022',200000,250000,26,N'Vi?t Nam','40')
--Insert into ChiTietSP values(NEWID(),'','','','','','10-10-2022',200000,250000,26,N'Vi?t Nam','40')
--Insert into ChiTietSP values(NEWID(),'','','','','','10-10-2022',200000,250000,26,N'Vi?t Nam','40')
--Insert into ChiTietSP values(NEWID(),'','','','','','10-10-2022',200000,250000,26,N'Vi?t Nam','40')
--Insert into ChiTietSP values(NEWID(),'','','','','','10-10-2022',200000,250000,26,N'Vi?t Nam','40')
--Insert into ChiTietSP values(NEWID(),'','','','','','10-10-2022',200000,250000,26,N'Vi?t Nam','40')
--Insert into ChiTietSP values(NEWID(),'','','','','','10-10-2022',200000,250000,26,N'Vi?t Nam','40')
--Insert into ChiTietSP values(NEWID(),'','','','','','10-10-2022',200000,250000,26,N'Vi?t Nam','40')

--Insert DoiTra
select * from KhachHang
Select * from SanPham
Select * from HoaDon
select * from DoiTra
Insert into DoiTra values(NEWID(),'A43A0D0F-F87F-4A8E-BAF4-A78EC7F36048','BECAED98-FD8A-4DC2-A6A1-166C68CA164A',N'S?n ph?m b? rách')

--Insert HoaDon
Select * from KhachHang
Select * from NhanVien
Select * from HoaDon
Insert into HoaDon values(NEWID(),'84165B18-2B3E-4E42-9912-3606D2AFE71F','D7290262-0DE5-4B02-8DDD-4BC52E15E50E','HD01','10-10-2022','10-10-2022',250000,1,0)
Insert into HoaDon values(NEWID(),'9287AAF6-FB00-4AF2-A479-DE0B200F9D31','4C259FDD-83CF-4EF0-AE6C-2D7B4DB9E5D3','HD02','9-10-2022','9-10-2022',480000,2,0)
--Insert HDCT
Select * from HoaDonChiTiet
Select * from HoaDon
select * from ChiTietSP
Insert into HoaDonChiTiet values(NEWID(),'A4DD7BA4-3ECF-4D24-B74B-3C9996175955','DF65C9CF-B3A5-484A-814C-7E6250C6B2F8',1,250000)
Insert into HoaDonChiTiet values(NEWID(),'EB72AE99-9C82-4C62-B68A-5E4A06C817F6','4469822C-B791-4538-AA23-FC73BE2E1FAC',2,480000)

--Insert Voucher
select * from Voucher
Insert into Voucher values(NEWID(),'VC01',N'Giảm giá dịp Noel',0.95,'03-12-2022','10-10-2022',N'Áp dụng toàn bộ sản phẩm',0)


