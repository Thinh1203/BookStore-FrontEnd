<template>
  <div class="header">
    <div class="menu">
      <form class="d-flex search">
        <input class="form-control ms-4 mt-3" type="search" placeholder="Search" aria-label="Search" v-model="search">
      </form>
        <div class="search-filter">
          <div v-for="book in filterBook" :key="book.title">
            <router-link :to="`/about/`">{{ book.title }}</router-link>
          </div>
        </div>
      <router-link :to="`/`"><img :src="require(`../assets/Logo.png`)" height="65" alt="logo" class="logo"/></router-link>
        <router-link :to="`/dashboard`" v-if="loggedInUser" class="flex-center username-text"> {{ loggedInUser.username }} </router-link>
        <a v-if="loggedInUser" class="flex-center logout" @click.prevent="logout"> Đăng xuất </a>
      <div>
          <router-link v-if="!loggedInUser" :to="`/login`" class="link">Đăng nhập</router-link>
          <router-link v-if="!loggedInUser" :to="`/register`" class="link">Đăng kí</router-link>

        <router-link :to="`/cart`">
          <a class="cart"><ThemifyIcon icon="bag" class="icon-cart"/>
            <div class="cart-info">
              <span class="cartCount">{{ getProductInCart.length }}</span>
            </div>
          </a>
        </router-link>
      </div>
    </div>
  </div>
</template>

<script>
import ThemifyIcon from "vue-themify-icons";
import { mapGetters, mapMutations } from "vuex";
// import ProductService from "../services/Product.service";

export default {
  name: 'Header',
  components: {
    ThemifyIcon
  },
  data() {
    return {
      currentUser: null,
      search: "",
      books: [],
      idLookup: []
    };
  },
  methods: {
    ...mapMutations([
            "initAuthState" 
        ]),
    logout() {
      this.$store.commit("logout");
      this.$router.push("login");
    }
  },
  computed: {
        ...mapGetters([
            "getProductInCart",
            "loggedInUser"
        ]),
        filterBook(){
          if(!this.search){
            return [];
          }else{
            return this.books.filter(book => book.title.includes(this.search));
          }
        }
  },
  mounted() {
    this.initAuthState();
  },
  // created() {
  //     this.handle(ProductService.getAllProduct())
  //     .then(response => {
  //       // console.log(response[1].data);
  //       this.books = response[1].data;
  //       console.log(this.books);
  //     });
  //   }
}
</script>

<style>
.header {
  /* background: rgb(245, 213, 213); */
  height: 80px;
  display: flex;
  align-items: center;
  margin-bottom: 32px;
}
.logo {
  margin-right: 270px;
}
.menu {
  padding: 0 16px;
  width: 100%;
  display: flex;
  justify-content: space-between;
}
.menu-item {
    font-family: "Cormorant Garamond",sans-serif;
    font-size: 20px;
    line-height: 23px;
    font-weight: 500;
    width: 100px;
    text-decoration: none;
    margin: 12px;
}
.icon-cart {
  font-size: 24px;
  float: right;
  margin-top: 24px;
  margin-left: 16px;
  margin-right: 54px;
  position: relative;
}
.cart {
  color: black;
  
}
.cart:hover {
  color: rgb(248, 90, 90);
}

.link {
  color: black;
  text-decoration: none;
  font-size: 20px;
  padding: 8px;
  line-height: 3.5;
}
.username-text, .logout {
  color: black;
  text-decoration: none;
  font-size: 20px;
  padding: 8px;
  line-height: 2.5;
}
.username-text {
  margin-right: -84px;
}
.logout{
  font-size: 17px;
  line-height: 2.5;
  color: rgb(214, 64, 64);
}
.search {
  width: 24%;
  height: 10%;
  opacity: 0;
}
.cart-info {
  position: absolute;
    right: 68px;
    top: 18px;
    font-size: 11px;
    background: #f2735c;
    color: #fff;
    padding: 0 3px;
    width: 20px;
    height: 20px;
    line-height: 20px;
    border-radius: 50%;
}
.cartCount {
  display: flex;
  justify-content: center;
  align-items: center;
}
.search-filter {
  z-index: 99;
  display: flex;
  width: 40px;
  flex-direction: column;
}
</style>
