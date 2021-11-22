<template>

<header>

  <img src="https://minibladet.se/wp-content/uploads/2017/11/Pyramiderna.jpg" alt="" id="huvudbild">
  <h1 id="rubrik">Välkommen till BurgerOnline</h1>
</header>
<main>
  <section class="väljburgare">
    <h3> välj burgare </h3>
    <p> här väljer du burgare </p>
    <div class="wrapper">
      <Burger v-for="burger in burgers"
              v-bind:burger="burger"
              v-bind:key="burger.name"
              v-on:orderedBurger="addToOrder($event)" />

    </div>

  </section>


  <section id="contact" class="kunduppgifter">


    <h3>kunduppgifter </h3>
    <p> fyll i dina uppgifter </p>
    <form class="" action="index.html" method="post">
      <p>
        <label for="firstname">Full name </label><br>
        <input type="text" id="firstname" v-model="fn" required="required" placeholder="first and lastname">
      </p>

      <p>
        <label for="email">E-mail</label><br>
        <input type="email" id="email" v-model="em" required="required" placeholder="E-mail address">
      </p>

    </form>

    <p>
      <label for="recipient">payment</label>
      <select id="recipient" v-model="rcp">
        <option>pengar</option>
        <option>kort</option>
        <option>swish</option>
        <option>paypal</option>
        <option>klarna</option>
      </select>
    </p>
    <div>
      <p>Kön</p>
      <input type="radio" id="huey1" v-model="gender" value="man">
      <label for="man">man</label>
      <input type="radio" id="huey2" v-model="gender" value="kvinna">
      <label for="kvinna">kvinna</label>
      <input type="radio" id="huey3" v-model="gender" value="annat">
      <label for="annat">annat</label>
    </div>
    <div id="mapsection">
    <div id="map" v-on:click="setLocation">
      <div v-bind:style= "{left: location.x +'px', top: location.y+'px'}">
         T
      </div>
    </div>
    </div>

    <button id = "orderbutton" type="submit" v-on:click="order">
      <img
        src=data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAOEAAADhCAMAAAAJbSJIAAAAgVBMVEVnwQD///9gvwBhvwBcvgD///34/PL3/PCy3o634JR4xyp6yC////xpwgDt9+K54Zjh8tHe8cyS0VqHzUbs9+bG56e/5KCm2XiT0WPW7cGLz0v5/PXm9NqLzlDk89V+yTvI563Q67eo2Yeq24Gd1WvH56vZ78Wp2n5zxiCh13Oc1WkGWWOZAAAJe0lEQVR4nO2daXOjOBCGjSQMxgdOfMdOCJ5Zh8n//4ELdg6QBBKoW4Dx+2VraqsCj3W1+mLk3LtGbb8Auh6E/deDsP96EPZfD8L+60HYfz0I+68HIYjcsbdexptw4vvn89n3J+EmXq69sWvj4ciE7mK53e1XCWGMkUyU0ut/s38nq/1uu1wgcyISegf/JRixDGokV4bLRsGLf/DwXgOJ8Bjv5ukolaFxoOmIznfxEedVEAjd0+SVMD24HCYjr5MTwowFJ3zzI6I5duJYksh/g34hWEJvGzTF+4EMtrCLEpDQvewZMaD7FmH7C+BsBSMcb6a1116ZKJtuxlAvBkTo+QkY340x8YEmKwjh+INATM+iCPkAGUcAQs+n8HxXRgoxjsaEs3COw3dlnIeztgkPAR7flTE4tEq4WDFUvkxstWiN0A2NTnddURKaHI8GhMsId4L+ikTLNgh90AOwWpT51gkXEf4KzItFTVdjQ8L3kb0BvImO3m0S7uwO4E1sZ43Qs7bFFEWiJiZOA8In6zP0W3T0ZIMwbovvyhjjE07aWIK/YhNsws92AVPET1zCfduAKeIekdB9bmcTLYo81zJT6xC6qy4ApoirOog1CLsCWBOxBmEnpuhN5BmDcN8dwBRRf7vRJmz9mChK/9DQJWz5oBelffRrEsZdA0wRY0jCpzZt0TJRPTNci9BrG6ZEWpcpLcKoi0OYDmIERbjr0jmRF9G59WsQvndvl/kW0/DdqAkXbWNUSu2BUxN2dBHepLEUlYR+d+doJrWrWEW47DZgiqhy+CsI3U7P0Uw0UtykFIRhVw+KX5HQhHDRfcAUsXo/rSZcdX2OZqKr5oSHrm8zN7HKQHgV4Sxo+901FVSlM1QR9mCbualys6kg9OZtv7m25hX3qApCvy9DmA5ihWVTTjjuwz76LVqeIFZO+NGfIUwH8aM+odcnwBSxdCWWErayCpsvjPKVWEY4TgBfXPs1DRIEkrKVWEa4acGcIX8NYiNsU4/QndrfSWl0dI6Nn0unJbeoEsJLGxZpdkc4Nf5l2aUW4d7+EH69YWNrn5aEo+SEnv0h/HG4NHYMMfmBISfcWj8qcjHPpoFKsq1BaP3aRJPfuq5j06cH+oRv1oeQ5jwRl6ZPJ9KaKSmhdXsmHwucBU13ObldIyO07kJkf3JPbx5tljsWZYQny0NIX3MPXxts4+SkSTixS0gLJuWzwfwhsti+jPDV7iRl+Q0iNvl1C5OhgvBodwjZf7lnN99mriKSWmIJod28i2Ic94/ZryvLz5AQ7mxOUvqS3/8Whj8ulYS9JYRWnYjzdf7RL6Y/7lyH0KrVXYz+ma8PifUtEtoMVrCCsQzgOZGEMERCiyYb+Vd4suE2c/2LouEmEhqvBW3RaSGiAmFK0Rc1oWvx5lTYZRwQ11AgmKYCob30Gc6xAuTdEwLCAqG15AsuQRQo0iWmZgiEthwYfKo2UPKc6MoQCC1ZNJSL2z4BTR3RqhEILfkRKbdeoC7dok+RJ3TtpF/wJvIWavVToRSDJ7QTkeGz0QBDeUKEhie0EjakfEHIJ9zEEQKJPKGJm0RXlP+dG/sPJWJrjogntHEcMs5hBBroEg5EntDCBV9IXQatVhGu+TzhBn0dCkkFsAuD8JFSnhA9D6rotshk4j8UJeRH8YT4vlJ+rwO+cQs+U57Q/P5b/QcYHz05Ah/Awh0YnHC+SSr+hJhPAO1SUBKeDRcFC53jn9K+LpzbItUC2kikZ1xCeo1SnkqaK9FISAQFN4OxCb8P83d5AzDB1wd//CoJzZYF+QkEejuxh5SYDwK9zYzQd5pcNN55m3Ljw8RMXgD/IS8lodF5SIv+2G1hqhKxNhkjX0B5HhrZNAlnrnj/fndVzjl6FcZtW2nTGNmlopPk6WeqSuo+UAoblXap2eYmqXjc3jpBSwIKRxgk/hViBaHh/ZC/+qXy9umuKksE+YdiAivvh4ZXGZpIijsuUybpY7HEsfGVd3xTP420YcUslCTVISXtKP00xr42Js+fE4SVhKz0tZn7S4lWqwMsn57aXwrg857rtP8F9B8WpPZ5A8QtpHk7nJ6wXAkacQuA2JO6vnqGliivEXuCcJgSVe/fEM1nqRE/BIkBz/lDqag1YvRHHQMGieMrWh3A+g8L0ojjw+RiVPYaRczY0cnFAHJ+VfQ4wiwv1sqngfqFS6vkMVOStHKigPLaSuuQwP2HeWnltUHlJkq8FlehZiBr5SaCZWMUkn9/hBq+08wvBXsHKqnwmKFmr2rmCIPleQvRbAfFf5iTZp433EoRW1Q2Ly/UkW6uPmAMUXAC4xY6aNdbANbMsOJ1GLkxmnbNDGTdU6FjxRE330q/7gnS6igsDeTmffq1a6DxhFxdGnZZY436Q9Aa0l9TEbvor0YNKWwa7fzLBsduYlCrDhi0quTLwYfeBLVWLTdsHu2teOsTeRXWq8cH7qmQhaSg0pzLH1KvpwJwXwy6gKmmqHpEzb4YwNsCXaHXGtXtbQKeDY2ePV67P02fOn1lqt9jaAB9ou6/19cA+rX1aSU267k3gL6J99/7cgD9S++/B+0A+ggPoBd0HzYbs37eA+jJfv999QfwbYQBfN9iAN8ouf/vzAzgW0GdXYpw33sawDe77v+7a7Z7uGkJ9tt5A/j+4QC+YTmA75AO4FuyA/gecGcQ0b7pPIDvcjv3/211pwOHhv4x0ZCw7aNf+6BvTujEbdqoNK79vvUJnSf8kHUZ30jP2DYldDyDz8GYiERa1yUAwvTW38ZirKzDgSZ03q3PVDrS8MkAEjqLyO4wskjtVYMlzFzF9oaRqh2/CITO0tqGQyKV6x6H0HFDsQcNgigJaxmigITpaixplwQptmq6AiEIHecQIGenB6qaYmxCZxbKW0LB8M3DqiQEO4SpieNTHEZC/SZGDDyh44w/CELDJ/Kh05xBKRDCbBwT0OORsgRi/DIBEabjuJmCMVI23YCMXyYwwvR4vOwZxGQlbH8xOQA5ARKm8rYBMbICKCHBFmh6fgmWMNWbHzWFTPEiX1q7ZCJwwnS2niavpPaapIy8Tk6As/NbCISZjvEuYUxzLClhLNnFkhpeCCERZvIO/kswSjFpGWj6fwgbBS/+AXbpFYRImMldLLe7/SpJR4mRTBlUpuzfyWq/2y4XCDMzL2TCm9yxt17Gm3Di++fz2fcn4SZerr0xMttNVghb1YOw/3oQ9l8Pwv7rQdh/PQj7rwdh//Ug7L/+B42OnUdSivbFAAAAAElFTkSuQmCC
        style="height:20px;">
      Send info
    </button>



  </section>

