<template>
  <div class="page-wrapper">
    <!-- Hero Section -->
    <section class="hero-section">
      <div class="hero-background"></div>
      <div class="container">
        <div class="hero-content">
          <h1 class="hero-title">SubbedIn</h1>
          <div class="hero-subtitle">
            <p>You've spent enough time on the bench,</p>
            <p>get SubbedIn now!</p>
          </div>
        </div>
      </div>
    </section>

    <div style="background: linear-gradient(90deg,black,rgb(110,110,110));">
    <!-- Coming Soon Section -->
    <section class="coming-soon-section">
      <div class="container">
        <div class="section-content">
          <h2 class="section-title">Coming Soon</h2>
          <div class="section-description">
            <p>The ultimate community platform for sports management professionals</p>
            <p>Connect, collaborate and advance your career in sports management</p>
          </div>

          <div class="cta-buttons">
            <button 
              id="enroll" 
              class="btn btn-secondary" 
              :class="{ active: enrollCheck }"
              @click="updateCheck"
            >
              Enroll Now
            </button>
            <button 
              id="leave-suggestion" 
              class="btn btn-secondary" 
              :class="{ active: suggestionCheck }"
              @click="updateCheck"
            >
              Leave a Suggestion
            </button>
          </div>
        </div>
      </div>
    </section>

    <!-- Alert Notification -->
    <transition name="fade">
      <div v-if="alertText" class="alert-notification">
        <div class="alert-content">
          <span>{{ alertText }}</span>
        </div>
      </div>
    </transition>

    <!-- Forms Section -->
    <section class="forms-section" v-if="enrollCheck || suggestionCheck">
      <div class="container">
        <!-- Enrollment Form -->
        <form v-show="enrollCheck" id="enroll-form" class="modern-form" @submit.prevent="sendData">
          <div class="form-header">
            <h2 class="form-title">Join SubbedIn</h2>
            <p class="form-subtitle">Be the first to be notified when SubbedIn launches</p>
          </div>
          
          <div class="form-body">
            <div class="form-group">
              <label for="name" class="form-label">Full Name</label>
              <input 
                id="name" 
                class="form-input" 
                type="text" 
                v-model="name" 
                placeholder="Enter your full name (e.g., John Doe)" 
                required 
              />
            </div>
            
            <div class="form-group">
              <label for="email" class="form-label">Email Address</label>
              <input 
                id="email" 
                class="form-input" 
                type="email" 
                v-model="email" 
                placeholder="Enter your email address (e.g. john@example.com)" 
                required
              />
            </div>
            
            <button class="btn btn-primary form-submit" type="submit">
              Submit Enrollment
            </button>
          </div>
        </form>

        <!-- Suggestion Form -->
        <form v-show="suggestionCheck" id="suggestion-form" class="modern-form" @submit.prevent="sendData">
          <div class="form-header">
            <h2 class="form-title">Share Your Ideas</h2>
            <p class="form-subtitle">Help us improve SubbedIn with your suggestions</p>
          </div>
          
          <div class="form-body">
            <div class="form-group">
              <label for="suggestion-email" class="form-label">Email Address</label>
              <input 
                id="suggestion-email" 
                class="form-input" 
                type="email" 
                v-model="email" 
                placeholder="Enter your email address" 
                required
              />
            </div>
            
            <div class="form-group">
              <label for="suggestion" class="form-label">Your Suggestion</label>
              <textarea 
                id="suggestion" 
                class="form-input form-textarea" 
                v-model="suggestion" 
                placeholder="Share your ideas (e.g. A search bar for new events)" 
                maxlength="250" 
                rows="4"
                required
              ></textarea>
            </div>
            
            <button class="btn btn-primary form-submit" type="submit">
              Submit Suggestion
            </button>
          </div>
        </form>
      </div>
    </section>

    <h1 class="header" style="margin-bottom: 2%;font-size: clamp(2em,4vw,5em);">What’s coming to SubbedIn ?</h1>
    
    <div class="widget-container">
        <widget_card :img_path="job_img" title="Job opportunities" description="Effortlessly discover and apply for sports management opportunities. Streamline your job hunt, explore tailored roles, and connect with top employers all in one place for a smooth, stress-free experience."></widget_card>
        <widget_card :img_path="sessionTalk_img" title="Real conversations" description="Engage in open, transparent conversations about the industry with peers. Share insights, exchange experiences, and build meaningful professional connections that foster learning, growth, and collaboration."></widget_card>
        <widget_card :img_path="network_img" title="Community network" description="Create a strong, valuable network within the sports management community. Connect with professionals, share knowledge and cultivate relationships that support career growth and industry opportunities"></widget_card>
    </div>
    <div class="footer">
      <span class="text" style="font-size: clamp(0.75em,1.25vw,2em);font-weight: bold;text-align: center;">Got a question ? Email us @<span id="contactEmail" class="text" style="color: rgb(5, 75, 170);font-size: clamp(0.75em,1.25vw,2em);font-weight: bold;text-align: center;" @click.prevent="redirectToEmail"> contact@subbedin.com </span></span>
      <div class="socials-container">
        <!-- <button class="social" :style="{ backgroundImage: `url(${meta_logo})` }"></button> -->
        <button class="social" :style="{ backgroundImage: `url(${twitter_logo})` }" @click="redirectToX"></button>
        <button class="social" :style="{ backgroundImage: `url(${insta_logo})` }" @click="redirectToInstagram"></button>
        <button class="social" :style="{ backgroundImage: `url(${linkedin_logo})` }" @click="redirectToLinkedIn"></button>
      </div>
    </div>
  </div>
