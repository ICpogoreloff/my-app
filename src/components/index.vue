
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
    <v-text-field
        v-model="pass_dt"
        :error-messages="nameErrors"
        label="Дата паспорта"
        required
        @input="$v.pass_dt.$touch()"
        @blur="$v.pass_dt.$touch()"
    ></v-text-field>
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
  export default {
    name: 'HelloWorld',

  }
</script>

