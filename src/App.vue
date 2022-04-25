<template>
    <h1>Todo Vue-Typescript</h1>
    
    <div>
        <TodoInput :item="todoText" @in="updateTodoText" @add="saveTodo"/>
       
        <TodoList v-for="(todo, index) in todoItems" 
            :key="index" 
            :index="index" 
            :todo="todo"
            @removeTodo="removeTodo"
            @updateTodo="updateTodo"
            /> 

    </div>
</template>

<script setup lang="ts">
import { ref, computed, onMounted } from 'vue';
import TodoInput from './components/TodoInput.vue';
import TodoList from './components/TodoList.vue';
import * as _ from "lodash";
import Todo from './models/Todo';


const LOCAL_STORAGE_KEY = 'V1';

const todoText   = ref<string>("")
const todoItems = ref<Array<Todo>>([]);

function updateTodo(index: number) {
    debugger;
    let todo: Todo | undefined = todoItems.value.at(index);
    if (todo) {
        todo.done = !todo.done
        saveLocalstorage();
    }
}
function fetchTodo() : Array<Todo> {
    let todos : string = localStorage.getItem(LOCAL_STORAGE_KEY) || '[]';
    return JSON.parse(todos); 
    // todoItems.value = JSON.parse(todos);
    // sortTodo(); 
}

function updateTodoText(value: string){
    todoText.value = value;
}

function saveTodo(){
    debugger;
    // localStorage.setItem(todoText.value, todoText.value);
    // let todos = localStorage.getItem(LOCAL_STORAGE_KEY) || '[]';
    // let todoJson : Array<any> = JSON.parse(todos);
    // todoJson.push(todoText.value);
    // todoItems.value = todoJson;
    let todo : Todo = {
        title: todoText.value,
        done : false
    };

    todoItems.value.push(todo);
    sortTodo();
    saveLocalstorage();
    todoText.value = "";
}

function saveLocalstorage() : void{
    localStorage.setItem(LOCAL_STORAGE_KEY, JSON.stringify(todoItems.value));
}

function sortTodo(): void{
    todoItems.value = _.orderBy(todoItems.value, ['title'],['asc']);
}

function removeTodo(index: number){
    // let inx = index;
    _.remove(todoItems.value, (n, i) =>{
        return i == index 
    });

    saveLocalstorage();
}

onMounted(()=>{
    todoItems.value =  fetchTodo();
})

</script>

<style scoped>

</style>