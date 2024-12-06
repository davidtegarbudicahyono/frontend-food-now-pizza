<template>
    <div class="home-page container">
      <div class="row">
        <!-- Pilihan Pizza -->
        <section class="cart1 col-lg-9 mt-5 mb-5">
          <section class="choose-pizza">
            <h2 class="section-title">Choose your pizza</h2>
            <div class="pizza-list row">
              <div class="pizza-item col-md-4" v-for="pizza in pizzas" :key="pizza.id">
                <div class="card">
                  <div 
                    class="card-body" 
                    :class="{ selected: selectedPizza === pizza.id }"
                    @click="selectPizza(pizza.id)"
                  >
                    <div class="offer-badge" v-if="pizza.discount.is_active">
                        <img src="@/assets/img/ribbon.svg" alt="Offer Badge" />
                    </div>
                    <div>
                        <img 
                        class="pizza-image" :src="getStaticImageSrc(pizza.name)" :alt="pizza.name"/>
                    </div>
                    <div>
                        <h5 class="card-title">{{ pizza.name }}</h5>
                        <p class="price-pizza">
                            <span class="current-price ">${{ pizza.discount.final_price }}.00</span>
                            <span v-if="pizza.discount.is_active" class="original-price">${{ pizza.price }}.00</span>
                        </p>
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </section>

          <!-- Customisasi Pizza -->
          <section class="custom-pizza mt-5">
            <h2 class="section-title">Custom Pizza</h2>
      
            <!-- Pilihan Ukuran -->
            <div class="size-options mb-4">
              <h5>Size</h5>
              <div 
                class="form-check form-check-inline" 
                v-for="size in sizes" 
                :key="size.id">
                <input
                  class="form-check-input"
                  type="radio"
                  :id="'size-' + size.id"
                  :value="size.id"
                  v-model="selectedSize"
                />
                <label class="form-check-label" :for="'size-' + size.id">
                  {{ size.name }} ({{ size.extra_price > 0 ? `+ $${size.extra_price}` : 'Free' }})
                </label>
              </div>
            </div>
      
            <!-- Pilihan Topping -->
            <div class="toppings">
              <h5>Toppings</h5>
              <div class="row gx-2 gy-3">
                <div
                  class="col-6 col-sm-4 col-md-2"
                  v-for="topping in toppings"
                  :key="topping.id"
                >
                  <button
                    class="topping-button"
                    :class="{ 'btn-primary': selectedToppings.includes(topping.id) }"
                    @click="toggleTopping(topping.id)"
                    :disabled="!isToppingAvailableForSelectedPizza(topping.id)"
                  >
                    <p class="topping-name mb-0">{{ topping.name }}</p>
                    <small class="topping-price text-muted">+ ${{ topping.price }}</small>
                  </button>
                </div>
              </div>
            </div>

          </section>
        </section>
  
        <!-- Harga Total -->
        <div class="col-lg-3 mt-5 mb-5">
            <aside class="payment-summary">
              <h3>Payment Summary</h3>
              <ul class="payment-list">
                <li>
                  <span class="item-name">Pizza</span>
                  <span class="item-price">{{ selectedPizzaName }}</span>
                </li>
                <li>
                  <span class="item-name">Size</span>
                  <span class="item-price">{{ selectedSizeName }}</span>
                </li>
                <li v-for="topping in selectedToppingsDetails" :key="topping.id">
                  <span class="item-name">{{ topping.name }}</span>
                  <span class="item-price">+${{ topping.price }}</span>
                </li>
              </ul>
              <hr>
              <p class="total-price">Total Price: <span>${{ calculateTotalPrice().toFixed(2) }}</span> </p>
              <button class="button-order w-100" @click="ShowModal = true">Order Now</button>
            </aside>
        </div>
        <!-- Modal Order Success -->
        <div
          v-if="ShowModal"
          class="modal fade show d-block"
          tabindex="-1"
          role="dialog"
          aria-labelledby="orderSuccessModalLabel"
          aria-hidden="true"
          style="background: rgba(0, 0, 0, 0.5);"
        >
          <div class="modal-dialog modal-dialog-centered" role="document">
            <div class="modal-content">
              <div class="modal-body text-center">
                <img
                  src="@/assets/img/modal.gif"
                  alt="Success Icon"
                  class="mb-3"
                />
                <h5 class="modal-title mb-3" id="orderSuccessModalLabel">
                  Order Success
                </h5>
                <p>Thank you, we have received your order successfully.</p>
                <button 
                  type="button" 
                  class="button-close mt-3" 
                  @click="ShowModal = false">
                  Close
                </button>

              </div>
            </div>
          </div>
        </div>
    </div>
  </div>
</template>

<script>
import pizzaData from "@/assets/json/pizza-list.json";
import sizeData from "@/assets/json/size-list.json";
import toppingData from "@/assets/json/topping-list.json";

export default {
  data() {
    return {
      pizzas: pizzaData.data,
      sizes: sizeData.data,
      toppings: toppingData.data,
      selectedPizza: null,
      selectedSize: 1,
      selectedToppings: [],
      ShowModal: false,
    };
  },
  computed: {
    selectedPizzaName() {
      const pizza = this.pizzas.find((p) => p.id === this.selectedPizza);
      return pizza ? pizza.name : "None";
    },
    selectedSizeName() {
      const size = this.sizes.find((s) => s.id === this.selectedSize);
      return size ? size.name : "Small";
    },
    selectedToppingsDetails() {
      return this.selectedToppings.map((id) =>
        this.toppings.find((topping) => topping.id === id)
      );
    },
  },
  methods: {
    selectPizza(id) {
      this.selectedPizza = id;
      this.selectedToppings = [];
    },
    toggleTopping(toppingId) {
      if (this.selectedToppings.includes(toppingId)) {
        this.selectedToppings = this.selectedToppings.filter((id) => id !== toppingId);
      } else {
        this.selectedToppings.push(toppingId);
      }
    },
    getStaticImageSrc(pizzaName) {
      const formattedName = pizzaName.replace(/\s+/g, "-").toLowerCase(); 
      return `/src/assets/img/pizza/${formattedName}.png`;
    },
    calculateTotalPrice() {
      const pizza = this.pizzas.find((p) => p.id === this.selectedPizza);
      const size = this.sizes.find((s) => s.id === this.selectedSize);
      const toppingsPrice = this.selectedToppingsDetails.reduce(
        (sum, topping) => sum + (topping ? topping.price : 0),
        0 
      );

      return (
        (pizza ? pizza.discount.final_price : 0) +
        (size ? size.extra_price : 0) +
        toppingsPrice
      );
    },
    isToppingAvailableForSelectedPizza(toppingId) {
      const pizza = this.pizzas.find((p) => p.id === this.selectedPizza);
      return pizza ? pizza.toppings.includes(toppingId) : true;
    },
  },
};
</script>
