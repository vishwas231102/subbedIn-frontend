<template>
  <div class="container">
    <div id="theme">
      <h1 class="header" style="font-size: clamp(3.5em,10vw,10em);opacity: 0.85;margin-top: 1vh;margin-bottom: 1vh;">SubbedIn</h1>
        <p class="text" style="font-style: italic;font-weight: bold;font-size: clamp(0.85em,2vw,5em);opacity: 0.85;text-align: center;margin: 0%;">You've spent enough time on the bench,</p>
        <p class="text" style="font-style: italic;font-weight: bold;font-size: clamp(0.85em,2vw,5em);opacity: 0.85;text-align: center;margin: 0%;">get SubbedIn now!</p>
    </div>

    <h1 class="header" style="font-size: clamp(2em,4vw,5em);">Coming Soon</h1>
    <p class="text" style="text-align: center;margin-right: 1vh;margin-left: 1vw;font-size: clamp(0.75em,1.5vw,5em)">The ultimate community platform for sports management professionals</p>
    <p class="text" style="text-align: center;margin-right: 1vh;margin-left: 1vw;font-size: clamp(0.75em,1.5vw,5em)">Connect, collaborate and advance your career in sports management</p>

    <div class="btn-container">
        <button id="enroll" class="btns" @click="updateCheck">Enroll now</button>
        <button id="leave-suggestion" class="btns" @click="updateCheck">Leave a suggestion</button>
    </div>

    <transition name="fade">
      <div v-if="alertText" id="alert">
        <span>{{ alertText }}</span>
    </div>
    </transition>

    <form v-show="enrollCheck" id="enroll-form" class="form" @submit.prevent="sendData">
        <h1 class="header" style="font-size: clamp(1em,5.5vw,2em);">Enroll to SubbedIn</h1>
        <span class="text" style="font-size: clamp(0.5em,3vw,1em);font-weight: medium;">Be the first to be notified when SubbedIn launches</span><br>
        <div class="input-container">
          <label for="name" class="text" style="font-size: clamp(0.5em,3vw,1em);font-weight: bold;">Full name</label>
          <input id="name" class="input" type="text" v-model="name" placeholder="Enter you full name here ( e.g John Doe )" style="font-size: clamp(0.5em,3vw,0.85em);" required />
        </div>
        <div class="input-container">
          <label for="email" class="text" style="font-size: clamp(0.5em,3vw,1em);font-weight: bold;">Email address</label>
          <input id="email" class="input" type="email" v-model="email" placeholder="Enter your email address here ( e.g johndoe@xyz.com )"
          style="font-size: clamp(0.5em,3vw,0.85em);" required/>
        </div>
        <button class="submit-btn btns" type="submit">Click to submit</button>
    </form>

    <form v-show="suggestionCheck" id="suggestion-form" class="form" @submit.prevent="sendData">
      <h1 class="header" style="font-size: clamp(1em,5.5vw,2em);">Leave a suggestion</h1>
      <span class="text" style="font-size: clamp(0.5em,3vw,1em);font-weight: medium;">Leave your suggestions to help us improve SubbedIn</span><br>
      <div class="input-container">
        <label for="email" class="text" style="font-size: clamp(0.5em,3vw,1em);font-weight: bold;">Email address</label>
        <input id="email" class="input" type="email" v-model="email" placeholder="Enter your email address here ( e.g johndoe@xyz.com )"
        style="font-size: clamp(0.5em,3vw,0.85em);" required/>
      </div>
      <div class="input-container">
        <label for="suggestion" class="text" style="font-size: clamp(0.5em,3vw,1em);font-weight: bold;">Your suggestion</label>
        <input id="suggestion" class="input" type="text" v-model="suggestion" placeholder="Enter you suggestion here ( e.g A search bar for new events )" style="font-size: clamp(0.5em,3vw,0.85em);" maxlength="250" required>
        </div>
        <button class="submit-btn btns" type="submit">Click to submit</button>
    </form>

    <h1 class="header" style="margin-bottom: 0%;font-size: clamp(2em,4vw,5em);">What’s coming to SubbedIn ?</h1>
    
    <div class="widget-container">
        <widget_card :img_path="job_img" title="Job opportunities" description="Effortlessly discover and apply for sports management opportunities. Streamline your job hunt, explore tailored roles, and connect with top employers—all in one place for a smooth, stress-free experience."></widget_card>
        <widget_card :img_path="sessionTalk_img" title="Real conversations" description="Engage in open, transparent conversations about the industry with peers. Share insights, exchange experiences, and build meaningful professional connections that foster learning, growth, and collaboration."></widget_card>
        <widget_card :img_path="network_img" title="Community network" description="Create a strong, valuable network within the sports management community. Connect with professionals, share knowledge, foster collaborations, and cultivate relationships that support career growth and industry opportunities."></widget_card>
    </div>

    <span id="footer" class="text" style="font-size: clamp(0.55em,1.25vw,2em);font-weight: bold;">Got a question ? We are just an email away :<span style="color: rgb(5, 70, 140);"> contact@subbedin.com </span></span>
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
  opacity: 0.35;
  top: 0; left: 0;
  position: absolute;
  right: 0; bottom: 0;
  background-size: cover;
  background-position: 15%;
  background-repeat: no-repeat;
  background-image: url("../assets/home/theme_bkgd.png");
}

