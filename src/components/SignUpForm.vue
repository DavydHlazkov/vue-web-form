<template>
  <form @submit.prevent="handleSubmit">
    <label>Email:</label>
    <input type="email" required v-model="email" />
    <label>Password:</label>
    <input type="password" required v-model="password" />
    <p>{{ passwordError }}</p>
    <label>Role:</label>
    <select v-model="role">
      <option value="developer">Web Developer</option>
      <option value="designer">Web Designer</option>
      <option value="qa">QA</option>
    </select>
    <label>Skills:</label>
    <input type="text" v-model="tempSkills" @keyup="addSkill" />
    <div
      class="pill"
      v-for="skill in skills"
      :key="skill"
      @click="deleteSkill(skill)"
    >
      {{ skill }}
    </div>
    <div class="terms">
      <input type="checkbox" required v-model="terms" />
      <label>Accept terms and conditionals</label>
    </div>
    <div class="submuit">
      <button>Create an account</button>
    </div>
  </form>
  <p>Email: {{ email }}</p>
  <p>Password: {{ password }}</p>
  <p>Position: {{ role }}</p>
  <p>Terms: {{ terms ? "accept" : "don't accept" }}</p>
</template>

<script>
export default {
  data() {
    return {
      email: "",
      password: "",
      role: "developer",
      terms: true,
      tempSkills: "",
      skills: [],
      passwordError: "",
    };
  },
  methods: {
    addSkill(e) {
      if (e.key === "," && this.tempSkills && this.tempSkills !== ",") {
        if (!this.skills.includes(this.tempSkills)) {
          this.skills.push(this.tempSkills.split(",")[0]);
        }

        this.tempSkills = "";
      }
    },
    deleteSkill(skill) {
      this.skills = this.skills.filter((el) => el !== skill);
    },
    handleSubmit() {
      this.passwordError =
        this.password.length > 5 ? "" : "Password is too short";
    },
  },
};
</script>

<style>
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
  font-size: 0.6em;
  text-transform: uppercase;
  font-weight: bold;
}

input,
select {
  display: block;
  padding: 10px 6px;
  width: 100%;
  box-sizing: border-box;
  border: none;
  border-bottom: 1px solid #ddd;
  color: #555;
}

input[type="checkbox"] {
  display: inline-block;
  width: 16px;
  margin: 0 10px 0 0;
  position: relative;
  top: 2px;
}
.persons {
  display: flex;
  flex-direction: row;
  justify-content: center;
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
  background: #0b6dff;
  border: 0;
  padding: 10px 20px;
  margin-top: 20px;
  margin: 20px auto 0px auto;
  color: white;
  border-radius: 20px;
  cursor: pointer;
}
</style>
