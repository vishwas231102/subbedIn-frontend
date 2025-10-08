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
.container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: flex-start;
  padding: 2.5rem 2rem;
  background: rgba(255, 255, 255, 0.1);
  backdrop-filter: blur(30px);
  border-radius: 24px;
  border: 1px solid rgba(255, 255, 255, 0.2);
  box-shadow: 0 20px 60px rgba(0, 0, 0, 0.15);
  transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
  height: 100%;
  min-height: 350px;
  position: relative;
  overflow: hidden;
}

.container::before {
  content: '';
  position: absolute;
  top: 0;
  left: -100%;
  width: 100%;
  height: 100%;
  background: linear-gradient(90deg, transparent, rgba(255,255,255,0.1), transparent);
  transition: left 0.6s;
}

.container:hover::before {
  left: 100%;
}

.container:hover {
  transform: translateY(-8px);
  box-shadow: 0 25px 80px rgba(0, 0, 0, 0.25);
  border-color: rgba(255, 255, 255, 0.3);
}

.img {
  width: 80px;
  height: 80px;
  margin-bottom: 2rem;
  object-fit: contain;
  filter: brightness(1.1);
  transition: all 0.3s ease;
}

.container:hover .img {
  transform: scale(1.1);
  filter: brightness(1.3);
}

.header {
  font-family: 'Poppins', -apple-system, BlinkMacSystemFont, sans-serif;
  color: white;
  font-size: clamp(1.1rem, 2vw, 1.4rem);
  font-weight: 700;
  text-align: center;
  margin-bottom: 1.5rem;
  line-height: 1.3;
  letter-spacing: -0.01em;
}

.text {
  color: rgba(255, 255, 255, 0.9);
  font-size: clamp(0.85rem, 1.4vw, 0.95rem);
  line-height: 1.7;
  text-align: center;
  font-weight: 400;
  max-width: 100%;
  margin: 0;
}

/* Responsive adjustments */
@media (max-width: 768px) {
  .container {
    padding: 2rem 1.5rem;
    min-height: 300px;
  }
  
  .img {
    width: 64px;
    height: 64px;
    margin-bottom: 1.5rem;
  }
  
  .header {
    margin-bottom: 1rem;
  }
}

@media (max-width: 480px) {
  .container {
    padding: 1.5rem 1.25rem;
    min-height: 280px;
  }
  
  .img {
    width: 56px;
    height: 56px;
    margin-bottom: 1rem;
  }
}

/* Accessibility improvements */
@media (prefers-reduced-motion: reduce) {
  .container {
    transition: none;
  }
  
  .container:hover {
    transform: none;
  }
  
  .container::before {
    display: none;
  }
  
  .img {
    transition: none;
  }
  
  .container:hover .img {
    transform: none;
  }
}

/* High contrast mode support */
@media (prefers-contrast: high) {
  .container {
    border: 2px solid white;
    background: rgba(0, 0, 0, 0.8);
  }
  
  .text {
    color: white;
  }
}
</style>