#theme>h1{
  color: white;
  position: relative;
}

.header{
  margin-top: 2vh;
  font-weight: bold;
  margin-bottom: 2vh;
  text-align: center;
  background-clip: text;
  font-family: 'Poppins';
  background-color: white;
  -webkit-background-clip: text;
  font-size: clamp(1em,10vw,4em);
  -webkit-text-fill-color: transparent;
}

.text{
  margin-top: 1vh;
  color: white;
  margin-bottom: 1vh;
  font-family: 'Montserrat';
}

.btn-container{
  gap: 0.5em;
  width: 100%;
  display: flex;
  margin-top : 3.5vh;
  flex-direction: row;
  align-items: center;
  margin-bottom: 3.5vh;
  justify-content: center;
}

.btns{
  border: none;
  min-height: 8vh;
  min-width : 12vw;
  font-weight: 650;
  color: white;
  margin-left: 1.5vw;
  margin-right: 1.5vw;
  font-family: 'Montserrat';
  background-color: transparent;
  transition-property: opacity 0.5s;
  font-size: clamp(0.75em,1vw,1.25em);
  border-bottom: 0.15em solid white;
}

.btns:hover{
  opacity: 0.65;
  cursor: pointer;
}

#alert{
  top: 0.5vh;
  height: 6vh;
  width: 99.5%;
  display: flex;
  position: fixed;
  flex-direction: row;
  align-items: center;
  justify-content: center;
  background-color: whitesmoke;
}

#alert>span{
  font-weight: bold;
  color: darkgrey;
  font-family: 'Montserrat';
  font-size: clamp(0.5em,1vw,1em);
}

.fade-enter-from, .fade-leave-to{
  opacity: 0;
}

.fade-enter-active, .fade-leave-active{
  transition: opacity 0.5s ease;
}

.form{
  display: flex;
  min-width: 28vw;
  margin-left: 5vw;
  margin-right: 5vw;
  margin-top: 2.5vh;
  margin-bottom: 4vh;
  min-height: 59.5vh;
  border-radius: 10%;
  align-items: center;
  flex-direction: column;
  justify-content: flex-start;
  padding: clamp(1.75em,5vw,3em);
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
  padding: 0%;
  border: none;
  margin-top: 2vh;
  color: grey;
  min-height: 8vh;
  margin-bottom: 4.5vh;
  background: white;
}

.widget-container{
  width: 95%;
  display: flex;
  margin-top: 5.5vh;
  align-items: center;
  margin-bottom: 5.5vh;
  flex-direction: column;
  justify-content: center;
}

#footer{
  margin-top: 5vh;
  margin-bottom: 5vh;
}
</style>
