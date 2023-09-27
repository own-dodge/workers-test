<template>
  <div class="container">
    <div class="form-block">
      <ButtonUI @click="isActiveForm = !isActiveForm" class="btn-table">Добавить</ButtonUI>
      <ModalComponent v-model:show="isActiveForm">
        <FormComponent v-if="isActiveForm" @addPerson="addPerson" :grid-data-persons="gridDataPersons" />
      </ModalComponent>
    </div>
    <TableComponent @sortBy="sortBy(columnDir)" :table-columns-list="tableColumnsList"
      :grid-data-persons="gridDataPersons" />
  </div>
</template>

<script>
import FormComponent from '@/components/FormComponent.vue';
import TableComponent from '@/components/TableComponent.vue';
import ModalComponent from '@/components/ModalComponent.vue';
import ButtonUI from '@/components/UI/ButtonUI.vue';

export default {
  name: 'App',
  components: { FormComponent, TableComponent, ModalComponent, ButtonUI },
  data() {
    return {
      tableColumnsList: ['Имя', 'Телефон'],
      gridDataPersons:
        [
          { name: 'Марина', tel: '+7 941 123 21 42', boss: '', employees: [] },
          { name: 'Петр', tel: '+7 941 123 21 43', boss: '', employees: [] },
          { name: 'Борис', tel: '+7 941 123 21 44', boss: '', employees: [] },
        ],
      isActiveForm: false,
      columnDir: false,
    }
  },
  mounted() {
    this.getGridDataPersons();
  },
  watch: {
    gridDataPersons: {
      handler(UpdatedGridDataPersons) {
        localStorage.setItem('gridDataPersons', JSON.stringify(UpdatedGridDataPersons))
      },
      deep: true,
    }
  },
  methods: {
    addPerson(person) {
      if (!this.isPersonExists(person)) {
        if (this.hasBoss(person)) {
          this.gridDataPersons.find(el => el.name === person.boss).employees.push(person);
        }
        else {
          this.gridDataPersons.push(person);
        }
      }
      this.isActiveForm = !this.isActiveForm;
    },
    getGridDataPersons() {
      const localGridDataPersons = localStorage.getItem('gridDataPersons');
      if (localGridDataPersons) {
        this.gridDataPersons = JSON.parse(localGridDataPersons);
      }
    },
    sortBy(direction) {
      this.columnDir = !this.columnDir;
      this.gridDataPersons.sort((a, b) => {
        if ((!direction == false ? a.name < b.name : a.name > b.name))
          return -1;
      })
    },
    isPersonExists(person) {
      let res = this.gridDataPersons.some((pers) => {
        return pers.employees.some(emp => {
          return emp.name === person.name;
        })
      });
      return res;
    },
    hasBoss(person) {
      return person.boss !== '' && person.boss !== null;
    }
  }
}
</script>

<style>
.form-block {
  display: flex;
  flex-direction: column;
  max-width: 330px;
}

.btn-table {
  margin-bottom: 30px;
  max-width: 150px;
  align-self: flex-end;
}
</style>
