<template>
  <div class="welcome container">
    <div v-if="showLoginForm">
      <h1>Login</h1>
      <LoginForm @login="enterChat" />
      <p>
        No account yet?
        <span @click="showLoginForm = false">Sign up</span> instead
      </p>
    </div>
    <div v-else>
      <h1>Sign up</h1>
      <SignupForm @signup="enterChat" />
      <p>
        Already registered
        <span @click="showLoginForm = true">Login</span> instead
      </p>
    </div>
  </div>
</template>

<script>
import { ref } from 'vue'
import { useRouter } from 'vue-router'

import SignupForm from '@/components/SignupForm'
import LoginForm from '@/components/LoginForm'

export default {
  components: {
    SignupForm,
    LoginForm,
  },

  setup() {
    const router = useRouter()

    const showLoginForm = ref(true)

    const enterChat = () => {
      router.push({ name: 'Chatroom' })
    }

    return {
      enterChat,
      showLoginForm,
    }
  },
}
</script>

<style>
.welcome {
  text-align: center;
  padding: 20px 0;
}
/* form styles */
.welcome form {
  width: 300px;
  margin: 20px auto;
}
.welcome label {
  display: block;
  margin: 20px 0 10px;
}
.welcome input {
  width: 100%;
  padding: 10px;
  border-radius: 20px;
  border: 1px solid #eee;
  outline: none;
  color: #999;
  margin: 10px auto;
}
</style>
