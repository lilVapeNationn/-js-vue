<template>
  <div class="container">
    <h1>Учет заработной платы </h1>
    <form>
      <label for="name">Полное имя : </label>
      <input type="text" v-model="name" required />
      <br />
      <label for="date">Дата выдачи зарплаты: </label>
      <input type="date" v-model="date" required />
      <br />
      <label for="daysWorked">Количество отработанных дней: </label>
      <input type="number" v-model="daysWorked" required />
      <br />
      <label for="salary">Размер заработной платы сотрудника: </label>
      <input type="number" v-model="salary" required />
      <br />
      <button type="submit" onclick="return false" @click="addEmployee">Add</button>
    </form>
    <table>
      <thead>
        <tr>
          <th>Номер</th>
          <th>Полное имя </th>
          <th>Дата выдачи зарплаты </th>
          <th>Количество отработанных дней</th>
          <th>Грязная зарплата</th>
          <th>Чистая зарплата</th>
          <th class="clear"></th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(employee, index) in employees" :key="index">
          <td>{{ index + 1 }}</td>
          <td>{{ employee.name }}</td>
          <td>{{ employee.date }}</td>
          <td>{{ employee.daysWorked }}</td>
          <td>{{ employee.salary }}</td>
          <td>{{ employee.salary * 0.85 }}</td>
          <td class="clear">
            <button class="red" @click="removeEmployee(index)">Remove</button>
          </td>
        </tr>
      </tbody>
    </table>
    <p>Total Without Tax Deductions: {{ totalWithoutTax }}</p>
    <p>Total With Tax Deductions: {{ totalWithTax }}</p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      name: '',
      date: '',
      daysWorked: 0,
      salary: 0,
      employees: []
    }
  },
  computed: {
    totalWithoutTax() {
      return this.employees.reduce((acc, employee) => acc + employee.salary, 0)
    },
    totalWithTax() {
      return this.employees.reduce((acc, employee) => acc + employee.salary * 0.85, 0)
    }
  },
  methods: {
    addEmployee() {

      if (this.name && this.date && this.daysWorked && this.salary) {
        this.employees.push({
          name: this.name,
          date: this.date,
          daysWorked: this.daysWorked,
          salary: this.salary
        })
        this.name = ''
        this.date = ''
        this.daysWorked = 0
        this.salary = 0
      } else {
        alert('Заполните строки')
      }
    },
    removeEmployee(index) {
      this.employees.splice(index, 1)
    }
  }
}
</script>
<style>
.container{
  border: 1px solid black;
  border-radius: 5px;
  width: 800px;
  height: 300px;
  background-color: rgba(240, 255, 255, 0.63);
}
.clear{
  border: 0;

}
th,td{
  border: 1px solid black;
}
.red{
  border: 1px solid red;
  background-color: rgba(204, 50, 50, 0.907);
  border-radius: 7px;

}
.red:hover{
  background-color: rgba(204, 50, 50, 0.656);
}
</style>