# Database
    - e-commerce, shopping online, จองโรงแรม
## การออกแบบ database
    ** Requirements Analysis **
      - สำคัญที่สุด มีความละเอียดอ่อนมาก ถึงจะเป็นธุรกิจแบบเดียวกันแต่อาจจะเก็บข้อมูลคนละแบบก็ได้
      - สิ่งที่ลูกค้าต้องการ ต้องการเก็บข้อมูลเป็นอะไรบ้าง(ไปคุยกับลูกค้า ขอเอกสารต่างๆ)
      - ถ้าออกแบบผิด ไม่ได้ตามที่ลูกค้าต้องการ ก็เหมือนผิดตั้งแต่ต้น

      - ขั้นตอนการทำ
          - understand (ทำความเข้าใจ)
              - เข้าใจ business model ของธุรกิจนั้นๆ
              - Data อะไรที่จะถูกเก็บในฐานข้อมูล
              - Operations อะไรที่กระทำกับ Data ตัวนั้นบ้าง
          - วิธีการหา Requirements
              - นัดประชุมกับ user(ลูกค้า) >> ดีที่สุดคือคุยกับลูกค้าโดยตรง
              - ดู Environment ในการทำงานเป็นยังไง
              - ดูจากเอกสาร แล้วนำมาปรับให้เข้ากัน
          - ** ต้องออกแบบเผื่อไว้สำหรับการเปลี่ยนแปลง เผื่อไว้แต่แรก (scalable) **
          - การซ้ำซ้อนของข้อมูลที่ไม่จำเป็น (repetition)  หมายถึง ข้อมูลที่อาจจะมีความเปลี่ยนแปลงได้หรือเป็นข้อมูลซ้ำๆกันในตารางหลัก จะลดด้วยการแยกตาราง database ออกมาโดยจะเชื่อมโยงกลับไปด้วย foreign key
          - primary key จะแยกความแตกต่างของแต่ละ key ได้

    Conceptual Database Design
      - ER Diagram คือ Entity Relationship Diagram เอาไว้อธิบายความสัมพันธ์ของข้อมูล (ตารางที่เราสร้าง)
          - เอนทิตี้ (Entity) 
              เป็นวัตถุ หรือสิ่งของที่เราสนใจในระบบงานนั้น ๆ, 
              1 row คือ 1 entity,
              entity set คือ entity หลายๆอันรวมกัน (1 table),
              เขียนด้วยสัญลักษณ์ สี่เหลี่ยม

          - แอททริบิว (Attribute) 
              เป็นคุณสมบัติของวัตถุที่เราสนใจ, ชื่อที่เราตั้งไว้บนหัวตาราง 1 ช่อง 1 attribute,
              Domain หรือ value set
                  ค่าที่เป็นไปได้ของ attribute,
              Attribute Constraint คือ ข้อจำกัดของ Attribute เช่น อายุต้องเป็นตัวเลขเท่านั้น รหัสนิสิตต้องห้ามมีค่าซ้ำกัน แต่ attribute สามารถเป็น null ได้,
              เขียนด้วยสัญลักษณ์ วงรี,
              Simple Attribute คือ Attribute ที่ไม่สามารถแยกออกเป็นส่วนย่อยได้เช่น รหัสนิสิต เพศ,
              Composite Attribute คือ Attribute ที่สามารถแยกออกเป็นส่วนย่อยได้เช่น ชื่อเต็ม (Full Name) แยกได้เป็น ชื่อกับนามสกุล

          - ความสัมพันธ์ (Relationship) 
              คือ ความสัมพันธ์ระหว่างเอนทิตี้ (table) สามารถมี Attribute (Descriptive Attributes) ได้ คือ attribute ที่เพิ่มมาระหว่างความสัมพันธ์ของสองตัว (ใน many to many),
              เขียนด้วยสัญลักษณ์ สี่เหลี่ยมขนมเปียกปูน,
              - ความสัมพันธ์เอนทิตี้เดียว (Unary Relationships) หมายถึง เอนทิตี้หนึ่ง มีความสัมพันธ์กับตัวมันเอง
              - ความสัมพันธ์สองเอนทิตี้ (Binary Relationships) หมายถึง เอนทิตี้สองเอนทิตี้จะมีความสัมพันธ์กัน
              - ความสัมพันธ์สามเอนทิตี้(Ternary Relationships) หมายถึง เอนทิตี้สามเอนทิตี้มีความสัมพันธ์กัน
              - อาจจะมี 4 5 6 แต่ไม่ค่อยมี หลักๆจะเป็น 2
              
              Maximum Cardinality (Ratio Constraints) แบ่งเป็น
                  - ความสัมพันธ์แบบ One to One Relationships
                  - ความสัมพันธ์แบบ One to Many Relationships
                  - ความสัมพันธ์แบบ Many to One Relationships
                  - ความสัมพันธ์แบบ Many to Many Relationships

              Minimum Cardinality (Participation Constraints)
                  - Total ทุก Entity ใน Entity set ต้องมีอย่างน้อย 1 relationship (ต้องมี, เป็น null ไม่ได้)
                      เช่น นักเรียนทุกคนต้องมีอาจารย์อย่างน้อย 1 คน เป็นที่ปรึกษา
                  - Partial มีแค่บาง Entity ใน Entity Set มี relationship (มีหรือไม่มีก็ได้, เป็น null ก็ได้)
                      เช่น ไม่จำเป็นที่อาจารย์ทุกคนต้องเป็นที่ปรึกษาให้กับนักเรียน
      
      - Key 
          - Super Key (ใหญ่สุด)
              คือ Attribute หรือกลุ่มของ Attribute ซึ่งมีค่าแตกต่างกันไปในแต่ละเอนทิตี้ และทำให้สามารถระบุเอนทิตี้เฉพาะตัวหนึ่ง ๆ ได้
          - Candidate Key  
              คือ Subset ที่เล็กที่สุดของ Super Key ที่สามารถระบุเฉพาะเอนทิตี้นั้นได้
          - Primary Key 
              คือ Candidate Key ที่ถูกเลือกให้เป็นตัวระบุหรือ Identity เอนทิตี้เฉพาะตัว
          - Foreign Key (FK)
              คือ การสร้างกฏความสัมพันธ์ระหว่างสองตารางเข้าด้วยกัน โดยที่ Foreign Key จะเป็นคอลัมน์ที่ใช้เชื่อมโยง Primary Key (PK) ของตารางที่มีความสัมพันธ์กัน
      
      Strong Entity and Weak Entity
          - Strong Entity คือ Entity ทั่ว ๆ ไป ที่มี Attribute หนึ่งแยกความแตกต่างของข้อมูลได้ เช่น Entity Student มี Student Id แยกความแตกต่างได้
          - Weak Entity คือ Entity ที่ต้องอาศัย Attribute จาก Entity (foreig

# SQL
    - ภาษาโปรแกรมมิ่งภาษานึง 
    Structor Query Language
      - เอาไว้จัดการกับ Database
      - ฐานข้อมูลที่โครงสร้างแน่นอน (คอลัมน์แน่นอน, ชนิดข้อมูลแน่นอน)
      - mySQL คือโปรแกรมสำหรับจัดการกับภาษา SQL ได้ง่ายขึ้น
      - MongoDB คือ No SQL

## MySQLServer
    - ต้อง start server database ก่อน
    - แล้วใช้ command ในการจัดการ database
## mySQL workbench
    - คำสั่งนิยมใช้ตัวพิมพ์ใหญ่ทั้งหมด
    - ถ้ารันคำสั่งแล้วต้องกด refresh ด้านบนขวาเล็กๆตรง SCHEMAS ไม่งั้นมันจะไม่อัพเดทอะไรให้
    - สัญลักษณ์สายฟ้า ไว้ทำให้คำสั่งทำงาน ถ้าไม่คลุมคำสั่ง ระบบจะทำงานทุกคำสั่งในหน้านั้น และจะทำงานใหม่ทุกครั้งตั้งแต่บรรทัดแรก
    - -- คำสั่ง คือ comment(--) คำสั่งนั้นๆ
    - การตั้งชื่อ table จะตามด้วย s เป็นความนิยมใช้หรือประเพณีการกำหนด
    - การตั้งชื่อตัวแปรจะไม่ใช้  camelCase แต่จะใช้ _ คั่นคำแทน
    >> CREATE DATABASE database_name
        คำสั่งในการสร้าง database
    >> CREATE TABLE table_name(
        ชื่อ      ประเภท   ขนาดของข้อมูล  ข้อกำหนด
        column1 datatype (size) constraint,
        column2 datatype (size) constraint,
        column3 datatype (size) constraint,
        ....
        columnN datatype (size) constraint,
        PRIMARY KEY( one or more columns )
    );
        ex. 
            CREATE TABLE provinces(
                id INT AUTO_INCREMENT NOT NULL,
                name_th VARCHAR(50) NOT NULL,
                name_en VARCHAR(50) NOT NULL,
                PRIMARY KEY(id)
            )
                - id คือ ชื่อ column
                - INT คือ ประเภทข้อมูล
                - ใน CREATE TABLE : AUTO_INCREMENT คือจะเพิ่มค่าเรื่อยๆไปทีละ 1 เมื่อ insert ค่าเข้าไป
                - VARCHAR(30) => ตัวอักษรไม่เกิน 30 ตัว
                - NOT NULL คือ ค่าห้ามเป็น null
                - PRIMARY KEY (id) คือจะกำหนดอะไรเป็น key ของตัวนั้นในตัวอย่างคือให้ id เป็น Primary key
            - FOREIGN KEY(province_id) REFERENCES provinces(id)
                กำหนด FK โดยให้ province_id เป็น FK และ ref คือ เอามาจากที่ไหน หรือใช้เป็น UNIQUE (province_id) ก็ได้
            - ถ้าจะตั้งเป็น unique key หลาย column ให้ใช้ CONSTRAINT
        
### Datatype SQL
    varchar(n) ==> ตัวอักษร n ตัว
    int ==> จำนวนเต็ม
    decimal(x, y) ==> จำนวนหลัก, จำนวนทศนิยม (เก็บเป็นข้อความ)
        
### Constraints
    - NOT NULL ==> column นั้นห้ามเป็น null
    - UNIQUE ==> column นั้นห้ามมีค่าที่ซ้ำกัน
    - PRIMARY KEY ==> NOT NULL + UNIQUE มีไว้เพื่อง่ายต่อการเข้าถึงและง่ายต่อการค้นหา
    - FOREIGN KEY → เป็น KEY ที่อ้างถึงตารางอื่น (PRIMARY KEY ของตารางอื่น)
    - DEFAULT  → ตั้งค่าเริ่มต้นให้กับ Column(s) นั้น

    - Drops ==> เอาไว้ลบตาราง
    - สัญลักษณ์ประแจ ตอน hover ที่ตารางไว้แก้ไขแทนการใช้ command line 
        - Column ==> ไว้แก้ไขข้อมูลต่างๆ >> ชื่อ ประเภท 
            PK - Primary Key
            NN - NOT NULL
            UQ - UNIQUE
            B - BINARY
            UN - UNSIGN
            ZF - ให้เติมค่า 0 ในช่องนั้น
            AI - AUTO INCREMENT เพิ่มค่าขึ้นเรื่อยๆ ทีละ 1
            G - GENERATED COLUMN
        -Index
            - จะแสดง Primary key และ foreign key ที่เรากำหนด
        - Foreign Keys 
            - จะแสดง foreign key ที่มีใน table นั้น
            - Foreign Key option
                On update/ On delete
                    RESTRICT - ขัดขวางการลบ parent แต่ลบ child ได้
                    CASCADE - ลบหมดทั้ง parent ทั้ง child
                    SET NULL - ทำให้ค่ากลายเป็น NULL เมื่อ update/delete แต่ระวังถ้าเรากำหนดห้ามเป็น null ใน table อาจจะ error ได้
                    NO ACTION - ไม่ทำอะไรเลย แต่อาจจะทำให้เกิด error ได้
                    - parent child เปรียบเสมือน one to many
                - การตั้งชื่อ fk_ชื่อตารางที่จะใส่_ตารางที่เป็น ref_column อะไร

### INSERT
    INSERT INTO TABLE_NAME (column1, column2, column3,...columnN)  //ไม่จำเป็นต้องใส่ทุก column
    VALUES (value1, value2, value3,...valueN);
    
    INSERT INTO TABLE_NAME VALUES (value1,value2,value3,...valueN);

    INSERT INTO districts (name_th, name_en, province_id)
    VALUES ('ราชเทวี', 'Ratchathewi', 1), ('ปากเกร็ด', 'Pakkret', 2)
        - ถ้าจะ insert ค่า id ที่เชื่อมโยงไปยัง table อื่นต้อง insert ค่าที่มันมีด้วยไม่งั้นจะ error

### UPDATE 
    UPDATE districts
    SET province_id = 1, name_th = 'พญาไท', name_en = 'Phayathai' 
    where id = 10

    UPDATE districts คือ update ตารางอะไร
    SET province_id = 1, name_th = 'พญาไท', name_en = 'Phayathai' คือ เปลี่ยนค่าอะไร
    where id = 10 คือ ใส่เพื่อกันไม่ให้มัน update ทุก column ในตาราง

### DELETE
    DELETE FROM provinces WHERE id = 2
    ต้องมี where ด้วยเสมอไม่งั้น จะถูกลบทั้ง table
    
    - สร้าง table ด้วย tool
        - คลิ๊กขวาที่ table >> create table
        -charset/collation >> utf8mb4, utf8mb4_unicode_ci 

#### Join
    - INNER JOIN : แสดงผลข้อมูลที่มีค่าทั้ง 2 table เหมือนกันใน column ที่ระบุ (Default) (intersect)

    - LEFT JOIN : แสดงผลข้อมูลของ table ทางซ้ายทั้งหมด (table 1) และ ข้อมูลของ table ทางขวาที่ตรงเงื่อนไข (table 2) ซ้ายเป็นหลัก

    - RIGHT JOIN : แสดงผลข้อมูลของ table ทางซ้ายที่ตรงเงื่อนไข (table 1) และ ข้อมูลของ table ทางขวาทั้งหมด (table 2) ขวาเป็นหลัก

    - FULL JOIN : แสดงข้อมูลทั้งหมดของทั้ง 2 table ทั้งที่มีข้อมูลเหมือนกัน และ ไม่เหมือนกัน (union เอาหมด)

    - SELF JOIN : ทำการเชื่อมความสัมพันธ์ของ table ตัวเอง โดยเปรียบเสมือนสร้าง table ตัวเองเป็นอีก table หนึ่งมา JOIN กันเอง

    - CARTESIAN JOIN หรือ CROSS JOIN : (CARTESIAN เหมือนในคณิตศาสตร์ การกระจายข้อมูลทั้งหมด)ทำการเอาข้อมูลทุก table มาเชื่อมกันทุกแถว ผลลัพธ์ที่ได้ของจำนวนบรรทัด จะเท่ากับผลคุณของ จำนวนบรรทัดทั้ง 2 table

    ** หลักการสำคัญในการ JOIN **
    - ต้องดูก่อนว่าอยากใช้ข้อมูลอะไรบ้าง
    - หาข้อมูลที่เหมือนกันในแต่ละตารางเพื่อเป็นตัวเชื่อมสำหรับการ JOIN

#### ตรรกศาสตร์
    - AND : เชื่อมเงื่อนไขตั้งแต่ 2 เงื่อนไขขึ้นไป ต้องเป็นจริงทั้งหมดถึงจะจริง
    - BETWEEN : เปรียบเทียบข้อมูลว่าอยู่ระหว่างค่าต่ำสุด และ สูงสุด
    - EXISTS : เปรียบเทียบข้อมูลว่ามีปรากฎอยู่ในแถวที่กำหนด
    - IN : เปรียบเทียบข้อมูลกับชุดข้อมูล โดยถ้ามีอย่างน้อย 1 ค่าที่เหมือนกัน จะมีค่าเป็นจริง
    - LIKE : เปรียบเทียบข้อมูลว่าเป็นส่วนประกอบภายในข้อมูลอีกค่าหนึ่ง
    - NOT : เงื่อนไขปฏิเสธ
    - OR : เชื่อมเงื่อนไขตั้ง 2 เงื่อนไขขึ้นไป ถ้าเป็นจริงอันหนึ่งทั้งหมดจะเป็นจริง
    - IS NULL : ตรวจสอบค่าว่าง (จะไม่ใช้ = NULL)
        
#### Aggregate Operators> จะใช้ต่อจาก SELECT เท่านั้น
    - COUNT(A) : นับแถวที่มีค่าใน Column A
    - SUM(A) :	 ผลรวมของค่าทั้งของในแถวของ Column A
    - AVG(A) :	 หาค่าเฉลี่ยของ Column A
    - MAX(A) :	 หาค่ามากที่สุดของ Column A
    - MIN(A) :	 หาค่าน้อยที่สุดของ Column A
        ex.
        - SELECT SUM(age) as Avg_Age FROM sailors
        - SELECT sailors.sname, sailors.age FROM sailors WHERE sailors.age = (SELECT MAX(sailors.age) FROM sailors)
    
#### SELECT Statements (Advanced)>
    - GROUP BY clause :  แบ่งเป็น Group ตาม clause
        - จะกรุ๊ปข้อมูลตามที่เรากำหนดเป็นชุดเดียวกัน เวลาทำพยายาม SELECT หัวข้อที่จะ GROUP BY มาด้วยจะได้รู้ว่าเป็นข้อมูลอะไร
        ex.
            SELECT customer_name, SUM(account_number) FROM depositor GROUP BY customer_name
            จากตัวอย่างจะกรุ๊ปข้อมูลด้วย customer_name ข้อมูลที่ customer_name ซ้ำกันจะเอามารวมกันที่ไว้ในที่เดียว 
        ex.2
            SELECT d.customer_name, SUM(a.balance) FROM depositor as d JOIN account as a
            ON a.account_number = d.account_number 
            GROUP BY customer_name

    - HAVING clause :  Filter แถว
    - ORDER BY clause ASC :  จัดเรียงลำดับตาม clause
        กำหนดเงื่อนในการ ORDER ได้โดย 
            ASC - น้อยไปมาก (default)
            DESC - มากไปน้อย
                        

    - BETWEEN and AND operators
        เลือกค่าตั้งแต่ตัวแรกจนตัวที่สอง (Inclusive)
        ใช้ได้กับ number, Date, String
            ex.
            SELECT sname FROM sailors WHERE age BETWEEN 45 AND 70
               
#### AS
    - จะย่อเป็นตัวอักษรแรกถ้าซ้ำก็เพิ่มตัวที่สองตามมา
    - SELECT s.sname as sailor_name, r.day as reserve_date FROM sailors AS s 
        JOIN reserves as r WHERE s.sid = r.sid
        s.sname as sailor_name และ r.day as reserve_date คือจะเปลี่ยนชื่อ column ที่แสดง

#### LIKE
    - % กี่ตัวก็ได้, _ ต้องมีอย่างน้อย .. ตัว
    - SELECT sname FROM sailors WHERE sname LIKE '%b%'
        %b% แปลว่า ขึ้นต้นด้วยตัวอะไรก็ได้ ลงท้ายด้วยตัวอะไรก็ได้แต่ต้องมีตัว b อยู่ในนั้น
        %b แปลว่า หาข้อมูลที่มีตัว b ลงท้าย
        b% แปลว่า หาข้อมูลที่ขึ้นต้นด้วยตัว b
        _b% แปลว่า ต้องมีข้อมูลอย่างน้อย 1 ตัวที่อยู่หน้า b
        __b% แปลว่า ต้องมีข้อมูลอย่างน้อย 2 ตัวที่อยู่หน้า b 
        __% แปลว่า หาข้อมูลที่มีอย่างน้อย 2 ตัว (ตัวเดียวไม่เอามา)
        __ แปลว่า หาข้อมูลที่มี 2 ตัว
        A__% แปลว่า มี A ขึ้นต้นและตามหลัง A อย่างน้อย 2 ตัว
    
        ? ถ้า %ar% แล้วพิมพ์ ar ?
    
#### IN
    SELECT * FROM sailors AS s
    JOIN reserves as r ON s.sid = r.sid
    JOIN boats as b ON r.bid = b.bid
    WHERE b.color IN ('Red', 'Green', 'Yellow')

    ใช้ IN แทนการใช้ OR เทียบว่า b.color อยุ่ในสิ่งที่เรากำหนดหรือไม่
    
#### UNION (ใช้น้อย)
    - เวลา SELECT ควร SELECT column เหมือนๆกันทั้งสองตารางที่จะเชื่อมกัน
        ex.
        SELECT s.sname FROM sailors as s WHERE s.rating > 5
        UNION
        SELECT b.color FROM boats as b
        ไม่งั้นอาจจะทำให้ error หรือเชื่อมข้อมูลผิดประเภทกัน

### การใช้ SECLECT
    SELECT * from sailors WHERE age > 30 OR rating > 5 ORDER BY age DESC
        หมายความว่า เลือกทุกตัวจาก sailors โดย age มากกว่า 30 หรือ rating มากกว่า 5 โดยเรียงจากมากไปน้อย

    DISTINCT (เอาที่ไม่ซ้ำกัน)

    SELECT * FROM sailors JOIN reserves ON sailors.sid = reserves.sid
        หมายความว่า เลือกทุกอย่างจาก sailors ต่อด้วย reserves โดยมีเงื่อนไขว่า sailors.sid = reserves.sid
        ** ON คือเงื่อนไข
        ** JOIN เปล่าๆคือ INNER JOIN
    
    lab2 หาชื่อของกะลาสีเรือทั้งหมดที่จองเรือรหัส 103
        SELECT sname FROM sailors JOIN reserves ON sailors.sid = reserves.sid AND bid = 103 (ใส่ where ต่อท้ายได้อีก)
    เฉลย lab2 
        SELECT sname FROM sailors 
        JOIN reserves ON sailors.sid = reserves.sid 
        WHERE bid = 103
            คือ เลือกข้อมูล sname จากตาราง sailors
            และต่อกับตาราง reserves ด้วยเงื่อนไข sid ของตาราง sailors = sid ของตาราง reserves
            โดย bid = 103 เท่านั้น
            - จะไม่ค่อยใช้ AND หลัง ON แบบนั้น เพราะ ON จะใช้แค่ในการเชื่อมตารางแค่นั้น ปกติจะใช้ WHERE ในการกำหนด conditions ต่างๆ

    
#### JOIN ซ้อน JOIN
    lab3 หา sids ทั้งหมดของกะลาสีเรือที่จองเรือสีแดง
        SELECT DISTINCT sailors.sid, sailors.sname FROM sailors 
        JOIN reserves ON sailors.sid = reserves.sid 
        JOIN boats ON reserves.bid = boats.bid WHERE BINARY color = 'red'
            - JOIN 3 ตารางเข้าด้วยกัน
            - ใส่ BINARY คือแปลงค่าให้เป็น BINARY แล้วเปรียบเทียบแบบ case sensitive (ตัวเล็กตัวใหญ่ต่างกัน)

    lab5 หาสีของเรือทั้งหมดที่ถูกจองโดยกะลาสีเรือชื่อ ‘Lubber’
        SELECT DISTINCT boats.color FROM sailors 
        JOIN reserves ON sailors.sid = reserves.sid 
        JOIN boats ON reserves.bid = boats.bid 
        WHERE BINARY sailors.sname = 'Lubber'

        คือ เลือกข้อมูล boats.color ที่ไม่ซ้ำจากตาราง sailors
        โดยต่อกับตาราง reserves ด้วยเงื่อนไข sailors.sid = reserves.sid 
        จากนั้นต่อกับตาราง boats ด้วยเงื่อนไข reserves.bid = boats.bid
        โดย sailors.sname จะต้องเท่ากับ 'Lubber' แบบเทียบถึงตัวเล็กตัวใหญ่ของตัวอักษร

    lab6
        SELECT DISTINCT sailors.sname FROM sailors 
        JOIN reserves ON sailors.sid = reserves.sid 
        JOIN boats ON reserves.bid = boats.bid
        WHERE B.color = 'Red' OR B.color = 'Green';

        เลือกข้อมูล sailors.sname ที่ไม่ซ้ำจากตาราง sailors 
        โดยต่อกับตาราง reserves ด้วยเงื่อนไข sailors.sid = reserves.sid
        และต่อกับตาราง boats ด้วยเงื่อนไข reserves.bid = boats.bid


    lab7 หาคนที่จองเรือทั้งสีเขียวและแดง แต่ต้องใช้ UNION เพราะว่า ใช้ and ตรง b.color ทั้ง red และ green ไม่ได้ เพราะสีตรงได้แค่สีเดียว
        - ละการเขียน as ได้
        SELECT * FROM sailors s JOIN reserves r ON s.sid = r.sid
        JOIN boats b ON b.bid = r.bid WHERE b.color = 'Red' AND b.color = 'Green'
        - แบบข้างบนนี้ไม่ได้

        SELECT * FROM sailors WHERE 
        sid IN (SELECT s.sid FROM sailors as s JOIN reserves as r ON s.sid = r.sid  
        JOIN boats as b ON b.bid = r.bid WHERE b.color = 'Red')
        AND sid IN
        (SELECT s.sid FROM sailors as s JOIN reserves as r ON s.sid = r.sid  
        JOIN boats as b ON b.bid = r.bid WHERE b.color = 'Green')

        - ก้อน SELECT ในวงเล็บแรกคือเอาไอดีคนที่จองสีแดงออกมาก่อน จากนั้น ก้อน SELECT ก้อนที่สองในวงเล็บคือเอาไอดีคนที่จองสีเขียวมา และ SELECT แรกด้านบนสุดคือ เลือกจากสิ่งที่เลือกมาแล้วว่าให้เลือกจากไอดีคนที่จองสีแดงและต้องจองสีเขียวด้วย (แต่งานจริงน่าจะใช้ js เข้ามาช่วย)

    ผลคูณคาร์ทีเซียน เอา set a กับ set b มา cross กัน (คาร์ทีเซียนจะ join แบบ inner join) จริงๆไม่ควรใช้เพราะว่าเป็นการคูณจะทำให้เปลืองทรัพยากร
        SELECT * FROM sailors, reserves, boats
            - เอา sailors มาคูณ reserves ไล่กระจายทีละบรรทัดเชื่อมกันให้ครบ (กระจายทุกแบบให้เข้ากันได้)
            ex.
            - sailors แถว 1 reserves แถว 1 boat แถว 1
            - sailors แถว 1 reserves แถว 1 boat แถว 2
            - sailors แถว 1 reserves แถว 1 boat แถว 3
            - sailors แถว 1 reserves แถว 1 boat แถว 4

    lab7 with คาร์ทีเซียน ไม่ได้!!
        SELECT * FROM sailors as s, reserves as r, boats as b WHERE s.sid = r.sid AND r.bid = b.bid


        MySQL >> ecommerce
            ex. หาจำนวนคนที่อยู่ในกรุงเทพ
            SELECT address, count(id) AS amount FROM customers 
            WHERE address LIKE '%กรุงเทพ' 
            GROUP BY address ORDER BY amount DESC, address
                - กรองที่ขึ้นต้นด้วยกรุงเทพแล้วกรุ๊ปด้วย address จากนั้นเรียงโดย amount ถ้า amount เท่ากันเรียงจาก address ต่อ

            ex. หาจำนวน order ที่คนชื่อ นัท สั่ง
            SELECT * FROM ecommerce.customers AS c
            JOIN ecommerce.orders AS o ON c.id = o.customer_id
            WHERE c.name = 'นัท'
                - เลือกข้อมูลทั้งหมดจากตาราง customers โดย c เป็นตัวแทนตาราง
                ต่อกับตาราง orders ที่แทนด้วย o ด้วยเงื่อนไข c.id = o.customer_id
                โดย name จากตาราง customers ต้องเท่ากับ นัท

            ex. หาจำนวน order ของแต่ละคนและเรียงจากมากไปน้อย
            SELECT c.name, COUNT(c.id) AS amount FROM ecommerce.customers AS c
            JOIN ecommerce.orders AS o ON c.id = o.customer_id
            GROUP BY o.customer_id ORDER BY amount DESC
                - เลือกข้อมูล c.name, COUNT(c.id) คือ นับ row ของ id จากตาราง customers แทนด้วย amount โดยเอาข้อมูลจากตาราง customers
                ต่อกับตาราง orders แทนด้วย o ด้วยเงื่อนไข c.id = o.customer_id
                โดยจัดกลุ่มของข้อมูลจาก column customer ของตาราง orders และเรียงจาก amount จากมากไปน้อย
            
            ex. หาจำนวน order ในแต่ละวัน
            SELECT o.date, COUNT(*) AS amount FROM ecommerce.orders AS o 
            GROUP BY o.date

            ex. หาคนที่ order ในแต่ละวัน
            SELECT o.date, c.name, COUNT(c.name) as amount FROM ecommerce.orders AS o 
            JOIN ecommerce.customers AS c ON c.id = o.customer_id
            GROUP BY c.name, o.date
            ORDER BY o.date
                - GROUP BY c.name, o.date แปลว่า ต้องมีทั้งชื่อและวันที่ซ้ำกันถึงจะรวมกลุ่มกัน

            ex. หายอดขายทั้งหมด
            SELECT SUM(oi.amount * (oi.price * (1 - oi.discount))) AS total From order_items AS oi

            ex. หาว่าแต่ละ order มียอดขายเท่าไหร่
            SELECT oi.order_id, SUM(oi.amount * (oi.price * (1 - oi.discount))) AS amount FROM order_items oi 
            JOIN orders o ON oi.order_id = o.id
            GROUP BY o.id
                - sum คือ ผลรวมของ (oi.amount * (oi.price * (1 - oi.discount))) ในทุก row จากตาราง order_items ที่ต่อกับตาราง orders 

            ex. ยอดสั่งซื้อของลูกค้าแต่ละคน
            SELECT c.name, SUM(oi.amount * (oi.price * (1 - oi.discount))) AS sales FROM customers c 
            JOIN orders o ON c.id = o.customer_id
            JOIN order_items oi ON o.id = oi.order_id
            GROUP BY c.id

            ex. หายอดขายและจำนวนของแต่ละ product
            SELECT p.name, SUM(oi.amount) as amount, SUM(oi.amount * (oi.price * (1 - oi.discount))) as sales FROM products p
            JOIN order_items oi ON p.id = oi.product_id
            GROUP BY p.id
                - COUNT(oi.amount) ใช้ count แบบนี้ไม่ได้เพราะว่า มันจะนับแต่แถวที่มี แต่ไม่นับรวมจำนวนให้เราเลยต้องใช้ SUM(oi.amount)
                oi.price เพราะเป็นราคาที่ขายไปแล้วแต่ถ้าใช้ p.price ราคามันไม่แน่นอน

### การเรียงลำดับการใช้คำสั่ง mysql
    SELECT product_id , SUM(price * amount * (1 - discount)) AS total 
    FROM order_items
    WHERE
    GROUP BY product_id
    HAVING total > 20000
    ORDER BY total DESC
    LIMIT 5 
    OFFSET 10
    - WHERE จะใช้กับพวก column
    - HAVING จะใช้กับการกำหนดเงื่อนไขของ aggregate function(COUNT, MAX, MIN, SUM)) มั่กจะใช้คู่กับ GROUP BY แต่ไม่ใช้ก็ได้แต่อาจจะทำให้ความหมายผิดเล็กน้อย
    - LIMIT 10 ==> ข้อมูล 10 อันแรก
    - OFFSET 10 ==> คือเลื่อนไปอีก 10 เริ่มเอาข้อมูลที่ 11 และการใช้ OFFSET ต้องใช้คู่กับ LIMIT ใช้เดี่ยวๆไม่ได้
    - เวลาใช้กับ GRUOP BY, ORDER จะทำ GROUP BY, ORDER ก่อน ค่อยทำ LIMIT

