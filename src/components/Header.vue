<template>
  <div>
    <header v-if="!$route.meta.hide" elevate-on-scroll>
      <div class="logo" id="center">
        <v-icon
          v-if="userIsAuthenticated"
          class="ml-5 mt-2"
          color="teal accent-2"
          x-large
          id="icon"
          >account_circle</v-icon
        >
        <v-icon v-else id="icon" class="ml-5 mt-2" color="grey darken-3" x-large
          >account_circle</v-icon
        >
      </div>

      <v-menu transition="slide-y-transition" bottom>
        <template v-slot:activator="{ on, attrs }">
          <v-btn id="listBtn" class="btn" v-bind="attrs" v-on="on">
            <v-icon class="icon" color="black">menu</v-icon>
          </v-btn>
        </template>
        <v-card id="list">
          <v-list>
            <v-list-item
              v-for="item in menuItems"
              :key="item.title"
              :to="item.link"
            >
              <v-icon id="iColor" class="icon">{{ item.icon }}</v-icon>
              <v-list-item-title>{{ item.title }}</v-list-item-title>
            </v-list-item>
            <v-icon id="iColor" class="icon">menu</v-icon>
          </v-list>
        </v-card>
      </v-menu>

      <div class="basket">
        <game-basket></game-basket>
      </div>
    </header>
  </div>
</template>

<script>
export default {
  data: () => ({
    drawer: false,
  }),
  computed: {
    menuItems() {
      let menuItems = [
        { icon: "home", title: "Home", link: "/home" },
        { icon: "videogame_asset", title: "Games", link: "/games" },
        { icon: "info", title: "About", link: "/about" },
        { icon: "login", title: "LogIn", link: "/login" },
      ];
      if (this.userIsAuthenticated) {
        menuItems = [
          { icon: "home", title: "Home", link: "/home" },
          { icon: "videogame_asset", title: "Games", link: "/games" },
          { icon: "info", title: "About", link: "/about" },
          { icon: "login", title: "LogIn", link: "/login" },
          { icon: "lock", title: "Admin", link: "/admin" },
        ];
      }
      return menuItems;
    },
    userIsAuthenticated() {
      return (
        this.$store.getters.user !== null &&
        this.$store.getters.user !== undefined
      );
    },
  },
};
</script>

<style lang="scss" scoped>
header {
  height: 60px;
  width: 100%;
  display: flex;
  justify-content: space-between;
}

.logo {
  position: fixed;
  z-index: 3;
  #icon {
    background-color: map-get($Colorscheme, header);
    border-radius: 50px;
  }
}
.btn {
  width: 200px;
  height: 50px !important;
  border-radius: 0 0 70px 70px;
  position: fixed;
  left: 50%;
  transform: translate(-50%);
  z-index: 3;
}
#list {
  border-radius: 0 0 50px 50px;
}
.theme--light.v-list {
  text-align: center;
  z-index: 2;
  background-color: transparent;
}
.v-menu__content {
  border-radius: 0 0 50px 50px;
  box-shadow: rgba(0, 0, 0, 0.8) 0 0 10px;
  margin-top: -20px;
}
.basket {
  position: fixed;
  z-index: 3;
  right: 0;
}

.icon {
  margin: 10px;
  cursor: pointer;
}

#listBtn,
#list {
  background-color: map-get($Colorscheme, header) !important;
}
#iColor {
  color: map-get($Colorscheme, icons);
}

#listBtn:hover {
  .icon {
    color: map-get($Colorscheme, icons) !important;
  }
}

a {
  text-decoration: none;
}
</style>