</main>
<hr>
<footer>copyright</footer>
</template>

<script>
import menu from '../assets/menu.json'
import Burger from '../components/Burger.vue'
import io from 'socket.io-client'

const socket = io();

/* const MenuItem = { name: 'nm',
               this.img ='url',
               this.kcal ='kcal',
               this.gluten= 'gl',
               this.lactose= 'lt',
            }
*/



export default {
  name: 'Home',
  components: {
    Burger
  },
  data: function() {
    return {
      burgers:menu,
      hn:'',
      em: '',
      ln:'',
      fn:'',
      gender:'',
      rcp:'',
      orderedBurgers: {},
      location: {x:0, y:0}
    }
  },
  methods: {
    order: function(){
    socket.emit("addOrder", {
      orderId: this.getOrderNumber(),
      details: {
        x: this.location.x,
        y: this.location.y


      },
      orderItems: this.orderedBurgers,
      customerinfo: [this.em, this.fn, this.rcp, this.gender]

    });

    },
    setLocation: function (event){
    this.location.x = event.clientX - 10 -event.currentTarget.getBoundingClientRect().left;
    this.location.y = event.clientY - 10 -event.currentTarget.getBoundingClientRect().top;
    },
    addToOrder: function (event) {
      this.orderedBurgers[event.name]=event.amount;
    },
    getOrderNumber: function() {
      return Math.floor(Math.random()*100000);
    },
    addOrder: function(event) {
      var offset = {
        x: event.currentTarget.getBoundingClientRect().left,
        y: event.currentTarget.getBoundingClientRect().top
      };
      socket.emit("addOrder", {
        orderId: this.getOrderNumber(),
        details: {
          x: event.clientX - 10 -offset.x,
          y: event.clientY - 10 -offset.y

        },
        orderItems: ["Beans", "Curry"]
      });
      this.location.x = event.clientX - 10 -offset.x;
      this.location.y = event.clientY - 10 -offset.y;
      }
  }
}
</script>

