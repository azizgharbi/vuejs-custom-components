<template>
  <div
    class="modal-content"
    :style="active ?'display:block;':'display:none;'"
    v-on:click="closeOutSide"
  >
    <div :class="['modal',state]">
      <span class="close" v-show="closeable" v-on:click="close">&times;</span>

      <div class="modal-body">
        <div class="icon-box" :class="['icon',state].join('-')">
          <i :class="['fas',icon]"></i>
        </div>
        <div>
          <h3>{{title}}</h3>
          <slot name="header"></slot>
          <slot></slot>
          <slot name="footer"></slot>
        </div>
      </div>
      <div class="confirmation-box">
        <button class="btn cancel" v-on:click="close">Annuler</button>
        <button class="btn confirm" :class="['btn',state].join('-')" v-on:click="confirm">Confirmer</button>
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
          return "fa-info-circle b-border";
          break;
        case "success":
          return "fa-check-circle g-border";
          break;
        case "alert":
          return "fa-exclamation-triangle";
          break;
        case "danger":
          return "fa-exclamation-circle r-border";
          break;
        default:
          return "fa-info-circle b-border";
      }
    }
  },
  methods: {
    close: function() {
      EventBus.$emit("close", false);
    },
    closeOutSide: function(e) {
      const modalContent = document.querySelector(".modal-content");

      if (this.closeOnOutsideClick && e.target == modalContent) {
        EventBus.$emit("close", false);
      }
    },
    confirm() {
      EventBus.$emit("confirm");
    }
  }
};
</script>