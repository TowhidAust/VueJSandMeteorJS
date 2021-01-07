<template>
  <div class="dataInputsContainer">
    <form @submit="submitInputData">
      <div>
        <label for="name">Enter your name</label>
        <input v-model="name" v-on:change="$emit('students-name-change', $event)" type="text" placeholder="enter students name" />
      </div>
      <div>
        <label for="email">Enter your Email</label>
        <input v-model="email" v-on:change="$emit('students-email-change', $event)" name="email" type="text" placeholder="enter students email" />
      </div>

      <div>
        <label for="phone">Enter your phone</label>
        <input v-model="phone" v-on:change="$emit('students-phone-change', $event)" name="phone" type="text" placeholder="enter students phone" />
      </div>

      <div>
        <label for="date">Enter your Date Of Birth</label>
        <input v-model="dateOfBirth" v-on:change="$emit('students-DOB-change', $event)" name="date" type="date"/>
      </div>

      <div>
        <label for="subjects">Chose Subjects</label>
        <select v-model="subject" v-on:change="$emit('students-subject-change', $event)">
            <option value="Bangla">Bangla</option>
            <option value="English">English</option>
            <option value="Math">Math</option>
        </select>
      </div>

      <button class="btn" type="submit">Submit</button>
    </form>

    <div class="outputTable">

        <!-- LIST OF STUDENTS -->
      <table>
        <caption>
          list of students
        </caption>
        <thead>
          <tr>
            <th scope="col">Name</th>
            <th scope="col">Email</th>
            <th scope="col">Phone</th>
            <th scope="col">Date of Birth</th>
            <th scope="col">Subjects</th>
          </tr>
        </thead>
        <tbody class="tbody" v-html="returnListOfStudents()">

        </tbody>
      </table>

    <br> <br>
        <!-- LIST OF SUBJECTS -->
      <table>
        <caption>
         list of subjects
        </caption>
        <thead>
          <tr>
            <th scope="col">Name</th>
            <th scope="col">Students</th>
          </tr>
        </thead>
        <tbody class="tbody" v-html="returnListOfSubjects()">
            <tr>
                <td>Bangla</td>
                <td>Towhid, John, Doe</td>
            </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
export default {
  name: "StudentsData",
  props: ["studentsInfoTable", "subjectsInfoTable"],
  data() {

      return{
          name: '',
          email: '',
          phone: '',
          dateOfBirth: '',
          subject: ''
      }
  },
  methods: {
      returnListOfStudents(){
        //   return the table rows according to the studentInfoTable array
          let studentsInfoTable = this.studentsInfoTable;
          let outputHtml = ''
          for(let index in studentsInfoTable){
              let studentName = studentsInfoTable[index].name;
              let studentEmail = studentsInfoTable[index].email;
              let studentPhone = studentsInfoTable[index].phone;
              let studentDOB = studentsInfoTable[index].dateOfBirth;
              let studentSubject = studentsInfoTable[index].subject;
              let rowHtml = `<tr>
                                <td>${studentName}</td>
                                <td>${studentEmail}</td>
                                <td>${studentPhone}</td>
                                <td>${studentDOB}</td>
                                <td>${studentSubject}</td>
                            </tr>` 
                outputHtml = outputHtml + rowHtml;
          }
          return outputHtml;
      },
      returnListOfSubjects(){
        //   return the table rows according to the studentInfoTable array
          let subjectsInfoTable = this.subjectsInfoTable;
          let outputHtml = ''
          for(let index in subjectsInfoTable){
              let subjectName = subjectsInfoTable[index].name;
              let students = subjectsInfoTable[index].students;
             
              let rowHtml = `<tr>
                                <td>${subjectName}</td>
                                <td>${students}</td>
                            </tr>` 
                outputHtml = outputHtml + rowHtml;
          }
          return outputHtml;
      },
      submitInputData(e){
          e.preventDefault();
          let newData = {
              name: this.name,
              email: this.email,
              phone: this.phone,
              dateOfBirth: this.dateOfBirth,
              subject: this.subject
          }

          this.$emit('submit-form', newData);
      }
  }
};
</script>

<style scoped>
.dataInputsContainer {
  padding: 2%;
}
.dataInputsContainer form {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}

.dataInputsContainer form div {
  width: 30%;
  margin-bottom:1%;
}

.dataInputsContainer form div label {
  margin-bottom: 2%;
  display: block;
}

.dataInputsContainer form input {
  padding: 2%;
  border: 1px solid #ddd;
  width: 95%;
  outline: none;
  border-radius: 5px;
}



select{
    width: 100%;
    padding: 2% 1%;
    outline: none;
    border: 1px solid #ddd;
    border-radius: 5px;
}

.btn{
  cursor: pointer;
  padding: 1%;
  width: 15em;
  text-align: center;
  white-space: nowrap;
  text-decoration: none !important;
  text-transform: none;
  text-transform: capitalize;
  color: #fff;
  border: 0 none;
  border-radius: var(--borderRadius);
  font-size: 13px;
  font-weight: 500;
  background: seagreen;
  box-shadow: 2px 5px 10px var(--color-smoke);
  border-radius: 5px;
}

.outputTable{
    margin-top: 5%;
}



 table {
  border: 1px solid #ccc;
  border-collapse: collapse;
  margin: 0;
  padding: 0;
  width: 100%;
  table-layout: fixed;
}

table caption {
  font-size: 1.5em;
  margin: 0.5em 0 0.75em;
}

table /deep/ tr {
  background-color: #f8f8f8;
  border: 1px solid #ddd;
  padding: 0.35em;
}

table /deep/ th,
table /deep/ td {
  padding: 0.625em;
  text-align: center;
}

table /deep/ th {
  font-size: 0.85em;
  letter-spacing: 0.1em;
  text-transform: uppercase;
}

@media screen and (max-width: 600px) {
  table {
    border: 0;
  }

  table /deep/ caption {
    font-size: 1.3em;
  }

  table /deep/ thead {
    border: none;
    clip: rect(0 0 0 0);
    height: 1px;
    margin: -1px;
    overflow: hidden;
    padding: 0;
    position: absolute;
    width: 1px;
  }

  table /deep/ tr {
    border-bottom: 3px solid #ddd;
    display: block;
    margin-bottom: 0.625em;
  }

  table /deep/ td {
    border-bottom: 1px solid #ddd;
    display: block;
    font-size: 0.8em;
    text-align: right;
  }

  table /deep/ td::before {
    /*
    * aria-label has no advantage, it won't be read inside a table
    content: attr(aria-label);
    */
    content: attr(data-label);
    float: left;
    font-weight: bold;
    text-transform: uppercase;
  }

  table /deep/ td:last-child {
    border-bottom: 0;
  }
}
</style>
