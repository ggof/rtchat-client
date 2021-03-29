<template>
  <h2 class="title">Welcome to RTChat!</h2>
  <h4 class="subtitle">please enter your username below so that you can join the room. </h4>
  <form class="form">
    <label for="id">username : </label>
    <input name="id" type="text" v-model="id"/>
    <button type="button" class="button" :disabled="id.length > 3" @click="onclick">SUBMIT</button>
  </form>
</template>
<script lang="ts">
import { defineComponent, ref, toRefs } from "vue"

interface Props {
  onclick: (id: string) => void;
}

export const Login = defineComponent<Props>({
  setup(props: Props) {
    const id = ref("")
  
    const onclick = () => props.onclick(id.value)

    return {
      id,
      onclick,
    }
  }
});

export default Login
</script>
<style lang="scss" scoped>
</style>
