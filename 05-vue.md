# Vue
## Concepts
    Encapsulation
      Ex. ถ้ามี component a กับ b 
        ถ้าจะ b จะใช้ตัวแปรจาก a จะใช้เลยไม่ได้ต้องให้ a ส่งมาให้ b และรวมถึงถ้า a อยากใช้ function จาก b ก็ต้องให้ b ส่ง function ข้ามมาให้เท่านั้น
      แสดงว่าอะไรที่อยู่ใน component นั้นก็จะอยู่แค่ใน component นั้นเท่านั้น

    1 component ประกอบด้วยอะไรบ้าง
      - Template
        <template>
          <div>
            <h1>Hello</h1>
          </div>
        </template>

      - Script
        export default {
          name: 'app',
          component: {
            Page
          }
        }

      - Style
        <style>
          .class {

          }
        </style>
    
    Two-way binding
      เมื่อ template เปลี่ยน ตัวแปรเปลี่ยน หรือ ตัวแปรเปลี่ยน template เปลี่ยนไปด้วย ด้วย watcher
  
# Conditionals
    How to use variable in return
      {{variable}}

    v-for
      - เวลาเกิดการอัพเดท item ถ้าไม่รู้ว่า item ไหน มันจะ loop แยกทุก item ทำให้ช้า ดังนั้นจึงควรใส่ key เพื่อให้ vue รู้ว่าต้องไปอัพเดท item ไหน, ควรจะเป็น key ที่ unique ที่สุด 
      ex.
      <ul>
        <li v-for="todo in todos" :key="todo.time">
          {{todo.text}}
        </li>
      </ul> 
    
    v-html
      ทำให้ใช้ tag html ได้แต่ต้องระวังเพราะอาจจะทำให้มี tag แปลกๆหลุดเข้ามาใน element นั้นได้
      ex.
      <li v-for="todo in todos" v-html="todo.text" :key="todo.time"></li>

    filters
      สามารถทำให้แปลงค่าต่างๆของตัวแปรได้ เช่น ทำให้ตัวอักษรกลายเป็นตัวพิมพ์ใหญ่
      ex. 
        <li v-for="todo in todos" :key="todo.time">
          {{todo.text | capitalize}}
        </li>
      export default {
        name: 'test',
        filters: {
          capitalize (value) {
            return value.toUpperCase()
          }
        },
      }

      v-if
        condition if else
        ex.
          <div v-if="todo.completed === false">Still {{todo.text}}</div>
          <div v-else-if="todo.completed === true">Compelted {{todo.text}}</div>
          <div v-else>{{todo.text}}</div>      

      v-show
        คล้ายกับ v-if แต่ไม่มี else สิ่งที่ต่างกันคือ component ใน console ของ v-show จะยังมี element นั้นอยู่แต่ display เป็น none แต่ของ v-if มันจะหายไปเลย, แต่จริงๆการใช้ v-show อาจจะดีกว่่าในเรื่อง performance
        ex.
          <div v-show="todo.completed === true">Show this {{todo.text}}</div>  

      v-bind (:varibale)
        v-bind:variable แต่ย่อได้เป็น :variable มีหน้าที่ทำให้ element นั้นสามารถเอา variable ที่ประกาศไว้ด้านล่างมาใช้ได้ และทำให้ variable นั้นกลายเป็น js
        ex.
          <img :src="srcUrl.replace('http://', 'https://')">
      
      Class and Style bindings
        เมื่อเงื่อนไขที่กำหนดใน class เป็นจริงจะเปิดใช้งาน class นั้นๆใน element ที่กำหนด style ก็เช่นกัน
        ex. class
          <li :class="{red: !todo.completed, green: todo.completed}"></li>

        ex. style
          <li :style="{color: color}"></li> ==> กลายเป็น inline style ตามตัวแปร color ที่ประกาศไว้ใน script

      css in vue
        <style scoped lang="scss">
          ทำให้ css ตัวนี้มีผลแค่ใน component นี้เท่านั้น มีข้อเสียในเรื่องการกิน performance นิดหน่อยต้องระวังในการใช้
          lang="scss" ทำให้เขียน scss ได้เลย
        </style>

      form
        <input type="text" v-model="text">
        ต้องประกาศตัวแปร(v-model)ไว้ใน script ด้วย
        data() {
          return {
            text: ''
          }
        }

