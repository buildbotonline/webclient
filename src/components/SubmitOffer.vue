<script>
export default {
    data() {
        return {
            productData: {
                title: 'Add title',
                price: '0000',
                description: 'Add description',
                image: '',
                chat_id: '',
                payment_token: '',
                bot_token: '',
                payment_currency: 'RUB'
            }
        }
    },
    methods: {
            submitted() {
              const requestOptions = {
                method: "POST",
                headers: { "Content-Type": "application/json" },
                body: JSON.stringify({ 
                  chat_id: this.productData.chat_id,
                  title: this.productData.title,
                  description: this.productData.description,
                  payload: "invoice_sent",
                  provider_token: this.productData.payment_token,
                  currency: this.productData.payment_currency,
                  prices: [{amount: this.productData.price, label: this.productData.title}],
                  photo_url: this.productData.image,
                  photo_width: 500,
                  photo_height: 500,
                  need_name: true,
                  need_phone_number: true,
                  need_email: true,
                  need_shipping_address: true,
                  send_phone_number_to_provider: true,
                  send_email_to_provider: true,
                  disable_notification: true,
                  provider_data: {
                    receipt: {
                      items: [{
                        description: `${this.productData.title} ${this.productData.description}`,
                        quantity: "1.00",
                        amount: {
                          value: this.productData.price,
                          currency: this.productData.payment_currency,
                        },
                        vat_code: 1,
                      }],
                    },
                  },
                })
              };
              fetch(`https://api.telegram.org/bot${this.productData.bot_token}/sendInvoice`, requestOptions)
                .then(response => response.json())
                .then(data => (this.postId = data.id));
                        }
                    }
}
</script>

<template>
  <form class="w-full max-w-lg">
  <div class="md:flex md:items-center mb-6">
    <div class="md:w-1/3">
      <label class="block text-gray-500 font-bold md:text-right mb-1 md:mb-0 pr-4" for="product-title">
        Product title
      </label>
    </div>
    <div class="md:w-2/3">
      <input v-model="productData.title" class="bg-gray-200 appearance-none border-2 border-gray-200 rounded w-full py-2 px-4 text-gray-700 leading-tight focus:outline-none focus:bg-white focus:border-purple-500" id="product-title" type="text">
    </div>
  </div>
  <div class="md:flex md:items-center mb-6">
    <div class="md:w-1/3">
      <label class="block text-gray-500 font-bold md:text-right mb-1 md:mb-0 pr-4" for="product-description">
        Product description
      </label>
    </div>
    <div class="md:w-2/3">
      <input v-model="productData.description" class="bg-gray-200 appearance-none border-2 border-gray-200 rounded w-full py-2 px-4 text-gray-700 leading-tight focus:outline-none focus:bg-white focus:border-purple-500" id="product-description" type="text">
    </div>
  </div>
  <div class="md:flex md:items-center mb-6">
    <div class="md:w-1/3">
      <label class="block text-gray-500 font-bold md:text-right mb-1 md:mb-0 pr-4" for="product-price">
        Product price
      </label>
    </div>
    <div class="md:w-2/3">
      <input v-model="productData.price" class="bg-gray-200 appearance-none border-2 border-gray-200 rounded w-full py-2 px-4 text-gray-700 leading-tight focus:outline-none focus:bg-white focus:border-purple-500" id="product-price" type="text">
    </div>
  </div>
  <div class="md:flex md:items-center mb-6">
    <div class="md:w-1/3">
      <label class="block text-gray-500 font-bold md:text-right mb-1 md:mb-0 pr-4" for="product-image">
        Product image
      </label>
    </div>
    <div class="md:w-2/3">
      <input v-model="productData.image" class="bg-gray-200 appearance-none border-2 border-gray-200 rounded w-full py-2 px-4 text-gray-700 leading-tight focus:outline-none focus:bg-white focus:border-purple-500" id="product-image" type="text">
    </div>
  </div>
  <div class="md:flex md:items-center mb-6">
    <div class="md:w-1/3">
      <label class="block text-gray-500 font-bold md:text-right mb-1 md:mb-0 pr-4" for="chat-id">
        Chat id
      </label>
    </div>
    <div class="md:w-2/3">
      <input v-model="productData.chat_id" class="bg-gray-200 appearance-none border-2 border-gray-200 rounded w-full py-2 px-4 text-gray-700 leading-tight focus:outline-none focus:bg-white focus:border-purple-500" id="chat-id" type="text">
    </div>
  </div>
  <div class="md:flex md:items-center mb-6">
    <div class="md:w-1/3">
      <label class="block text-gray-500 font-bold md:text-right mb-1 md:mb-0 pr-4" for="payment-token">
        Payment token
      </label>
    </div>
    <div class="md:w-2/3">
      <input v-model="productData.payment_token" class="bg-gray-200 appearance-none border-2 border-gray-200 rounded w-full py-2 px-4 text-gray-700 leading-tight focus:outline-none focus:bg-white focus:border-purple-500" id="payment-token" type="text">
    </div>
  </div>
  <div class="md:flex md:items-center mb-6">
    <div class="md:w-1/3">
      <label class="block text-gray-500 font-bold md:text-right mb-1 md:mb-0 pr-4" for="bot-token">
        Bot token
      </label>
    </div>
    <div class="md:w-2/3">
      <input v-model="productData.bot_token" class="bg-gray-200 appearance-none border-2 border-gray-200 rounded w-full py-2 px-4 text-gray-700 leading-tight focus:outline-none focus:bg-white focus:border-purple-500" id="bot-token" type="text">
    </div>
  </div>
  <div class="md:flex md:items-center mb-6">
    <div class="md:w-1/3">
      <label class="block text-gray-500 font-bold md:text-right mb-1 md:mb-0 pr-4" for="payment-currency">
        Currency
      </label>
    </div>
    <div class="md:w-2/3">
      <input v-model="productData.payment_currency" class="bg-gray-200 appearance-none border-2 border-gray-200 rounded w-full py-2 px-4 text-gray-700 leading-tight focus:outline-none focus:bg-white focus:border-purple-500" id="payment-currency" type="text">
    </div>
  </div>
  <div class="md:flex md:items-center">
    <div class="md:w-1/3"></div>
    <div class="md:w-2/3">
      <button @click.prevent="submitted" class="shadow bg-purple-500 hover:bg-purple-400 focus:shadow-outline focus:outline-none text-white font-bold py-2 px-4 rounded" type="button">
        Send to chat
      </button>
    </div>
  </div>
  </form>




</template>

<style scoped>
</style>
