<template>
  <v-container>
    <TitleSecondary :textTitle="'Nuestros artículos'"></TitleSecondary>
    <v-row>
      <v-col cols="12" md="4" justify="center" align="center">
        <div class="sidebar">
          <LinkActive
            v-for="link in links"
            :key="link.id"
            :btnActive="btnActive"
            :data="link"
            @btnActiveFunction="btnActiveFunction"
          ></LinkActive>
        </div>
      </v-col>
      <v-col cols="12" md="8">
        <v-row>
          <div v-if="products.length == 0">
            <h3>Sin productos que mostrar.</h3>
          </div>
          <CardProduct
            v-else
            v-for="product in products"
            :key="product.id"
            :product="product"
          />
        </v-row>
      </v-col>
    </v-row>
    <br />
    <TitleSecondary :textTitle="'Contáctanos'"></TitleSecondary>
    <v-row align="center" justify="center">
      <v-col cols="8">
        <v-form ref="form" v-model="validData" lazy-validation>
          <v-row>
            <v-col cols="6">
              <p class="label-personalized"><strong>Nombre</strong></p>
              <v-text-field
                v-model="name"
                :rules="[(v) => !!v || 'Nombre es requerido']"
                outlined
                required
              ></v-text-field>
            </v-col>
            <v-col cols="6">
              <p class="label-personalized"><strong>Apellido</strong></p>
              <v-text-field
                v-model="lastname"
                :rules="[(v) => !!v || 'Apellido es requerido']"
                outlined
                required
              ></v-text-field>
            </v-col>
            <v-col cols="6">
              <p class="label-personalized">
                <strong>Correo electronico</strong>
              </p>
              <v-text-field
                v-model="email"
                :rules="[(v) => !!v || 'Correo electronico es requerido']"
                outlined
                required
              ></v-text-field>
            </v-col>
            <v-col cols="6">
              <p class="label-personalized"><strong>Telefono</strong></p>
              <v-text-field
                v-model="phone"
                :rules="[(v) => !!v || 'Telefono es requerido']"
                outlined
                required
              ></v-text-field>
            </v-col>
          </v-row>
          <v-col class="text-right">
            <v-btn
              :disabled="!validData"
              class="mr-4 btn-meat"
              @click="sendData()"
            >
              Enviar
            </v-btn>
          </v-col>
        </v-form>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import CardProduct from "@/components/CardProduct.vue";
import LinkActive from "@/components/LinkActive.vue";
import TitleSecondary from "@/components/TitleSecondary.vue";

export default {
  name: "IndexPage",
  components: {
    CardProduct,
    LinkActive,
    TitleSecondary,
  },
  async asyncData({ $axios }) {
    try {
      const result = await $axios.$get(
        "https://5eed24da4cbc340016330f0d.mockapi.io/api/articles"
      );

      return {
        products: result,
      };
    } catch (error) {
      console.error("error :", error);
    }
  },
  data() {
    return {
      validData: false,
      name: "",
      lastname: "",
      email: "",
      phone: "",
      products: [],
      btnActive: {
        id: 1,
        text: "Todos",
        endpoint: "https://5eed24da4cbc340016330f0d.mockapi.io/api/articles",
      },
      links: [
        {
          id: 1,
          text: "Todos",
          endpoint: "https://5eed24da4cbc340016330f0d.mockapi.io/api/articles",
        },
        {
          id: 2,
          text: "Productos",
          endpoint:
            "https://5eed24da4cbc340016330f0d.mockapi.io/api/articles?filter=Productos",
        },
        {
          id: 3,
          text: "Recetas",
          endpoint:
            "https://5eed24da4cbc340016330f0d.mockapi.io/api/articles?filter=Recetas",
        },
        {
          id: 4,
          text: "Consejos",
          endpoint:
            "https://5eed24da4cbc340016330f0d.mockapi.io/api/articles?filter=Consejos",
        },
      ],
    };
  },

  methods: {
    async btnActiveFunction(btnActiveId) {
      this.btnActive = btnActiveId;
      const result = await this.$axios.$get(btnActiveId.endpoint);
      this.products = result;
    },

    async sendData() {
      this.$refs.form.validate();

      if (
        this.name === "" ||
        this.lastname === "" ||
        this.email === "" ||
        this.phone === ""
      ) {
        return;
      }
      console.log(this.phone);
      try {
        const result = await this.$axios.$post(
          "https://5eed24da4cbc340016330f0d.mockapi.io/api/newsletter",
          {
            firstname: this.name,
            lastname: this.lastname,
            email: this.email,
            phone: this.phone,
          }
        );
        this.$swal(
          "Excelente",
          "Se ha enviado tus datos correctamente",
          "success"
        );
      } catch (error) {
        this.$swal("Algo ha ocurrido", "Por favor intenta mas tarde", "error");
      }
    },
  },
};
</script>

<style>
.label-personalized {
  margin-bottom: 10px;
}

.title-secondary {
  font-family: "Caveat";
  line-height: 38px;
  font-size: 80px;
  color: #3f454a;
}

.brush-secondary {
  position: relative;
  width: 464px;
  height: 85px;
  /* left: 488px; */
  top: -55px;
  background: url("/BRUSH-5-1.png");
  margin-top: 31px;
}

.sidebar {
  padding-top: 24px;
  padding-left: 23px;
  padding-right: 23px;
  padding-bottom: 118px;
  width: 319px;
  background: #ffffff;
  box-shadow: 0px 4px 40px rgba(0, 0, 0, 0.07);
  border-radius: 10px;
}

.btn-meat {
  height: 55px !important;
  min-width: 64px !important;
  padding: 0 16px !important;
  width: 170px !important;
  background-color: #d8ad3d !important;
  border-radius: 25px !important;
  color: white !important;
  font-weight: 700;
  font-size: 15px !important;
  line-height: 28px;
}
@media (max-width: 1264px) {
  .sidebar {
    width: 280px;
  }
}
@media (max-width: 960px) {
  .sidebar {
    width: 100%;
  }
}
</style>
