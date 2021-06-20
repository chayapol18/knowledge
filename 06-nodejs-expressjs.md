# Node JS
    - single thread
    - เหมาะกับงานที่ต้องมีการ “รอ” เป็นจำนวนมาก
    - ให้ node เข้ามาทำงาน พิมพ์ node (ชื่อไฟล์)
    - สามารถทดสอบบน terminal
        ด้วยคำสั่ง node >> คำสั่ง js ที่ต้องการ (const b = 20, console.log(b))
    - .exit จะไว้ออกจาก node บน terminal

## import & export
    - Node ไม่สามารถใช้ ES6 ได้ แต่สามารถใช้ libraries ในการทำให้มันทำได้อยู่เหมือนกัน
    - import & export by "common js"
    - export 
        ด้วยคำสั่ง module.exports = สิ่งที่จะ export
    - export key = value ด้วยคำสั่ง โดยจะ exports กี่ key ก็ได้แต่จะรวมกันเป็น object เดียว
        exports.username = 'John'
        exports.password = '12345678'
        { username: 'John, password: '12345678}

    module.exports , exports.key 
        ใช้งานร่วมกันได้ก็จริงแต่ความสำคัญจะให้ module.exports มากกว่าโดยจะไม่ทำงานในส่วนของ exports.key เลย

    - import 
        ด้วยการประกาศตัวแปร const ตัวแปร = require('./ชื่อไฟล์')

## Node Package Manager
    - npm (Node Package Manager) คือตัวจัดการ package หรือ library หรือ module ใน Node.js
    - ปัจจุบันมี module ให้เราเลือกใช้อยู่มากมายโดยที่เราไม่จำเป็น
    ต้องเขียน Code เองทั้งหมด

    - module แบ่งออกได้เป็น 3 ประเภท คือ
    1. Built-in module 
        คือ module ที่อยู่ภายใน Node.js เช่น fs(file system), path, utils
    2. Custom module 
        คือ module ที่เราสร้างขึ้นมาใช้งานเอง
    3. Third party module 
        คือ module ที่โปรแกรมเมอร์ อื่นๆ พัฒนาขึ้นมา แล้วเราไปนำมาใช้ เช่น axios, cors, express, dotenv
    ใช้ npm จัดการส่วนที่เป็น Third party module 

    - react โดยปกติจะ npm init ให้แล้ว แต่ backend ไม่ใช่, 
    npm init ไว้ในการเริ่มสร้าง package.json
        - npm init ต้องกรอกข้อมูลเอง, 
        - npm init -y ไม่ต้องกรอกข้อมูล generate อัตโนมัติ
        - รูปแบบข้อมูลจะได้เป็น json
        - เวลา npm start ระบบจะวิ่งไปหา scripts ที่คำสั่ง start แล้วรันตามที่เราเขียนไว้ (ไว้ใช้เวลาขึ้น server)
        - scripts tag ตัวอื่นๆที่ไม่ใช่ start ต้องมีคำสั่ง run ด้วย  เช่น npm run dev
        
    - install package
        - ใช้คำสั่ง 
        npm install <package-name> หรือ 
        npm i <package-name>
        - อย่าลืมดู folder ด้วย ต้องมีไฟล์ package.json
        - จะเก็บ libraries ใน node_modules อาจจะมีตัวอื่นที่เราไม่ได้ลงด้วย แต่ libraries นั้นดึงมาใช้ก็เลยต้องลงมาด้วย
        - npm i, npm install 
            เมื่อรันคำสั่งจะวิ่งไปหาไฟล์ package.json เพื่อให้มันโหลด module ที่ใช้ในโปรเจคนั้น เช่นเวลาโคลนมาจาก github เหมือนไว้เช็คว่ามี package อะไรที่ต้องใช้บ้าง ถ้าไม่มีก็จะโหลดเข้ามาให้ในโปรเจค
        - install local, global
            local: ใช้ได้เฉพาะในโปรเจคนั้นๆ
            global: ใช้ได้ทุกโปรเจคที่อยู่ในเครื่องเรา ด้วยคำสั่ง npm install -g<package-name> แต่ไม่ควรใช้ global เพราะ version อาจจะไม่อัปเดทตามมา
        -  npm i -g nodemon จะทำให้อัปเดทไฟล์ทุกครั้งที่มีการ Save และรันไฟล์นั้น (ctrl + c ไว้ออกจาก nodemon)
        - npm install -D <package-name> ไว้ใช้ตอน dev เท่านั้น
        
        - เรียกใช้ package 
            ด้วย require เหมือนกันแต่ require ด้วยชื่อ module เลยไม่ต้องเรียกชื่อไฟล์ เช่น
            const express = require('express');
    - uninstall package
        - ใช้คำสั่ง 
            npm uninstall <package-name>
        - กรณี global 
            ใช้คำสั่ง npm uninstall -g <package-name>
        - กรณี dev mode 
            ใช้คำสั่ง npm uninstall -D <package-name>
    
    - npx
        - ทำให้เรา run script ใน Node.js โดยไม่ต้องติดตั้ง module ก่อน เช่น create-react-app 
            เมื่อก่อนต้องสั่ง npm i -g create-react-app ลงบนเครื่องก่อน แล้วค่อยใช้คำสั่ง create-react-app <project-name>
            ปัจจุบัน ใช้คำสั่ง npx create-react-app <project-name> ได้เลย โดย Node.js จะหา module create-react-app และ run script ให้เราโดยอัตโนมัติ

        - ต้องการใช้คำสั่งเป็นครั้งคราว
        เพราะมันจะวิ่งไปหาบน internet ให้ ปเรา แต่ไม่ได้ดาวโหลด package มาให้เรา
        - npx จะวิ่งหา version lastest ให้เสมอ

    - module version
        "dependencies": {
            "axios": "^0.21.1",
            "nodemon": "^2.0.7"
        }
        - เครื่องหมาย ^ จะดู version ของ minor คือเลขหลังจุดแรก (21 ใน axios)
        - การจะให้เปิดอัปเดทอะไรต้องระวังว่ามันจะใช้ได้แน่รึป่าว ไม่งั้น ลงมาแล้วอาจจะใช้ไม่ได้

