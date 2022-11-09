<template>
  <form class="flex">
    <div class="h-full w-full">
      <p></p>
      <textarea v-model="input" class="block w-full h-full" @paste="paste" />
    </div>
    <div
      class="h-full w-1/2 bg-primary-200 text-black bg-white border border-black"
    >
      {{ input && toTemplate }}
    </div>
  </form>
</template>

<script>
export default {
  data() {
    return {
      input: ""
    }
  },
  methods: {
    paste() {
      navigator.clipboard.writeText(this.toTemplate)
    }
  },
  computed: {
    toTemplate() {
      if (!this.input.includes("svg")) return
      let reg = /#[0-9a-f]{6}/gi

      const colorBlind = this.input.replace(reg, "currentColor")
      const template = `<template>
        ${colorBlind}
      </template>`

      const script = '<script lang="ts" setup>' + "</scripz>".replace("z", "t")

      const final = template + script
      return final
    }
  }
}
</script>
