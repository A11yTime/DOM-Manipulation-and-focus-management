<template>
  <div id="app">
    <h1 id="list-summary" ref="listSummary" tabindex="-1">{{ listSummary }}</h1>
    <to-do-form
    @todo-added="addToDo">

    </to-do-form>
    <div role="group" aria-labelledby="list-summary" >
      <ul class="stack-large">
      <li v-for="item in ToDoItems" :key="item.id">
        <to-do-item 
          :label="item.label" 
          :done="item.done"
          :id="item.id" 
          :name="item.name"
          @checkbox-changed="updateDoneStatus(item.id)"
          @item-deleted="deleteToDo(item.id)"
          @item-edited="editToDo(item.id, $event)">
        </to-do-item>
      </li>
    </ul>
  </div>
  </div>
</template>

<script>
import ToDoForm from './components/ToDoForm.vue'
import ToDoItem from './components/ToDoItem.vue'
import uniqueId from "lodash.uniqueid";

export default {
  name: 'App',
  components: {
    ToDoItem, ToDoForm
  },
  data() {
    return {
      ToDoItems: [
        { id: uniqueId("todo-"), label: "Learn Vue", done: false, name: "attribute_selection"},
        {
          id: uniqueId("todo-"),
          label: "Create a Vue project with the CLI",
          done: true, name: "attribute_selection"
        },
        { id: uniqueId("todo-"), label: "Have fun", done: false, name: "attribute_selection" },
        { id: uniqueId("todo-"), label: "Create a to-do list", done: false, name: "attribute_selection" },
      ],
    };
  },
  methods: {
    addToDo(todoLabel){
      this.ToDoItems.push({id:uniqueId('todo-'), label: todoLabel, done: false, name: "attribute_selection"})
    },
    updateDoneStatus(toDoId) {
       const todoUpdate = this.ToDoItems.find((item) => item.id === toDoId)
       todoUpdate.done = !todoUpdate.done
    },
    deleteToDo(toDoId) {
     const itemIndex = this.ToDoItems.findIndex((item) => item.id === toDoId)
     this.ToDoItems.splice(itemIndex, 1)
     this.$refs.listSummary.focus()
    },
    editToDo(toDoId, newLabel){
      const toDoEdit = this.ToDoItems.find((item) => item.id === toDoId)
      toDoEdit.label = newLabel
    }
  },
  computed: {
    listSummary () {
      const numberFinishedItems = this.ToDoItems.filter((item) => item.done).length
      return `${numberFinishedItems} out of ${this.ToDoItems.length} items completed`
    }
  }
}
</script>

<style>
  /* Global styles */
  .btn {
    padding: 0.8rem 1rem 0.7rem;
    border: 0.2rem solid #4d4d4d;
    cursor: pointer;
    text-transform: capitalize;
  }
  .btn__danger {
    color: #fff;
    background-color: #ca3c3c;
    border-color: #bd2130;
  }
  .btn__filter {
    border-color: lightgrey;
  }
  .btn__danger:focus {
    outline-color: #c82333;
  }
  .btn__primary {
    color: #fff;
    background-color: #000;
  }
  .btn-group {
    display: flex;
    justify-content: space-between;
  }
  .btn-group > * {
    flex: 1 1 auto;
  }
  .btn-group > * + * {
    margin-left: 0.8rem;
  }
  .label-wrapper {
    margin: 0;
    flex: 0 0 100%;
    text-align: center;
  }
  [class*="__lg"] {
    display: inline-block;
    width: 100%;
    font-size: 1.9rem;
  }
  [class*="__lg"]:not(:last-child) {
    margin-bottom: 1rem;
  }
  @media screen and (min-width: 620px) {
    [class*="__lg"] {
      font-size: 2.4rem;
    }
  }
  .visually-hidden {
    position: absolute;
    height: 1px;
    width: 1px;
    overflow: hidden;
    clip: rect(1px 1px 1px 1px);
    clip: rect(1px, 1px, 1px, 1px);
    clip-path: rect(1px, 1px, 1px, 1px);
    white-space: nowrap;
  }
  [class*="stack"] > * {
    margin-top: 0;
    margin-bottom: 0;
  }
  .stack-small > * + * {
    margin-top: 1.25rem;
  }
  .stack-large > * + * {
    margin-top: 2.5rem;
  }
  @media screen and (min-width: 550px) {
    .stack-small > * + * {
      margin-top: 1.4rem;
    }
    .stack-large > * + * {
      margin-top: 2.8rem;
    }
  }
  /* End global styles */
  #app {
    background: #fff;
    margin: 2rem 0 4rem 0;
    padding: 1rem;
    padding-top: 0;
    position: relative;
    box-shadow:
      0 2px 4px 0 rgb(0 0 0 / 20%),
      0 2.5rem 5rem 0 rgb(0 0 0 / 10%);
  }
  @media screen and (min-width: 550px) {
    #app {
      padding: 4rem;
    }
  }
  #app > * {
    max-width: 50rem;
    margin-left: auto;
    margin-right: auto;
  }
  #app > form {
    max-width: 100%;
  }
  #app h1 {
    display: block;
    min-width: 100%;
    width: 100%;
    text-align: center;
    margin: 0;
    margin-bottom: 1rem;
  }
</style>


