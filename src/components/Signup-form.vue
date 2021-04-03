<template>
  <div class="signup-form">
    <form @submit.prevent="handleSubmitEvent">
      <label>Email :</label>
      <input type="email" required v-model="email" />

      <label>Password :</label>
      <input type="password" required v-model="password" />
        <div class="error" v-if="passwordError">
            {{passwordError}}
        </div>

      <label>Role :</label>
      <select v-model="role">
        <option value="developer">Web Developer</option>
        <option value="designer">Web Designer</option>
      </select>

      <label>Skills (if you have more than 1 skill you must alt + , to add new skill):</label>
      <input type="text" v-model="tempSkill" @keydown="addSkill" />
      <div v-for="skill in skills" :key="skill" class="pill" >
        <!-- เราสามารถใช้ skill จาก v-for ที่วนลูปได้เลย เพราะมันรู้ว่าแต่ละตัวอยู่ไหน -->
        <span @click="deleteSkill(skill)">{{ skill }}</span>
      </div>
      <div class="terms">
        <input type="checkbox" required v-model="terms" />
        <label>Accept terms and conditions</label>
      </div>
      <div class="submit">
          <button>Create an Account</button>
      </div>
      <!--  
      /** ถ้าหากมี checkbox หลายช่องจะต้องใส่ value ลงไปด้วยเพื่อระบุว่าช่องๆนั้นคืออะไร
      <div>
        <input type="checkbox" value="Luigi" v-model="names" />
        <label>Luigi</label>
      </div>
      <div>
        <input type="checkbox" value="Yoshi" v-model="names" />
        <label>Yoshi</label>
      </div>
      <div>
        <input type="checkbox" value="Mario" v-model="names" />
        <label>Mario</label>
      </div>
      */ -->
    </form>
    <p>Role : {{ role }}</p>
    <p>Terms Accepted: {{ terms }}</p>
    <!-- <p>Names : {{ names }}</p> -->
  </div>
</template>

<script>
export default {
  data() {
    return {
      email: "",
      password: "",
      role: "designer",
      terms: false,
      skills: [],
      tempSkill: "",
      passwordError : '',
      //   names: []
    };
  },
  methods: {
    addSkill(e) {
    //   console.log(e);
      if (e.key === "," && this.tempSkill) {
        //   Check every array in skills that have tempSkill
        if (!this.skills.includes(this.tempSkill)) {
          this.skills.push(this.tempSkill);
        //   console.log(this.skills);
        }
          this.tempSkill = "";

      }
    },
    deleteSkill(skill){
        this.skills = this.skills.filter((item)=>{
            // ถ้า skill ที่รับเข้ามาไม่ตรงกับ item จะ return true ทำให้ยังเก็บไว้
            // แต่ถ้า skill ที่รับเข้ามาเท่ากับ item จะ return false (filter ทำให้สิ่งที่ return false หายไป)
            return skill!==item
        })
    },
    handleSubmitEvent(){
        console.log('Form Submit')
        // Validate Password
        // เหมือนเป็นการทำ if แบบสั้นๆ         ด้านซ้ายจะเป็นTrue    ด้านขวาเป็น false
        this.passwordError = this.password.length > 5 ? '' : 'Password must at least 6 characters long'
        if(!this.passwordError){
            console.log(this.email)
            console.log(this.password)
            console.log(this.role)
            console.log(this.terms)
            console.log(this.skills)
        }
    }
  }
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
  letter-spacing: 1px;
  font-weight: bold;
}
input,
select {
  color: #555;
  display: block;
  padding: 10px 6px;
  width: 100%;
  box-sizing: border-box;
  border: none;
  border-bottom: 1px solid #ddd;
}
input[type="checkbox"] {
  display: inline-block;
  width: 16px;
  margin: 0 10px 0 0;
  position: relative;
  top: 2px;
}
.pill{
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
    color: #ff0a62;
    margin-top: 10px;
    font-size: 0.8em;
    font-weight: bold;
}
</style>