## สร้าง Web server
    -response ควรใช้ตามที่เขากำหนดมา เพื่อให้เป็นการสื่อสารที่เข้าใจเหมือนๆกัน
    - module http
    - const http = require('http');
    -const server = http.createServer((req, res) => {});
    - (req, res) => { }; เรียกว่า requestListener รับ parameter 2 ตัว คือ

      req คือ object ของ class IncomingMessage มี property ที่สำคัญ คือ
        req.method ใช้อ่านค่าmethod ของ request (GET, POST etc.)
        req.url ใช้อ่านค่า url ของ request (/home, /about)
        req.headers ใช้อ่านค่า headersของ request

      res คือ object ของ class ServerResponse มี property และ method ที่สำคัญ คือ
        res.statusCode ใช้ set ค่า response status code (200, 400, 401, 404, 500 etc.)
        res.setHeader() ใช้ set ค่า header ของ response
        res.end() ใช้เพื่อบอกว่า response พร้อมจะส่งกลับไปที่ client
        
    - refresh เท่ากับ request 1 ครั้ง

# Express
    - framework ที่นิยมมากในการสร้าง web app บน Node.js
    - community กว้าง คนใช้เยอะเลยทำให้หาวิธีแก้ไขปัญหาต่างๆได้
    - *** set up >> (in folder) npm init -y >> npm i express ***

