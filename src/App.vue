<template>
  <TodoList
  :completedTodoList = 'completedTodoList'
  :todoList = 'todoList'
  @addTodo = 'addTodo'
  @input = 'inp'
  @complet = 'compl'
  @redactEl = 'redactEl'
  @deleteEl = 'deleteEl'
  @complAndMove = 'complAndMove'
  :newTodo = 'newTodo'
  :btns = 'btns'
  />
  <selector 
    :translatedArr='translatedArr'
    @translateFunc='translateFunc'
  />
  <!-- <div>{{btns}}</div> -->
  
  <button @click = 'translateFunc(translatedArr, "En")'>Перевод на английский</button>
  <button @click = 'translateFunc(translatedArr, "Ру")'>Перевод на русский</button>
  <button @click = 'translateFunc(translatedArr, "Алб")'>Перевод на Албанский</button>
</template>
<script>
  import { ref } from 'vue'
  import TodoList from './components/TodoList.vue'
  import selector from './components/selector.vue'

  export default {
    name: 'App',
    components: {
      TodoList,
      selector,
    },
    setup()
    {
      const newTodo = ref('')
      const completedTodoList = ref([])
      let btns = ref([])
      const translatedArr = ref(
      [
        {
          lang: 'Ру',
          btns:
          {
            btnCompl: 'Выполнен',
            btnRedact: 'Редактировать задачу'
          }
        },
        {
          lang: 'En',
          btns:
          {
            btnCompl: 'Completed',
            btnRedact: 'Redact'
          }
        },
        {
          lang: 'Алб',
          btns:
          {
            btnCompl: 'Алб Completed',
            btnRedact: 'Алб Redact'
          }
        },
      ])
      const todoList = ref(
      [
        {
          id: 1,
          name: 'Заполнить банки водой',
          completed: false,
        },
        {
          id: 2,
          name: 'Поспать пару часов',
          completed: false,
        },
        {
          id: 3,
          name: 'Пойти на тренировки',
          completed: false,
        }
      ])
      const addTodo = ()=>
      {
        todoList.value.push(
        {
          id: todoList.value.length + 1,
          name: newTodo.value,
          completed: false
        })
        newTodo.value = '';
      }
      const inp = (val)=>
      {
        newTodo.value = val
      }
      const compl = (el)=>
      {
        el.completed = !el.completed
      }
      const redactEl = (el)=>
      {
        el.name = newTodo.value
        newTodo.value = ''
      }
      const deleteEl = (idx)=>
      {
        todoList.value.splice(idx,1)
      }
      const complAndMove = ()=>
      {
        completedTodoList.value = todoList.value.filter((el)=>
        {
          return el.completed === true
        })
      }
      const translateFunc = (arr, lang)=>
      {
        let inArr = []
        arr.forEach((el)=>
        {
          inArr.push(el)
        })
        btns.value = inArr.find(el => el.lang === lang)
      }
      translateFunc(translatedArr.value, 'Ру')
      
      // onMounted(()=>
      // {
      //   translateFunc(translatedArr.value, 'Ру')
      //   // console.log('ss',btns)
      // })
      return {
        newTodo,
        completedTodoList,
        todoList,
        addTodo,
        inp,
        compl,
        redactEl,
        deleteEl,
        complAndMove,
        translateFunc,
        translatedArr,
        btns,
      }
    }
  }
</script>

<style>
  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    color: #2c3e50;
    margin-top: 60px;
  }
</style>
