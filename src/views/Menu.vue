<template>
    <v-container>
        <v-row>
            <v-col offset-md="1" md="5">
                 <h1>Menu items</h1>
                <div class="pa-2" id="info">
                    <v-simple-table id="menu-table">
                        <thead>
                        <tr>
                            <th class="text-left" style="width:70%;">Name of item</th>
                            <th class="text-left" style="width:100px">Price</th>
                            <th class="text-left" style="width:100px">Add to basket</th>
                        </tr>
                        </thead>
                        <tbody>
                        <tr v-for="item in menuItems" :key="item.name">
                            <td>
                                <span id="td_name">{{ item.name }}</span><br>
                                <span id="menu_item_description">{{ item.description }}</span>
                            </td>
                            <td>{{ item.price }}</td>
                            <td> 
                                <v-btn small text v-on:click="addToBasket(item)">
                                <v-icon color="orange"> add_box </v-icon>
                                </v-btn>
                            </td>
                        </tr>
                        </tbody>
                     </v-simple-table>
                </div>
            </v-col>
            <v-col  offset-md="1" md="4">
                  <h1>Current basket</h1>
                <div class="pa-2" id="info">
                     <v-simple-table id="menu-table" v-if="basket.length > 0"  >
                        <thead>
                        <tr>
                            <th class="text-left" style="width:30%;">Quantity</th>
                            <th class="text-left" style="width:50%">Name of item</th>
                            <th class="text-left" style="width:20%">Price</th>
                        </tr>
                        </thead>
                        <tbody>
                        <tr v-for="item in basket" :key="item.name">
                            <td>
                               <v-icon color="orange" @click="increaseQtn(item)">add_box</v-icon>
                               {{ item.quantity }}
                                 <v-icon color="orange" @click="decreaseQtn(item)">indeterminate_check_box</v-icon>
                            </td>
                            <td>{{ item.name }}</td>
                            <td> {{ item.price }}</td>
                        </tr>
                        </tbody>

                        
                     </v-simple-table>
                     <v-simple-table v-else>
                         <p>The basket is empty</p>
                     </v-simple-table>
                     <v-divider></v-divider>
                     <v-row  id="basket_checkout" class="mt-4" style="margin=0;">
                         <v-col>
                            <p>Subtotal:</p>
                            <p>Delivery:</p>
                            <p>Total amount:</p>
                         </v-col>
                         <v-col class="text-right">
                             <p> {{ subtotal }} DKK</p>
                            <p>10 DKK</p>
                            <p><b> {{ total }} DKK</b></p>
                         </v-col>
                     </v-row>
                     <v-row style="margin=0;">
                             <v-spacer></v-spacer>
                             <v-btn color="orange">Checkout</v-btn>
                     </v-row>
                </div>
            </v-col>
        </v-row>
    </v-container>
</template>

<script>
   export default {
    data () {
      return {
          basket: [],
        menuItems: [
          {
            name: 'Frozen Yogurt',
            description: "unique watches made for you",
            price: 159,
          },
          {
            name: 'Ice cream sandwich',
            description: "unique watches made for you",
            price: 237,
          },
          {
            name: 'Eclair',
            description: "unique watches made for you",
            price: 262,
          },
          {
            name: 'Cupcake',
            description: "unique watches made for you",
            price: 305,
          },
          {
            name: 'Gingerbread',
            description: "unique watches made for you",
            price: 356,
          }
        ],
      }
    },

    methods: {
        addToBasket(item) {
            this.basket.push({
                name: item.name,
                price: item.price,
                quantity: 1
            })
    },
    increaseQtn(item) {
        item.quantity++
    },
    decreaseQtn(item){
        item.quantity--;

        if (item.quantity === 0 ){
            this.basket.splice(this.basket.indexOf(item), 1)
        }
    }
  },
  computed: {
      subtotal () {
          var subCost = 0;
        for( var items in this.basket) {
            var individualItem = this.basket [items];
            subCost += individualItem.quantity * individualItem.price;
        }
        return subCost
      },
      total () {
          var deliveryPrice = 10;
          var totalCost = this.subtotal 
          return totalCost + deliveryPrice
      }
  }
  }
</script>

<style lang="scss" scoped>
 .col h1 {
   @include infobox_mixin(5px, map-get($colorz, white), 10px, 5px, map-get($colorz, white));
   //I kinda got out of the previous struggles but I couldn't solve this. this is the  error !!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
    font-weight: bold;
    text-transform: uppercase;
    font-size: 16px;
    text-align: right;
  }
  .col:last-child h1 {
    text-align: left;
  }

 #info {
     background-color: white;
 }
 tr th {
     font-weight: 300;
 }
 #td_name {
     font-weight: bold;
 }
tr td {
    padding: 10x 10px 10px 16px;
}
#menu_item_description {
    font-style: italic;
    font-weight: 300;
    color: darkgray;
    font-size: 13px;
}

#basket_checkout {
    font-size: 13px;

}
#basket_checkout p:first-child {
    line-height: 2px;
}
</style>