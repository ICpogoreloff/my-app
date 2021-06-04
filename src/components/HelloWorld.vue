
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
                v-model="selectedEmp"
                color="primary">
              <v-list-item
                  v-for="(empLS) in empStorage" :key="empLS"
              >
            <v-list-item-content>
              <v-list-item-title vclass="empLS">{{empLS}}</v-list-item-title>
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
  <div>
    <v-text-field
        v-model="fio"
        label="Фамилия Имя Отчество"
        required
    ></v-text-field>
    <v-text-field
        v-model="pass_ser"
        label="Номер паспорта"
        required
        :counter="4"
    ></v-text-field>
    <v-text-field
        v-model="pass_no"
        label="Серия паспорта"
        required
        :counter="6"
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
        @click="removeEmp(selectedEmp)"
    >
      Удалить
    </v-btn>
    <v-btn class="mr-4"
           @click="addEmp"
    >
      Сохранить
    </v-btn>
    </v-col>
  </div>
          <v-col>
                <v-text-field
                    v-model="newEmp"
                    label="Временный ввод для localStorage"
                    required
                ></v-text-field>
          </v-col>
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

      selectedEmp: 1,
      empStorage:[],
      newEmp:null
    }),

    computed: {
      computedDateMoment () {
        return this.date ? moment(this.date).format('YYYY-MM-DDThh:mm:ssZ') : ''
      },
    },
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

      clear () {
        this.fio = ''
        this.pass_no = ''
        this.pass_ser = ''
        this.pass_dt = ''
      },
      addEmp() {
        // ensure they actually typed something
        if(!this.newEmp) return
        this.empStorage.push(this.newEmp)
        this.newEmp = ''
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
    },
  }

console.log(_.isArray([1,2]))

</script>


