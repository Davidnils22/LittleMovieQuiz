<script>
  import Quiz from './components/Quiz.vue'

  export default {
    components: {
      Quiz,
     
    }
  }
</script>

<template>
   <header>
      <nav class="navbar-container">
        <ul>
          <li class="list"><a href="about.html">About me</a></li>
          <li class="list"><a href="portfolio.html">Portfolio</a></li>
          <li class="list"><a href="gallery.html">Gallery</a></li>
          <li><button class="btnLogin-popup">Login</button></li>
        </ul>
     </nav>
    </header>
<main>
    <section>
        <h2 class="person-title"> Hi, it's me David</h2>
    </section>
</main>
  
  <Quiz />
</template>

<style>
 

body{
    display: flex;
    justify-content: center;
    align-items: center;
    min-height: 100vh;
    background-image: url(../assets/sunset-1373171_1920.jpg);
    background-size: cover;
    background-position: center;
}

header{
    display: flex;
    justify-content: space-between;
    background-color: rgb(174, 54, 178, 0.2);
    position: fixed;
    top: 0;
    left: 0;
    min-width: 100%;
    padding: 20px 100px;
    backdrop-filter: blur(10px);
    align-items: center;
    z-index: 99;
    display: block;
    margin-block-end: 1em;
    margin-inline-start: 0px;
    margin-inline-end: 0px;
    padding-inline-start: 40px;
}

header .navbar-container ul {
    float: right;
    margin-right: 20px;
}

header .navbar-container ul li {
    display: inline-block;
    line-height: 35px;
    margin: 0 5px;
}

header .navbar-container ul li a{
    position: relative;
    font-size: 1.1em;
    color: white;
    text-decoration: none;
    font-style: italic;
    font-weight: 400;
    margin-left: 20px;
    padding: 6px 14px;
    border-radius: 3px;
    text-transform: uppercase;
}
header .navbar-container ul{
    list-style-type: none;
}

header .navbar-container ul li a::after{
    content: '';
    position: absolute;
    left: 0;
    bottom: -6px;
    width: 100%;
    height: 3px;
    border-radius: 5px;
    transform-origin: 50% 90%;
    transform: scaleX(0);
    transition: transform .5s;
    box-shadow: 0 0 10px (255, 255, 255, 0.8);
    background: linear-gradient(to right, #450c4d , #f3f3f3);
}

header .navbar-container ul li a:hover::after{
    transform-origin: left;
    transform: scaleX(0.85);
}

header .navbar-container ul li .btnLogin-popup{
    width: 120px;
    height: 45px;
    margin-left: 80px;
    background: transparent;
    border: solid rgb(201, 183, 183) 2px;
    outline: none;
    border-radius: 10px;
    cursor: pointer;
    transition: background-color 0.7s ease-in-out;
    font-size: 1.2em;
    color: white;
}

header .navbar-container ul li .btnLogin-popup:hover{
    background-color: rgba(0, 0, 0, 0.645);
    color: #fff;
}

.person-title{
    color: rgb(60, 8, 62);
    position: absolute;
    font-size: 4.0rem;
    font-style: italic;
    top: 20%;
    left: 10%;
    transition: color 0.9s ease-in-out;
}
.person-title:hover{
    color: #ffffff5c;
}

.cover_box{
    display: flex;
    justify-content: space-evenly;
    min-height: 450px;
    min-width: 400px;
    border: solid black 2px;
    border-radius: 20px;

}

h2{
    font-size: 2rem;
    text-align: center;
    color: rgb(60, 8, 62);
    margin-right: 50px;
}

.input-box{
    align-items: center;
    padding: 20px;

}
.remember-forgot{
    color: black;
    font-size: .9em;
    font-weight: 500;
    margin: -15px, 0px, 15px;
    display: flex;
    justify-content: space-between;
}
.remember-forgot label input{
    margin-right: 15px;
    color:black;
}
.remember-forgot a {
    font-size: 0.8rem;
    text-decoration: underline;
    margin-right: 20px;
    color: #fff;
}

.login-register p{
    color: red;
    margin-top: 50px;

}
.register-link{
    font-size: 1.2rem;
    margin-left: 30px;
    color: #fff;
}
.btn{

    display: flex;
    justify-content: center;
    width: 200px;
    font-size: 1rem;
    font-weight: bold;
    margin-top: 25px;
    margin-left: 75px;
    border-radius: 25px;
    border: solid black 1px;
    transition: background-color 0.5s ease-in-out;

}
.btn:hover{
    background-color: gray;
    filter: grayscale(60%);
    
}
.icon-close{
    margin: 10px 0 0 10px;

}
.icon-close ion-icon{
    font-size: 25px;
}
  
  
</style>
