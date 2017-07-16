<template>
  <input title="edit field"
         class="edit-field"
         ref="field"
         v-model="newText"
         @focus="$event.target.select()"
         @blur="blur"
         @keyup.enter="updateText" />
</template>

<script>
export default {
  data() {
    return {
      newText: this.text,
    }
  },
  props: [
    'text',
  ],
  mounted() {
    this.$refs.field.focus()
  },
  methods: {
    blur() {
      this.$emit('blur')
    },
    updateText() {
      this.$emit('updateText', this.newText)
    },
  },
}
</script>

<style scoped>
.edit-field {
  border: 0;
  padding: 0;
  font-size: 1rem;
  line-height: 1.5;
}

.edit-field:focus {
  outline: 0;
}
</style>
