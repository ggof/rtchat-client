<template>
  <div class="App">
    <Login v-if="state === 'LOGIN'" />
    <Room v-if="state === 'ROOM'" />
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue'

import Login from './pages/Login.vue'
import Room from './pages/Room.vue'

type State = "LOGIN" | "ROOM"

export default defineComponent({
  components: {
    Login,
    Room,
  },

  setup() {
    const state = ref<State>("LOGIN")

    return {
      state
    }
  },
})
</script>

<style>
.App {
  text-align: center;
}
.App-header {
  background-color: #f9f6f6;
  color: #32485f;
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  font-size: calc(10px + 2vmin);
}
.App-link {
  color: #00c185;
}
.App-logo {
  height: 40vmin;
  pointer-events: none;
  margin-bottom: 1rem;
  animation: App-logo-spin infinite 1.6s ease-in-out alternate;
}
.App-tsx {
  display: flex;
}
.App-tsx > div {
  margin-left: 30px;
  font-size: 16px;
}
@keyframes App-logo-spin {
  from {
    transform: scale(1);
  }
  to {
    transform: scale(1.06);
  }
}
</style>
