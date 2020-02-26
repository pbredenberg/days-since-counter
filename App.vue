<template>
    <div class="container">
        <h1 class="headline">
            <span class="counter">{{ timer }} Seconds </span>
            <span class="message">{{ message }}</span>
        </h1>
        <div class="controls">
            <button class="button reset" @click="timer = 0">Reset</button>
        </div>
        <div class="editor">
            <span class="edit" @click="toggleEditor">Edit</span>
            <div class="panel" v-if="isEditorShown">
                <input class="message-input" type="text" v-model="message">
                <button class="button save" @click="toggleEditor">Save</button>
            </div>
        </div>
    </div>
</template>

<script lang="ts">
import Vue from 'vue';

export default Vue.extend({
  data() {
    return {
      timer: 0,
      message: 'Since last incident.',
      isEditorShown: false
    };
  },

  methods: {
      toggleEditor() {
          this.isEditorShown = !this.isEditorShown;
      }
  },

  mounted() {
      setInterval(() => {
          this.timer = this.timer + 1;
      }, 1000)
  }
});
</script>

<style lang="scss" scoped>
@mixin font {
    font-family: 'VT323', sans-serif;
    font-size: 2rem;
}
.container {
  background: black;
  color: white;
  font-family: 'VT323', sans-serif;
  text-align: center;
  padding: 2% 5%;
}
.headline {
    font-size: 60px;
}
.button {
    @include font();
    border: 0;
    cursor: pointer;
    &.reset {
        background-color: red;
        color: white;
        border-radius: 100%;
        padding: 80px 70px;
        &:active {
            opacity: .8;
        }
    }
    &:focus {
        outline: none;
    }
}
.message-input {
    padding: 12px;
    @include font();
}
</style>