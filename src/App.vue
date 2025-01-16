<script setup>
import {ref} from 'vue'

const message = ref('')

const onSend = () => {
  console.log(`Message: ${message.value}`)
}
</script>

<template>
  <div
      class="container-fluid vw-100 vh-100 bg-primary py-5 d-flex justify-content-center"
  >
    <div>
      <div class="card" style="max-width: 600px; width: 90vw">
        <div class="card-content">
          <h5 class="card-header">
            <div class="row">
              <div class="col-auto d-flex align-items-center">
                <img
                    src="/images/ralphmaron.png"
                    alt="Ralph Maron A. Eda"
                    style="
                    height: 40px;
                    width: 40px;
                    object-fit: cover;
                    border-radius: 50%;
                  "
                />
                <div class="ms-3">
                  <span class="text-secondary fs-6"
                  >@edaralphmaron@gmail.com</span
                  >
                  <p class="fs-6 mb-0">Send me anonymous messages!</p>
                </div>
              </div>
            </div>
          </h5>
          <form @submit.prevent="onSend">
            <div class="card-body">
              <textarea
                  class="form-control mb-4"
                  placeholder="Say me anonymous messages! Say it here!"
                  v-model="message"
              ></textarea>

              <button class="btn btn-primary w-100">Send!</button>
            </div>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>