## Basic Routing
    - routing คือ วิธีที่บอกให้ server จัดการกับ request จาก client ในแต่ละ endpoint
    - endpoint ประกอบด้วย URI (path) และ http request method (GET, POST etc.) 
    - สร้าง routing โดยใช้คำสั่ง <app.METHOD(PATH, HANDLER)>
        - app คือ express object ที่สร้างจาก express()
        - METHOD คือ http request method (GET, POST, PUT, PATCH, DELETE)
        - PATH คือ path ที่ส่งมาจาก http request
        - HANDLER คือ callback function ที่ใช้จัดการกับ request และ response
    ถ้า http request มี method และ path ตรงกับที่เราสร้าง route ไว้ จะทำงานใน handler function หากไม่ตรงกันจะไม่ทำงาน

    - path กับ method ต้องตรงกันเสมอไม่งั้นจะไม่สามารถส่ง request ได้

    -ใน browser จะเป็น method get เสมอ อะไรที่ไม่ใช่ method get ปกติจึงไป test ใน postman

    - app.post('/', (req, res) => {
        res.status(200).send('<h1>Hello My fisrt express project</h1>')
        }) >> หลัง , ตัวแรกคือ handle function (callback function)

### Response Object
    response object คือ object ที่เก็บข้อมูล http response และจะถูกส่งกลับไปที่ client เมื่อ
    มี http request เข้ามา
        method ที่สำคัญ
            - **res.status(code) ใช้ set ค่า response code (200, 400 etc.)
            - **res.send(body) ใช้เพื่อส่ง response กลับไป bodyอาจเป็น text, array etc.
            - **res.json(body) ใช้เพื่อส่ง response กลับไป โดยส่ง response ออกไปในรูปแบบ JSON 
            - res.redirect(path) ใช้เพื่อสั่งให้ response redirect ไปที่ path ที่ต้องการ  
            
### Request Object
    - request object คือ object ที่เก็บข้อมูล http request เมื่อรับ request มาจาก client
    ส่วนต่างๆ ของ url path

    https://shopee.co.th/flash_sale/2?fromItem=8812942592&promotionId=2009691392

        https: คือ protocol
        shopee.co.th คือ hostname
        flash_sale คือ path
        fromItem=8812942592&promotionId=2009691392 คือ query string (หลังเครื่องหมายคำถาม)
        2 คือ parameters

#### Client and Server side
    - Client Side
            >> React เขียนหน้าตาให้คนอื่นใช้

    - Server Side
            >> backend หลังบ้านที่ผู้ใช้ไม่เห็น
            >> Node.js

    - request สิ่งที่เชื่อมกันระหว่าง Client Side และ Server Side เวลา request เหมือนต้องมีจดหมายแนะนำตัวว่า request อะไรไป ฝั่ง server ก็จะดูจดหมายแล้วจะคิดว่าทำยังไงแล้ว response กลับมา

### Request(req) and Response(res)

    app.get('/user', (req, res) => {
        res.status(200).json({ path: 'user', method: 'POST' })
    })

    - express จะทำการแกะ request มาว่าตรงตามเงื่อนไขที่ request มารึป่าว ถ้า method และ path ตรงก็จะทำงานคำสั่งนั้นๆ ถ้าไม่ตรงก็จะหาคำสั่งต่อไป จะไล่เช็ค(ทำงาน)จากบนลงล่าง

    - res.status... จะจบการ request ด้วยการ response ส่งอะไรที่เรากำหนดออกไป จริงๆ .status จะเขียนหรือไม่เขียนก็ได้ ถ้าไม่เขียน ระบบจะส่ง 200 ออกไป

