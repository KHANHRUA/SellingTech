<template>
  <div class="Container">
    <div class="Head">
      <div class="TopHead">
        <div class="AlignSign">
          <div class="Log"><Key class="Key"></Key> Đăng nhập</div>
          <div class="Sign"><User class="User"></User> Đăng ký</div>
        </div>
        <div class="Input">
          <input placeholder="Tìm kiếm" type="text" />
          <Search class="Search"></Search>
        </div>
      </div>
      <div class="UnderHead">
        <div class="Follow">
          <Point class="Point"></Point>
          Theo dõi đơn hàng
          <Triangle class="Triangle"></Triangle>
          <div class="HoverFollow">
            <input type="text" placeholder="Vui lòng nhập mã đơn hàng" />
            <input type="text" placeholder="Vui lòng nhập email đặt hàng" />
            <div class="Text">
              Nếu bạn có thắc mắc ?
              <a>Bấm vào đây</a>
            </div>
            <button>THEO DÕI</button>
          </div>
        </div>
        <div class="Guarantee">Tra cứu bảo hành</div>
      </div>
    </div>
    <div class="Information">
      <div class="Align">
        <div class="Phone">
          <img src="../../assets/phone.png" />
          <a href="tel:0824.672.075"> 0824.672.075 </a>
        </div>
        <div class="Cart">
          <img src="../../assets/cartblack.png" />
          <div class="Text">
            <h1>Giỏ hàng</h1>
            <RouterLink class="Link" to="/cart"> {{ this.Number }} sản phẩm</RouterLink>
          </div>
        </div>
      </div>
    </div>
    <div class="Nav">
      <div v-if="this.Nav" class="NavTemp1">
        <RouterLink to="/" class="IconHome">
          <Home class="Home"></Home>
        </RouterLink>
        <div class="point-list">
          <div class="Content">
            TIN TỨC
            <Triangle class="Triangle"></Triangle>
          </div>
          <ul class="hover-list">
            <li>Tin khuyến mãi</li>
            <li>Tin RC trong nước</li>
            <li>Tin RC quốc tế</li>
            <li>Hướng dẫn cho người mới chơi</li>
          </ul>
        </div>
        <div class="point-list">
          <div class="Content">
            LIÊN HỆ
            <Triangle class="Triangle"></Triangle>
          </div>
          <ul class="hover-list">
            <li>Giới thiệu</li>
            <li>Liên hệ cửa hàng</li>
            <li>Tài khoản ngân hàng</li>
            <li>Hướng dẫn mua hàng</li>
            <li>Chính sách ngân hàng</li>
          </ul>
        </div>
      </div>
      <div v-else class="NavTemp2">
        <RouterLink to="/" class="IconHome">
          <Home class="Home"></Home>
        </RouterLink>
        <div class="point-list">
          <div class="Content">
            TIN TỨC
            <Triangle class="Triangle"></Triangle>
          </div>
          <ul class="hover-list">
            <li>Tin khuyến mãi</li>
            <li>Tin RC trong nước</li>
            <li>Tin RC quốc tế</li>
            <li>Hướng dẫn cho người mới chơi</li>
          </ul>
        </div>
        <div class="point-list">
          <div class="Content">
            LIÊN HỆ
            <Triangle class="Triangle"></Triangle>
          </div>
          <ul class="hover-list">
            <li>Giới thiệu</li>
            <li>Liên hệ cửa hàng</li>
            <li>Tài khoản ngân hàng</li>
            <li>Hướng dẫn mua hàng</li>
            <li>Chính sách ngân hàng</li>
          </ul>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import Key from '../icons/Key.vue'
import Point from '../icons/Point.vue'
import Search from '../icons/Search.vue'
import Triangle from '../icons/Triangle.vue'
import User from '../icons/User.vue'
import Home from '../icons/HomeIcon.vue'
import { RouterLink } from 'vue-router'
</script>

<script>
export default {
  name: 'header',
  data() {
    return {
      Nav: 1,
      Number: 0
    }
  },
  mounted() {
    if (localStorage.cart) {
      let Object = JSON.parse('[' + localStorage.cart + ']')
      console.log(Object.length)
      this.Number = Object.length
    }
    let scrollPos = window.scrollY
    window.addEventListener('scroll', () => {
      //check where the scroll y is
      this.currentPath = window.location.pathname
      scrollPos = window.scrollY
      if (scrollPos >= 50) {
        this.Nav = 0
      } else {
        this.Nav = 1
      }
    })
  }
}
</script>

<style scoped src="./Header.css"></style>
