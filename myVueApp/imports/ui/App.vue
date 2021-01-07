<template>
  <div className="container">
    <header>
      <h1>Table list</h1>
    </header>
    <ul>
      <!-- <Task v-for="(task, index) in tasks" v-bind:key="index" v-bind:task="task"/> -->
      <StudentsData 
      v-bind:studentsInfoTable="studentsInfoTable" 
      v-bind:subjectsInfoTable="subjectsInfoTable" 
      v-on:students-name-change="studentNameChangeHandler" 
      v-on:students-email-change="studentEmailChangeHandler"
      v-on:students-phone-change="studentPhoneChangeHandler"
      v-on:students-DOB-change="studentDOBChangeHandler"
      v-on:students-subject-change="studentSubjectChangeHandler"
      v-on:submit-form="onSubmitForm"
      />
    </ul>
  </div>
</template>
 
<script>
import Vue from "vue";
import Task from "./Task.vue";
import { Tasks } from "../api/tasks.js";
import StudentsData from "./StudentsData.vue"
 
export default {
  components: {
    Task,
    StudentsData

  },
  data() {
    return {
      submitData: {},
      studentsInfoTable: [
        {
          name: 'Md. Towhidul Islam', 
          email:'t@gmail.com', 
          phone: '09875456', 
          dateOfBirth: '17-11-1995', 
          subject: 'Bangla'
        },
        {
          name: 'Md. Towhidul Islam2', 
          email:'t2@gmail.com', 
          phone: '209875456', 
          dateOfBirth: '17-11-1980', 
          subject: 'Bangla, English'
        }
        
        ],

        subjectsInfoTable: [
          {
            name: 'Bangla',
            students: 'Towhid, John' 
          },
          {
            name: 'English',
            students: 'Towhid, John Kabir' 
          },
        ]
    };
  },
  methods: {
    studentNameChangeHandler(e){
      // let studentsName = e.target.value;
      // TODO validation
    },

    studentEmailChangeHandler(e){
      // console.log(e.target.value);
      // TODO validation


    },
    studentPhoneChangeHandler(e){
      // console.log(e.target.value);
      // TODO validation

    },
    studentDOBChangeHandler(e){
      // console.log(e.target.value);
      // TODO validation


    },
    studentSubjectChangeHandler(e){
      // console.log(e.target.value);
      // TODO validation

    },

    onSubmitForm(newData){
      console.log("on submit new data",newData);
      this.studentsInfoTable.push(newData);

      // now find out the subjects info and add them into the subjects info array to make the subjects info table

      let mySubjectsArr = [];
      let updatedStudentsInfoTable = this.studentsInfoTable;
      for(let index in updatedStudentsInfoTable){
        let subject = updatedStudentsInfoTable[index].subject;
        let student = updatedStudentsInfoTable[index].name;
        if(subject === "Bangla"){
          let data = {
            name: 'Bangla',
            students: student 
          }
          mySubjectsArr.push(data);
        }else if(subject === "English"){
          let data = {
                      name: 'English',
                      students: student 
                    }
          mySubjectsArr.push(data);
        }else if(subject === "Math"){
          let data = {
                      name: 'Math',
                      students: student 
                    }
          mySubjectsArr.push(data);
        }
      }

      this.subjectsInfoTable = mySubjectsArr
      console.log('updatedStudentsInfoTable',updatedStudentsInfoTable) 
    }
  },
  meteor: {
    tasks() {
      return Tasks.find({}).fetch();
    }
  }

};
</script>