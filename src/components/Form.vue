<script>
export default {
  data() {
    return {
      email: "",
      password: "",
      role: "Designer",
      term: false,
      names: [],
      tempSkill: "",
      Skills: [],
      passwordError: ''
    };
  },
  methods: {
    skillPush() {
      if (!this.Skills.includes(this.tempSkill)) {
        this.Skills.push(this.tempSkill);
        this.tempSkill = "";
      }
    },
    removeHandler(e) {
      console.log(e.target.textContent);
      this.Skills.pop(e.target.textContent);
    },
    submitHandler() {
      console.log("form submitted!");
      if(this.password.length<5){
        this.passwordError = "password must be atleast 5 characters long!";
        setTimeout(() => {
            this.passwordError='';
        }, 5000);
        return;
      }
      const formData = {
        email: this.email,
        password: this.password,
        role: this.role,
        term: this.term,
        names: this.names,
        skills: this.Skills
      }
      console.log("formdata: ",formData);
      console.log("formdata: ",JSON.stringify(formData));
      this.email = "";
      this.password = "";
      this.role = "Designer";
      this.term = false;
      this.names = [];
      this.tempSkill = "";
      this.Skills = [];
    },
  },
};
</script>

<template>
  <div>
    <form @submit.prevent="submitHandler">
      <label>Email:</label>
      <input
        type="email"
        v-model="email"
        autocomplete="on"
        autofocus
        required
      />
      <label>Password:</label>
      <input type="password" v-model="password" />
      <div v-if="passwordError" class="error">{{ passwordError }}</div>
      <label>Role:</label>
      <select v-model="role">
        <option value="Developer">Web Developer</option>
        <option value="Designer">Web Designer</option>
      </select>
      <label>Skills:</label>
      <input type="text" v-model="tempSkill" @keyup.enter="skillPush" />
      <div
        class="pill"
        v-for="(Skill, index) in Skills"
        v-bind:key="index"
        @click="removeHandler"
      >
        <!-- <li>{{ Skill }} index: {{ index }}</li> -->
        <li>{{ Skill }}</li>
      </div>
      <div class="terms">
        <input type="checkbox" v-model="term" required />
        <label>Accept terms and conditions</label>
      </div>
      <div>
        <input type="checkbox" value="Mayank" v-model="names" />
        <label>Mayank</label>
      </div>
      <div>
        <input type="checkbox" value="Manav" v-model="names" />
        <label>Manav</label>
      </div>
      <div>
        <input type="checkbox" value="Rahul" v-model="names" />
        <label>Rahul</label>
      </div>
      <div class="submit">
        <button>Create an Account</button>
      </div>
    </form>
    <p>Email: {{ email }}</p>
    <p>Password: {{ password }}</p>
    <p>Role: {{ role }}</p>
    <p>terms accepted: {{ term }}</p>
    <p>names: {{ names }}</p>
    <p>tempSkill: {{ tempSkill }}</p>
    <p>Skills: {{ Skills }}</p>
  </div>
</template>
<style scoped>
.error{
    color: red;
    margin-top: 10px;
    font-size: 0.8rem;
    font-weight: bold;
}
form {
  max-width: 420px;
  margin: 30px auto;
  background: white;
  text-align: left;
  padding: 40px;
  border-radius: 10px;
}
label {
  color: #aaa;
  display: inline-block;
  margin: 25px 0 15px;
  font-size: 0.6rem;
  letter-spacing: 1px;
  font-weight: bold;
}
.pill {
  cursor: pointer;
  list-style: none;
  display: inline-block;
  margin: 20px 10px 0 0;
  padding: 6px 12px;
  background: #eee;
  border-radius: 20px;
  font-size: 12px;
  letter-spacing: 1px;
  font-weight: bold;
  color: #777;
}
button {
  background: #0b6dff;
  border: 0px;
  padding: 10px 20px;
  margin-top: 20px;
  color: white;
  border-radius: 20px;
  cursor: pointer;
}
button:hover {
  background-color: turquoise;
  font-weight: bold;
}
.submit {
  text-align: center;
}
input,
select {
  display: block;
  padding: 10px 6px;
  width: 100%;
  box-sizing: border-box;
  border: none;
  border-bottom: 1px solid #aaa;
  color: #555;
}
p {
  text-align: center;
}
input[type="checkbox"] {
  display: inline-block;
  width: 16px;
  margin: 0 10px 0 0;
  position: relative;
  top: 2px;
}
</style>
