<template>
  <nav>
    <div v-if="user">
      <p>Hey there... {{ user.displayName }}</p>
      <p class="email">Currently logged in as... {{ user.email }}</p>
    </div>
    <button @click="handleClick">Logout</button>
  </nav>
</template>

<script>
import getUser from '@/hooks/getUser'
import useLogout from '@/hooks/useLogout'

export default {
  setup() {
    const { user } = getUser()
    const { error, logout } = useLogout()

    const handleClick = async () => {
      await logout()

      if (!error.value) {
        console.log('user logged out')
      }
    }

    return {
      handleClick,
      user,
    }
  },
}
</script>

<style>
nav {
  padding: 20px;
  border-bottom: 1px solid #eee;
  display: flex;
  justify-content: space-between;
  align-items: center;
}
nav p {
  margin: 2px auto;
  font-size: 16px;
  color: #444;
}
nav p.email {
  font-size: 14px;
  color: #999;
}
</style>
