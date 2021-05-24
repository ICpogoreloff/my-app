
<template>

  <v-container>
    <v-row>
      <v-col>
      <p class="subheading font-weight-regular">
        Здесь будет список сотрудников
      </p>
      </v-col>
      <v-divider
          vertical
      >
      </v-divider>
        <v-col>
  <v-form>
    <v-text-field
        v-model="fio"
        :error-messages="nameErrors"
        label="Фамилия Имя Отчество"
        required
        @input="$v.fio.$touch()"
        @blur="$v.fio.$touch()"
    ></v-text-field>
    <v-text-field
        v-model="pass_ser"
        :error-messages="emailErrors"
        label="Номер паспорта"
        required
        :counter="4"
        @input="$v.pass_ser.$touch()"
        @blur="$v.pass_ser.$touch()"
    ></v-text-field>
    <v-text-field
        v-model="pass_no"
        :error-messages="nameErrors"
        label="Серия паспорта"
        required
        :counter="6"
        @input="$v.pass_no.$touch()"
        @blur="$v.pass_no.$touch()"
    ></v-text-field>
    <v-menu
        v-model="menu1"
        :close-on-content-click="false"
        max-width="290"
    >
      <template v-slot:activator="{ on, attrs }">
        <v-text-field
            :value="computedDateFormattedMomentjs"
            clearable
            label="Дата выдачи"
            readonly
            v-bind="attrs"
            v-on="on"
            @click:clear="date = null"
        ></v-text-field>
      </template>
      <v-date-picker
          v-model="date"
          @change="menu1 = false"
          :first-day-of-week="1"
          locale="ru-ru"
      ></v-date-picker>
    </v-menu>
    <v-col>
    <v-btn
        class="mr-4"
        @click="clear"
    >
      Удалить
    </v-btn>
    <v-btn class="mr-4"
           @click="saveEmp"
    >
      Сохранить
    </v-btn>
    </v-col>
  </v-form>
    </v-col>
    </v-row>
  </v-container>
</template>

<script>
import moment from 'moment'
import { format, parseISO } from 'date-fns'

  export default {
    name: 'HelloWorld',
    data: () => ({
      // https://github.com/date-fns/date-fns/blob/master/docs/upgradeGuide.md#string-arguments
      date: format(parseISO(new Date().toISOString()), 'yyyy-MM-dd'),
      menu1: false,
      menu2: false,
    }),

    computed: {
      computedDateFormattedMomentjs () {
        return this.date ? moment(this.date).format('dddd, MMMM Do YYYY') : ''
      },
    },
  }
</script>


