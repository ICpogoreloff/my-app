<template>
  <v-app>
    <v-app-bar
      app
      color="primary"
      dark
    >
      <v-btn
          class="ma-2"
          outlined
      >
        <span class="mr-2">Добавить</span>

      </v-btn>

      <v-spacer></v-spacer>
      <div class="d-flex align-center">
        <span v-once>Клик на Сотруднике - открывает форму сотрудника</span>
      </div>

    </v-app-bar>

    <v-main>
      <HelloWorld/>
    </v-main>
  </v-app>
</template>

<script>
import HelloWorld from './components';

export default {
  name: 'App',

  components: {
    HelloWorld,
  },

  data: () => ({
    //
  }),
};
</script>
