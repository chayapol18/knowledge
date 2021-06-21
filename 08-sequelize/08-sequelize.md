# Sequelize
    - ทำให้เราไม่ต้องเขียน raw sql เอง
    - mapping คือการ convert sql to object.js การเอาชื่อ column มาเป็น key และข้อมูลในแต่ละ row จะเป็น value

    SQL
        id     name     address
        1      ลีโอ      ปทุมธานี

    Object.js
        {
            id: 1,
            name: "ลีโอ",
            address: "ปทุมธานี"
        }

    -จริงๆจะใช้หรือไม่ใช้ sequelize ก็ได้ ถ้าไม่ใช้ก็จะต้องเขียน raw sql เอง (ถ้าตารางข้อมูลเยอะๆจะเหมาะกับการใช้ sequelize)

    - set up ==> npm i sequelize
    - const Sequelize = require('sequelize')

## Op (Operator)
    ใช้กับ
    [Op.or], 
    [Op.gte] (greater than or equal >=), gt = greater than
    [Op.lte] (less than or equal <=), lt = less than
    ...
    แต่ถ้าเป็น and ใช้ short hand ได้เลยก็คือเขียนต่อไปเรื่อยๆ

## Connect sequlize to express>
    setup
      - npm i -g sequelize-cli
          ทำให้รันคำสั่ง sequelize บน command line ได้
      - (npx) sequelize-cli init:config
          จะสร้าง folder config และ กำหนดการเชื่อมต่อกับ database ให้ โดนไปแก้ไขเล็กๆน้อยเช่น password, ชื่อ database
      - (npx) sequelize-cli init:models
          จะสร้าง folder models และ file index.js
              - index.js จะคอยเอาไฟล์อื่นๆมาสร้าง model ให้และส่งออกไปใช้ต่อที่อื่นๆ

    transaction
      - ไว้สำหรับการทำคำสั่งมากกว่า 1 คำสั่งพร้อมกัน โดยป้องกันการผิดพลาดของการบันทึกข้อมูล

    คำสั่งใน sequelize ส่วนใหญ้เป็น promise ดังนั้นต้องมี await เสมอ

    ถ้าใช้ raw sql ใน sequelize ต้อง import
      const { QueryTypes } = require('sequelize')
      มาใช้ด้วยเสมอ