<template>
  <div id="app">

    <new-student-form v-on:student-added="newStudentAdded"></new-student-form>

    <StudentTable 
      v-bind:students="students" 
      v-on:student-arrived-or-left="studentArrivedOrLeft"
      v-on:delete-student="StudentDeleted">
    </StudentTable>


    <StudentMessage v-bind:student="mostRecentStudent"></StudentMessage>



  </div>
</template>

<script>
import NewStudentForm from './components/NewStudentForm.vue'
import StudentMessage from './components/StudentMessage.vue'
import StudentTable from './components/StudentTable.vue'

export default {
  name: 'App',
  components: {
    NewStudentForm,
    StudentMessage,
    StudentTable
  },
  data() {
    return {
      students: [],
      mostRecentStudent: {}
    }
  },
  methods: {
    newStudentAdded (student) {
      this.students.push(student)
      this.students.sort(function(s1, s2) {
        return s1.name.toLowerCase() < s2.name.tolowerCase() ? -1 : 1
      })

    },
    studentArrivedOrLeft(student, present) {
      // find stundent in array of students
      // update present attribute

      let updateStudent = this.students.find( function(s) {
        if (s.name === student.name && s.startID === student.startID) {
          return true
        }
      })
      if (updateStudent) {
        updateStudent.present = present
        this.mostRecentStudent = updateStudent
      }
    },
    StudentDeleted(student){
      this.students = this.students.filter (function(s) { // filter returns a new array of all students for whom the function returns true 
        if (s !=student ) {
          return true
        }
      })

      this.mostRecentStudent = {}  // clear welcome/goodbye message.

    }
  }
}
</script>

<style>

@import "https://cdn.jsdelivr.net/npm/bootstrap@4.3.1/dist/css/bootstrap.min.css";






#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
