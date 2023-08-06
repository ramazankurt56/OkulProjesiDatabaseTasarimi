## OkulProjesiDatabaseTasarimi
#Eğitim Projemdeki SQL Ödevim


![Ekran görüntüsü 2023-08-06 130907](https://github.com/ramazankurt56/OkulProjesiDatabaseTasarimi/assets/93058427/d4e9e0f6-333e-4705-9e61-c139b1984b91)



Persons tablosunu oluşturuyoruz. Buradaki amaçlarımız gereksiz veri tekrarından kaçınmak, Kod karmaşasını azaltmak ve veri konsistansını artırmaktır.
Persons tablosundaki alanların amaçlarını sırasıyla aşağıda veriyorum
1)FirtsName alanı kullanıcının adı için kullanılır.

2)LastName alanı kullanıcının soyadı için kullanılır.

3)IdentityNumber kullanıcını TC kimlik numarası alanıdır.

4)PhoneNumber kullanıcının telefon alanıdır.
5)Email kullanıcının mail alanıdır.
6)Birthday kullanıcının doğum tarihidir.
7)Gender kullanıcının cinsiyet alanıdır
8)RoleId kullanıcının rolünü belirler. Örnek verecek olursak kullanıcı öğrenciyse Role tablosundan 1 numaralı Id alması gerekiyor.
9)Photo kullanıcının fotoğraf alanınıdır
10)CreatedDate kayıtı oluşturma tarihi alanıdır.
11)UpdatedDate kayıtı güncelleme tarihi alanıdır.
```SQL
CREATE TABLE [dbo].[Persons](
	[Id] [int] IDENTITY(1,1) NOT NULL,
	[FirstName] [varchar](50) NOT NULL,
	[LastName] [varchar](50) NOT NULL,
	[IdentityNumber] [char](11) NOT NULL,
	[PhoneNumber] [varchar](13) NOT NULL,
	[Email] [varchar](150) NOT NULL,
	[Birthday] [datetime] NOT NULL,
	[Gender] [varchar](10) NOT NULL,
	[RoleId] [int] NOT NULL,
	[Photo] [varchar](max) NULL,
	[CreatedDate] [datetime] NOT NULL,
	[UpdatedDate] [datetime] NULL,
 CONSTRAINT [PK_Person] PRIMARY KEY CLUSTERED 
(
	[Id] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY] TEXTIMAGE_ON [PRIMARY]
```

Teachers tablosu, öğretmenlerin ilgili alanlarını tutar.
Teachers tablosundaki alanların amaçlarını sırasıyla aşağıda veriyorum. 
1)PersonId alanımız Persons tablosu ile ilişki kurmamızı sağlar. Böylelikle Persons tablosundaki öğretmen kullanıcılarıyla ilişki kurabilir.
2)YearsOfExperience alanı öğretmenin kaç yıl tecrübesi olduğunu belirtir.
3)Branch öğretmenin ilgili olduğu dal alanıdır.
4)Salary öğretmenin maaş alanıdır.
5)Graduation öğretmenin mezun olduğu bölüm alanıdır.
6)StartDate öğretmenin işe başlama tarih alanıdır.
7)EndDate öğretmenin işten ayrılma tarih alanıdır.
```SQL
CREATE TABLE [dbo].[Teachers](
	[Id] [int] IDENTITY(1,1) NOT NULL,
	[PersonId] [int] NOT NULL,
	[YearsOfExperience] [varchar](10) NOT NULL,
	[Branch] [varchar](50) NOT NULL,
	[Salary] [money] NOT NULL,
	[Graduation] [varchar](150) NOT NULL,
	[StartDate] [datetime] NOT NULL,
	[EndDate] [datetime] NULL,
 CONSTRAINT [PK_Teachers] PRIMARY KEY CLUSTERED 
(
	[Id] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
```

