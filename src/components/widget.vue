<template>
    <div class="container">
        <img class="img" :src="img_path" alt="img">
        <h1 class="header">{{ title }}</h1>
        <span class="text">{{ description }}</span>
    </div>
</template>

<script>
export default{
    name : 'widget_card',
    props : ['img_path','title', 'description'],
}
</script>

<style scoped>
.container{
    display: flex;
    min-width: 25vw;
    min-height: 40vh;
    margin-top: 4.5vh;
    margin-left: 1.5vw;
    margin-right: 1.5vw;
    align-items: center;
    margin-bottom: 4.55vh;
    flex-direction: column;
    justify-content: center;
    padding: clamp(0.5em,1vw,2em);
    background-color: transparent;
}

.img{
    margin-top: 2.5vh;
    margin-bottom: 2.5vh;
    width: clamp(4em,5vw,5em);
    height: clamp(2em,9vh,5em);
}

.header{
  color: white;
  margin-top: 3.5vh;
  text-align: center;
  margin-bottom: 3.5vh;
  font-family: 'Poppins';
  font-size: clamp(1em,2vw,2em);
}

.text{
  margin-top: 1vh;
  line-height: 1.8;  
  color: white;
  margin-bottom: 1vh;
  text-align: center;
  font-family: 'Montserrat';
  width: clamp(25em,20vw,30em); 
  font-size: clamp(0.8em,1.5vw,2em);
}
</style>