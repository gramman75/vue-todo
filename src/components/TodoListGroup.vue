<template>
  <v-card
    class="mx-auto"
    max-width="500"
  >
    <v-list shaped>
      <v-list-item-group
        multiple
      >
        <template v-for="(item, index) in todoList">
          <v-list-item
            :value="item.title"
            active-class="deep-purple--text text--accent-4"
          >
            <template>
              <v-list-item-content>
                <v-list-item-title v-text="item.title"></v-list-item-title>
              </v-list-item-content>

              <v-list-item-action>
                <v-checkbox
                  color="deep-purple accent-4"
                ></v-checkbox>
              </v-list-item-action>
            </template>
          </v-list-item>
        </template>
      </v-list-item-group>
    </v-list>
  </v-card>
</template>

<script setup lang="ts">
import Todo from '@/models/Todo';
import { defineProps, PropType } from 'vue';

const props = defineProps({
    todoList : {type : Array() as PropType<Array<Todo>>, required: true}

});

</script>

<style scoped>

</style>