</div>
</template>

<script>
import axios from 'axios'
import widget_card from './widget.vue'
import job_img from '@/assets/home/job.png'
import meta_logo from '@/assets/home/meta.png'
import insta_logo from '@/assets/home/insta.png'
import network_img from '@/assets/home/network.png'
import twitter_logo from '@/assets/home/twitter.png'
import linkedin_logo from '@/assets/home/linkedin.png'
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
      insta_logo,linkedin_logo,meta_logo,twitter_logo
    }
  },
  methods: {
    updateCheck(event){
      if(event.target.id==='enroll'){
        this.enrollCheck=true;
        this.suggestionCheck=false;
        setTimeout(() => {
          const formsSection = document.querySelector('.forms-section');
          if(formsSection) {
            formsSection.scrollIntoView({
              behavior: 'smooth',
              block: 'start'
            });
          }
        },200)
      }
      else if(event.target.id==='leave-suggestion'){
        this.suggestionCheck=true;
        this.enrollCheck=false;
        setTimeout(() => {
          const formsSection = document.querySelector('.forms-section');
          if(formsSection) {
            formsSection.scrollIntoView({
              behavior: 'smooth',
              block: 'start'
            });
          }
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
    },
    redirectToEmail(){
      window.location.href="mailto:contact@subbedin.com";
    },
    redirectToX(){
      window.location.href=`http://x.com/subbedindotcom`
    },
    redirectToInstagram(){
      window.location.href=`https://www.instagram.com/subbedindotcom/`
    },
    redirectToLinkedIn(){
      window.location.href=`https://www.linkedin.com/company/subbedin/`
    }
  },
  components:{
    widget_card
  }
}
</script>

<style scoped>
/* Page wrapper */
.page-wrapper {
  width: 100%;
  min-height: 100vh;
}

/* Hero Section */
.hero-section {
  position: relative;
  height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  overflow: hidden;
}

.hero-background {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-image: url("../assets/home/theme_bkgd.png");
  background-size: cover;
  background-position: 15% center;
  background-repeat: no-repeat;
  opacity: 0.2;
  z-index: -1;
}

.hero-content {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  text-align: center;
  z-index: 1;
  max-width: 800px;
  width: 100%;
  padding: 0 20px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

.hero-title {
  font-family: 'Poppins', -apple-system, BlinkMacSystemFont, sans-serif;
  font-size: clamp(3rem, 8vw, 6rem);
  font-weight: 800;
  color: white;
  opacity : 0.7;
  margin: 0 auto 0.5rem auto;
  text-shadow: 0 4px 20px rgba(0, 0, 0, 0.3);
  letter-spacing: -0.02em;
  text-align: center;
  width: 100%;
}

.hero-subtitle {
  font-family: 'Poppins', -apple-system, BlinkMacSystemFont, sans-serif;
  font-size: clamp(1rem, 2.5vw, 1.4rem);
  font-weight: 500;
  opacity : 0.7;
  color: rgba(255, 255, 255, 0.9);
  margin: 0 auto 3rem auto;
  line-height: 1.4;
  text-align: center;
  width: 100%;
}

.hero-subtitle p {
  margin: 0.5rem auto;
  text-align: center;
}

/* Coming Soon Section */
.coming-soon-section {
  padding: 1rem 0;
}

.section-content {
  text-align: center;
  max-width: 800px;
  margin: 0 auto;
}

.section-title {
  font-family: 'Poppins', -apple-system, BlinkMacSystemFont, sans-serif;
  font-size: clamp(2.5rem, 6vw, 4rem);
  font-weight: 700;
  color: white;
  margin-bottom: 2rem;
  text-shadow: 0 2px 10px rgba(0, 0, 0, 0.2);
}

.section-description {
  font-size: clamp(1.1rem, 2.5vw, 1.4rem);
  color: rgba(255, 255, 255, 0.8);
  margin-bottom: 3rem;
  line-height: 1.6;
}

.section-description p {
  margin: 1rem 0;
}

/* CTA Buttons */
.cta-buttons {
  display: flex;
  gap: 1.5rem;
  justify-content: center;
  flex-wrap: wrap;
  margin-bottom: 2rem;
}

/* Alert Notification */
.alert-notification {
  position: fixed;
  top: 2rem;
  left: 50%;
  transform: translateX(-50%);
  z-index: 1000;
  max-width: 90%;
  width: auto;
}

.alert-content {
  background: rgba(255, 255, 255, 0.95);
  backdrop-filter: blur(20px);
  padding: 1rem 2rem;
  border-radius: 12px;
  box-shadow: 0 8px 32px rgba(0, 0, 0, 0.2);
  border: 1px solid rgba(255, 255, 255, 0.3);
}

.alert-content span {
  color: #333;
  font-weight: 600;
  font-size: 1rem;
}

/* Forms Section */
.forms-section {
  padding: 1rem 0;
}

.modern-form {
  max-width: 450px;
  min-height: 600px;
  margin: 0 auto;
  background: rgba(255, 255, 255, 0.1);
  backdrop-filter: blur(30px);
  border-radius: 24px;
  padding: 3.5rem 2.5rem;
  border: 1px solid rgba(255, 255, 255, 0.2);
  box-shadow: 0 20px 60px rgba(0, 0, 0, 0.2);
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

.form-header {
  text-align: center;
  margin-bottom: 3rem;
  flex-shrink: 0;
}

.form-title {
  font-family: 'Poppins', -apple-system, BlinkMacSystemFont, sans-serif;
  font-size: clamp(1.8rem, 4vw, 2.2rem);
  font-weight: 700;
  color: white;
  margin-bottom: 1.2rem;
}

.form-subtitle {
  font-size: clamp(0.95rem, 2vw, 1.1rem);
  color: rgba(255, 255, 255, 0.8);
  line-height: 1.5;
}

.form-body {
  width: 100%;
  flex-grow: 1;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

.form-submit {
  width: 100%;
  margin-top: 2rem;
  font-size: 1.1rem;
  font-weight: 600;
  flex-shrink: 0;
}

/* Features Section */
.header {
  font-family: 'Poppins', -apple-system, BlinkMacSystemFont, sans-serif;
  font-size: clamp(2rem, 5vw, 3.5rem);
  font-weight: 700;
  color: white;
  text-align: center;
  margin: 4rem 0 3rem;
  text-shadow: 0 2px 10px rgba(0, 0, 0, 0.3);
  padding: 0 1rem;
}

.widget-container {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
  gap: 2rem;
  max-width: 1200px;
  margin: 0 auto;
  padding: 2rem 1rem;
}

/* Footer */
.footer {
  padding: 4rem 0 2rem;
  text-align: center;
}

.footer .text {
  color: white;
  font-size: clamp(1rem, 2vw, 1.3rem);
  margin-bottom: 2rem;
  line-height: 1.6;
}

#contactEmail {
  color: #667eea;
  transition: all 0.3s ease;
  cursor: pointer;
}

#contactEmail:hover {
  cursor: pointer;
}

.socials-container {
  display: flex;
  justify-content: center;
  gap: 1.5rem;
  flex-wrap: wrap;
  margin-top: 2rem;
}

.social {
  width: 48px;
  height: 48px;
  border: none;
  border-radius: 12px;
  background-color: rgba(255, 255, 255, 0.1);
  background-size: 24px;
  background-position: center;
  background-repeat: no-repeat;
  backdrop-filter: blur(20px);
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
  cursor: pointer;
  border: 1px solid rgba(255, 255, 255, 0.2);
}

.social:hover {
  background-color: rgba(255, 255, 255, 0.2);
  transform: translateY(-3px);
  box-shadow: 0 8px 25px rgba(0, 0, 0, 0.2);
}

/* Responsive Design */
@media (max-width: 768px) {
  .hero-content {
    padding: 0 1rem;
    max-width: 90%;
    align-items: center;
    justify-content: center;
  }
  
  .cta-buttons {
    flex-direction: column;
    align-items: center;
    gap: 1rem;
  }
  
  .cta-buttons .btn {
    width: 100%;
    max-width: 300px;
  }
  
  .modern-form {
    margin: 0 1rem;
    padding: 2.5rem 1.8rem;
    max-width: 400px;
    min-height: 550px;
  }
  
  .widget-container {
    grid-template-columns: 1fr;
    gap: 1.5rem;
    padding: 1rem;
  }
  
  .socials-container {
    gap: 1rem;
  }
  
  .social {
    width: 44px;
    height: 44px;
  }
}

@media (max-width: 480px) {
  .hero-section {
    min-height: 90vh;
  }
  
  .coming-soon-section {
    padding: 4rem 0;
  }
  
  .forms-section {
    padding: 3rem 0;
  }
  
  .modern-form {
    padding: 2rem 1.2rem;
    max-width: 350px;
    min-height: 500px;
  }
  
  .footer {
    padding: 3rem 0 1.5rem;
  }
  
  .alert-notification {
    top: 1rem;
    max-width: 95%;
  }
  
  .alert-content {
    padding: 0.8rem 1.5rem;
  }
}

/* Animation improvements */
.fade-enter-from, .fade-leave-to {
  opacity: 0;
}

.fade-enter-active, .fade-leave-active {
  transition: opacity 0.6s cubic-bezier(0.4, 0, 0.2, 1);
}

/* Accessibility improvements */
@media (prefers-reduced-motion: reduce) {
  .social:hover {
    transform: none;
  }
  
  .btn-primary:hover {
    transform: none;
  }
  
  .form-input:focus {
    transform: none;
  }
}

/* High contrast mode support */
@media (prefers-contrast: high) {
  .hero-title,
  .section-title,
  .form-title {
    text-shadow: none;
  }
  
  .modern-form {
    border: 2px solid white;
  }
}
</style>
