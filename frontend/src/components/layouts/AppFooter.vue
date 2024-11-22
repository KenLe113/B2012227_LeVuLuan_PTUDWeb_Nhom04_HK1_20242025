<template>
  <footer class="page-footer blue">
    <div class="container">
      <div class="row">
        <div class="col l6 s12">
          <h5 class="white-text">Về cửa hàng LBooks </h5>
          <p class="grey-text text-lighten-4">
            LBooks là một cửa hàng sách hiện đại và thân thiện, nơi hội tụ hàng nghìn đầu sách đa dạng từ các lĩnh vực
            như văn học, kinh doanh, kỹ năng sống, khoa học, công nghệ, thiếu nhi và nhiều thể loại khác. Với sứ mệnh
            "Chia sẻ tri thức – Kết nối đam mê", LBooks không chỉ mang đến những cuốn sách chất lượng mà còn tạo ra một
            không gian để những người yêu sách có thể khám phá, học hỏi và phát triển bản thân.
          </p>
        </div>
        <div class="col l3 s12">
          <h5 class="white-text">Địa chỉ</h5>
          <ul>
            <li>
              <a class="white-text" href="#!">Khu 1 Đại học Cần Thơ</a>
            </li>
            <li>
              <a class="white-text" href="#!">Khu 2 Đại học Cần Thơ</a>
            </li>
            <li>
              <a Nga class="white-text" href="#!">Khu 3 Đại học Cần Thơ </a>
            </li>

          </ul>
        </div>
        <div class="col l3 s12">
          <h5 class="white-text">Liên hệ:</h5>
          <ul>
            <li><a class="white-text" href="#!">Facebook</a></li>
            <li><a class="white-text" href="#!">Zalo</a></li>
            <li><a class="white-text" href="#!">Instagram</a></li>
            <li><a class="white-text" href="#!">Tiktok</a></li>
          </ul>
        </div>
      </div>
    </div>
    <div class="footer-copyright">
      <div class="container">
        Made by
        <a class="orange-text text-lighten-3" href="#">Le Vu Luan B2012227</a>
      </div>
    </div>
  </footer>
</template>

<script>
import store from '../../vuex/store';
import '/public/assets/css/style.css';
export default {
  name: 'AppFooter',

  data() {
    return {
      page: 0,
    };
  },

  computed: {
    user: function () {
      return store.getters.getUser;
    },

    login: function () {
      return store.getters.getLogin;
    },
  },
};
</script>
