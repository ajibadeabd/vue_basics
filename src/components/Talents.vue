<template>
  <div class="hello">
   <!-- {{name}}
   {{btnState ? "the btn is disabled":"the button is active"}}
   <button  v-on:click="changeName" v-bind:disabled="btnState">change name</button>
   -->
   <div class="holder">
     <form @submit.prevent="addTalent" >
      <!-- <input type="text" name="Talent" id=""  placeholder='Enter a Talents you have' v-model="Talent"  v-validate="'min:5'" />
  <p class="alert"  v-if="errors.has('Talent')">{{errors.first('Talent')}}</p>
   -->
      <!-- <input type="text" name="Talent" id=""   v-model="Talent" placeholder='Enter a Talents you have' /><br/> -->
        <transition name="alert-in" enter-active-class="animated flipInX" leave-active-class="animated flipOutX">
         
        </transition>
 
  
  </form>
     <ul>
       <li v-for="(Talent, index) in Talents" :key='index'  > {{index}} . {{Talent.Talent}}
       <div class="remove" v-on:click="remove(index)">x</div>
       </li>
     </ul>
     <p v-if="Talents.length < 1"  >you have no Talents</p>
     <p v-else>you have more than {{Talents.length}} Talents</p>
     <ul>
       <li v-for="(Item, index) in Items" :key='index'  >
          <p>{{Item.title}}</p>
          <button @click="addItem(index)">
            add to cart
          </button>
          </li>
     </ul>
     <p>shopping cart</p>
     <ul>
       <li  v-for="(id, index) in Cart" :key='index'>
         {{id.title}}  <br/>
        {{id.price| currency}}*{{id.qty}} =
        {{id.allprice| currency}}
        <button @click='reduceItem(id)'>
          -
        </button>
         <button @click="increaseItem(id)">
          +
        </button>
         
         <br><br>
         </li>
    
     </ul>
  <div v-if="Cart.length">
 <p>Total:{{total | currency}}</p>
  </div>
  <div v-else>
 <p>no item added</p>
  </div>

     </div>
   </div>
</template>

<script>
export default {
  name: 'Talents',
data() {
   return{
     total:0,
  
    
     Items:[
       {id:1,"title":"item1",price:300},
        {id:2,"title":"item2",price:600},
         {id:3,"title":"item3",price:900}
         
     ],
      
      Talents:[
        {"Talent":"capentary"},
        {"Talent":"shoemaking"},
        {"Talent":"sleeping"}
      ],Cart: [],
   
   }
},
       methods:{

         addTalent(id){
           this.Talents.push({Talent:this.Talent})
           this.Talents.splice(id,1)
          //  this.Talent=''
         },
         remove(id){
              this.Talents.splice(id,1)
         },
         addItem(index){
          let Item= this.Items[index]
           this.total+=Item.price
           
           let found=false;
                  for(let i=0; i<this.Cart.length; i++){
                    if(this.Cart[i].id===Item.id){
                      found=true;
                      this.Cart[i].qty++
                      this.Cart[i].allprice+=Item.price
                    }
                  }if(!found){
                    this.Cart.push(
                    {   id:Item.id,
                        price:Item.price,
                        title:Item.title,
                        qty:1,
                        allprice:Item.price
                        }
                    )
                    }
      
         },
         reduceItem(id){
           id.qty--
             id.allprice-=id.price
          this.total-=id.price
          if(id.qty<=0){
          for(let i=0;i<this.Cart.length; i++){
              if(id.id==this.Cart[i].id){
                this.Cart.splice(i,1)
              }
          }
          }

         },
        increaseItem(id){
          id.qty++
          this.total+=id.price
        //  this.Cart[id].allprice+=id.price
        id.allprice+=id.price
         }
       },
       filters:{
          currency(price){
            return '$'+price.toFixed(2)
            // "$".concat(price)
          }
       }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style src="./Talents.css">
/* h3 {
  margin: 40px 0  0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
} */
</style>
