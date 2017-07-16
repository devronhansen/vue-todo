<template>
  <li class="button is-fullwidth" :class="{'is-success': checked, 'is-editable': editMode}" @click="check">
    <span class="icon is-small check">
      <i class="fa" :class="{'fa-check-square-o': checked, 'fa-square-o': !checked}"></i>
    </span>
    <div style="overflow: hidden; text-overflow: ellipsis; margin-right: 10px">
      <span v-show="!editMode" class="text">{{ text }}</span>
    </div>
    <edit-field v-if="editMode" :text="text" @blur="exitEditMode" @updateText="updateText"></edit-field>
    <span class="icons-right">
      <span v-show="!checked" class="icon is-small edit" @click.stop="edit">
        <i class="fa fa-pencil"></i>
      </span>
      <span class="icon is-small bin" @click.stop="destroy">
        <i class="fa fa-trash"></i>
      </span>
    </span>
  </li>
</template>

<script>
import EditField from './EditField.vue'

export default {
  components: {
    EditField
  },
  data() {
    return {
      editMode: false,
      newText: this.text
    }
  },
  props: [
    'text',
    'checked',
    'id',
  ],
  methods: {
    check() {
      if (this.editMode) return
      this.$emit('check', this.id)
    },
    edit() {
      this.editMode = true
    },
    destroy() {
      this.$emit('destroy', this.id)
    },
    exitEditMode() {
      this.editMode = false
    },
    updateText(newText) {
      this.$emit('updateText', newText, this.id)
      this.editMode = false
    }
  },
}
</script>

<style scoped>
  .button {
    justify-content: flex-start;
    margin: 5px 0;
  }

  .button.is-success.text {
    text-decoration: line-through;
  }

  .button.is-editable {
    border-color: #00d1b2;
  }

  .icons-right {
    margin: 0 0 0 auto !important;
  }

  .icon.is-small.check {
    margin-top: 0.25em;
  }
</style>
