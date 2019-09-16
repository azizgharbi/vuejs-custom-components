<template>
  <div
    class="modal-content"
    v-on:click="closeOutSide"
    :style="active ?'display:block;':'display:none;'"
  >
    <div class="modal">
      <span class="close" v-show="closeable" v-on:click="close">&times;</span>
      <div class="modal-body">
        <slot name="header"></slot>
        <slot></slot>
        <slot name="footer"></slot>
      </div>
    </div>
  </div>
</template>

<script>
import "./../public/css/modal.scss";
//Bus Event
import { EventBus } from "./eventBus";

export default {
  name: "Modal",
  props: {
    active: Boolean,
    title: String,
    closeOnOutsideClick: Boolean,
    state: String,
    closeable: Boolean
  },
  methods: {
    close: function(e) {
      EventBus.$emit("close", false);
    },
    closeOutSide: function(e) {
      const modalContent = document.querySelector(".modal-content");

      if (this.closeOnOutsideClick && e.target == modalContent) {
        EventBus.$emit("close", false);
      }
    }
  }
};
</script>