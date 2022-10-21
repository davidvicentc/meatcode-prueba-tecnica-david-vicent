<template>
  <v-app dark>
    <header class="header">
      <v-container>
        <v-row class="navbar-personalized">
          <h1 class="logo-navbar-class">Logo</h1>
          <div class="box-social">
            <img class="icon-social" src="/fb_icon.png" alt="" srcset="" />
            <img class="icon-social" src="/youtube_icon.png" alt="" srcset="" />
            <img src="/instagram_icon.png" alt="" srcset="" />
          </div>
        </v-row>
        <v-row style="margin-top: 144px">
          <h1 class="header-title">El secreto <br />de tu cocina</h1>
          <div class="brush"></div>
        </v-row>
      </v-container>
    </header>
    <Nuxt style="margin-top: 14px" />
  </v-app>
</template>

<script>
export default {
  name: "DefaultLayout",
  data() {
    return {};
  },
};
</script>

<style>
.box-social {
  display: flex;
  align-items: center;
}

.logo-navbar-class {
  font-family: "Caveat";
  color: #3f454a;
}

.navbar-personalized {
  display: flex;
  justify-content: space-between;
}

.header {
  padding: 60px;
  text-align: center;
  background: url("/bg.png");
  /* background: linear-gradient(180deg, rgba(255,255,255,1) 66%); */
  background-image: linear-gradient(
      to bottom,
      rgba(255, 255, 255, 0) 90%,
      rgb(255, 255, 255)
    ),
    url("/bg.png");
  height: 800px;
  font-size: 30px;
}

.header-title {
  font-family: "Caveat";
  color: #3f454a;
  font-size: 120px;
  line-height: 100px;
  font-weight: 700;
  z-index: 1;
}

.brush {
  background: url("/BRUSH.png");
  position: absolute;
  width: 1312px;
  height: 174px;
  left: -475.85px;
  top: 373.62px;
}

.icon-social {
  margin-right: 30px;
}
</style>