# Event & Lifecycle
    methods
      syntax in script tag
        methods: {
          //function
        }
      ex. 
        methods: {
          save() {
            console.log('save)
          }
        }
      how to use
        <tag @click="functionName"></tag>
          - @ + event ==> @click, @change, ...

        ex. <button @click="save">Save</button>

      how to use function in function
        methods: {
          save() {
            console.log('save')
          }
          save2() {
            this.save()
            //this.สิ่งที่จะอ้างถึง ในตัวอย่างจะอ้างถึง function
          }
          }
    
    computed
      - จริงๆแล้วใช้งานคล้ายกับ data เลยแต่สิ่งที่ต่างออกไปคือ เมื่อตัวแปรใดๆใน computed นั้นเปลี่ยน computed นั้นจะ trigger และทำงานใหม่อีกครั้ง เช่น อยากให้ dropdown เปลี่ยนแปลงค่าตาม value ที่เลือก computed ก็สามารถเข้าไปจัดการตรงส่วนนั้นได้
      syntax in script
        computed: {
          //function
        }

      ex.
        computed: {
          sortItems() {
            return this.todos.sort((a,b) => {b.time - a.time})
          }
        }

    Lifecycle 
      1. create => เข้า state นี้เมื่อ initial แต่ยังไม่ render
      2. mounted => เข้า state นี้เมื่อ render แล้ว
      3. updated => เข้า state นี้เมื่อ data เกิดการอัพเดท
      4. destroy => เมื่อตัวมันถูกทำลายหรือถูกถอด vue ออกจาก component
      
      รู้ lifecycle เพื่อเข้าไปจัดการ state ต่างๆของ vue ได้เช่นเมื่อ create ให้ทำสิ่งนี้

      ตัวอย่างคำสั่งเกี่ยวกับ lifecycle
      - before + (create/mounted/updated/destroy)
      ex. 
        beforeCreate() {
          console.log('before create')
        }
      - create(), mounted() เปรียบเสมือน onload ใน js, updated(), destroy()
      ex.
        mounted() {
          console.log('mounted')
        }

    - watcher
      ไว้ติดตามการเปลี่ยนแปลงของตัวแปรบางอย่าง
      syntax 
        watcher: {
          variableName (oldValue, newValue) {
            //function
          }
        }
      แต่การใช้ watcher ต้องระวังเพราะเนื่องจากกิน performance มากๆจึงไม่ควรใช้เยอะ ใช้ computed, methods อื่นๆดีกว่าถ้าใช้ได้

# Vue Multiple Components
    props
    เป็น one way down แปลว่าค่าที่ส่งเข้ามาจะไม่สามารถเปลี่ยนแปลงได้ แก้ไขก็ไม่ส่งผลถึงข้างบนที่ส่งมา
    ex. 
      (หน้าที่จะส่ง props มา)
      <todoList :todoItems="todoItems"></todoList>
      todoItems คือ ตัวแปรในหน้าที่ส่ง props ไปและจะต้อง bind(:) props ก่อนส่งไปด้วยไม่งั้นมันจะเข้าใจว่าเป็น string หรือ text ธรรมดา

      (หน้าที่รับ props)
      <s>
        export default {
          name: 'todoList',
          // ส่วนที่รับ props
          // props: ['todoList'], ==> สามารถเขียนย่อแบบนี้ได้
          props: {
            todoItems: {
              type: Array // บ่งบอกว่าส่งมาเป็นอะไร
            }
          },
          mounted() {
            console.log(this.todoItems) // วิธีใช้งาน props 
          }
        }
      </script>
    
    props validation
      ถ้าส่ง props ไม่ผ่านจะส่งออกมาที่ console ให้ดู
      props: {
          todoItems: {
            type: [Array, Number] // เป็น array และ number แต่ arg ที่ส่งลงไปต้องเป็น array เท่านั้น
          }
          //default type
          todoItems: {
            type: Array,
            default: [] // ถ้ามีค่าเป็น array ถ้าไม่มีเป็น array ว่างๆ, สามารถเขียนเป็น function ได้ เช่น
              default: function (val) {
                return 'a' + 'b'
              }
          }

          //custom validate 
          todoItems: {
            type: Array,
            validator: function(params) {
              return ['a','b'].includes(params)
            }
          }
        },
    
    custom event
      ต้องการส่งสัญญาณไปหา component ที่ส่ง props เข้ามาว่าต้องการเปลี่ยนแปลงค่านะ เลยต้องใช้ custom event ในการจัดการ

      ex.
        component ข้างใน (ตัวรับ props)
        <template>
          <div>
            <input type="text" v-model="text" />
            <button @click="save()" >Save</button>
          </div>
        </template>

        <s>
          export default {
            data() {
              return {
                text: null
              }
            }
          },
          methods: {
            save() {
              this.$emit('eventName ที่จะส่ง', variable/value ที่ต้องการส่งออกมา)
              this.$emit('save', this.text)
              // ตอนที่มัน save ให้มัน emit event ออกมา
            }
          }
        </s>

        component ข้างนอก (ตัวส่ง props)
        <template>
          <div>
            <todoList></todoList>
            <InputItem @save="addTodoItem"></InputItem>
            // เรียกใช้ function ที่ emit ไว้ด้วย @ + <funtionName ที่ emit> ตามด้วย = และ funtion ที่จะใช้งาน เช่น @save="addTodoItem"
          </div>
        </template>

        <script>
          export default {
            name: 'Page',
            methods: {
              addTodoItem (text) {
                this.todoItems.push({
                  text,
                  time: Date.now(),
                  completed: false
                })
              }
            }
          }
        </script>

    slot
      slot component เป็นการสร้างกรอบขึ้นมากรอบนึงใหญ่ๆ
      โดยให้สร้างเป็น component แยกออกมาก่อน

      <template>
        <div class="alert">
          <slot name="header"></slot>
          <slot name="text"></slot>
        </div>
      </template>

      <script>
        export default {
          name: 'Alert'
        }
      </script>

      <style>
        .alert {
          border: 1px solid red;
          padding: 10px;
        }
      </style>

      หน้าที่เอาไปใช้ก็ import component มาปกติ และใช้แบบนี้
      <template>
        <div>
          <Alert>
            <h1 slot="header">Alert</h1>
            <p slot="text">text here</p>
          </Alert>
        </div>
      </template>

    Using multiple components
      - แยกไฟล์ของแต่ component ออกจากกันก่อน
      - กำหนด name กับ ชื่อไฟล์ก็จะกันสับสนได้
      - tag ที่ใช้กับ name ที่ export มาต้องตรงกัน
      - import เข้ามา 
      - export ใน 
          components: {
            componentName,
          } 
    
    Mixins (.js เท่านั้น)
      - คล้ายๆ class ของ js เพราะ vue ไม่สามารถเขียน class แบบปกติได้จึงเอา mixins มาช่วยจัดการ
      - ถ้าเกิดว่าเอา mixins ไปใช้ใน component จะเอามารวมกันแต่ถ้ามี methods ที่ชื่อซ้ำกัน จะเลือกของ component จะไม่ใช้ของ mixins
      - แต่ถ้าเกิดว่าเป็น lifecycle hook ของ mixins จะถูกเรียกก่อน lifecycle ของ component นั้นๆ เช่น create ของ mixins และ component => ของ mixins จะถูกเรียกก่อน
      - วิธีใช้ import เข้ามา
        import firstMixins from '../Mixins/firstMixins
        <script>
          export default {
            name: 'Main',
            mixins: [firstMixins], [secondMixins]
          }
        </script>
  
# Vue Router

    Single Page Application (SPA)
      - ทุกๆอย่างทำงานใน index หน้าเดียวแต่ router เป็นตัวบ่งบอกว่า ถ้าเปลี่ยน url เป็นอันนี้ให้เอา component นั้นมาใช้ในพื้นที่ที่จองเอาไว้ เช่น path /home = component home

    Using vues router
      - import component ที่จะใช้เข้ามา
      - syntax
        export default {
          routes: [
            {
              path: '/pathName'
              (ถ้ามี params ก็ใส่ต่อได้เลย /pathName/:id)
              name: 'componentName' //กำหนดให้ชัดเจน
              component: componentName
            }
          ]
        }

      ในหน้าที่เอา params ไปใช้จะเขียนแบบนี้
        <script>
          export default {
            name: 'Product',
            mounted() {
              console.log(this.$route.params.id)
              // เอาค่า params ที่ส่งมาไปใช้, id คือชื่อ params ที่เรากำหนดตอนจะส่งมา
            }
          }
        </script> 

    Defining Route & Dynamic route
      history api === <router-link to="/product">product</router-link> แต่ไม่ค่อยโอเคเท่าไหร่ให้เขียนแบบนี้ bind(:) เข้าไปและส่งเป็น object, define เป็น name ไว้ทำให้เวลาเปลี่ยน path ไม่ต้องมาเปลี่ยนที่ route อีกเพราะเราใช้ชื่อในการเข้าถึง

      <router-link :to="{name:'product', params:{id:1}">Product</router-link>

    .push() , .go()
      <script>
        export default {
          mounted() {
            // function ของ router ในการเปลี่ยนหน้า
            this.$router.push({name: 'product'})

            //ย้อนหลังไป 1 หน้า
            this.$router.go(-1)
            //ไปข้างหน้า 1 หน้า 
            this.$router.go(1)  
          }
        }
      </script>

  # Vuex

    store management (น่าจะคล้ายๆ useContext)

    Vuex Store  
      syntax  
        import Vue from 'vue'
        import Vuex from 'vuex'

        Vue.use(Vuex)

        export default new Vuex.Store({
          state: {
            //ตัวแปรที่เราจะใช้ ว่านี่คือตัวแปรที่เราจะใช้ร่วมกัน ใครคนนึงเปลี่ยนทุกคนเปลี่ยน
          },
          mutations: {
            //ไว้สร้าง function สำหรับเปลี่ยนแปลงข้อมูล
          },
          actions: {
            //ไม่จำเป็นต้องใช้ก็ได้ จะใช้เมื่อมีการเรียกใช้ mutations ตัวแปร 2 ตัว 3 ตัวก็ให้ใส่ action ครอบไว้ 
          },
          getters: {
            //ไม่จำเป็นต้องมีก็ได้ แต่ไว้เรียกใช้ตัว state ได้, คืนตัวแปรใน state ออกไปและเปลี่ยนแปลงค่านิดหน่อย
          }

          ex.
          state: {
            itemCount: 0,
            items: []
          },
          mutations: {
            changeCount (state, count) {
              state.itemCount = count
            },
            addItem (state, item) {
              state.items.push(item)
            }
          },
          actions: {
            addTodo ({ commit, state}, item) {
              //commit('mutationsName', item)
              commit('addItem', item)
              commit('changeCount', state.items.length)
            }
          },
          getters: {
            countText (state) {
              return 'Items' + state.count
            }
          }
        })
      
      - import store ไปที่หน้า main ด้วย
      - actions, mutations เหมือนเป็น function ขารับ
      - getters เหมือนเป็น function ขาออก

    State & Mutation Mapping
      - import { mapState,  mapMutations, mapActions, mapGetters } from vuex

      - map เอาไว้เปลี่ยน store ให้เป็นส่วนๆนึงของ component 
        - mutations, actions จะ map เป็น methods
        - state, getters จะ map เป็น computed

      <script>
        export default {
          name: 'home',
          mounted() {
            //วิธีใช้จากการ map
            this.changeCount() // mutations
            this.addTodo() // actions
            this.count // state
          },
          methods: {
            ...mapMutations(['changeCount', 'addItem'])
            ...mapActions(['addTodo'])
            //ใส่ ... (spread operator) เพราะว่าบ่งบอกให้เอา function ที่ map มา, merge รวมกับของที่มีอยู่่
          },
          computed: {
            ...mapState(['count'])
          },
          components: {
            HelloWorld
          }
        }
      </script>
    
    Anoter way to Map
      <script>
        export default {
          name: 'home',
          mounted() {
            this.$store.commit('changeCount', 1) // map mutations
            this.$store.dispatch('addItem', {}) // map actions
          },
          methods: {

          },
          computed: {
            ...mapState(['count'])
            // code บนกับล่างมีผลเหมือนกัน
            count() {
              return this.$store.state.count
            }
          },
          components: {
            HelloWorld
          }
        }
      </script>

# Building Todo App

    import TodoList from '@/components/TodoList'
      - สัญลักษณ์ @ จะแทนว่าเป็น folder src

    Step การเอา component ไปใช้ในหน้าหลัก
      - สร้าง component แยกออกมาก่อน
      - import เข้าไปในหน้าที่จะใช้
      - เช็คดูว่า component ที่จะใช้ต้องส่งตัวแปรอะไรมาบ้าง

# Vue 3

    - เขียนด้วย typeScript
    - Global treeshaking => คอย detect v-if v-for  v-model ถ้า build แล้วจะไม่โหลดพวกนี้มา
    - ไม่ต้องใช้ this.$set(this.objectVal, 'main', 2) ==> this.objectVal.main = 2 ได้เลย
    - ใส่ v-model ได้หลายตัวใน form ตัวเดียว
    - fragment มี parent component ได้หลายตัว
    - composition API
    - suspense ==> auto detect ว่า component นั้นโหลดเสร็จรึยัง Lazy reload, เอา display ไหนมาแสดงก่อนถ้าโหลดไม่เสร็จได้

    Composition API
      - ปกติการเอา component ไป reuse จะใช้ mixins แต่ยังก็ใช้งานได้ไม่สมบูรณ์ เลยเกิด composition API
      - method:, computed:, data() {return {}}, watch:, จะถูกรวมเข้าไปใน setup() { return {}} ทั้งหมด
        ex.
          - การ return ตัวแปรใน data() ทำได้สองวิธีคือ 1. ref 2. reactive
          
          import { ref, reactive } from 'vue'
          
          export default {
            setup (props) {
              let count = ref(0) // เหมือน data() { return { count: 0 } }
              let todolist = reactive([])
              return {
                // อะไรที่จะใช้ใน template ต้อง return ออกไปด้วย
                count, 
                todolist
              }
            }
          }

      ref vs reactive
        - ความสามารถพอๆกัน
        - ref ควรใช้กับตัวแปรแบบเดี่ยว (count: 0, username: 'abc')
        - reactive ควรใช้กับ object, array (object ใหญ่ๆ)
        - access ค่าของ ref ใช้โดย count.value (ref ต้องตามด้วย .value เสมอ)
        - access ค่าของ reactive ใช้โดย todolist  

      การเขียน methods
        - เขียนเป็น function javascript ปกติใน setup ได้เลย
          ex. 
            setup () {
              function addTodoItem() {
                return true
              },
              const addTodoItem = function() {
                return true
              }

              return {
                addTodoItem
              }
            }
      
        การเขียน computed
          ex.
            import { computed } from 'vue'

            setup () {
              const sortItems = computed(() => {
                return todoItem.sort()
              })

              return {
                sortItems
              }
            }

        watchEffect 
          - ทำงานคล้าย computed แต่ไม่จำเป็นต้อง return ตัวแปรออกไปแต่เมื่อมีคัวแปรที่อยู่ใน watchEffect เปลี่ยน ก็จะทำงานทันที
          ex. 
          watchEffect(() => {
            count.value = todoItem.length
          })

        การเขียน watch 
          - เขียนใน setup() ได้เลย
            ex. 
            import { watch } from 'vue'

            watch for ref
              watch(varibleName, (val, prevVal) => {

              })
            watch for reactive
              watch(() => todoItem.count, (val, prevVal) => {

              })

        lifecycle
          - on + Lifecycle ==> onMounted, onUpdated แต่ beforeCreate, create จะถูกตัดออกไป
          ex. 
            import { onMounted } from 'vue'
            setup() {
              onMounted(() => {
                console.log('Hello')
              })
            }

        how to reuse
          - สร้าง file ขึ้นมา file นึงสำหรับใช้ของที่จะ use
            ex. file state.js

            import { ref, reactive, onMounted } from 'vue'

            export function useStates () {
              const todoItem = reactive({ count: 0 })
              const count = ref(1)

              onMounted(() => {
                console.log('Hello')
              })

              return {
                todoItem,
                count
              }
            }

          - component ที่จะใช้ import เข้ามา
            ex.
            import { useStates } from '@/state'

            setup() {
              const { todoItem, count } = useStates
            }

        ex. change Options API to Composition API
          import { reactive, computed } from 'vue'

          export default {
            setup () {
              const todoItem = reactive([
                {
                  name: 'a',
                  age: 30
                },
                {
                  name: 'b',
                  age: 24
                }
              ])

              const sortItems = computed(() => {
                return todoItem.sort((a,b) => {b.time - a.time})
              })

              const addTodoItem = (text) => {
                todoItem.push({
                  text,
                  completed: 'false',
                  time: Date.now()
                })
              }

              return {
                todoItem,
                sortItems,
                addTodoItem
              }
            }
          }

# Setting up Vue 3
    vue create projectName => vue3

    ย้าย vue 2 to vue 3
      - upgrade vue cli
        command: vue upgrade --next ==> yes
      - upgrade plugin, vue (expect vue router)
        command: vue add vue-next (in folder vue)
      - upgrade vue router
        command: vue add router@next

    composition in vue 2
      npm @vue/composition-api

      import Vue from 'vue'
      import VueCompositionAPI from '@vue/composition-api'

      Vue.use(VueCompositionAPI)

      import { reactive, computed } from '@vue/composition-api'

    context.root === this
      ex.
        export default {
          setup (props, context) {
            context.root.store
          }
          หรือ
          setup (props, {root}) {
            root.store // this.store
          }
        }

    vue router 4
      ex.
        import { useRouter, useRoute } from 'vue-router'
        import { useStore } from 'vuex'

        export default {
          setup (props, context) {
            const route = useRoute()
            const router = useRouter()

            const store = useStore()

            store.state

            store.dispatch
          }
        }
