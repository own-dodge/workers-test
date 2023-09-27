<template>
  <table>
    <thead>
      <tr>
        <th v-for="tableName in tableColumnsList" @click="sortBy"
          :key="tableName">
          {{ tableName }}
        </th>
      </tr>
    </thead>
    <tbody>
      <template v-for="(person, index) in gridDataPersons" :key="index">
        <tr v-if="findPerson(person)">
          <td v-for="(key, index) in Object.values(person).slice(0, 2)" :key="index">
            {{ key }}
          </td>
        </tr>
        <template v-if="person.employees.length > 0">
          <tr v-for="(person, index) in person.employees" :key="index">
            <td v-for="(key, index) in Object.values(person).slice(0, 2)" :key="index">
              {{ index === 0 ? "+" + key : key }}
            </td>
          </tr>
        </template>
      </template>
    </tbody>
  </table>
</template>

<script>
export default {
  props: ['tableColumnsList', 'gridDataPersons'],
  methods : {
    sortBy(direction) {
      this.$emit('sortBy', direction)
    },
    findPerson(person) {
      this.gridDataPersons.forEach(element => {
        element.employees.forEach((el) => {
          if (el === person) {
            return false
          } else { return true }
        }) 
      });
    }
  }
}
</script>

<style scoped>
table {
  border: 2px solid #42b983;
  border-radius: 3px;
  background-color: #fff;
}

th {
  background-color: #42b983;
  color: white;
  cursor: pointer;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

td {
  background-color: #f9f9f9;
}

th,
td {
  min-width: 120px;
  padding: 10px 20px;
}

th.active {
  color: #fff;
}

th.active .arrow {
  opacity: 1;
}

.arrow {
  display: inline-block;
  vertical-align: middle;
  width: 0;
  height: 0;
  margin-left: 5px;
  opacity: 0.66;
}

.arrow.asc {
  border-left: 4px solid transparent;
  border-right: 4px solid transparent;
  border-bottom: 4px solid #fff;
}

.arrow.dsc {
  border-left: 4px solid transparent;
  border-right: 4px solid transparent;
  border-top: 4px solid #fff;
}
</style>