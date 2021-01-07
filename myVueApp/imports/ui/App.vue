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
import StudentsData from "./StudentsData.vue";

export default {
  components: {
    Task,
    StudentsData,
  },
  data() {
    return {
      submitData: {},
      studentsInfoTable: [
        {
          name: "Md. Towhidul Islam",
          email: "t@gmail.com",
          phone: "09875456",
          dateOfBirth: "17-11-1995",
          subject: ["Bangla"],
        },
        {
          name: "Md. Towhidul Islam2",
          email: "t2@gmail.com",
          phone: "209875456",
          dateOfBirth: "17-11-1980",
          subject: ["Bangla, English"],
        },
      ],

      subjectsInfoTable: [
        {
          name: "Bangla",
          students: ["Towhid, John"],
        },
        {
          name: "English",
          students: ["Towhid, John Kabir"],
        },
      ],
    };
  },
  methods: {
    studentNameChangeHandler(e) {
      // let studentsName = e.target.value;
      // TODO validation
    },

    studentEmailChangeHandler(e) {
      // console.log(e.target.value);
      // TODO validation
    },
    studentPhoneChangeHandler(e) {
      // console.log(e.target.value);
      // TODO validation
    },
    studentDOBChangeHandler(e) {
      // console.log(e.target.value);
      // TODO validation
    },
    studentSubjectChangeHandler(e) {
      // console.log(e.target.value);
      // TODO validation
    },

    onSubmitForm(newData) {




      /**
       * ================ STUDENTS INFO TABLE FUNCTIONALITIES===========================
       * THIS BELOW CODE MERGE THE ARRAY studentsInfoTable FOR MULTIPLE REPETITIVE NAMES
       */
      this.studentsInfoTable.push(newData);
      let updatedStudData = this.studentsInfoTable;
      var outputArr = [];
      updatedStudData.forEach(function (item) {
        var existing = outputArr.filter(function (v, i) {
          return v.name == item.name;
        });
        if (existing.length) {
          var existingIndex = outputArr.indexOf(existing[0]);
          outputArr[existingIndex].subject = outputArr[existingIndex].subject.concat(
            item.subject
          );
        } else {
          if (typeof item.subject == "string") {
            item.subject = [item.subject]
          };
          outputArr.push(item);
        }
      });

      this.studentsInfoTable = outputArr;



      
      /**
       * ================ SUBJECTS INFO TABLE FUNCTIONALITIES===========================
       * THIS BELOW CODE MERGE THE ARRAY subjectsInfoTable FOR MULTIPLE REPETITIVE SUBJECTS
       */

      // now find out the subjects info and add them into the subjects info array to make the subjects info table
      let mySubjectsArr = [];
      let updatedStudentsInfoTable = this.studentsInfoTable;

      for (let index in updatedStudentsInfoTable) {
        let subject = updatedStudentsInfoTable[index].subject;
        let student = updatedStudentsInfoTable[index].name;
        for(let subjIndex in subject){
          let _subject = subject[subjIndex];
            console.log('_subject', _subject);
            if (_subject === "Bangla") {
              console.log("bangla true");
              let data = {
                name: "Bangla",
                students: student,
              };
              mySubjectsArr.push(data);
            } else if (_subject === "English") {
              console.log("English true");

              let data = {
                name: "English",
                students: student,
              };
              mySubjectsArr.push(data);
            } else if (_subject === "Math") {
              console.log("MAth true");

              let data = {
                name: "Math",
                students: student,
              };
               mySubjectsArr.push(data);
            }
      
        }

      }

      // merge the data according to multiple studnets in one subject
      var output = [];
      mySubjectsArr.forEach(function (item) {
        var existing = output.filter(function (v, i) {
          return v.name == item.name;
        });
        if (existing.length) {
          var existingIndex = output.indexOf(existing[0]);
          output[existingIndex].students = output[existingIndex].students.concat(
            item.students
          );
        } else {
          if (typeof item.students == "string") {
            item.students = [item.students]
          };
          output.push(item);
        }
      });
      
      this.subjectsInfoTable = output;
    },
  },
  meteor: {
    tasks() {
      return Tasks.find({}).fetch();
    },
  },
};
</script>
