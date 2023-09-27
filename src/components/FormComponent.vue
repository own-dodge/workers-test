<template>
  <form class="form" @submit.prevent="addPerson">
    Имя<input class="form-field" v-model="person.name" type="text" required>
    Телефон<input class="form-field" v-model="person.tel" type="tel" required>
    Начальник<select class="form-field" v-model="person.boss">
      <option v-for="(person, index) in gridDataPersons" :key="index" :value="person.name">
      {{ person.name }}
      </option>
    </select>
    <ButtonUI class="btn-form" type="submit">Сохранить</ButtonUI>
  </form>
</template>

<script>
import ButtonUI from '@/components/UI/ButtonUI.vue';

export default {
  components: { ButtonUI },
  props: ['gridDataPersons'],
  data() {
    return {
      person: {
        name: null,
        tel: null,
        boss: null,
        employees: []
      },
    }
  },
  methods: {
    addPerson() {
      this.$emit('addPerson', this.person)
      this.person = {
        name: null,
        tel: null,
        boss: null,
        employees: []
      }
    },
  },
}
</script>

<style scoped>
.form {
  display: flex;
  flex-direction: column;
}

.form-field {
  margin-bottom: 15px;
  height: 20px;
}

.btn-form {
  align-self: center;
  width: 30%;
}
</style>