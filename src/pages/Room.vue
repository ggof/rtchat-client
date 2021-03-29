<template>
  <div class="page">
    <div class="messages">
    </div>
    <form class="form">
      <input type="text" class="message" v-model="text" />
      <button type="button" class="button" :disabled="text.length == 0" @click="onsend" placeholder="Type here ..."/>
    </form>
  </div>
</template>
<script lang="ts">
import { defineComponent, ref } from "vue"

interface Props {
  id: string;
}

interface Message {
  id: string;
  ts: number;
  msg: string;
}

export const Room = defineComponent<Props>({
  setup(props) {
    const text = ref("")
    const ws = new WebSocket(`http://localhost:5000/ws/${props.id}`)
    const messages = ref<Message[]>([])

    ws.onmessage = ev => {
      const message: Message = JSON.parse(ev.data)
      messages.value = [...messages.value, message]
    }

    const onsend = () => {
      const ts = new Date().getTime()
      messages.value = [...messages.value, { ts, id: props.id, msg: text.value }]
      ws.send(text.value)
      text.value = ""
    }

    return {
      text,
      onsend,
      messages,
    }
  }
})

export default Room
</script>
<style lang="scss" scoped>
</style>
