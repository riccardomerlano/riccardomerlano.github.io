---
title: RCDC
permalink: /rcdc/
---

<html>
    <head>
        <link href="https://fonts.googleapis.com/css2?family=Permanent+Marker&display=swap" rel="stylesheet"> 
    </head>
    <style>
        .body{
    background-color: black;
}

.centerd {
    text-align: center;
    font-family: 'Permanent Marker', cursive;
}

h1{
    color: darkgreen;
    text-align: center;
    font-size: 150px;
    flex-wrap: wrap;
}

h2{
  color: darkgreen;
  text-align: center;
  font-size: 85px;
  flex-wrap: wrap;
}

.g{
  font-family: 'Permanent Marker', cursive;
  font-size: 85px;
  border-radius: 12px;
  border-color: darkgreen;
  background-color: saddlebrown;
  color: pink;
}

.f1{
    animation: fadeInOut ease-in-out 10s;
}

.f2 {
    animation: fadeIn ease 3s;
}

.breathing {
    -webkit-animation: breathing 7s ease-in-out infinite normal;
    animation: breathing 7s ease-in-out infinite normal;
}

@-webkit-keyframes breathing {
  0% {
    -webkit-transform: scale(0.9);
    transform: scale(0.9);
  }

  /*25% {
    -webkit-transform: scale(1);
    transform: scale(1);
  }

  60% {
    -webkit-transform: scale(0.9);
    transform: scale(0.9);
  }*/

  50% {
    -webkit-transform: scale(1);
    -ms-transform: scale(1);
    transform: scale(1);
  }

  100% {
    -webkit-transform: scale(0.9);
    transform: scale(0.9);
  }
}

@keyframes breathing {
  0% {
    -webkit-transform: scale(0.9);
    -ms-transform: scale(0.9);
    transform: scale(0.9);
  }

  /*25% {
    -webkit-transform: scale(1);
    -ms-transform: scale(1);
    transform: scale(1);
  }

  60% {
    -webkit-transform: scale(0.9);
    -ms-transform: scale(0.9);
    transform: scale(0.9);
  }*/

  50% {
    -webkit-transform: scale(1);
    -ms-transform: scale(1);
    transform: scale(1);
  }

  100% {
    -webkit-transform: scale(0.9);
    -ms-transform: scale(0.9);
    transform: scale(0.9);
  }
}

@keyframes fadeIn {
0% {opacity:0}
100% {opacity:1}
}

@keyframes fadeInOut{
    0% {opacity:0;}
    45% {opacity:1;}
    55% {opacity:1;}
    100% {opacity:0;}
}

@keyframes breath{
    0% {width: 100%; height: 100%;}
    100% {width: 50%; height: 50%;}
}
    </style>
    <script>
        function waterfall(){
    document.getElementById("d").innerHTML = "<h1 class=f1>A new era is beginning</h1>"


    setTimeout(()=>{
        document.getElementById("d").innerHTML = "<h1 class=f1>But the Real Carta Da Culo legend continues</h1>"

        setTimeout(()=>{
            document.getElementById("d").innerHTML = "<h2 class='f2'>Fear the beasts</h2><div class='f3'><img class='breathing' src='/assets/images/penezia3.png' width='65%' height='auto'></div><audio src='/assets/audio/m.mp3' autoplay>";
        }, 10000)

    }, 9800)
}
    </script>
    <body id="d" class="centerd"> <!--onload="waterfall()">-->
        <input class="g" type="button" value="click for RCDC experience" onclick="waterfall()">
    </body>
</html>