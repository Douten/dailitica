<template>
  <div id="tasks" class="md-layout">
    <div class="md-layout-item md-small-size-25 md-xsmall-hide"></div>
    <ul class="md-layout-item md-small-size-50 md-medium-size-50 md-xsmall-size-100 tasks-list">  
      <li v-for="item of tasks" class="md-layout">
          <div class="md-layout-item md-layout task">
            <md-checkbox class="md-primary" :id="item.id" v-model="array" v-bind:value="item.id" ></md-checkbox>
            <div class="task-desc md-layout-item">{{item.text}}</div>
          </div>
          <div class="md-layout-item md-size-5">
            <span v-if="item.streak > 0">{{item.streak}}</span>
          </div>
      </li>
    </ul>
    <div class="md-layout-item md-small-size-25 md-xsmall-hide"></div>
  </div>
</template>

<script>

var axios = require('axios');
//run cron
export default {
  name: 'app',
  data () {
    return {
      tasks: {},
      array: []
    }
  },
  props: ['values'],
  created(){
    axios.get('https://habitica.com/api/v3/tasks/user?type=dailys&todos', {
      'headers': {
        "x-api-user": "ad0d7cb3-d8c0-4d36-9fd9-5d9d50fc7ca1",
        "x-api-key": "87b461d3-6ced-4977-b49d-1aacf8067e23"
        },
      'param':{
        'type': "todos"
        }
      })
    .then(
      response => {this.tasks = response.data.data;
      console.log(this.tasks);
    })
    .catch(function (error) {
      console.log(error);
    });
  }
}
</script>

<style lang="scss">
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.tasks-list{
  max-width: 480px;
}

.md-checkbox{
  padding: .7rem;
  margin: 0;
}

.task-desc{
  margin: .7rem .7rem .7rem 0;
  font-size: 1.25rem;
  font-weight: 300;
}

.task .md-list-item-content{
  padding: 0px;
}
.md-button-clean{
  white-space: normal;
}

//check box border
.md-checkbox.md-theme-default .md-checkbox-container{
  border-color: rgba(0,0,0,0.2);
}

.md-checkbox .md-checkbox-container{
  border-radius: 5px;
}


.md-ripple-enter-active.md-centered {
    transition-duration: 1.25s;
}

.md-ripple-wave{
  background: #42a5f5;
  overflow: hidden;
}

.md-ripple-enter {
    opacity: 1;
}

h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

a {
  color: #42b983;
}
</style>
