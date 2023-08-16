<template>
  <div class="Container">
    <div class="Index">
      <div class="CoreIndex">
        <div class="Text">Danh mục sản phẩm</div>
        <ul>
          <li v-for="(part, index) in Index.type" :key="index" @click="Search(0, part.name)">
            {{ part.name }}
            <Triangle v-if="part.children.length !== 0" class="Triangle"></Triangle>
            <ul class="HoverList">
              <li
                v-for="(part1, index1) in part.children"
                :key="index1"
                @click="Search(part.name, part1.name)"
              >
                {{ part1.name }}
              </li>
            </ul>
          </li>
        </ul>
      </div>
      <div class="Swiper">
        <div class="swiper">
          <!-- Additional required wrapper -->
          <div class="swiper-wrapper">
            <!-- Slides -->
            <div class="swiper-slide">
              <img
                class="Img"
                src="https://pos.nvncdn.net/585eb4-8380/bn/20210111_GLV2ht02lDoLc6hJZXeaZ3PR.jpg"
              />
            </div>
            <div class="swiper-slide">
              <img
                class="Img"
                src="https://pos.nvncdn.net/585eb4-8380/bn/20210111_3n9Gcy4lKbLNzOf3Kq46BAiu.jpg"
              />
            </div>
          </div>
          <div class="swiper-scrollbar"></div>
        </div>
      </div>
    </div>
    <div v-if="this.modal" class="ContainerModal">
      <div class="outside" @click="Off()"></div>
      <div class="modal">
        <div class="Picture">
          <img :src="`${this.temp.url}`" alt="error" class="Img" />
        </div>
        <div class="in4">
          <div class="name">{{ this.temp.name }}</div>
          <div class="rate">
            <div
              v-for="n of Array.from({ length: this.temp.rate / 2 }, (_, index) => index + 1)"
              :key="n"
            >
              <Star class="icon"></Star>
            </div>
            <div v-if="this.temp.rate % 2 === 1">
              <StarHalf class="icon"></StarHalf>
            </div>
            <div v-if="this.temp.rate % 2 === 0 && this.temp.rate / 2 != 5">
              <StarEmpty class="icon"></StarEmpty>
            </div>
            <div
              v-for="n of Array.from({ length: 4.5 - this.temp.rate / 2 }, (_, index) => index + 1)"
              :key="n"
            >
              <StarEmpty class="icon"></StarEmpty>
            </div>
          </div>
          <div class="price">{{ this.temp.price }} VNĐ</div>
          <div class="id">Mã sản phẩm: {{ this.temp.name }}</div>
          <div class="quantity">
            <div class="Text">SL:</div>
            <div class="Down" @click="Down()">-</div>
            <input
              id="input"
              class="Number"
              :value="this.quantity"
              @keydown.enter="set()"
              @blur="set()"
            />
            <div class="Up" @click="Up()">+</div>
            <div class="Order" @click="AddToCart(this.temp)">ĐẶT HÀNG</div>
          </div>
        </div>
        <div class="Close" @click="Off()">x</div>
      </div>
    </div>
    <div v-for="(part, index) in Data.data.type" :key="index" class="Part">
      <div class="Title">
        {{ part.name }}
        <div>Xem tất cả</div>
      </div>
      <div class="Type">
        <div
          v-for="(part1, index1) in part.category"
          :key="index1"
          @click="Search(part.name, part1.name)"
          class="Button"
        >
          {{ part1.name }}
        </div>
      </div>
      <div class="Products">
        <div v-for="(part1, index1) in part.product" :key="index1" class="Product">
          <div class="ButtonHover">
            <button @click="On(part1)" class="Eyes">
              <Eyes></Eyes>
            </button>
            <button class="Heart">
              <Heart></Heart>
            </button>
          </div>
          <img :src="`${part1.url}`" alt="error" class="Img" />
          <div class="Name">
            {{ part1.name }}
          </div>
          <div class="Price">{{ part1.price }} VNĐ</div>
          <div class="Rate">
            <div
              v-for="n of Array.from({ length: part1.rate / 2 }, (_, index) => index + 1)"
              :key="n"
            >
              <Star></Star>
            </div>
            <div v-if="part1.rate % 2 === 1">
              <StarHalf></StarHalf>
            </div>
            <div v-if="part1.rate % 2 === 0 && part1.rate / 2 != 5">
              <StarEmpty></StarEmpty>
            </div>
            <div
              v-for="n of Array.from({ length: 4.5 - part1.rate / 2 }, (_, index) => index + 1)"
              :key="n"
            >
              <StarEmpty></StarEmpty>
            </div>
          </div>
          <button @click="AddToCart(part1)">MUA NGAY</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import Triangle from '../../components/icons/Triangle.vue'