### connect node express with MySQL

    pool.execute(`INSERT INTO products (name, price) VALUES (${name}, ${price})`, (err, result, fields)
        - insert ค่าเข้าไปตรงๆ (${name}, ${price}) ค่อนข้างไม่ปลอดภัย อาจทำให้ database เพี้ยนได้  (sql injection) เช่น ลบ table เราทิ้งหรืออื่นๆ

    pool.execute(`INSERT INTO products (name, price) VALUES (?, ?)`, [name, price], (err, result, fields)
        - ใช้วิธีนี้ในการป้องกัน sql injection 
            ? ตัวแรก = name
            ? ตัวสอง = price

    pool.execute('SELECT * FROM products', (err, result, fields) => {
        console.log(result)
        console.log(fields)
    })
        - result จะขึ้นอยู่กับว่าใช้กับคำสั่งอะไร
        [
            BinaryRow { id: 1, name: 'coke', price: '20.00' },
            BinaryRow { id: 2, name: 'Pepsi', price: '19.00' }
        ]
            1 row คือ 1 object
            1 table คือ array ที่ประกอบด้วยหลายๆ object
        - fields 
            จะบอก data type แต่ต่องมานั่งแปลเอง ทำให้อ่านยาก

#### promise chaining 
    คือ การเอาค่าที่ return จาก promise ไปใช้ใน then ถัดไป
    ex.
        db.execute('SELECT * FROM products')
        .then(result1 => {
            console.log(result1)
            return result1[0] // return new Promise() เลยใช้ .then ต่อได้
        })
        .then(result2 => {
            console.log(result2)
            return result2.filter(product => product.id === 1);
        })
        .then(result3 => {
            console.log(result3)
        })
        .catch (err) {
            next(err)
        }

    - ถ้าใส่ await จะไม่ได้ return เป็น promise จะ return เป็น array ออกมา
    - async, await ใช้ได้กับสิ่งที่ return promise เท่านั้น
    - promise จะช่วยในการลด duplicate code

### ใช้ model ด้วย class
    - syntax ของ class
        class ClassName {
            constructor(para1, paraN) {
                this.para1 = para1;
                this.paraN = paraN;
            }

            functionName(para) {
                return para
            }

            static functionName(para) {
                return para
            }
        }
        
    - การใช้ model ด้วย class ชื่อ class จะตั้งตัวแรกเป็นตัวใหญ่
    - สร้าง class ไว้เป็นตัวแทนแต่ละ row ใน column
    - static method คือ method ที่ติดมากับ class นั้นๆ
    - object ที่สร้างมาจาก class นั้น method ที่เรียกใช้คือ instant method (object จะสร้างขึ้นมากี่ตัวก็ได้แค่ประกาศ new ใหม่)
        ex.1 (object ที่สร้างมาจาก class, now คือ instant method)
            const today = new Date();
            today.now();
        ex.2 (now คือ static method, class method ที่มาจาก class โดยตรง)
            Date.now() ;
    - class ไม่มี key, value ต้องส่งเป็น parameter เข้าไป
    - กำหนด static หน้า method จะทำให้เรียกจากชื่อคลาสได้โดยตรงได้เลย
        ex.
            ClassName.functionName();
    - ถ้าไม่กำหนด static หน้า method จะต้องประกาศตัวแปรและใช้ new ClassName() ถึงจะใช้ได้และไม่สามารถใช้ method ที่มี static หน้า method ได้
        ex.
            const x = new ClassName();
            x.functionName();
    - เราเลือกใช้ class เพราะจะเขียนให้ดูไม่รกกว่าการใช้ promise 

### HTTP Status Codes
    200 - ok
    201 - created
    204 - no content
    400 - bad request
    404 - not found
    500 - internal server error
    502 - bad gateway
    504 - gateway timeout

### res.affectedRows
    คือผลจากการกระทำคำสั่งเรามันมีผลกระทบกับ row ใน table เรากี่ row
    
### bind values คือ การผูกค่าเข้ากับ parameter 
    ex.
    'DELETE FROM products WHERE id = ?', [id]
    โดย id = ? จะ bind เข้ากับ [id] 
    ซึ่งค่าจะเป็น undefined ไม่ได้จะ error

### Transaction mysql (ช่วงธุรกรรม เหมือนให้ทำอยู่ในกล่องนั้นๆ ทำเสร็จจะ save(commit) หรือย้อนกลับก็ได้)
    connection, 
    commit === บันทึกลง database จริงๆ,
    rollback === คำสั่งลบใน Transaction อะไรที่พยายาม save ลงไป เอาออกหมด ย้อนไปถึง begin transaction,
    ช่วงตั้งแต่ begin ลงมาถึง commit คือ transaction
    
### nestTables === ตารางซ้อนตาราง (แต่อาจจะทำให้เอาข้อมูลไปใช้ต่อยาก ควรเลือกเป็นช่องที่ต้องการดีกว่า)
    nestTables: true ==> จะแสดงข้อมูลแยกกันระหว่างสองตารางที่เอามา
        ex.
        "o1": {
            "name": "coke"
        },
        "o2": {
            "date": "22-03-2021"
        }
    nestTables: '_' ==> จะแสดงข้อมูลตารางที่มา JOIN กันรวมกันโดยแยกเป็นชื่อ key ตารางตามด้วย _ + ชื่อ column
        ex.
        "o1_employee_id": 3,
        "o2_id": 7,

### ตัวอย่างรูปแบบการส่ง json body ใน function createOrder
    {
        "customerId": 1,
        "employeeId": 5,
        "items": [
            {
                "productId": 1,
                "amount": 1,
                "discount": 0.05
            },
            {
                "productId": 2,
                "amount": 2 
            }
        ]
    }