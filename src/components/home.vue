<template>
  <div class="container">
    <div id="theme">
      <h1 class="header" style="font-size: 10em;opacity: 0.5;">SubbedIn</h1>
      <p class="text" style="font-style: italic;font-size: 1.75em;margin-top: 2.5vh;margin-bottom: 5vh;opacity: 0.5;">You've spent enough time on the bench, get SubbedIn now !</p>
    </div>
    <h1 class="header">Coming Soon</h1>
    <p class="text">The ultimate community platform for sports management professionals</p>
    <p class="text">Connect, collaborate and advance your career in sports management</p>
    <div class="btn-container">
        <button id="enroll" class="btns" @click="updateCheck">Enroll now</button>
        <button id="leave-suggestion" class="btns" @click="updateCheck">Leave a suggestion</button>
    </div>
    <transition name="fade">
      <div id="alert">
        <span>{{ alertText }}</span>
    </div>
    </transition>
    <form v-show="enrollCheck" id="enroll-form" class="form" @submit.prevent="sendData">
        <h1 class="header" style="font-size: 2em;">Enroll to SubbedIn</h1>
        <span class="text" style="font-size: 1em;font-weight: medium;">Be the first to be notified when SubbedIn launches !</span><br>
        <div class="input-container">
          <label for="name" class="text" style="font-size: 1em;font-weight: bold;">Full name</label>
          <input id="name" class="input" type="text" v-model="name" placeholder="Enter you full name here ( e.g John Doe )" required />
        </div>
        <div class="input-container">
          <label for="email" class="text" style="font-size: 1em;font-weight: bold;">Email address</label>
          <input id="email" class="input" type="email" v-model="email" placeholder="Enter your email address here ( e.g johndoe@xyz.com )" required/>
        </div>
        <button class="submit-btn btns" type="submit">Click to submit</button>
    </form>
    <form v-show="suggestionCheck" id="suggestion-form" class="form" @submit.prevent="sendData">
      <h1 class="header" style="font-size: 2em;">Leave a suggestion</h1>
      <span class="text" style="font-size: 1em;font-weight: medium;">Leave a suggestion to help us grow SubbedIn !</span><br>
      <div class="input-container">
        <label for="email" class="text" style="font-size: 1em;font-weight: bold;">Email address</label>
        <input id="email" class="input" type="email" v-model="email" placeholder="Enter your email address here ( e.g johndoe@xyz.com )" required/>
      </div>
      <div class="input-container">
        <label for="suggestion" class="text" style="font-size: 1em;font-weight: bold;">Your suggestion</label>
        <input id="suggestion" class="input" type="text" v-model="suggestion" placeholder="Enter you suggestion here ( Character limit : 250 )" maxlength="250" required>
        </div>
        <button class="submit-btn btns" type="submit">Click to submit</button>
    </form>
    <h1 class="header" style="margin-bottom: 0%;">What's coming to SubbedIn ?</h1>
    <div class="widget-container">
        <widget_card :img_path="job_img" title="Job opportunities" description="Seamlessly search and apply for sports management jobs with ease"></widget_card>
        <widget_card :img_path="sessionTalk_img" title="Real conversations" description="Have honest discussions about the industry with fellow professionals"></widget_card>
        <widget_card :img_path="network_img" title="Community network" description="Build a meaningful network within the sports management community"></widget_card>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import widget_card from './widget.vue'
import job_img from '@/assets/home/job.png'
import network_img from '@/assets/home/network.png'
import sessionTalk_img from '@/assets/home/sessionTalk.png'

export default{
  name : 'home_page',
  data(){
    return{
      name : null,
      email : null,
      alertText : null,
      suggestion : null,
      enrollCheck : true,
      suggestionCheck : false,
      job_img,sessionTalk_img,network_img,
    }
  },
  methods: {
    updateCheck(event){
      if(event.target.id==='enroll'){
        this.enrollCheck=true;
        this.suggestionCheck=false;
        setTimeout(() => {
          document.querySelector('.btn-container')
          .scrollIntoView({
          behavior: 'smooth',
          block: 'start'})
        },200)
      }
      else if(event.target.id==='leave-suggestion'){
        this.suggestionCheck=true;
        this.enrollCheck=false;
        setTimeout(() => {
          document.querySelector('.btn-container')
          .scrollIntoView({
          behavior: 'smooth',
          block: 'start'})
        },200)
      }
    },
    async sendData(event){
      if(event.target.id==='enroll-form'){
        const response = await axios.post(
        `${process.env.VUE_APP_FASTAPI_BASE_URL}/enroll`,
        { email : this.email, 
          name : this.name
        })
        this.alertText = response.data.message
        setTimeout(() => {
          this.alertText = null
        },5000);
      }
      else if(event.target.id==='suggestion-form'){
        const response = await axios.post(
        `${process.env.VUE_APP_FASTAPI_BASE_URL}/submit_suggestion`,
        { email : this.email, 
          suggestion : this.suggestion
        })
        this.alertText = response.data.message
        setTimeout(() => {
          this.alertText = null
        },5000);
      }
    }
  },
  components:{
    widget_card
  }
}
</script>

