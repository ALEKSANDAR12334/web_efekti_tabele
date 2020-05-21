<template>
  <div class="home">
    <table>
      <tr>
        <th>Rbr</th>
        <th>Ime</th>
        <th>Prezime</th>
        <th>Škola</th>
        <th>Poeni</th>
      </tr>

      <tr
        v-for="(student, index) in studentsList"
        :key="`${index}-student`"
        :class="rowClasses(student, index)"
      >
        <td>{{index + 1}}</td>
        <td>{{student.name}}</td>
        <td>{{student.surname}}</td>
        <td>{{student.school}}</td>
        <td>{{student.points}}</td>
      </tr>
    </table>

    <button @click.prevent="sortList">Sortiraj</button>
    <button @click.prevent="toggleColorAltRows">Oboji alternativne redove</button>
    <button @click.prevent="toggleColorGreenRows">Markiraj one koji su položili</button>
    <button @click.prevent="toggleColorRedRows">Markiraj one koji nisu položili</button>
    <button @click.prevent="filterPassedStudents">Izdvoji one koji su položili</button>
  </div>
</template>

<script>
// @ is an alias to /src
import {studentsList} from './students'


export default {
  name: 'Home',
  data: () => ({
    studentsList,
    altRowsColored: false,
    greenRowsColored: false,
    redRowsColored: false
  }),
  methods: {
    rowClasses (student, index) {
      return {
        'row-alt': (index % 2 === 1 && this.altRowsColored),
        'row-green': (student.points > 50 && this.greenRowsColored),
        'row-red': (student.points <= 50 && this.redRowsColored)
      }
    },
    filterPassedStudents () {
      this.studentsList = this.studentsList.filter(student => student.points > 50)
      this.sortList()
    },
    sortList () {
      this.studentsList.sort((a, b) => {
        return b.points - a.points
      })
    },
    toggleColorAltRows () {
      this.altRowsColored = !this.altRowsColored
    },
    toggleColorGreenRows () {
      this.greenRowsColored = !this.greenRowsColored
    },
    toggleColorRedRows () {
      this.redRowsColored = !this.redRowsColored
    }
  }
}
</script>

<style scoped>
  table {
    font-family: arial, sans-serif;
    border-collapse: collapse;
    width: 100%;
  }

  td, th {
    border: 1px solid #dddddd;
    text-align: left;
    padding: 8px;
  }

  th {
    background-color: #42b983;
    color: white;
  }

  .row-alt {
    background-color: #dddddd;
  }

  .row-green {
    color: #42b983;
  }

  .row-red {
    color: #d62d1e;
  }

  button {
    margin: 20px 10px;
  }
</style>
