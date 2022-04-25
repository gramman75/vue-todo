<template>
    <v-container>
        <v-row>
            <v-col offset=2 />
            <v-col :cols=6>
                <v-text-field 
                    label="할일"
                    @input="changeText"
                />                
            </v-col>
            <v-col :cols=2>
                <v-btn depressed color="primary" @click="addTodo"> Save</v-btn>
            </v-col>
            <v-col offset=2 />
        </v-row>
        <v-row>
            <v-col offset=2 />
            <v-col cols="8">
                <v-alert v-show="showAlert" dense type="info" >Input todo</v-alert>
            </v-col>
            <v-col offset="2" />
        </v-row>
    </v-container>
</template>

<script setup lang="ts">

import { isTemplateNode } from "@vue/compiler-core";
import _ from "lodash";
import { defineEmits, defineProps, computed } from "vue";

// type-based
const emit = defineEmits<{
  (e: 'in', id: string): void,
  (e: 'add'): void
}>()

const props = defineProps({
    item : {type: String, required: true}
})

const showAlert = computed(() => _.isEmpty(props.item) ? true : false);

function changeText(event: Event) {
    let target = event.target as HTMLInputElement;
    emit("in", target.value);
}

function addTodo() {
    emit("add");
}

</script>

<style scoped>

</style>