<style>
#map {
  width:1920px;
  height: 1078px;
  background: url("/img/polacks.jpg");
  position: absolute;
  background-repeat: no-repeat;


}
#mapsection{
overflow: scroll;
position:relative;
width:1000px;
height: 600px;
}
#map div{
  position:absolute;
  background: black;
  color: white;
  border-radius: 10px;
  width:20px;
  height:20px;
  text-align: center;
  }

@import 'https://fonts.googleapis.com/css?family=Arial|Dosis';

header {
  margin: 4em;
  height: 10em;
  overflow: hidden;
}

#rubrik {
  position: absolute;
  padding: 1.5em;
  padding-left: 14em;
  margin-top: -24em;
}

#huvudbild {
  opacity: 0.7;
  width: 100%;
  height: auto;

}

body {
  font-family: Arial;
}

.väljburgare {

  border: 2px solid #ff9900;

  color: white;
  background-color: black;


}

#kött {
  font-weight: bold;
}

.kunduppgifter {}

button {
  margin: 4em;
}

button:hover {
  background-color: blue;


}

section {
  margin: 4em;
  padding: 3em;
  border: 2px solid purple;

}

.wrapper {
  border: 2px solid #ff9900;
  display: grid;
  grid-gap: 100px;
  grid-template-columns: 300px 300px 300px;
  background-color: black;
  color: white;
  padding: 2em;
}
</style>
