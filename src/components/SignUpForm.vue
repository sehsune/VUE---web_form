<template>
  <div class="wrapper">
    <form @submit.prevent="handleSubmit">
      <label for="">Email</label>
      <input type="email" required v-model="email" />

      <label for="">Password</label>
      <input type="password" required v-model="password" />
      <div v-if="passwordError" class="error">{{ passwordError }}</div>

      <label>Role:</label>
      <select v-model="role">
        <option value="designer">Web designer</option>
        <option value="developer">Web developer</option>
      </select>

      <label>Skills</label>
      <input type="text" v-model="tempSkill" @keyup="addSkill" />

      <div class="pill" v-for="skill in skills" :key="skill">
        <span @click="deleteSkill(skill)">{{ skill }}</span>
      </div>

      <div class="terms">
        <input type="checkbox" required v-model="terms" />
        <label>Accept terms and coditons</label>
      </div>

      <div class="submit">
        <button>Create an Account</button>
      </div>
    </form>

    <p>Email: {{ email }}</p>
    <p>Password: {{ password }}</p>
    <p>Role: {{ role }}</p>
    <p>Terms accepted: {{ terms }}</p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      email: "",
      password: "",
      role: "",
      terms: false,
      tempSkill: "",
      skills: [],
      passwordError: "",
    };
  },
  methods: {
    addSkill(e) {
      if (e.key === "," && this.tempSkill) {
        if (!this.skills.includes(this.tempSkill)) {
          this.tempSkill = this.tempSkill.replace(",", "");
          this.skills.push(this.tempSkill);
        }
        this.tempSkill = "";
      }
    },
    deleteSkill(skill) {
      this.skills = this.skills.filter((item) => {
        return skill !== item;
      });
    },
    handleSubmit() {
      this.passwordError =
        this.password.length > 5
          ? ""
          : "Password must be at least 6 chars long.";
    },
  },
};
</script>


<style>
form {
  max-width: 420px;
  margin: 30px auto;
  padding: 40px;
  text-transform: uppercase;
  letter-spacing: 1px;
  font-weight: bold;
  background-color: white;
  text-align: left;
  border-radius: 10px;
}

label {
  display: inline-block;
  color: #bbb;
  margin: 25px 0 15px;
  font-size: 15px;
  letter-spacing: 1px;
}

input,
select {
  width: 100%;
  padding: 10px 5px;
  border: none;
  border-bottom: 1px solid #ddd;
  color: #555;
  font-size: 15px;
  box-sizing: border-box;
  border: none;
  border-bottom: 1px solid #bbb;
}
input[type="checkbox"] {
  display: inline-block;
  width: 16px;
  margin: 0 10px 0 0;
}

p {
  text-align: center;
}

.pill {
  display: inline-block;
  margin: 20px 10px 0 0;
  padding: 6px 12px;
  background: #eee;
  border-radius: 20px;
  font-size: 12px;
  letter-spacing: 1px;
  font-weight: bold;
  color: #777;
  cursor: pointer;
}
.submit {
  text-align: center;
}

button {
  background-color: cadetblue;
  border: 0;
  padding: 10px 20px;
  color: white;
  border-radius: 20px;
  margin-top: 20px;
}

.error {
  color: red;
  margin-top: 10px;
  font-size: 15px;
  font-weight: bold;
}
</style>