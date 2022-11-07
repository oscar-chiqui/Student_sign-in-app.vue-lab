<template>
    <div>

        <div class="alert alert-danger" v-show="errors.length > 0 ">
            <li v-for="error in errors">{{ error }}</li>

        </div>



        <div class="card add-student m-2 p-2">
            <h4 class="card-title">Add new student</h4>

            <div class="form-group">
                <label for="name">Name</label>
                <!-- Add v-model and .trim attribute to each input:  newStudentName -->
                <input id="name" class="form-control" v-model.trim="newStudentName"> 
            </div>

            <div class="form-group">
                <label for="starID">Star ID</label>
                <!-- Add v-model and .trim  attribute to each input: newStarID -->
                <input id="starID" class="form-control" v-model.trim="newStartID"> 
            </div>

            <!-- v-on:click event handler -->
            <button class="btn btn-primary" v-on:click="addStudent">Add</button>
        </div>

    </div>
</template>

<script>
export default {
    name: 'NewStudentForm',
    emits: ['student-added'],  // Document events this component emits 
    data() {
        return {
            newStudentName: '',
            newStartID: '',
            errors: []

        }
    },
    methods: {
        addStudent() {
                this.errors = []

                if(!this.newStudentName) {
                    this.errors.push('Student name must be entered')
                }

                if(!this.newStartID) {
                    this.errors.push (' StartID must be entered')
                }


                // if there are no errors

                if (this.errors.length == 0 ) {

                let student = {name: this.newStudentName, startID: this.newStartID, present: false}

                // emit message to parent with new student
                    this.$emit('student-added', student)
                


               
                this.newStudentName = '' // two single quotes - an empty string
                this.newStartID = ''

            } else {
                this.errors.push('Name and StartID are required.')
            }

        },
    }


}

</script>

<style scoped>

</style>