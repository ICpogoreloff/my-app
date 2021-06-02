
<template>

  <v-container>
    <v-row>
      <v-col>
      <div>
          <v-list
              class="pa-2"
              outlined
              tile>
            <v-list-item-group
                v-model="selectedItem"
                color="primary">
              <v-list-item
                  v-for="(item, empStore) in items"
                  :key="empStore"
              >
            <v-list-item-content>
              <v-list-item-title v-text="item.text"></v-list-item-title>
            </v-list-item-content>
              </v-list-item>
            </v-list-item-group>
          </v-list>
      </div>
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
        v-model="pass_dt"
        :close-on-content-click="false"
        max-width="290"
    >
      <template v-slot:activator="{ on, attrs }">
        <v-text-field
            :value="computedDateMoment"
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
          @change="pass_dt = false"
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
import _ from 'lodash'


  export default {
    name: 'HelloWorld',

    data: () => ({

      // https://github.com/date-fns/date-fns/blob/master/docs/upgradeGuide.md#string-arguments
      date: format(parseISO(new Date().toISOString()), 'yyyy-MM-dd'),
      pass_dt: false,
      fio: '',
      pass_no: '',
      pass_ser: '',

      selectedItem: 1,
      items: [
        { text: 'Test' },
        { text: 'Test' },
        { text: 'Test' },
        { text: 'Test' },
        { text: 'Test' },
      ],
    }),

    computed: {
      computedDateMoment () {
        return this.date ? moment(this.date).format('YYYY-MM-DDThh:mm:ssZ') : ''
      },

      _() {
        return _;
      },

    },

    methods: {
      saveEmp () {
      },
      clear () {
        this.fio = ''
        this.pass_no = ''
        this.pass_ser = ''
        this.pass_dt = ''
      },
    },

  }


</script>


