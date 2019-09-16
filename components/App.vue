<template>
  <div>
    <div class="demo">
      <button v-on:click="open">open</button>
      <Modal :active="active" :closeable="closeable" :closeOnOutsideClick="closeOnOutsideClick">
        <div slot="header">header</div>
        <p>hello</p>
        <i class="fa fa-twitter"></i>
        <i class="fa fa-camera-retro"></i>
        <div slot="footer">footer</div>
      </Modal>
    </div>

    <div class="options">
      <h1>Options</h1>
      <input type="checkbox" id="closeable" v-model="closeable">
      <label for="closeable">closeable : {{ closeable }}</label>
      <input type="checkbox" id="closeOnOutsideClick" v-model="closeOnOutsideClick">
      <label for="closeOnOutsideClick">closeOnOutsideClick : {{ closeOnOutsideClick }}</label>
    </div>
  </div>
</template>

<script>
import "./../public/css/app.scss";
//UI components
import Modal from "./Modal";
//Bus event
import { EventBus } from "./eventBus";

export default {
  name: "App",
  components: {
    Modal
  },
  data() {
    return {
      active: false,
      closeable: true,
      closeOnOutsideClick: false,
      state: "normal"
    };
  },
  methods: {
    open: function() {
      this.active = !this.active;
    }
  },
  created() {
    EventBus.$on("close", c => {
      this.active = c;
    });
  }
};
</script>