### Middleware
    - เป็น function ที่อยู่ระหว่าง request และ response 
    - สามารถแก้ไข request และ response object ได้
    - จบการทำงานได้โดย res....
    - ใช้ next() ในการทำ Middleware ตัวถัดไป
    - ** เมื่อมี request ก็ต้องมี response อะไรออกไปให้มัน **
    - ไม่จำเป็นต้องผ่าน middleware ที่กำหนดทุกตัว อาจจะจบที่ middleware ตัวไหนก็ได้

    - รูปแบบของ middleware >> (req, res, next) => {};
        - req คือ request object ซึ่งประกอบไปด้วยข้อมูลต่างๆ ที่ส่งมาจาก http request
        res คือ response object ซึ่งประกอบไปด้วยข้อมูลต่างๆที่เราต้องการส่งไปใน http response
        next คือ function ที่สั่งให้ไปทำงานใน middleware ตัวต่อๆไป 
    
    - เรียกใช้ middleware 
        app.use((req, res, next) => {});

        -ข้อสังเกตุคือไม่มี path เหมือนกับ(handler function ) get, post, ... ซึ่งหมายความว่าทุก request ที่เข้ามาจะต้องผ่านตัวนี้

        - ตัวอย่างการใช้ middleware 2 ตัว 
            app.use((req, res, next) => {
                req.user = { id: 1, username: 'John', role: 'admin' };
                next();
            });
            app.use((req, res, next) => {
                if (req.user.role !== 'admin') return res.status(401).json({ message: 'Un' });
                next();
            });
          
        - req.user เป็นสิ่งที่เราเพิ่มเข้าไป(เพิ่ม property user) ไม่ใช่สิ่งที่ express สร้างขึ้นมาให้

        - ถ้าไม่มี next() ก็จะไม่วิ่งไปทำงานที่ middleware ตัวถัดไป

        -ถึงจะ response แล้วก็จริงแต่ถ้ามี next() ก็จะทำงาน middleware ตัวต่อไปเรื่อยๆ แต่ถ้าใส่ response เข้าไปอีก จะทำให้เกิด error เพราะ 1 request แต่จะส่ง response ออกไปสองรอบ 
        *** 1 request 1 response ***
    
### Router-level middleware
    -ยุบรวม path ได้
    - const router = express.Router(); >> เป็น middleware ตัวนึง
    
    const router = express.Router();

    router.get('/login', (req, res, next) => {})
    router.post('/register', (req, res, next) => {})
    router.get('/profile', (req, res, next) => {})
    router.get('/post', (req, res, next) => {})
    router.post('/profile', (req, res, next) => {})
    router.delete('/post', (req, res, next) => {})

    app.use('/user', router);

    -การทำงานคือจะวิ่งมาเช็คที่ app.use ก่อนว่า path เราใช่ /user รึป่าว >> ถ้าใช่จะวิ่งเข้าไปเช็ค path ถัดไปที่ router ต่อ >> ถ้าใช่อีกก้จะทำงานคำสั่งภายในนั้น การเขียนแบบนี้จะเป็นการ group รวม path หลักไว้ก่อน
    
    -การเขียนด้านบนมีผลเหมือนกับ code 6 บรรทัดด้านล่างนี้
    app.post('/user/login', (req, res, next) => {})
    app.post('/user/register', (req, res, next) => {})
    app.get('/user/profile', (req, res, next) => {})
    app.get('/user/post', (req, res, next) => {})
    app.post('/user/profile', (req, res, next) => {})
    app.delete('/user/post', (req, res, next) => {})
        
### Error-handling middleware
    app.use((err, req, res, next) => {});

    - ไว้จัดการ error ที่เกิดขึ้นในระบบ (ทำงานเมื่อเกิด error)

    - แก้ error ตรงไหนก็ตามจะวิ่งหา error middleware ทันที โดยข้าม middleware ตัวอื่นๆไปเลย

    - ต้องใส่ parameter 4 ตัว ให้ครบไม่งั้นมันจะมองว่าเป็น middleware ปกติ

### Multi export
    - export แบบหลายตัว
      - กำหนด exports หน้าตัวแปร 
          <exports.ตัวแปร>
      - ส่งแบบ key ไปหลายๆค่า โดยรูปแบบนี้ต้องคู่กับ const
      module.exports = {
          calAge, // calAge: calAge, 
          getTimeDiff // getTimeDiff: getTimeDiff
      }
    
