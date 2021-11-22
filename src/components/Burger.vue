<template>
<div>

  <h4>{{burger.name}}</h4>
  <img v-bind:src="burger.url" style="height:200px;">
  <ol>

    <li>{{burger.kcal}} kCal</li>
    <li v-if=burger.lactose> innehåller <span id="kött">lactose</span> </li>
    <li v-if=burger.gluten> innehåller <span id="kött">gluten</span> </li>
    <li>ost</li>
    <li>bröd</li>
  </ol>
    <div>
        <button v-on:click="increaseCounter">+</button>
          {{amountOrdered}}
        <button v-on:click="decreaseCounter">-</button>
    </div>
</div>
</template>

<script>

export default {
  name: 'Burger',
  props: {
    burger: Object
  },
  data: function(){
    return {
      amountOrdered: 0
    }
},
  methods: {
    increaseCounter: function() {
      this.amountOrdered += 1;
      this.$emit('orderedBurger', { name:   this.burger.name,
                                    amount: this.amountOrdered
                              }
                              );
    },
    decreaseCounter: function() {
      if(this.amountOrdered>0){
        this.amountOrdered -= 1;
        this.$emit('orderedBurger', { name:   this.burger.name,
                                      amount: this.amountOrdered
                              }
                              );
        }
    },

  }
  }







</script>




<style scoped></style>
