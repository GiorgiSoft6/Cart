<template>
  <div class="MtDiv">
    <button v-on:click="Tst =! Tst">Shop ~ Cart</button>
    <div v-if="Tst" class="Shop">
      <div v-for="item in Products" :key="item" class="ShopPr">
        <img :src="item.Image" alt="">
        <h1>{{ item.name }}</h1>
        <h3>${{ item.Price }}</h3>
        <button v-on:click="AdToCart(item)">Add To Cart</button>
      </div>
    </div>
    <div v-if="!Tst" class="Cart">
      <h3>You Have {{ Psp.length }} Product</h3>
      <div ref="Npn" v-for="(DelPr, index) in Psp" :key="index" class="CartPr">
          <img :src="DelPr.Image" alt="">
          <div>
          <h2>{{ DelPr.name }}</h2>
          <h3>${{ DelPr.Price }}</h3>
          <button v-on:click="RemoveCart(index, DelPr)">Remove Product</button>
        </div>
      </div>
    </div>
  </div>
  <h1 v-if="Tst == false">total price: {{ TotalPrice4.toFixed(2) }}$</h1>
  <div ref="Test" class="AddedPr">
    <div>
      <h2>Succes</h2>
      <h3>Your Have in  Cart {{ Psp.length }}</h3>
    </div>
    <div class="TestDiv2" ref="TestDiv">

    </div>
  </div>
</template>


<script>
export default{
  data() {
    return {
      Psp: [],
      Tst: true,
      TotalPrice4: 0,
      Products: [
        {
          name: "Mercedes",
          Price: 3.99,
          Image: "https://mbfwtbilisi.online/wp-content/uploads/2020/11/Cover-Image-e1605001751814.png"
        },
        {
          name: "BMW",
          Price: 2.99,
          Image: "https://www.bmw-georgia.com/content/dam/bmw/common/all-models/m-series/series-overview/bmw-m-series-seo-overview-ms-04.jpg"
        },
        {
          name: "Audi",
          Price: 4.99,
          Image: "https://hips.hearstapps.com/hmg-prod/images/2023-audi-r8-gt-front-three-quarters-motion-3-1664827965.jpg?crop=0.595xw:0.668xh;0.0705xw,0.224xh&resize=768:*"
        },
      ]
    }
  },
  methods: {
    AdToCart(item){
      this.TotalPrice4 += item.Price
      this.$refs.Test.classList.add('active');
      this.$refs.TestDiv.classList.add('active2');
      this.Psp.push(item)
      setTimeout(() =>{
        this.$refs.Test.classList.remove('active');
        this.$refs.TestDiv.classList.remove('active2');
      }, 3500)
    },
    RemoveCart(index, DelPr){
        this.Psp.splice(index, 1)
        this.TotalPrice4 -= DelPr.Price
    },
  }
}
</script>

<style>
.MtDiv > button{
  width: 150px;
  height: 35px;
  border-radius: 5px;
  border: 1px solid black;
  cursor: pointer;
  font-size: 20px;
  margin-bottom: 40px;
  margin-left: 150px;
}
.TestDiv2.active2{
  width: 0px;
}
.AddedPr.active{
  right: 5px;
}
.TestDiv2{
  position: absolute;
  width: 100%;
  height: 5px;
  background-color: rgb(16, 96, 255);
  bottom: 0;
  left: 0;
  transition: 3.5s;
}
.AddedPr div:nth-child(1){
  display: flex;
  flex-direction: column;
}
h2{
  font-family: Arial, Helvetica, sans-serif;
  font-weight:500;
  font-size: 17px;
}
h3{
  color: rgb(79, 79, 79);
}
.AddedPr{
  padding: 0 35px;
  width: 280px;
  height: 90px;
  background-color: white;
  box-shadow: 0px 0px 10px 1px black;
  position: relative;
  position: absolute;
  top: 5px;
  right: -350px;
  border-radius: 10px;
  display: flex;
  align-items: center;
  transition: 0.5s;
  overflow: hidden;
}
.CartPr{
  width: 100%;
  height: 150px;
  border: 1px solid black;
  display: flex;
  align-items: center;
  justify-content: space-evenly;
}
.CartPr img{
  height: 150px;
  width: 150px;
}
.CartPr > div:nth-child(2){
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 5px;
}
.CartPr > div button{
  width: 150px;
  height: 35px;
  border: 1px solid black;
  cursor: pointer;
  border-radius: 5px;
}
.Cart h1{
  position: absolute;
  left: 5px;
  bottom: 10px;
  font-size: 25px;
}
.Cart{
  padding: 5px;
  width: 500px;
  height: 610px;
  background-color: whitesmoke;
  display: flex;
  flex-direction: column;
  overflow-y: scroll;
  overflow-x: hidden;
  position: relative;
}
h3{
  margin: 0 0 10px 0;
  padding: 0;
  font-family: Arial, Helvetica, sans-serif;
  font-weight: unset;
}
h1{
  font-family: Arial, Helvetica, sans-serif;
  font-weight: unset;
}
.Shop{
  width: 500px;
  height: 610px;
  background-color: whitesmoke;
  display: grid;
  grid-template-columns: 1fr 1fr;
  grid-auto-rows: 300px;
  gap: 10px;
}
button{
  cursor: pointer;
}
.ShopPr{
  border: 1px solid black;
  display: flex;
  align-items: center;
  flex-direction: column;
}
img{
  width: 100%;
  height: 50%;
  object-fit: cover;
}
body{
  overflow-x: hidden;
}
</style>