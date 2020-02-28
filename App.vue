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
  padding: 5%;
  box-sizing: border-box;
  position: absolute;
  height: 100%;
  width: 100%;
  display: flex;
  flex-flow: column;
  align-content: center;
  justify-content: center;
}
.headline {
    font-size: 52px;
    @media (min-width: 645px) {
        font-size: 9.5vw;
    }
}
.editor {
    padding-top: 20px;
    opacity: .5;
    &:hover {
        opacity: 1;
    }
}
.edit {
    cursor: pointer;
    display: inline-block;
    padding: 6px;
}
.button {
    @include font();
    border: 0;
    cursor: pointer;
    transition: all .3s cubic-bezier(0.075, 0.82, 0.165, 1);
    &.reset {
        background-color: red;
        color: white;
        border-radius: 100%;
        padding: 80px 70px;
        &:active {
            opacity: .8;
            background-color: darken(red, 25%);
        }
    }
    &:focus {
        outline: none;
    }
    &:hover {
        background-color: darken(red, 25%);
        color: white;
    }
}
.message-input,
.save {
    padding: 12px;
    @include font();
}
.message-input {
    border: 0;
}
</style>