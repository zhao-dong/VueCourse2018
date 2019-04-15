<template>
  <div class="hello">
  <!--  <h1>{{ msg }}</h1>
    <h1>{{ name }}</h1>

    {{ btnState ? 'The button is disabled' : 'The button is active'}}

    <button v-on:click="changeName" v-bind:disabled="btnState"> Change Name </button> -->


    <form @submit.prevent="addSkill">
      <input type="text" placeholder="Enter a skill you have.." v-model="skill" v-validate="'min:5'" name="skill">

    <!--  <p class="alert" v-if="errors.has('skill')">{{ errors.first('skill')}}</p>
    -->
    <transition name="alert-in" enter-active-class="animated flipInX" leave-active-class="animated flipOutX">
        <p class="alert" v-if="errors.has('skill')">{{ errors.first('skill')}} </p>
    </transition>
  <!--    <input type="checkbox" id="checkbox" v-model ="checked"> -->
    </form>
    {{skill}}

    <div class="holder">
        <ul>

          <transition-group name="list" enter-active-class="animated bounceInUp" leave-active-class="animated bounceOutDown">
              <li v-for="(data, index) in skills" :key = 'index'>
                {{index}}.{{data.skill}}
                <i class="fa fa-minus-circle" v-on:click="remove(index)"></i>
              </li>
        </transition-group>

        </ul>

        <p> These are the skills that you possesses. </p>
        <p v-if="seen">See me!</p>
        <ol>
          <li v-for="skill in skills">
            {{skill.skill}}
          </li>
        </ol>
        <p> input is : {{input}} </p>
        <input v-model="input">

        <button v-on:click="btnClick('my test world')">my world</button>

<!--
        <p v-if="skills.length >1"> You have more than 1 skills </p>
        <p v-else>You have less than or equal to 1 skill</p>
-->
<!--
      <div v-bind:class="alertObject"> </div>
-->
    </div>


  </div>
</template>

<script>
export default {
  name: 'Skills',
  data () {
    return {

      seen: true,
      //msg: 'Welcome to Your Vue.js App',
      //name: 'Coursetro',
      //btnState: true,
      checked: false,

      input:'dont know',

      skill: '',
      skills: [
        {"skill": "Vue.js"},
        {"skill": "Frontend Developer"},
      ],
      alertObject: {
        alert: true,
      },

    }
  },
  methods: {
    addSkill()
    {
      this.$validator.validateAll().then((result) => {
          if (result) {
            this.skills.push({skill: this.skill})
            this.skill = '';
          } else {
            console.log('Not valid');
          }
        })
    },
    remove(id) {
     this.skills.splice(id,1);
    },
    btnClick(pname)
    {
      this.input=pname;
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<!-- <style src="./Skills.css" scoped> -->
<style scoped>
@import "https://cdn.jsdelivr.net/npm/animate.css@3.5.1";
@import "https://maxcdn.bootstrapcdn.com/font-awesome/4.7.0/css/font-awesome.min.css";
  .holder {
    background: #fff;
  }
  ul {
    margin: 0;
    padding: 0;
    list-style-type: none;
  }

  ul li {
    padding: 20px;
    font-size: 1.3em;
    background-color: #E0EDF4;
    border-left: 5px solid #3EB3F6;
    margin-bottom: 2px;
    color: #3E5252;
  }
  p {
    text-align:center;
    padding: 30px 0;
    color: gray;
  }
  .container {
    box-shadow: 0px 0px 40px lightgray;
  }

  input {
  width: calc(100% - 40px);
  border: 0;
  padding: 20px;
  font-size: 1.3em;
  background-color: #323333;
  color: #687F7F;
  }

  .alert {
    background: #fdf2ce;
    font-weight: bold;
    display: inline-block;
    padding: 5px;
    margin-top: -20px;
  }

  .alert-in-enter-active {
   animation: bounce-in .5s;
 }
 .alert-in-leave-active {
   animation: bounce-in .5s reverse;
 }
@keyframes bounce-in {
 0% {
   transform: scale(0);
 }
 50% {
   transform: scale(1.5);
 }
 100% {
   transform: scale(1);
 }
}

i {
  float:right;
  cursor:pointer;
}

</style>
