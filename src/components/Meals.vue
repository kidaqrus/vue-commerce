<template>
  <b-container>
    <div v-if="meals.length">
      <b-row>
        <div v-bind:key="meal.index" v-for="meal in meals">
          <b-col l="4">
            <b-card
              v-bind:img-src="
                `http://localhost:1337/uploads/burrito_chicken_delicious_dinner_461198_ad901865a5.jpeg`
              "
              v-bind:title="meal.title"
              img-alt="Image"
              img-top
              tag="article"
              style="max-width: 20rem;"
              class="mb-2"
            >
              <b-card-text>{{ `${meal.description}` }}</b-card-text>
              <span>
                <strong>Price: ${{ `${meal.price}` }} </strong>
              </span>
              <b-button @click="placeOrder" variant="primary">Order meal</b-button>
            </b-card>
          </b-col>
        </div>
      </b-row>
    </div>
  <div v-else>
      <h5 >Fetching meals . . .</h5>
    </div>
  </b-container>
</template>





<script>
export default {
  data() {
    return {
      meals: [],
      
    };
  },
  methods: {
    placeOrder() {
      window.FlutterwaveCheckout({
        public_key: "FLWPUBK_TEST-3ae2cc9e4849ef284fa47f649fe8e626-X",
        tx_ref: "new-sale"+ new Date(),
        amount:0.00,
        currency: "USD",
        country: "NG",
        payment_options: "card",
        customer: {
          email: "adikwusule@gmail.com",
          phone_number: "+2347068581947",
          name: "Ahmed Sule",
        },
        callback: function(data) {
          console.log(data);
        },
        onclose: function() {},
        customizations: {
          title: "MealsHub",
          description: "Payment for selected meal",
          logo: "http://localhost:1337/uploads/beef_b538baa14d.png",
        },
      });
    },
  },
  mounted() {
    fetch("http://localhost:1337/products")
      .then((res) => res.json())
      .then((data) => {
        this.meals = data;
      });
  },
  created() {
        const script = document.createElement("script");
        script.src = "https://checkout.flutterwave.com/v3.js";
        document.getElementsByTagName("head")[0].appendChild(script);
      },
};
</script>