Students tablosu, öğrencinin ilgili alanlarını tutar.
Students tablosundaki alanların amaçlarını sırasıyla aşağıda veriyorum. 
1)PersonId alanımız Persons tablosu ile ilişki kurmamızı sağlar. Böylelikle Persons tablosundaki öğrenci kullanıcılarıyla ilişki kurabilir.
2)FatherName öğrencinin baba adı alanını tutar.
3)MotherName öğrencinin anne adı alanını tutar.
4)GraduationDate öğrencinin mezuniyet tarih alanıdır.
5)EmergencyContact öğrenciye acil durumlarda ulaşım sağlamak için numara alanıdır.
6)ClassRoomId öğrencinin hangi sınıfta olduğunu belirten alandır.
```SQL
CREATE TABLE [dbo].[Students](
	[Id] [int] IDENTITY(1,1) NOT NULL,
	[PersonId] [int] NOT NULL,
	[FatherName] [varchar](50) NOT NULL,
	[MotherName] [varchar](50) NOT NULL,
	[GraduationDate] [datetime] NULL,
	[EmergencyContact] [varchar](13) NOT NULL,
	[ClassRoomId] [int] NOT NULL,
 CONSTRAINT [PK_Students] PRIMARY KEY CLUSTERED 
(
	[Id] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
```

Addresses tablosu, Kullanıcı adreslerinin ilgili alanlarını tutar.
Addresses tablosundaki alanların amaçlarını sırasıyla aşağıda veriyorum.
1)City şehir alanıdır.
2)Town ilçe alanıdır.
3)Neighborhood mahalle cadde alanıdır.
4)Street sokak alanıdır.
5)BuildingNumber bina numara alanıdır.
6)Floor kat alanıdır.
7)Apartment apartman alanıdır.
8)Descriptions Açıklama alanıdır.
9)PersonId alanımız Persons tablosu ile ilişki kurmamızı sağlar. Böylelikle Persons tablosundaki kullanıcılarla ilişki kurabilir.
```SQL
CREATE TABLE [dbo].[Addresses](
	[Id] [int] IDENTITY(1,1) NOT NULL,
	[City] [varchar](100) NOT NULL,
	[Town] [varchar](100) NOT NULL,
	[Neighborhood] [varchar](100) NOT NULL,
	[Street] [varchar](100) NOT NULL,
	[BuildingNumber] [varchar](100) NOT NULL,
	[Floor] [varchar](100) NULL,
	[Apartment] [varchar](100) NULL,
	[Descriptions] [varchar](150) NULL,
	[PersonId] [int] NULL,
 CONSTRAINT [PK_Addresses] PRIMARY KEY CLUSTERED 
(
	[Id] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
```

ClassRooms tablosu, sınıfların ilgili alanlarını tutar.
ClassRooms tablosundaki alanların amaçlarını sırasıyla aşağıda veriyorum.
1)Name sınıfın adı alanıdır.
2)Capacity sınıfın öğrenci kapasite alanıdır.
3)IsActive sınıfın kullanılabilirlik durumu alanıdır.
4)CreatedDate sınıfın oluşturulma tarih alanıdır.
5)UpdatedDate sınıfın güncellenme tarih alanıdır.
6)HomeroomTeacherId ilgili sınıfın sınıf öğretmen alanıdır.
```SQL
CREATE TABLE [dbo].[ClassRooms](
	[Id] [int] IDENTITY(1,1) NOT NULL,
	[Name] [varchar](50) NOT NULL,
	[Capacity] [int] NOT NULL,
	[IsActive] [bit] NOT NULL,
	[CreatedDate] [datetime] NOT NULL,
	[UpdatedDate] [datetime] NULL,
	[HomeroomTeacherId] [int] NULL,
 CONSTRAINT [PK_ClassRooms] PRIMARY KEY CLUSTERED 
(
	[Id] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
```

Attendances tablosu, öğrencilerin yoklamasıyla ilgili alanlarını tutar.
Attendances tablosundaki alanların amaçlarını sırasıyla aşağıda veriyorum.
1)StudentId öğrenci tablosundaki ilgili öğrencinin alanını tutar.
1)Date öğrencinin devamsızlık tarihini tutar.
1)StatusId öğrencinin devamsızlık durumunu tutar.
```SQL
CREATE TABLE [dbo].[Attendances](
	[Id] [int] IDENTITY(1,1) NOT NULL,
	[StudentId] [int] NOT NULL,
	[Date] [datetime] NOT NULL,
	[StatusId] [int] NOT NULL,
 CONSTRAINT [PK_Attendances] PRIMARY KEY CLUSTERED 
(
	[Id] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
```

