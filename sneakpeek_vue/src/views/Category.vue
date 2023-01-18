<template>
  <div class="page-category">
    <div class="columns is-multiline">
      <div class="column is-12">
        <h2 class="is-size-2 has-text-centered">{{ category.name }}</h2>
      </div>

      <ProductBox 
   v-for="product in category.products"
   v-bind:key="product.id"
   v-bind:product="product" />
    </div>
  </div>
</template>

<script>
import axios from "axios";
import { toast } from "bulma-toast";
import ProductBox from "@/components/ProductBox.vue";

export default {
  name: "Category",
  components: {
    ProductBox
  },
  data() {
    return {
      category: {
        products: [],
      },
    };
  },
  mounted() {
    this.getCategory();
  },
//   makes sure category swithces smooth
  watch: {
    $route(to, from) {
        if (to.name === 'Category') {
            this.getCategory()
        }
    }
  },
  methods: {
    getCategory() {
      const categorySlug = this.$route.params.category_slug;

      axios
        .get(`/api/v1/products/${categorySlug}`)
        .then((response) => {
          this.category = response.data;
        })
        .catch((error) => {
          console.log(error);

          toast({
            message: "Sneaker was added to the cart",
            type: "is-success",
            dismissible: true,
            pauseOnHover: true,
            duration: 2000,
            position: "bottom-right",
          });
        });
    },
  },
};
</script>
