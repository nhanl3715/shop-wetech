<template>
  <div>
    <base-header
      class="header pb-8 pt-5 pt-lg-8 d-flex align-items-center"
      style="
        min-height: 100px;
        background-image: url(img/theme/profile-cover.jpg);
        background-size: cover;
        background-position: center top;
      "
    >
      <!-- Mask -->
      <span class="mask bg-gradient-success opacity-8"></span>
      <!-- Header container -->
      <div class="container-fluid d-flex align-items-center"></div>
    </base-header>
    <!-- Main content -->
    <!-- Page content -->
    <div class="container-fluid mt--7">
      <div class="row">
        <div class="col">
          <div class="card">
            <!-- Card header -->
            <div class="card-header border-0">
              <h5>Xem chi tiết - Cập nhật</h5>
            </div>
            <div class="card-body">
              <form>
                <h6 class="heading-small text-muted mb-4">Thông tin cơ bản</h6>
                <div class="pl-lg-4">
                  <div class="row">
                    <!-- Tên sản phẩm -->
                    <div class="col-lg-6">
                      <div class="form-group">
                        <label class="form-control-label"> Tên sản phẩm </label>
                        <input
                          type="text"
                          class="form-control"
                          placeholder="Tên sản phẩm"
                          :value="product.product_name"
                          readonly
                        />
                      </div>
                    </div>
                    <!-- Thương hiệu -->
                    <div class="col-lg-6">
                      <div class="form-group">
                        <label class="form-control-label">Thương hiệu</label>
                        <input
                          type="text"
                          class="form-control"
                          placeholder="Thương hiệu"
                          :value="product.brand"
                          readonly
                        />
                      </div>
                    </div>
                  </div>
                  <div class="row">
                    <!-- danh mục chính -->
                    <div class="col-lg-6">
                      <div class="form-group">
                        <label class="form-control-label" for
                          >Danh mục chính</label
                        >
                        <input
                          type="text"
                          class="form-control"
                          readonly
                          :value="product.category"
                        />
                      </div>
                    </div>
                    <!-- danh mục con -->
                    <div class="col-lg-6">
                      <div class="form-group">
                        <label class="form-control-label" for
                          >Danh mục con</label
                        >
                        <input
                          type="text"
                          class="form-control"
                          :value="product.cate_name"
                          readonly
                        />
                      </div>
                    </div>
                  </div>
                </div>
                <hr class="my-4" />
                <!-- Chi tiết sản phẩm -->
                <h6 class="heading-small text-muted mb-4">Chi tiết sản phẩm</h6>
                <div class="pl-lg-4" id="detailNext">
                  <div class="row">
                    <!-- Kích thước sản phẩm -->
                    <div class="col-lg-4">
                      <div class="form-group">
                        <label class="form-control-label"
                          >Thông số kích thước</label
                        >
                        <input
                          class="form-control"
                          type="text"
                          placeholder="VD: 5 x 6 x 7"
                          v-model="product.dimension"
                        />
                      </div>
                    </div>
                    <!-- Cân nặng  -->
                    <div class="col-lg-4">
                      <div class="form-group">
                        <label class="form-control-label">Cân nặng (Kg)</label>
                        <input
                          type="number"
                          class="form-control"
                          placeholder
                          v-model="product.weight"
                          min="0"
                        />
                      </div>
                    </div>
                    <!-- Nguồn gốc -->
                    <div class="col-lg-4">
                      <div class="form-group">
                        <label class="form-control-label">Nguồn gốc</label>
                        <input
                          type="text"
                          class="form-control"
                          placeholder="VD: NXB; Tác giả; Quốc gia;..."
                          v-model="product.origin"
                        />
                      </div>
                    </div>
                  </div>

                  <div class="row">
                    <!-- Đơn giá -->
                    <div class="col-lg-4">
                      <div class="form-group">
                        <label class="form-control-label">Đơn giá</label>
                        <div class="input-group mb-3">
                          <input
                            type="number"
                            class="form-control"
                            placeholder="VD:99000"
                            v-model="product.price"
                          />
                          <div class="input-group-append">
                            <span class="input-group-text">VNĐ</span>
                          </div>
                        </div>
                      </div>
                    </div>
                    <!-- Số lượng kho -->
                    <div class="col-lg-4">
                      <div class="form-group">
                        <label class="form-control-label">Số lượng nhập</label>
                        <input
                          type="number"
                          class="form-control"
                          placeholder="VD: 1; 2;..."
                          min="0"
                          v-model="product.quantity"
                        />
                      </div>
                    </div>
                    <div class="col-lg-4">
                      <div class="form-group">
                        <label class="form-control-label">Khuyến mãi ?</label>
                        <select
                          class="form-control"
                          v-model="product.status_discount"
                        >
                          <option value="1" selected>Khuyến mãi</option>
                          <option value="0" selected>Không khuyến mãi</option>
                        </select>
                      </div>
                    </div>
                  </div>
                  <div class="row" v-if="product.status_discount==1">
                    <!-- Giá giảm -->
                    <div class="col-lg-4">
                      <div class="form-group">
                        <label class="form-control-label">Giảm giá (%)</label>
                        <div class="input-group mb-3">
                          <input
                            type="number"
                            class="form-control"
                            placeholder="VD: 55; 45..."
                            v-model="product.percent"
                            min="0"
                            max="100"
                          />
                          <div class="input-group-append">
                            <span class="input-group-text">%</span>
                          </div>
                        </div>
                      </div>
                    </div>
                    <!-- Từ ngày -->
                    <div class="col-lg-4">
                      <div class="form-group">
                        <label class="form-control-label">Từ ngày</label>
                        <input
                          type="datetime-local"
                          class="form-control"
                          v-model="product.from_day"
                        />
                      </div>
                    </div>
                    <!-- Từ ngày -->
                    <div class="col-lg-4">
                      <div class="form-group">
                        <label class="form-control-label">Đến ngày</label>
                        <input
                          type="datetime-local"
                          class="form-control"
                          v-model="product.to_day"
                        />
                      </div>
                    </div>
                  </div>

                  <div class="row">
                    <!-- Kích thước sản phẩm -->
                    <div class="col-lg-6">
                      <div class="form-group">
                        <label class="form-control-label">Màu sắc</label>
                        <input
                          class="form-control"
                          type="color"
                          placeholder="VD: Đỏ; Xanh; Trắng,..."
                          v-model="product.color"
                        />
                      </div>
                    </div>
                    <!-- Cân nặng  -->
                    <div class="col-lg-6">
                      <div class="form-group">
                        <label class="form-control-label">Công suất</label>
                        <div class="input-group mb-3">
                          <input
                            class="form-control"
                            type="text"
                            placeholder="VD: 1W; 0.5W;..."
                            v-model="product.wattage"
                          />
                        </div>
                      </div>
                    </div>
                  </div>

                  <div class="row">
                    <!-- Kích thước sản phẩm -->
                    <div class="col-lg-6">
                      <div class="form-group">
                        <label class="form-control-label">Chất liệu</label>
                        <input
                          class="form-control"
                          type="text"
                          placeholder="VD: Giấy; nhựa;..."
                          v-model="product.material"
                        />
                      </div>
                    </div>
                    <!-- Cân nặng  -->
                    <div class="col-lg-6">
                      <div class="form-group">
                        <label class="form-control-label"
                          >Sản phẩm đi kèm / Quà tặng</label
                        >
                        <div class="input-group mb-3">
                          <input
                            class="form-control"
                            type="text"
                            placeholder="Nhập sản phẩm kèm theo..."
                            v-model="product.accessory"
                          />
                        </div>
                      </div>
                    </div>
                  </div>
                </div>
                <hr class="my-4" />
                <!-- Description -->
                <h6 class="heading-small text-muted mb-4">Mô tả</h6>
                <div class="pl-lg-4">
                  <div class="form-group">
                    <label class="form-control-label">Mô tả ngắn</label>
                    <ckeditor
                      v-model="product.introduction"
                      :config="editorConfig"
                      :editor-url="editorUrl"
                    ></ckeditor>
                  </div>
                  <div class="form-group">
                    <label class="form-control-label">Thêm hình ảnh</label>
                    <div class="row text-center">
                      <div class="col-2" v-for="(img,index) in imageData" :key="index">
                        <RefUpdate :imageProps="img.image" />
                      </div>
                    </div>
                  </div>
                  <div class="form-group">
                    <label class="form-control-label">Mô tả chi tiết</label>
                    <ckeditor
                      v-model="product.description"
                      :config="editorConfig"
                      :editor-url="editorUrl"
                    ></ckeditor>
                  </div>
                  <div class="form-group">
                    <input
                      type="button"
                      class="btn btn-primary"
                      value="Cập nhật sản phẩm"
                      @click="updateProduct"
                    />
                    <input type="button" class="btn btn-danger" value="Hủy" />
                  </div>
                </div>
              </form>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Axios from "axios";
