<template>
  <div class="todo-list">
    <h2>Ma Todo List</h2>
    <form @submit.prevent="addTask" class="task-form">
      <input v-model="newTaskTitle" placeholder="Titre de la tâche" class="input-title" />
      <textarea v-model="newTaskDescription" placeholder="Description de la tâche" class="input-description"></textarea>
      <button type="submit" class="btn-add">Ajouter une tâche</button>
    </form>

    <ul class="task-list">
      <li v-for="(task, index) in tasks" :key="index" :class="{'completed': task.completed}" class="task-item">
        <input 
          type="checkbox" 
          v-model="task.completed" 
          class="checkbox" 
        />
        <div class="task-content">
          <h3 class="task-title">{{ task.title }}</h3>
          <p class="task-description">{{ task.description }}</p>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newTaskTitle: '',
      newTaskDescription: '',
      tasks: []
    };
  },
  methods: {
    addTask() {
      if (this.newTaskTitle.trim() && this.newTaskDescription.trim()) {
        this.tasks.push({
          title: this.newTaskTitle,
          description: this.newTaskDescription,
          completed: false
        });
        this.newTaskTitle = '';
        this.newTaskDescription = '';
      }
    }
  }
};
</script>

<style scoped>
.todo-list {
  max-width: 600px;
  margin: auto;
  padding: 20px;
  background-color: #f9f9f9;
  border-radius: 8px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
}

h2 {
  text-align: center;
  color: #333;
}

.task-form {
  margin-bottom: 20px;
}

.input-title,
.input-description {
  width: calc(100% - 20px);
  padding: 10px;
  margin: 10px 0;
  border: 1px solid #ddd;
  border-radius: 4px;
  box-sizing: border-box;
}

.input-title {
  font-size: 1.2em;
}

.input-description {
  height: 100px;
}

.btn-add {
  width: 100%;
  padding: 10px;
  border: none;
  background-color: #007bff;
  color: white;
  font-size: 1em;
  border-radius: 4px;
  cursor: pointer;
}

.btn-add:hover {
  background-color: #0056b3;
}

.task-list {
  list-style-type: none;
  padding: 0;
}

.task-item {
  padding: 15px;
  margin-bottom: 10px;
  background-color: #fff;
  border-radius: 4px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  display: flex;
  align-items: center;
}

.task-item.completed {
  background-color: #e0e0e0;
  text-decoration: line-through;
}

.checkbox {
  margin-right: 15px;
}

.task-content {
  flex: 1;
}

.task-title {
  font-size: 1.2em;
  margin: 0;
}

.task-description {
  margin: 5px 0 0;
}
</style>
