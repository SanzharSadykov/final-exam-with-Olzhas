<template>
  <div class="container mx-auto w-full flex">
    <div v-for="tv of tvs" :key="tv.id">
      <!-- <div class="flex items-center justify-between"> -->
        <div class="bg-pink-500 w-3/4 rounded-xl p-4">
          <div class="flex items-center justify-between">
            <p v-if="tv.credit != null" class=" bg-teal-800 text-sm font-semibold w-max text-white py-0 rounded-xl px-2">{{displayedCredit}}</p>        
            <p class="font-semibold text-xl text-black"><i class="far fa-heart"></i></p>
          </div>
          <div class="w-3/4 container mx-auto">
            <img class="cursor-pointer w-full" :src="tv.img" alt="">
          </div>
          <p class="text-lg font-semibold">{{displayedInch}} {{tv.title}}</p>
          <div class="flex items-center justify-start">
            <div v-for="(inch, index) of tv.inches" :key="inch" class="pt-4 pb-12">
              <p @click="changeInch(index, tv)" class="cursor-pointer mr-4 px-1 py-0 text-sm" :class="{'border border-black rounded-xl': tv.selected === index+1}">{{inch}}</p>
            </div>
          </div>
          <div v-if="tv.discount != null" class="py-6">
            <p class="font-bold text-lg mb-2">{{tv.discount}} ₸</p>
            <div class="flex items-center justify-start text-xs">
              <p class="line-through mr-2">{{tv.price}} ₸</p>
              <p class="font-bold text-blue-400">Скидка {{parseInt(tv.price)-parseInt(tv.discount)}} ₸</p>
            </div>
          </div>
          <p v-else class="py-2">{{tv.price}}</p>
          <div class="flex items-center justify-star">
            <p class="text-sm text-yellow-400 mr-1"><i class="fas fa-star"></i></p>
            <p class="text-sm text-yellow-400 mr-1"><i class="fas fa-star"></i></p>
            <p class="text-sm text-yellow-400 mr-1"><i class="fas fa-star"></i></p>
            <p class="text-sm text-yellow-400 mr-1"><i class="fas fa-star"></i></p>
            <p class="text-sm text-yellow-400 mr-1"><i class="fas fa-star"></i></p>
            <p class="font-semibold mx-1">{{tv.rating[tv.selected-1][0]}}</p>
            <p class="font-semibold">({{tv.rating[tv.selected-1][1]}})</p>
          </div> 
          <div class="border-gray-400 my-2 border-b"></div>
          <div v-for="option of tv.options" :key="option">
            <div class="flex items-center justify-start">
              <!-- <div class="w-full">
                <img class="w-1/8" :src="option.logo" alt="">
              </div> -->
              <p class="text-sm">{{option.title}}</p>
            </div>
          </div>              
          <div class="border-gray-400 my-2 border-b"></div>
          <div>
            <button class="border border-black w-full rounded-2xl bg-black text-white py-2 px-6 mb-2">Добавить в корзину</button>
            <button class="border border-black w-full rounded-2xl bg-white text-black py-2 px-6">Узнать больше</button>
          </div>
          <div class="flex items-center justify-around mt-4 mb-5">
            <a class="cursor-pointer font-medium text-sm hover:text-gray-300"><i class="fas fa-map-marker-alt mr-1"></i> Где купить?</a>
            <a class="cursor-pointer font-medium text-sm hover:text-gray-300"><i class="fas fa-balance-scale mr-1"></i> Сравнить</a>
          </div>
        </div>
      <!-- </div> -->
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: 'HomeView',
  data() {
    return {
      tvs: null,
      selected: 1,
      displayedInch: "43\"",
      displayedCredit: "0-0-36",
      selectedImage: 0
    };
  },  
  async mounted() {
    this.tvs = (
      await axios.get("https://6286235096bccbf32d6fe5bf.mockapi.io/tvs")
    ).data;
  },
  methods: {
    changeInch(index, tv) {  
      this.displayedInch = tv.inches[index]
      this.displayedCredit = tv.credit[index]     
      // if (index+1 > tv.length) {
      //   this.selected = tv.length-1 
      // } else {
      //   this.selected = index+1 
      // }
      // console.log(this.selected)   
      // console.log(tv.length)   
      tv.selected = this.selected
    }
  }
}
</script>
