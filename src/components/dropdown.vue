<template>
<div class="dropdown">
    <div class="dropdownBotton">
    <botton class="botton" @click=" collapsed = !collapsed">Dropdown</botton>
    </div>
        <div v-if="options > options[6]">
    <div v-bind:class="{'itemsList' : collapsed }" >
        <input v-model="search" type="search" class="dropdownSearch" placeholder="Buscar">
        <div class="scroll" @scroll="handleScroll">
        <div class="dropdownList" v-for="option in filteredList" > <img v-bind:src="option.img" height="15"/> {{option.text}}</div>
    </div>
    </div>
    </div>
    <div v-else>
        <div v-bind:class="{'itemsList' : collapsed }" >
        <input v-model="search" type="search" class="dropdownSearch" placeholder="Buscar">
        <div class="dropdownList" v-for="option in filteredList" > <img :src="option.img" > {{option.text}}</div>
    </div>
    </div>
</div>
</template>

<script>
export default{
        data() {
        return{
            search:'',
     options:[{text:'one',img:require('./img/cuadro1.png')},{text:'two',img:require('./img/cuadro2.png')},{text:'three',img:require('./img/cuadro3.png')},{text:'four',img:require('./img/cuadro4.png')},{text:'five',img:require('./img/cuadro5.png')},
            {text:'six',img:require('./img/cuadro6.png')},{text:'seven',img:require('./img/cuadro7.png')},{text:'eight',img:require('./img/cuadro8.png')},{text:'nine',img:require('./img/cuadro9.png')},{text:'ten',img:require('./img/cuadro10.png')}],
            collapsed: true,
            scrolled: false,
    }
  },
      computed: {
    filteredList:function() {
      return this.options.filter((option) => {
        return option.text.match(this.search)
      });
    }
  },
    
methods: {
  handleScroll () {
    this.scrolled = window.scrollY > 0;
  }
},
beforeMount () {
  window.addEventListener('scroll', this.handleScroll);
},
beforeDestroy () {
  window.removeEventListener('scroll', this.handleScroll);
}
}

</script>

<style >
    .scroll{
     max-height: 150px;
    overflow-y: scroll;
    }
    .dropdown{
    width: 200px;
    margin: 20px auto 0;
    font-size: 14px;
    font-family: sans-serif;
    background: #EEEEEE;
    }
    .botton:hover, .botton:focus {
    background-color: #EEEEEE;
}
    .botton{
    float: left;
    width: 100%;
    background: whitesmoke;
    padding: 10px 12px;

    cursor: pointer;
    border: 1px solid lightgray;
    box-sizing: border-box;
    }
    .dropdownSearch{
        box-sizing: border-box;
        margin: 5px;
        background: #EEEEEE;
    }
    .dropdownList:hover, .dropdownList:focus {
        background-color: #EEEEEE;
    }
    .itemsList{
        display: none;
        margin: 0px;
        background: #EEEEEE;
          overflow-y: scroll;
        
    }
    .dropdownList{
    float: left;
    width: 100%;
    background: whitesmoke;
    padding: 10px 12px;
    cursor: pointer;
    border: 1px solid lightgray;
    box-sizing: border-box;
    }
     input[type="search"] {
        padding: 5px 0;
    }
</style>