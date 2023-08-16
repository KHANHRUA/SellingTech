<template>
  <div class="Container">
    <div class="part1">
      <div class="Contact">
        <div class="Text">LIÊN HỆ VỚI CHÚNG TÔI</div>
        <ul>
          <li>Cửa hàng đồ chơi mô hình Thai Tuan hobby</li>

          <li>
            <Location class="Location"></Location> Địa chỉ: Số 7 khu giãn dân Mộ Lao - Tổ 16 -
            Phường Mộ Lao - Quận Hà Đông- Hà Nội
          </li>
          <li><Phone class="Phone"></Phone> 0936.336.128</li>
          <li><Mail class="Mail"></Mail> Email: hobbyshop1988@gmail.com</li>
        </ul>
      </div>
      <div class="Information">
        <div class="Text">THÔNG TIN CHUNG</div>
        <ul>
          <li>Giới thiệu</li>
          <li>Hướng dẫn mua hàng</li>
          <li>Bản đồ</li>
          <li>Thông tin tài khoản</li>
          <li>Thông tin khuyến mại</li>
        </ul>
      </div>
      <div class="Policy">
        <div class="Text">CHÍNH SÁCH CỬA HÀNG</div>
        <ul>
          <li>Chính sách bán hàng online</li>
          <li>Quy định bảo hành</li>
          <li>Quy định đổi trả hàng</li>
          <li>Chính sách thẻ khách hàng</li>
          <li>Chính sách dành cho đại lý</li>
        </ul>
      </div>
      <div class="Link">
        <div class="Text">LIÊN KẾT NHANH</div>
        <ul>
          <li>Brands</li>
          <li>Gift Vouchers</li>
          <li>Affiliates</li>
          <li>Specials</li>
        </ul>
      </div>
      <div class="FaceBook">
        <div class="Text">ĐỒNG HÀNH CÙNG CHÚNG TÔI</div>
        <div>
          <iframe
            src="https://www.facebook.com/plugins/page.php?href=https%3A%2F%2Fwww.facebook.com%2Fthaituanhobby&amp;tabs=timeline&amp;width=320&amp;height=230&amp;small_header=false&amp;adapt_container_width=true&amp;hide_cover=false&amp;show_facepile=true"
            width="320"
            height="230"
            style="border: none; overflow: hidden"
            scrolling="no"
            frameborder="0"
            allowtransparency="true"
            allow="encrypted-media"
          ></iframe>
        </div>
      </div>
    </div>
    <div class="part2">
      <div class="Left">
        <div class="Text">ĐĂNG KÝ NHẬN TIN</div>
        <div class="Input">
          <input type="text" placeholder="Điền địa chỉ Email của bạn" />
          <button>GỬI</button>
        </div>
      </div>
      <div class="Right">
        <div class="Text">ĐỒNG HÀNH CÙNG CHÚNG TÔI</div>
        <div class="AlignIcons">
          <FB class="Icon"></FB>
          <G class="Icon"></G>
          <YT class="Icon"></YT>
        </div>
      </div>
    </div>
    <div class="part3">Thiết kế web bởi NHANH.VN</div>
  </div>
</template>

<script setup>
import Phone from '../icons/Phone.vue'
import Mail from '../icons/Mail.vue'
import Location from '../icons/Location.vue'
import YT from '../icons/YT.vue'
import FB from '../icons/Fb.vue'
import G from '../icons/G+.vue'
</script>

<style scoped src="./Footer.css"></style>