AttendanceStatus tablosu, yoklama durumunun ilgili alanını tutar.
AttendanceStatus tablosundaki name alanın amacı yoklamadaki durumu tutmasıdır. Örnek verecek olursak tam gün, yarım gün veya izinli vb. durumlardır.
```SQL
CREATE TABLE [dbo].[AttendanceStatus](
	[Id] [int] NOT NULL,
	[Name] [varchar](50) NOT NULL,
 CONSTRAINT [PK_AttendanceStatus] PRIMARY KEY CLUSTERED 
(
	[Id] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
```

ClassRoomCourses tablosu, hangi sınıfın hangi derslerinin olduğunu gösterir. Bu sayede sınıfı belli olan öğrencinin dersleride belli olmuş olacak.
ClassRoomCourses tablosundaki alanların amaçlarını sırasıyla aşağıda veriyorum.
1)ClassRoomId ilgili sınıfın ilişkisini sağlar.
2)CourseId ilgili dersin ilişkisini sağlar.
3)CreatedDate sınıfın oluşturulma tarih alanıdır.
4)UpdatedDate sınıfın güncellenme tarih alanıdır.
```SQL
CREATE TABLE [dbo].[ClassRoomCourses](
	[Id] [int] IDENTITY(1,1) NOT NULL,
	[ClassRoomId] [int] NOT NULL,
	[CourseId] [int] NOT NULL,
	[CreatedDate] [datetime] NOT NULL,
	[UpdatedDate] [datetime] NULL,
 CONSTRAINT [PK_ClassRoomCourses] PRIMARY KEY CLUSTERED 
(
	[Id] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
```

Courses tablosu, derslerle ilgili alanını tutar.
Courses tablosundaki alanların amaçlarını sırasıyla aşağıda veriyorum
1)Name alanı dersin verilerini tutar.
2)CourseCode ders kodunun verilerini tutar.
3)CreditHours dersin kredi saat alanını tutar.
4)CreatedDate sınıfın oluşturulma tarih alanıdır.
5)UpdatedDate sınıfın güncellenme tarih alanıdır.
```SQL
CREATE TABLE [dbo].[Courses](
	[Id] [int] IDENTITY(1,1) NOT NULL,
	[Name] [varchar](250) NOT NULL,
	[CourseCode] [int] NOT NULL,
	[CreditHours] [int] NOT NULL,
	[CreatedDate] [datetime] NOT NULL,
	[UpdatedDate] [datetime] NULL,
 CONSTRAINT [PK_Courses] PRIMARY KEY CLUSTERED 
(
	[Id] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
```

Courses tablosu, derslerle ilgili alanını tutar.
Courses tablosundaki alanların amaçlarını sırasıyla aşağıda veriyorum
1)StudentId alanı öğrenci tablosu ile ilişki kurmayı sağlar. Böylelikle hangi öğrencinin sınavı olduğu belirlenmiş olur.
2)CourseId alanı öğrencinin hangi dersin sınavı olduğu belirtilir.
3)TeacherId alanı yapılan sınavların hangi öğretmene ait olduğunu belirler. Öğretmen tablosu ile ilişki kurar.
4)ExamDate alanı sınav tarihi verilerini tutar.
5)ExamTypeId burada sınav tipi tablosu ile ilişki kurar. Buradaki amaç öğrencinin sınav tipini belirtmektir.
6)ExamScore alanı öğrencinin almış olduğu puanı tutar.
7)CreatedDate sınıfın oluşturulma tarih alanıdır.
8)UpdatedDate sınıfın güncellenme tarih alanıdır.
9)Percentage alanı ise sınavların yüzde değerlerini tutar. Örn yazılı sınavlar ders notunun %70' ini etkiler.
```SQL
GO
CREATE TABLE [dbo].[Exams](
	[Id] [int] IDENTITY(1,1) NOT NULL,
	[StudentId] [int] NOT NULL,
	[CourseId] [int] NOT NULL,
	[TeacherId] [int] NOT NULL,
	[ExamDate] [datetime] NOT NULL,
	[ExamTypeId] [int] NOT NULL,
	[ExamScore] [decimal](5, 2) NOT NULL,
	[CreatedDate] [datetime] NOT NULL,
	[UpdatedDate] [datetime] NULL,
	[Percentage] [decimal](5, 2) NOT NULL,
 CONSTRAINT [PK_Exams] PRIMARY KEY CLUSTERED 
(
	[Id] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
```