### Url Path
    - Query String
        - อยู่หลังเครื่องหมาย ? บน url 
        - คือส่งข้อมูลเพิ่มเติมให้ server 
        - const query = req.query
        - เพิ่มค่าได้ใน postman โดยใส่ ? แล้วตามด้วย key value คั่นระหว่างตัวแปรด้วย & หรือใส่ในหน้า params ใน postman ได้
        - query ต้องอยุ่หลังสุด อยู่ก่อน id ไม่ได้จะ error
        - ใช้ในการ filter ข้อมูล, ส่งข้อมูลได้จำนวนมาก, ข้อมูลที่ไม่เป็นความลับ เพราะทุกคนสามารถเห็นได้
    
    - Parameter
        - params = parameters
        - ค่าที่รับเข้ามาเป็น string เสมอ
        - /product/:id >> :id เหมือนชื่อ key ที่เราจะกำหนด
        - /product/:id/:price >> เพิ่ม params price เข้าไป
        - เป็นการเปรียบเทียบค่าระหว่างก้อนที่สร้าง กับ ก้อนที่ส่งมา
            /product/:id/:price vs http://localhost:8000/product/8/50

    - Body
        - ส่ง body ไปที่ server 
            วิธีแรกผ่าน form
            - ส่งได้แค่ POST, PUT, PATCH >> การสร้างข้อมูล, อัพเดทข้อมูล
            - Delete ส่วนใหญ่จะส่งผ่าน parameter ไปให้ server ทำงาน
            - web ที่ไม่ใช้ react ในการทำงานจะส่งแบบนี้
            - Content-Type เป็น application/x-www-form-urlencoded (default enctype ของ form)

        - ส่งแบบ multipart/form-data
            ใช้กรณีที่ต้องการส่งข้อมูลแบบ binary


        - ส่งผ่านข้อมูลแบบ raw json 
            - สามารถส่งข้อมูลที่ซับซ้อนได้ดี
                {
                    "product": [
                        "coke",
                        "pepsi"
                    ]
                }
            - แปลงค่า raw json ที่ส่งมาด้วย app.use(express.json()) >> ทำงานคล้ายๆ JSON.stringtify
                - ต้องไว้ด้านบนเสมอ ไม่งั้นจะทำงานไม่ได้
                - ต้องเปลี่ยนชนิดเป็น json ด้วย

    *** ทุกอย่างที่ส่งมาจาก req จะได้เป็น string เสมอ ไม่ว่าจะเป็น params หรือ query ***

    - products[products.length -1].id + 1 คือเพิ่มค่า id สุดท้ายโดยไม่ใช้ hard code

    ** ต้องใส่ key ใน postman ให้ตรงกับที่กำหนดไว้ใน vs code **

    ** อย่าลืมต้อง validate data เช็คว่าข้อมูลส่งมาถูกต้องตามที่กำหนดรึป่าว ไม่งั้นอาจจะทำให้ข้อมูลเพี้ยนได้ **

### MVC Model
    - Model, View, Controller
    - เอามาช่วยในการพัฒนา web app ในการแบ่งส่วนต่างๆของ web

    - view (ส่วนที่ user เห็น) = html
    - controller (logic ของโปรแกรมทั้งหมดบนเว็บ)
    - model ส่วนที่เชื่อมกับระหว่าง database กับ โปรแกรมของเรา (object)

### Others technical

    - การเอา Middleware มาประยุกต์ใช้กับการ check หรือ validate ข้อมูลต่างๆ โดยการตั้ง middleware ขึ้นมาให้ทำงานก่อน middleware หลักของการทำงานนั้นๆ
        เช้น router.post('/add', productController.validateProduct, productController.addProduct)

    - เวลาสร้างโปรเจคจริง ควรสร้าง controller, route อะไรให้เรียบร้อยเลย refactor ที่หลังทำให้ทำงานยุ่งยาก

    - ตอนทำ asynchronous (async, await) ต้องทำ try catch ด้วย
    
    - function ที่จะใช้ async await ได้ต้องเป็น function ที่ return เป็น promise

    *** ใช้ restful api สำหรับ path ต่างๆบนเว็บด้วย ***
