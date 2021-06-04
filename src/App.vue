<template>
  <v-app>
    <v-app-bar
      app
      color="primary"
      dark
    >
      <v-col>
      <v-btn
          class="ma-2"
          outlined
      >
        <span class="mr-2">Добавить</span>

      </v-btn>
      </v-col>
      <v-col>
      <div class="d-flex align-center">
        <span v-once>Клик на Сотруднике - открывает форму сотрудника</span>
      </div>

      </v-col>
    </v-app-bar>
    <v-main>
      <HelloWorld/>
    </v-main>
  </v-app>
</template>

<script>
import HelloWorld from './components/HelloWorld'


export default {
  name: 'App',

  components: {
    HelloWorld,
  },

  data: () => ({
    empStorage:[],
    newEmp:null
  }),

  mounted() {

    if(localStorage.getItem('empStorage')) {
      try {
        this.empStorage = JSON.parse(localStorage.getItem('empStorage'))
      } catch(e) {
        localStorage.removeItem('empStorage')
      }
    }
  },
  methods: {
    addEmp() {
      // ensure they actually typed something
      if(!this.newCat) return
      this.empStorage.push(this.newCat)
      this.newCat = ''
      this.saveEmp()
    },
    removeEmp(x) {
      this.empStorage.splice(x,1)
      this.saveEmp()
    },
    saveEmp() {
      let parsed = JSON.stringify(this.empStorage)
      localStorage.setItem('empStorage', parsed)
    }
  }
}
</script>