ExamTypes tablosu, sınavın tipleriyle ilgili alanını tutar.
ExamTypes tablosundaki alanların amaçlarını sırasıyla aşağıda veriyorum
1)Name sınav tipinin alanını tutar.
2)CreatedDate sınıfın oluşturulma tarih alanıdır.
3)UpdatedDate sınıfın güncellenme tarih alanıdır.
```SQL
CREATE TABLE [dbo].[ExamTypes](
	[Id] [int] IDENTITY(1,1) NOT NULL,
	[Name] [varchar](50) NOT NULL,
	[CreatedDate] [datetime] NOT NULL,
	[UpdatedDate] [datetime] NULL,
 CONSTRAINT [PK_ExamTypes] PRIMARY KEY CLUSTERED 
(
	[Id] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
```

Facilities tablosu, ilgili sınıfın imkanların alanlarını tutar.
Örnek verecek olursak 6-A sınıfında akıllı tahta, projeksiyon ve bilgisayar vb. imkanlar bulunuyor.
```SQL
CREATE TABLE [dbo].[Facilities](
	[Id] [int] IDENTITY(1,1) NOT NULL,
	[ClassRoomId] [int] NOT NULL,
	[Name] [varchar](150) NOT NULL,
 CONSTRAINT [PK_Facilities] PRIMARY KEY CLUSTERED 
(
	[Id] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
```

Roles tablosu, Persons tablosundaki kullanıcıların rollerini tutar. Örnek verecek olursak müdür,öğretmen veya öğrenci gibi verileri tutar.
```SQL
CREATE TABLE [dbo].[Roles](
	[Id] [int] IDENTITY(1,1) NOT NULL,
	[Name] [varchar](50) NOT NULL,
 CONSTRAINT [PK_Roles] PRIMARY KEY CLUSTERED 
(
	[Id] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
```

SchoolManagers tablosu, okulun müdür veya müdür yardımcıssı alanlarını tutar.
SchoolManagers tablosundaki alanların amaçlarını sırasıyla aşağıda veriyorum
1)PersonId alanı Persons tablosundaki ilgili kullanıcı ile ilişki kurmamızı sağlar.
2)StartDate alanı okul yöneticilerinin işe başlama tarihini tutar.
3)EndDate alanı okul yöneticilerinin işten ayrılma tarihini tutar.
4)Salary alanı maaşları tutar.
5)Graduation alanı okul yöneticilerinin mezuniyet bilgisini tutar.
```SQL
CREATE TABLE [dbo].[SchoolManagers](
	[Id] [int] IDENTITY(1,1) NOT NULL,
	[PersonId] [int] NOT NULL,
	[StartDate] [datetime] NOT NULL,
	[EndDate] [datetime] NULL,
	[Salary] [money] NOT NULL,
	[Graduation] [varchar](150) NOT NULL,
 CONSTRAINT [PK_SchoolManagers] PRIMARY KEY CLUSTERED 
(
	[Id] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
```

TeacherClassRooms tablosu, Öğretmenlerin ilgili sınıfların alanını tutar.
TeacherClassRooms tablosundaki alanların amaçlarını sırasıyla aşağıda veriyorum
1)TeacherId alanı sayesinde ilgili öğretmenin ilişkisini kuruyoruz.
2)ClassRoomId alanında ise ilişkisini kurmuş olduğumuz öğretmenin birden fazla sınıflarda ilişki kurmamızı sağlıyor.
```SQL
CREATE TABLE [dbo].[TeacherClassRooms](
	[Id] [int] IDENTITY(1,1) NOT NULL,
	[TeacherId] [int] NOT NULL,
	[ClassRoomId] [int] NOT NULL,
 CONSTRAINT [PK_TeacherClassRooms_1] PRIMARY KEY CLUSTERED 
(
	[Id] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
```