import $ from "jquery";
import { store, EventBus, server } from "./../../main";
import RefUpdate from "./../ViewDetailsAndUpdate/RefUpdate.vue";
import swal from "sweetalert";

export default {
  data() {
    return {
      danhMucChinh: "",
      danhMucCon: "",
      imgArr: [],
      imageData:[],
      product_id: null,
      demo:"http://res.cloudinary.com/dtvapimtn/image/upload/c_fit,h_640,w_640/v1/products/pngtree-refund-money-icon-chargeback-contour-sign-quick-fund-cash-png-image_448788.png",
      
      product: {
        quantity: 0,
        size: null,
        color: null,
        price: null,
        status: null,
        origin: null,
        accessory: null,
        dimension: null,
        weight: null,
        system: null,
        material: null,
        screen_size: null,
        wattage: null,
        volume: null,
        resolution: null,
        memory: null,
        product_name: null,
        brand: null,
        introduction: null,
        description: null,
        tag: null,
        status_discount: "0",
        status_product: "0",
        percent: null,
        from_day: null,
        to_day: null,

        shop_id: null,

        cate_id: null,
      },

      editorUrl: "https://cdn.ckeditor.com/4.14.1/full-all/ckeditor.js",
      editorData: "",
      editorConfig: {
        toolbarGroups: [
          { name: "document", groups: ["mode", "document", "doctools"] },
          { name: "clipboard", groups: ["clipboard", "undo"] },
          {
            name: "editing",
            groups: ["find", "selection", "spellchecker", "editing"],
          },
          { name: "forms", groups: ["forms"] },
          { name: "basicstyles", groups: ["basicstyles", "cleanup"] },
          {
            name: "paragraph",
            groups: ["list", "indent", "blocks", "align", "bidi", "paragraph"],
          },
          { name: "links", groups: ["links"] },
          { name: "insert", groups: ["insert"] },
          { name: "styles", groups: ["styles"] },
          { name: "colors", groups: ["colors"] },
          { name: "tools", groups: ["tools"] },
          { name: "others", groups: ["others"] },
          { name: "about", groups: ["about"] },
        ],
        removeButtons:
          "NewPage,Print,Save,Templates,Replace,Find,SelectAll,Scayt,Form,Checkbox,Radio,TextField,Textarea,Select,Button,ImageButton,HiddenField,CreateDiv,Anchor,Flash,Smiley,PageBreak,ShowBlocks,About,Language,Iframe,Image",
      },
    };
  },
  components: {
    RefUpdate,
  },
  methods: {
    updateProduct() {
      Axios.post(`${server}/update-product`, {
        quantity: this.product.quantity,
        size: this.product.size,
        color: this.product.color,
        price: this.product.price,
        status: this.product.status,
        origin: this.product.origin,
        accessory: this.product.accessory,
        dimension: this.product.dimension,
        weight: this.product.weight,
        system: this.product.system,
        material: this.product.material,
        screen_size: this.product.screen_size,
        wattage: this.product.wattage,
        volume: this.product.volume,
        resolution: this.product.resolution,
        memory: this.product.memory,
        product_name: this.product.product_name,
        brand: this.product.brand,
        introduction: this.product.introduction,
        description: this.product.description,
        tag: this.product.tag,
        status_discount: this.product.status_discount,
        status_product: "0",
        percent: this.product.percent,
        from_day: null,
        to_day: null,

        shop_id: this.product.shop_id,

        cate_id: this.product.cate_id,
        image: JSON.stringify(this.imgArr),

        prodetail_id: this.product.prodetail_id,
        product_id: this.product.product_id,
      })
        .then((re) => {
          console.log(re.data);
          if (re.data.success) {
            setTimeout(function () {
              window.location.reload(1);
            }, 1000);
            swal({
              title: "Thành công!",
              icon: "success",
              buttons: false,
            });
          }
        })
        .catch(() => {
          swal({
            title: "Thất bại!",
            icon: "error",
            button: "Kiểm tra lại",
          });
        });
    },
  },
  created() {
    $(".modal-backdrop").removeClass("modal-backdrop");
    function getCookie(cname) {
      var name = cname + "=";
      var ca = document.cookie.split(";");
      for (var i = 0; i < ca.length; i++) {
        var c = ca[i];
        while (c.charAt(0) == " ") c = c.substring(1);
        if (c.indexOf(name) == 0) return c.substring(name.length, c.length);
      }
      return "";
    }

    this.product.shop_id = JSON.parse(getCookie("shop_id"));

    this.product = store.state.ViewProductDetail;
    this.product_id = store.state.category_id;

    //xử lý ngày
    //từ ngày
    let tuNgaytrave = this.product.created_at.replace(' ','T');
    let tuNgayNhan = tuNgaytrave.slice(0,16);
    this.product.from_day = tuNgayNhan;
    //đến ngày
    let denNgaytrave = this.product.updated_at.replace(' ','T');
    let denNgayNhan = denNgaytrave.slice(0,16);
    this.product.to_day = denNgayNhan;

    EventBus.$on("bus-upload-image", (data) => {
      this.imgArr.push(data);
    });

    this.imageData = store.state.iamageData
  },
};
</script>

<style>
.swal{
  padding-bottom: 40px;
}
</style>

