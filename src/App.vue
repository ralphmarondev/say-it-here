<script setup>
import {ref} from 'vue'
import emailjs from 'emailjs-com'

const isLoading = ref(false)
const message = ref('')

const onSend = () => {
  if (!message.value.trim()) {
    alert('Please enter a message before sending.')
    return
  }
  console.log(`Message: ${message.value}`)

  const serviceId = import.meta.env.VITE_SERVICE_ID
  const templateId = import.meta.env.VITE_TEMPLATE_ID
  const publicKey = import.meta.env.VITE_PUBLIC_KEY

  isLoading.value = true
  emailjs
      .send(serviceId, templateId, {message: message.value.trim()}, publicKey)
      .then((response) => {
        console.log('SUCCESS!', response.status, response.text)
        alert('Email sent successfully!')
        message.value = ''
      })
      .catch((error) => {
        console.log('ERROR!', error)
        alert('Failed to send email. Please try again later.')
      })
      .finally(() => {
        isLoading.value = false
      })
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
                  aria-label="Your anonymous message"
              ></textarea>

              <button class="btn btn-primary w-100" :disabled="isLoading" aria-label="Send message">Send!</button>
            </div>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>