TeacherCourses tablosu, öğretmenlerin birden fazla ders seçebilmelerini sağlıyoruz.
TeacherCourses tablosundaki alanların amaçlarını sırasıyla aşağıda veriyorum
1)TeacherId alanı öğretmen tablosu ile ilişki kurmamızı sağlıyor.
2)CourseId alanı ders tablosu ile ilişki kurmamızı sağlıyor. Böylelikle Hanhi öğretmenin hangi dersleri seçmiş olduğunu görebiliyoruz.
3)CreatedDate sınıfın oluşturulma tarih alanıdır.
4)UpdatedDate sınıfın güncellenme tarih alanıdır.
```SQL
CREATE TABLE [dbo].[TeacherCourses](
	[Id] [int] IDENTITY(1,1) NOT NULL,
	[TeacherId] [int] NOT NULL,
	[CourseId] [int] NOT NULL,
	[CreatedDate] [datetime] NOT NULL,
	[UpdatedDate] [datetime] NULL,
 CONSTRAINT [PK_TeacherCourses] PRIMARY KEY CLUSTERED 
(
	[Id] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
```

Aşağıda oluşturduğumuz prosedure sayesinde Persons tablomuza hızlıca kayıt yapabiliriz. 
```SQL
Create PROCEDURE [dbo].[CreatePerson]
	@firstName VARCHAR(50),
	@lastName VARCHAR(50),
	@identityNumber CHAR(11),
	@phoneNumber VARCHAR(MAX),
	@email VARCHAR(150),
	@birthday datetime,
	@gender VARCHAR(10),
	@roleId int,
	@photo VARCHAR(MAX)
AS
BEGIN	
	SET @phoneNumber = REPLACE(@phoneNumber, ' ', '');
	SET @firstName = REPLACE(@firstName, ' ', '');
	SET @firstName = UPPER(@firstName);
	SET @lastName = REPLACE(@lastName, ' ', '');
	SET @lastName = UPPER(@lastName);

	INSERT INTO Persons Values(
	@firstName,@lastName ,
	@identityNumber,@phoneNumber ,@email ,
	@birthday,@gender ,@roleId ,@photo,GETDATE(), null)
					
END
```

Aşağıda oluşturduğumuz prosedure sayesinde Stundents tablomuza hızlıca kayıt yapabiliriz. 
```SQL
create PROCEDURE [dbo].[CreateStudent]
	@personId int,
	@fatherName varchar(50),
	@motherName varchar(50),
	@EmergencyContact VARCHAR(13),
	@classRoomId int
AS
BEGIN	

	INSERT INTO Students Values(
	@personId ,
	@fatherName ,
	@motherName ,
	null ,
	@EmergencyContact,
	@classRoomId )
					
END
```

Aşağıda oluşturduğumuz prosedure sayesinde Teachers tablomuza hızlıca kayıt yapabiliriz. 
```SQL
CREATE PROCEDURE [dbo].[CreateTeacher]
	@personId int,
	@yearsOfExperience varchar(10),
	@branch varchar(50),
	@salary money,
	@graduation VARCHAR(150)
AS
BEGIN	

	INSERT INTO Teachers Values(
	@personId ,
	@yearsOfExperience ,
	@branch ,
	@salary ,
	@graduation ,
	GETDATE(),null)
					
END
```

Aşağıda oluşturduğumuz View sayesinde Öğrenci ve öğrencinin bağlı olduğu sınıfları hızlıca sorgulayabiliriz.
```SQL
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
Create view [dbo].[StudentClassRoomView] as
select p.FirstName, p.LastName, cr.Name AS Class from Students s left join Persons p on p.Id=s.PersonId
left join ClassRooms cr ON s.ClassRoomId = cr.Id
```

Aşağıda oluşturduğumuz View sayesinde öğretmenin detaylarını hızlıca sorgulayabiliriz.
```SQL
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
Create view [dbo].[TeacherDetailView] as
select p.FirstName,p.LastName,p.Birthday,p.IdentityNumber,p.PhoneNumber,p.Email,t.Branch,t.Salary,a.City,a.Town,a.Neighborhood from Teachers t left join Persons p on t.PersonId=p.Id
left join Addresses a on a.PersonId=p.Id
```



