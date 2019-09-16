<template>
  <div
    class="modal-content"
    :style="active ?'display:block;':'display:none;'"
    v-on:click="closeOutSide"
  >
    <div :class="['modal',state]">
      <span class="close" v-show="closeable" v-on:click="close">&times;</span>
      <div class="modal-body">
        <h3>
          <i :class="['fas',icon]"></i>
          {{title}}
        </h3>
        <slot name="header"></slot>
        <slot></slot>
        <slot name="footer"></slot>
      </div>
      <div class="confirmation-box">
        <button class="btn cancel">Annuler</button>
        <button class="btn confirm" :class="['btn',state].join('-')">Confirmer</button>
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
  computed: {
    icon: function() {
      switch (this.state) {
        case "info":
          return "fa-info-circle";
          break;
        case "success":
          return "fa-check-circle";
          break;
        case "alert":
          return "fa-exclamation-triangle";
          break;
        case "danger":
          return "fa-exclamation-circle";
          break;
        default:
          return "fa-info-circle";
      }
    }
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