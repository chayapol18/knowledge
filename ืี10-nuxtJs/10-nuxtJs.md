# Nuxt JS
    framework for vue js

## VueJS vs NuxtJS
    Vue 
      จะทำงานอยู่บน Client Side Rendering (CSR)

    Nuxt 
      จะทำงานได้ทั้ง Client Side Rendering (CSR) และ 
      Server Side Rendering (SSR) ซึ่งก็คือ Nuxt จะมา
      ช่วยในการจัดการฝั่ง SSR ให้ Vue

## Components
    สามารถสร้างไฟล์ใน folder components แล้วเอาไปใช้ได้เลยโดยไม่ต้อง import 
    เข้ามาแบบ vue

## Plugins
    ไว้สร้างไฟล์สำหรับสิ่งที่ต้องการ import เข้ามาแล้วเอาไปใช้ได้เลย 
    เพราะจะไม่มีการ import เข้ามาในแต่ละหน้าแบบ vue แล้ว เช่น element-ui 
    ก็ให้สร้างเป็น element-ui.js แล้ว import เข้ามาครั้งเดียว
    ex. file element-ui.js
      import Vue from ‘vue’
      import ElementUI from ‘element-ui’
      import ‘element-ui/lib/theme-chalk/index.css’;
      import lang from ‘element-ui/lib/locale/lang/en’
      import locale from ‘element-ui/lib/locale’
      locale.use(lang)
      Vue.use(ElementUI)

    dataTable ของ element ui ก็เช่นกันและ dataTable ของ element 
    จะไม่ support การทำงานของ SSR ดังนั้นจะต้องบอก nuxt ว่าไม่ต้อง run 
    dataTable ที่ฝั่ง server ดังนี้
        plugins: [
      ‘~/plugins/element-ui.js’,
      {
        src: ‘~/plugins/data-table.js’,
        ssr: false // บอก nuxt ว่าจะไม่รันตัวนี้ที่ ssr
      }
      ],
    หรือประกาศเป็น tag ใน template
      <no-ssr>
        <data-tables 
          :data=“users” 
          :total=“10" 
          @sort-change=“sortChange” 
          @current-page=“currentPage”
          @size-change=“sizeChange”>
          <div slot=“empty” style=“color: red”>Users is empty</div>
          <el-table-column prop=“username” label=“Username” width=“200" sortable>
          </el-table-column>
          <el-table-column prop=“name” label=“Name” width=“400” sortable>
          </el-table-column>
          <el-table-column prop=“email” label=“Email” width=“200" sortable>
          </el-table-column>
          <el-table-column fixed=“right”>
            <template slot-scope=“scope”>
              <el-button type=“text” size=“small” @click=“editUser(scope.row)“>Edit</el-button>
              <el-button type=“text” size=“small”>Delete</el-button>
            </template>
          </el-table-column>
        </data-tables>
      </no-ssr>

## asyncData() & fetch() 
    asyncData()
      - จะเหมือนกับ data() แต่สิ่งที่แตกต่างคือ asyncData() จะรันฝั่ง SSR,
      ส่วน data() จะรันฝั่ง CSR
      - asyncData() จะไม่มี this เหมือน vue แต่จะใช้ context แทน
        asyncData (context) สามารถ destructuring ได้เป็น asyncData({ $axios, params })
      - asyncData() จะเอาข้อมูลที่รับมา merge เข้าตัวแปรใน data() ปัจจุบันอัตโนมัติ
 
    fetch()
      จะเหมือนกับ asyncData() แต่ asyncData จะทำงานได้แค่ใน folder pages

## JWT
    สิ่งที่ควรทำเกี่ยวกับ jwt คือไม่ควรเก็บใน localStorage แต่ควรเก็บใน cookie ด้วย httpOnly

    ดังนั้นวิธี setup httpOnly คือ
    ตอน set cookie
      const token = jsonwebtoken.sign({ user: req.body.username }, jwtSecret);
      res.cookie(‘token’, token, { httpOnly: true, secure: true});
      //res.cookie(‘ชื่อ cookie’, ตัวแปร, { httpOnly: true, secure: true})) >> ตรง {} ทำให้ใช้ได้แค่ httpOnly อย่างเดียว

    ตอนใช้งาน cookie
    app.use(jwt({ secret: jwtSecret, algorithms: [‘HS256’], getToken: req => req.cookies.token }));


## Link
    ถ้าเกิดต้องการใช้ tag <a></a> เพื่อ link ไปที่อื่นของ nuxt js จะใช้ 
    <NuxtLink></NuxtLink> แทน

## Path *
    Path ของ Nuxt จะไม่สามารถสร้างเป็น folder router และประกาศแต่ละ path, component ได้
    ซึ่งเมื่อต้องการสร้าง path ขึ้นมาให้สร้าง folder pages และสร้าง index.vue เท่ากับว่าเราจะมี path / เรียบร้อย
    และถ้าต้องการให้มี / + path อื่นเข้าไป ให้สร้าง folder เป็น path นั้นๆเข้าไปอีกทีนึง
    เช่น
        folder pages
          index.vue
          folder home
            index.vue
            folder profile
              index.vue

        จากตัวอย่าง path ที่ใช้ได้คือ /, /home, /home/profile

    โดยปกติเมื่อเราต้องการใช้ path ในการเชื่อมไปที่ต่างๆ ปกติจะต้องดูชื่อ path ที่ vue devtool 
    หรือชื่อ path โดยทั่วไปจะต่อ path ย่อยๆด้านในด้วย - เช่น home-profile

  







