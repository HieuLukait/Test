<template>
  <q-page class="bg-grey column">
    <div class="row q-pa-row bg-primary">
      <q-input
        bg-color="white"
        @keyup.enter="addtask"
        class="col"
        square
        filled
        v-model="newtask"
        placeholder="Add interesting"
        dense
      >
        <template v-slot:append>
          <q-btn @click="addtask" round dense flat icon="add" />
        </template>
      </q-input>
    </div>
    <q-list class="bg-white" bordered separator>
      <q-item
        v-for="(task, index) in tasks"
        :key="task"
        v-ripple
        @click="task.done = !task.done"
        :class="{ 'done bg-red-2 ': task.done }"
        clickable
      >
        <q-item-section avatar>
          <q-checkbox
            v-model="task.done"
            :color="primary"
            class="no-pointer-event"
          />
        </q-item-section>
        <q-item-section>
          <q-item-label>{{ task.title }}</q-item-label>
        </q-item-section>
        <q-item-section v-if="task.done" side>
          <q-btn
            flat
            round
            dense
            color="primary"
            icon="delete"
            @click.stop="deleteTask(index)"
          />
        </q-item-section>
      </q-item>
    </q-list>
  </q-page>
</template>

<script>
import { defineComponent } from "vue";

export default defineComponent({
  name: "IndexPage",
  data() {
    return {
      newtask: "",
      tasks: [
        {
          title: "home",
          done: false,
        },
        {
          title: "gaming",
          done: false,
        },
        {
          title: "soccer",
          done: false,
        },
        {
          title: "cinema",
          done: false,
        },
      ],
    };
  },
  methods: {
    deleteTask(index) {
      $q.dialog({
        title: "Confirm",
        message: "Xóa ư ?",
        cancel: true,
        persistent: true,
      }).onOk(() => {
        this.tasks.splice(index, 1);
        this.$q.notify("Task delete");
      });
    },
  },
  addtask() {
    this.tasks.push({
      title: this.newtask,
      done: false,
    });
    this.newtask = "";
  },
});
</script>
<style lang="scss">
.done {
  .q-item__label {
    text-decoration: line-through;
  }
}
.col {
  border-color: light-green-13;
}
.col:hover {
  background-color: yellow;
}
</style>
