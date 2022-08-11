<template>
  <div class="header">
    <div class="header container">
      <div class="logo">
        <img src="../../assets/logo.svg" alt="" />
      </div>
      <div class="header-list">
        <router-link class="header-item" active-class="active" to="/" exact
          >Home</router-link
        >
        <router-link class="header-item" active-class="active" to="/about"
          >About</router-link
        >
        <router-link class="header-item" active-class="active" to="/product"
          >Product</router-link
        >
      </div>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      isActive: false,
    };
  },
};
</script>
<style>
.container {
  margin: 0 200px;
}
.header {
  background-color: pink;
}

.header .container {
  display: flex;
  justify-content: space-between;
  padding: 10px;
  align-items: center;
}

.logo img {
  width: 80px;
  height: 80px;
}

.header-list {
  display: flex;
  justify-content: space-between;
  width: 30%;
}

.header-item {
  font-size: 22px;
  text-decoration: none;
  color: #000;
  padding: 8px 16px;
}

.header-item:hover {
  color: #fff;
}

.active {
  color: #fff;
}
</style>
