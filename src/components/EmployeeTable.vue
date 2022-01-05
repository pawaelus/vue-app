<template>
  <div id="employee-table">
    <p v-if="employees.length < 1" class="empty-table">tabela jest pusta</p>
    <table v-else>
      <thead>
        <tr>
          <th>imię</th>
          <th>e-mail</th>
          <th>akcje</th>
        </tr>
      </thead>
      <tbody>
      <tr v-for="employee in employees" :key="employee.id">
        <td v-if="editing === employee.id">
          <input type="text" v-model="employee.name" />
        </td>
        <td v-else>{{employee.name}}</td>
        <td v-if="editing === employee.id">
          <input type="text" v-model="employee.email" />
        </td>
        <td v-else>{{employee.email}}</td>
        <td v-if="editing === employee.id">
          <button @click="editEmployee(employee)">Zapisz</button>
          <button class="muted-button" @click="editing = null">Anuluj</button>
        </td>
        <td v-else>
          <button @click="editMode(employee.id)">Edit</button>
          <!-- <button @click="$emit('delete:employee', employee.id)">Usuń</button> -->
          <button @click="$emit('delete:employee', employee.id)">Usuń to na boga</button>
        </td>
      </tr>
      </tbody>
    </table>
  </div>
</template>
<script>
  export default {
    name: 'employee-table',
    props: {
        employees: Array,
    },
    data() {
      return {
        editing: null,
      }
    },
    methods: {
      editMode(id) {
        this.editing = id
      },

      editEmployee(employee) {
        if (employee.name === '' || employee.email === '') return
        this.$emit('edit:employee', employee.id, employee)
        this.editing = null
      }
    }
    
  }
</script>

<style scoped></style>