<style scoped>
#logo{
  width: 35%;
  height: 10%;
}

.container{
  display: flex;
  align-items: center;
  flex-direction: column;
  justify-content: center;
}

#theme{
  width: 100%;
  height: 100vh;
  display: flex;
  margin-bottom: 3vh;
  position: relative;
  align-items: center;
  flex-direction: column;
  justify-content: center;
}

#theme::before{
  content: "";
  opacity: 0.25;
  top: 0; left: 0;
  position: absolute;
  right: 0; bottom: 0;
  background-size: cover;
  background-position: center;
  background-repeat: no-repeat;
  background-image: url("../assets/home/theme_bkgd.png");
}

#theme>h1{
  color: white;
  position: relative;
}

.header{
  font-size: 4em;
  margin-top: 3vh;
  margin-top: 3vh;
  font-weight: bold;
  margin-bottom: 3vh;
  text-align: center;
  background-clip: text;
  font-family: 'Poppins';
  background-color: white;
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}

.text{
  color: white;
  font-size: 1.25em;
  margin-top: 1vh;
  margin-bottom: 1vh;
  font-family: 'Montserrat';
}

.btn-container{
  display: flex;
  margin-top : 5.5vh;
  margin-bottom: 5.5vh;
  flex-direction: row;
  align-items: center;
  justify-content: center;
}

.btns{
  width: 15vw;
  height: 8vh;
  border: none;
  font-weight: 650;
  color: white;
  font-size: 1em;
  margin-left: 1.5vw;
  margin-right: 1.5vw;
  font-family: 'Montserrat';
  background-color: transparent;
  transition-property: opacity 0.5s;
  border-bottom: 0.15em solid white;
}

.btns:hover{
  opacity: 0.65;
  cursor: pointer;
}

#alert{
  top: 0.5vh;
  height: 5vh;
  width: 99.5%;
  display: flex;
  position: fixed;
  flex-direction: row;
  align-items: center;
  justify-content: center;
  background-color: whitesmoke;
}

#alert>span{
  font-size: 1em;
  font-weight: bold;
  color: darkgrey;
  font-family: 'Montserrat';
}

.fade-enter-from, .fade-leave-to{
  opacity: 0;
}

.fade-enter-active, .fade-leave-active{
  transition: opacity 1s ease;
}

.form{
  padding: 3.5%;
  width: 27.5vw;
  display: flex;
  height: 64.5vh;
  margin-top: 2.5vh;
  margin-bottom: 5vh;
  border-radius: 10%;
  align-items: center;
  flex-direction: column;
  justify-content: flex-start;
  background: linear-gradient(
  90deg,
  rgb(35, 35, 35),
  rgb(100,100,100)
  );
}

.input-container{
  width: 100%;
  display: flex;
  margin-top: 2vh;
  margin-bottom: 2vh;
  flex-direction: column;
  justify-content: center;
  align-items: flex-start;
}

.input{
  width: 100%;
  height: 5vh;
  padding: 0%;
  border: none;
  outline: none;
  color: white;
  font-family: 'Montserrat';
  background-color: transparent;
  border-bottom: 0.1em solid white;
}

.submit-btn{
  margin: 0%;
  width: 100%;
  height: 7.5vh;
  padding: 0%;
  border: none;
  margin-top: 2vh;
  color: grey;
  margin-bottom: 1vh;
  background: white;
}

.widget-container{
  width: 90%;
  display: grid;
  margin-top: 2.5vh;
  margin-bottom: 5vh;
  grid-template-columns: repeat(3, 1fr);
}
</style>