import Swiper from 'swiper'
import { Navigation, Pagination, Autoplay } from 'swiper/modules'
// import Swiper and modules styles
import 'swiper/css'
import 'swiper/css/navigation'
import 'swiper/css/pagination'
import 'swiper/css/autoplay'
import Data from './Data.json'
import Heart from '../../components/icons/Heart.vue'
import Eyes from '../../components/icons/Eyes.vue'
import Star from '../../components/icons/Star.vue'
import StarHalf from '../../components/icons/StarHalf.vue'
import StarEmpty from '../../components/icons/StarEmpty.vue'
import { convertViToEn } from '../../function.js'
import Index from './Index.json'
</script>

<script>
export default {
  name: 'home',
  data() {
    return {
      full: undefined,
      haft: undefined,
      quantity: 1,
      modal: 0,
      temp: undefined
    }
  },
  methods: {
    Search(object1, object2) {
      let a = object2
      a = convertViToEn(a)
      console.log(a)
      if (object1 === 0) {
        sessionStorage.setItem(
          'search',
          '[{' +
            String.fromCharCode(34) +
            'name' +
            String.fromCharCode(34) +
            ':' +
            String.fromCharCode(34) +
            object2 +
            String.fromCharCode(34) +
            '}]'
        )
      } else {
        sessionStorage.setItem(
          'search',
          '[{' +
            String.fromCharCode(34) +
            'name' +
            String.fromCharCode(34) +
            ':' +
            String.fromCharCode(34) +
            object1 +
            String.fromCharCode(34) +
            '},{' +
            String.fromCharCode(34) +
            'name' +
            String.fromCharCode(34) +
            ':' +
            String.fromCharCode(34) +
            object2 +
            String.fromCharCode(34) +
            '}]'
        )
      }
      this.$router.push((this.$router.params = a))
    },
    Down() {
      if (this.quantity !== 1) {
        this.quantity--
      }
    },
    set() {
      let a = document.getElementById('input')
      console.log('hello')
      this.quantity = a.value
    },
    Up() {
      this.quantity++
    },
    Off() {
      this.modal = 0
      this.quantity = 1
    },
    On(object) {
      this.modal = 1
      this.temp = object
    },
    AddToCart(object) {
      object['quantity'] = this.quantity
      let Object = JSON.stringify(object)
      if (!localStorage.cart) {
        localStorage.setItem('cart', Object)
      } else {
        let Cart = [localStorage.cart]
        console.log('added')
        Cart.push(Object)
        localStorage.setItem('cart', Cart)
      }
      this.$router.push({ name: 'cart' })
    }
  },
  mounted() {
    var swiper = new Swiper('.swiper', {
      // Optional parameters
      direction: 'horizontal',
      modules: [Navigation, Pagination, Autoplay],
      loop: true,
      speed: 3000,
      autoplay: {
        delay: 3000,
        disableOnInteraction: false,
        reverseDirection: true
      },

      // And if we need scrollbar
      scrollbar: {
        el: '.swiper-scrollbar',
        draggable: false
      }
    })
  }
}
</script>

<style scoped src="./Home.css"></style>
