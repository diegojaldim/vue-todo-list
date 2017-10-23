<template>

  <b-container>
    <b-row>

      <b-col col sm="12">
        <h1>{{title}}</h1>
      </b-col>

      <b-col col sm="12">
        <div>
          <b-input-group>
            <b-form-input type="text" v-model="task"></b-form-input>
            <b-input-group-button>
              <b-btn variant="success" @click="addTask()">Adicionar tarefa</b-btn>
            </b-input-group-button>
          </b-input-group>
          <hr>
        </div>
      </b-col>

      <b-col col sm="12">
        <b-list-group>
          <b-list-group-item v-for="(item, index) in list">{{ item.text }} <b-btn variant="danger" @click="removeTask(index)">Remover</b-btn></b-list-group-item>
        </b-list-group>
      </b-col>

    </b-row>
  </b-container>
</template>

<script>
export default {
  name: 'Todolist',
  data () {
    return {
      title: 'Lista de compras da Gagau',
      task: '',
      list: []
    }
  },
  created () {
    this.loadList();
  },
  methods: {
    loadList () {
      this.$http.get('list').then(
        response => {
          console.log(response.body);
        }
      );
    },
    addTask () {
      this.list.push({'text':this.task});
      this.task = '';
    },
    removeTask (index) {
      this.list.splice(index, 1);
    }
  }
}
</script>
