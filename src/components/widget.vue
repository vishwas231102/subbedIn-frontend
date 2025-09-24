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
    width: 22vw;
    height: 55vh;
    padding: 10%;
    display: flex;
    margin-left: 1vw;
    margin-right: 1vw;
    margin-bottom: 1vh;
    align-items: center;
    flex-direction: column;
    justify-content: center;
    background-color: transparent;
}

.img{
    width: 5vw;
    height: 10vh;
    margin-top: 2vh;
    margin-bottom: 2vh;
}

.header{
  font-size: 1.5em;
  color: white;
  margin-top: 3.5vh;
  text-align: center;
  margin-bottom: 3.5vh;
  font-family: 'Poppins';
}

.text{
  line-height: 1.8;  
  margin-top: 1vh;
  color: white;
  font-size: 1.25em;
  margin-bottom: 1vh;
  text-align: center;
  font-family: 'Montserrat';
}
</style>