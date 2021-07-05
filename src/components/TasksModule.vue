<template>
  <div class="task-module">
    <div class="card" v-for="(item, i) in tasks" :key="i">
      <p class="card-state">{{ item.state }}</p>
      <task-card
        v-for="(task, index) in item.taskCards"
        :key="index"
        :task="task"
        :item="item"
        @handleRemoveTask="handleRemoveTask"
      />
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import TaskCard from "./TaskCard.vue";

@Component({
  name: "Tasks",
  components: {
    TaskCard,
  },
})
export default class TasksModule extends Vue {
  tasks: any = [
    {
      id: 1,
      state: "new order",
      taskCards: [
        {
          id: 1,
          status: "new order",
          hours: "20",
          price: "25",
          remainingDays: 5,
        },
        {
          id: 2,
          status: "new order",
          hours: "20",
          price: "25",
          remainingDays: 4,
        },
      ],
    },
    {
      id: 2,
      state: "in progress",
      taskCards: [
        {
          id: 1,
          status: "in progress",
          hours: "20",
          price: "25",
          remainingDays: 5,
          username: 'John',
          progress: "20",
        },
      ],
    },
    {
      id: 3,
      state: "waiting for buyer",
      taskCards: [
        {
          id: 1,
          status: "delivered",
          hours: "20",
          price: "25",
          remainingDays: 5,
          progress: "20",
        },
      ],
    },
    {
      id: 4,
      state: "completed",
      taskCards: [
        {
          id: 1,
          status: "completed",
          hours: "20",
          price: "25",
          remainingDays: 5,
        },
        {
          id: 2,
          status: "completed",
          hours: "20",
          price: "25",
          remainingDays: 2,
        },
        {
          id: 3,
          status: "completed",
          hours: "20",
          price: "25",
          remainingDays: 5,
        },
      ],
    },
  ];

  handleRemoveTask(taskID: any, cardID: any): any {
    console.log({taskID, cardID})
    const columnIndex = this.tasks.findIndex(
      (column: any) => column.id == taskID
    );
    const cardIndex = this.tasks[columnIndex].taskCards.findIndex(
      (card: any) => card.id == cardID
    );
    this.tasks[columnIndex].taskCards.splice(cardIndex, 1);
  }
}
</script>

<style scoped lang="scss">
.task-module {
  display: flex;
  overflow-x: auto;
  padding: 1rem;
  .card {
    width: 24%;
    background-color: #e7e7e7;
    margin: 0.5rem;
    border-radius: 4px;
    text-align: left;
    padding: 0.8rem;
    min-width: 230px;

    .card-state {
      font-size: 1rem;
      line-height: 1rem;
      text-transform: uppercase;
      font-weight: 600;
      color: #847f7f;
      margin-top: 0.8rem;
      letter-spacing: 0.02rem;
    }
  }
}
</style>
