<template>
    <form class="form" @submit.prevent="handleSubmit">
        <label>Email</label>
        <input type="email" required v-model="email" >

        <label>Password</label>
        <input type="password" required v-model="password">
        <div v-if="passError" class="error">{{passError}}</div>

        <label>Role:</label>
        <select v-model="role" >
            <option value="developer">Web Developer</option>
            <option value="designer">Web Designer</option>
        </select>

        <label>Skills</label>
        <input type="text" @keyup.alt="addSkill" v-model="tempSkill">
        <div class="skill" v-for="skill in skills" :key="skill" >
            <span @click="deleteSkill(skill)">{{skill}}</span>
        </div>

        <div class="terms">
            <input type="checkbox" v-model="terms" required>
            <label> Terms & Conditions Applied</label>
        </div>    

        <div class="submit">
            <button>Create An Account</button>
        </div>
    </form>
    <div>
        <p>email: {{email}}</p>
        <p>password: {{password}}</p>
        <p>role: {{role}}</p>
        <p>Terms Accepted: {{terms}}</p>
    </div>
</template>

<script>
export default {
    name:"Form", 
    data() {
        return {
            email: '',
            password: '',
            role: '',
            terms: false,
            tempSkill: "",
            skills: [],
            passError: ""
        }
    },
    methods: {
        addSkill(e) {
            if (e.key === "," && this.tempSkill){
                if(!this.skills.includes(this.tempSkill)){
                    this.skills.push(this.tempSkill)
                }
                this.tempSkill = ''
            }            
        },
        deleteSkill(skill) {            
            this.skills = this.skills.filter(item => item !== skill)
        },
        handleSubmit() {
            // console.log("form Submitted");
            this.passError = this.passError.length > 5 ? '' : "Password must be atleast 6 chars long"
            if(!this.passError){
                console.log("email :", this.email);
                console.log("password :", this.password);
                console.log("role :", this.role);
                console.log("skills :", this.skills);
                console.log("terms accepted :", this.terms);
            }
        }
    }
}
</script>

<style>
.form{
    width: 450px;
    background: white;
    padding: 40px;
    border-radius: 10px;
    margin: 20px auto;
    text-align: left;
}
label{
    display: inline-block;
    color: #aaa;
    margin: 25px 0 15px;
    font-size: 0.6em;
    text-transform: uppercase;
    letter-spacing: 1px;
    font-weight: bold;
}
input, select{
    display: block;
    width: 100%;
    border: none;
    padding: 10px  6px;
    margin-top: 5px;
    box-sizing: border-box;
    border-bottom: 1px solid #ddd;
    color: #555;
}
input[type="checkbox"] {
    display: inline-block;
    width: 16px;
    margin-right: 10px;
    position: relative;
    top: 2px;
}
.skill {
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
    outline: none;
}
.submit{
    text-align: center;
}
.error{
    color: #ff0062;
    margin-top: 10px;
    font-size: 0.8em;
    font-weight: bold;
}
</style>