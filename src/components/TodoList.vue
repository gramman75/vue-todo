<template>
     <v-list-item >
        <template>
            <v-list-item-content>
            <v-list-item-title v-text="todo.title"></v-list-item-title>
            </v-list-item-content>

            <v-list-item-action>
            <v-checkbox color="deep-purple accent-4"
            ></v-checkbox>
            </v-list-item-action>
        </template>
    </v-list-item>

</template>

<script setup lang="ts">

import {defineProps, defineEmits, PropType, computed, ref} from 'vue';
import Todo from  '@/models/Todo';
import TodoInputVue from './TodoInput.vue';


// const completeClass = ref<string>("")

const emit = defineEmits<{
    (e: 'removeTodo', index: number): void,
    (e: 'updateTodo', index: number): void
}>()

const props = defineProps({
    todo : {type: Object as PropType<Todo>, required: true},
    index : {type: Number, required: true}
});

function removeItem(index: number){
    emit("removeTodo", index);
    console.log(index);
}

function completed() {
    /**
     * method안에서 prop 사용방법
     */
    // completeClass.value = completeClass.value == 'completed' ? '' : 'completed';
    emit("updateTodo", props.index);
}

/**
 * class를 computed와 object객체를 이용하여 적용.
 */
const completeClass = computed(() => ({'completed' : props.todo.done}))



</script>

<style scoped>

.completed {
    text-decoration: line-through;
}

</style>