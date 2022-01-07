<template>
  <form @submit.prevent="handleSubmit">
      <label>Email</label>
      <input type="email" required v-model="email">
      <label>Password</label>
      <input type="password" required v-model="password">
      <div v-if="passError" class="error" >{{passError}}</div>
      

      <label>Role:</label>
      <select v-model="role">
          <option value="developer">Web Developer</option>
          <option value="designer">Designer</option>
      </select>
    <label>Skills:</label>
      <input type="text" v-model="tempSkills" @keyup.alt="addSkill">

      <div v-for="skill in skills" :key="skill" class="pills">
          <span @click="deleteSkill(skill)">{{skill}}</span>
      </div>

      <div class="terms">
          <input type="checkbox" v-model="terms" required>
          <label>Accept terms and conditions</label>
      </div>

      <div class="submit">
          <button>Create an account</button>
      </div>
  </form>

  <p>Password: {{passError}}</p>
  <p>Email:{{email}}</p>
  <p>Password: {{password}}</p>
  <p>Role: {{role}}</p>
  <p>Terms accepted: {{terms}}</p>
</template>

<script>
export default {
    data(){
        return {
            email:'',
            password: '',
            role:'designer',
            terms:false,
            tempSkills:'',
            skills: [],
            passError:''
        }
    },
    methods:{
        addSkill(e){
            if(e.key === ',' && this.tempSkills){

                if(!this.skills.includes(this.tempSkills)){
                   this.skills.push(this.tempSkills)
                }
                this.tempSkills = ''
            }
        },
        deleteSkill(skill){
            this.skills = this.skills.filter((item)=>{
                return skill !== item
            })
        },
        handleSubmit(){
            this.passError = this.password.length > 5 ?'': 'Password must be at least 6 chars'
            if(!this.passError){
                console.log('Email:' , this.email)
                console.log('Password:' , this.password)
                console.log('Role:' , this.role)
                console.log('Skills:' , this.skills)
                console.log('Terms accept:' , this.terms)
            }
        }
    }

}
</script>

<style>
    form{
        max-width: 30%;
        margin: 30px auto;
        background:white;
        text-align: left;
        padding: 40px;
        border-radius: 10px;
    }
    label{
        color: #aaa;
        display: inline-block;
        margin: 25px 0 15px;
        font-size: 0.6em;
        text-transform: uppercase;
        letter-spacing: 1px;
        font-weight: bold;
    }
   select, input{
        display: block;
        padding: 10px 6px;
        width: 100%;
        box-sizing: border-box;
        border: none;
        color: #555;
        border-bottom: 1px solid #ddd;
    }
    input[type='checkbox'] {
        display: inline-block;
        width: 16px;
        margin: 0 10px 0 0;
        position: relative;
        top: 2px;
    }
    .pills {
        display: inline-block;
        margin: 20px 10px 0 0;
        padding: 6px 12px;
        border-radius: 20px;
        background: #eee;
        font-size: 12px;
        font-weight: bold;
        color: #777;
        cursor: pointer;
        margin-bottom: 10px;
    }
    button {
        background: #0b6dff;
        border: 0;
        padding: 10px 20px;
        margin-top: 20px;
        color: white;
        border-radius: 20px;
        cursor: pointer;
    }
    .submit {
        text-align: center;
    }
    .error {
        color: crimson;
        margin-top: 10px;
        font-size: .8em;
        font-weight: lighter;
    }
</style>