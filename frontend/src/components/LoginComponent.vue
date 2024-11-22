<template>
    <div class="section no-pad-bot" id="index-banner">
        <div class="container" style="margin-bottom: 50px;">
            <div class="row">
                <div class="col offset-m3 m6">
                    <h1 class="text-center" style="margin-bottom: 50px; text-align: center;">ĐĂNG NHẬP</h1>

                    <!-- Form đăng nhập -->
                    <form method="POST" v-on:submit.prevent="doLogin">
                        <div class="form-group">
                            <label class="text-white">Nhập email của bạn:</label>
                            <input type="email" class="form-control" name="email" autocomplete="off" required />
                        </div>

                        <br />

                        <div class="form-group">
                            <label class="text-white">Nhập mật khẩu của bạn:</label>
                            <input type="password" class="form-control" name="password" autocomplete="off" required />
                        </div>

                        <br />

                        <!-- Nút submit đăng nhập -->
                        <input type="submit" value="Vào cửa hàng" v-bind:disabled="isLoading" name="submit"
                            class="btn btn-primary" />
                    </form>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
import axios from "axios";
import swal from "sweetalert2";
import store from "../vuex/store";
import "materialize-css/dist/css/materialize.min.css";
import "materialize-css/dist/js/materialize.min.js";

export default {
    data() {
        return {
            // Trạng thái đang tải khi người dùng thực hiện đăng nhập
            isLoading: false,
        };
    },

    methods: {
        // Hàm thực hiện đăng nhập
        async doLogin(event) {
            const form = event.target; // Lấy form từ sự kiện
            const formData = new FormData(form); // Tạo dữ liệu form

            this.isLoading = true; // Kích hoạt trạng thái tải

            try {
                // Gửi yêu cầu đăng nhập tới API
                const response = await axios.post(this.$apiURL + "/login", formData);

                // Hiển thị thông báo kết quả
                swal.fire("Login", response.data.message, response.data.status);

                if (response.data.status === "success") {
                    // Reset form nếu đăng nhập thành công
                    form.reset();

                    // Lấy access token từ phản hồi của server
                    const accessToken = response.data.accessToken;
                    // Lưu token vào localStorage
                    localStorage.setItem(this.$accessTokenKey, accessToken);

                    // Cập nhật headers mặc định với token
                    this.$headers = {
                        "Content-Type": "application/json",
                        Authorization: "Bearer " + accessToken,
                    };

                    // Cập nhật trạng thái người dùng trong Vuex store
                    store.commit("setLogin", true);
                    store.commit("setUser", response.data.user);

                    // Khởi tạo dropdown sau khi đăng nhập
                    this.initDropdown();

                    // Chuyển hướng về trang chủ
                    this.$router.push("/");
                }
            } catch (error) {
                // Xử lý lỗi đăng nhập
                swal.fire("Error", "Đăng nhập thất bại. Vui lòng thử lại.", "error");
            } finally {
                // Tắt trạng thái tải
                this.isLoading = false;
            }
        },

        // Hàm khởi tạo dropdown
        initDropdown() {
            // Đảm bảo DOM đã sẵn sàng trước khi khởi tạo
            this.$nextTick(() => {
                const elems = document.querySelectorAll(".dropdown-trigger");
                if (elems.length > 0) {
                    // eslint-disable-next-line no-undef
                    M.Dropdown.init(elems, {});
                }
            });
        },
    },

    mounted() {
        // Khởi tạo dropdown sau khi component đã render
        this.initDropdown();
    },
};
</script>
<style>
/* Định dạng nhãn */
label {
    font-size: initial;
}
</style>
