<template>
  <div class="menu-buttons">
    <button
      id="start-pos-btn"
      class="uk-button uk-button-primary single-btn"
      v-on:click="ToggleBtn('isStartBtn')"
      :class="{'uk-button-secondary' : ButtonStatus.isStartBtn,'uk-button-primary' : !ButtonStatus.isStartBtn}"
    >Start</button>
    <button
      id="end-pos-btn"
      class="uk-button uk-button-primary single-btn"
      v-on:click="ToggleBtn('isEndBtn')"
      :class="{'uk-button-secondary' : ButtonStatus.isEndBtn,'uk-button-primary' : !ButtonStatus.isEndBtn}"
    >End</button>
    <div class="single-btn">
      <button
        id="make-walls-btn"
        class="uk-button uk-button-primary make-wall-btn"
        v-on:click="ToggleBtn('isWallBtn')"
        :class="{'uk-button-secondary' : ButtonStatus.isWallBtn,'uk-button-primary' : !ButtonStatus.isWallBtn}"
      >
        Make Wall
        <span>
          <i id="wall-icon" class="fas fa-play"></i>
        </span>
      </button>
    </div>
    <button
      id="find-path-btn"
      class="uk-button uk-button-primary single-btn"
      v-on:click="ToggleBtn('isFindPathBtn')"
    >Find Path</button>
    <button
      id="reset-btn"
      class="uk-button uk-button-primary single-btn"
      v-on:click="ToggleBtn('isResetBtn')"
    >Reset</button>
  </div>
</template>

<script>
import { EventBus } from "../main";

export default {
  data() {
    return {
      ButtonStatus: {
        isStartBtn: false,
        isEndBtn: false,
        isWallBtn: false,
        isFindPathBtn: false,
        isResetBtn: false
      }
    };
  },
  methods: {
    ToggleBtn: function(Btn) {
      if (this.ButtonStatus[Btn]) {
        this.ButtonStatus[Btn] = !this.ButtonStatus[Btn];
      } else {
        Object.keys(this.ButtonStatus).forEach(key => {
          this.ButtonStatus[key] = false;
          if (Btn == "isResetBtn") {
            EventBus.$emit("ResetNode", "Reset");
          } else if (Btn == "isFindPathBtn") {
            EventBus.$emit("FindPath", "FindPath");
          } else {
            this.ButtonStatus[Btn] = true;
            EventBus.$emit("ChangedButtonStatus", this.ButtonStatus);
          }
        });
      }
    }
  }
};
</script>