<template>
   <div class="goods-list-wrapper">
      <div class="list-maker-wrapper">
         <h2 class="list-maker-title">Add Your Items</h2>
         <div class="list-maker-inputs">
            <input class="item-title" type="text" placeholder="Item Title:" v-model="title" />
            <p class="error title-error">Please Write the title of your item</p>
         </div>
         <div class="list-maker-inputs">
            <input class="number-of-item" type="number" placeholder="Number of Item:" v-model="number"/>
            <p class="error number-error">Please Write the number of your items</p>
         </div>
         <button class="list-maker-submit-button" @click="addItem">Submit</button>
      </div>
      <div class="list-display-wrapper">
         <table v-if="items != ''">
            <tr>
               <th>Row</th>
               <th>Title</th>
               <th>Number</th>
            </tr>
            <tr v-for="(item, index) in items" :key="index">
               <td>{{ index + 1 }}</td>
               <td>{{ item.title }}</td>
               <td>{{ item.number }}</td>
            </tr>
         </table>
      </div>
      <div class="pdf-export-wrapper">

      </div>
   </div>
</template>

<script setup lang="ts">
// import jsPDF from 'jspdf'
// useHead({
//   script: [{ src: "js/jsPDF/dist/jspdf.umd.js" }],
// });

const title = ref('') as any
const number = ref('') as any

const items = ref([]) as any
const itemsElements = ref() as any
function addItem () {
   
   if (title.value === '') {
      const titleError = document.querySelector(".title-error") as any
      titleError.style.display = "initial"
      setTimeout(() => {
         titleError.style.display = 'none'
      },3000)
   } else if (number.value === '') {
      const numberError = document.querySelector(".number-error") as any
      numberError.style.display = "initial"
      setTimeout(() => {
         numberError.style.display = 'none'
      },3000)
   } else {
      itemsElements["title"] = title.value;
      itemsElements["number"] = number.value;
      items.value.push({...itemsElements})
      itemsElements.value = null
      title.value = ''
      number.value = ''
   }
}

// window.jsPDF = window.jspdf.jsPDF;
// let doc = ref(new jsPDF())
</script>

<style lang="scss">
@import '@/assets/scss/global.scss';

.goods-list-wrapper{
   width: 100%;
   display: flex;
   flex-direction: column;
   align-items: center;
   margin: 100px 0px;
}

.list-maker-wrapper{
   width: 60%;
   background: $primary;
   border-radius: 15px;
   display: flex;
   flex-direction: column;
   align-items: center;
   padding: 40px 0px;

   .list-maker-title {
      margin-bottom: 40px;
   }

   .list-maker-inputs{
      width: 100%;
      margin-bottom: 30px;
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      
      input {
         width: 80%;
         border-radius: 8px;
         height: 40px;
         outline: none;
         border: none;
         box-shadow: 0px 0px 2px 1px #404040;
         padding:  0 10px;
         font-size: 16px;
      }
      
   }

}

.list-maker-submit-button{
   background: $secondary;
   color: #fff;
   padding: 10px 0;
   width: 80%;
   border-radius: 8px;
   height: 50px;
   outline: none;
   border: none;
   cursor: pointer;
   box-shadow: 0px 0px 2px 1px #404040;
   border: 1px solid #404040;
   font-size: 16px;

   &:hover{
      opacity: 0.8;
   }
}

.error {
   display: none;
   color: red;
   font-size: 16px;
   margin-top: 10px;
   background: #ffffffad;
   width: 80%;
   border-radius: 8px;
   padding: 5px 10px;
}

.list-display-wrapper{
   margin-top: 80px;
   width: 100%;
   display: flex;
   flex-direction: column;
   align-items: center;
   text-align: center;
   th, td {
      border:1px solid black;
   }
   table {
      width: 60%;
      border:1px solid black;

      tr {
         td:nth-child(1){
            width: 5%;
         }
         td:nth-child(2){
            width: 70%;
         }
         td:nth-child(3){
            width: 25%;
         }
      }
   }
}
</style>