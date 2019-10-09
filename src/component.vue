<template>
  <div class="accordion" v-bind:class="{ disabled: !active}" v-bind:style="{background: backgroundColor}">
    <div class="accordion-header" @click="openClose()" :style="styleObject">
      <i :class="icon" :style="styleIcon"></i>
      <span class="accordion-title" :style="styleTitle">{{title}}</span>
      <i class="fas fa-angle-down" :style="styleIcon"></i>
    </div>
    <div class="accordion-body" v-bind:style="{ maxHeight: maxHeight }">
      <div class="accordion-content">
        <slot></slot>
      </div>
    </div>
  </div>
</template>

<script>
import '../fonts/fonts.css'

export default {
  props: {
    title: {
      type: String,
      required: true,
      default: 'Default'
    },
    icon: {
      type: String,
      required: true,
      default: 'fas fa-user-circle'
    },
    backgroundColor: {
        type: String,
        default: ''
    },
    hoverColor: {
        type: String,
        default: '#d05d1c'
    },
    iconColor: {
        type: String,
        default: 'red'
    },
    titleColor: {
        type: String,
        default: 'yellow'
    }
  },
  data: () => ({
    active: false,
    maxHeight: '0px'
  }),
  methods: {
    openClose () {
      let containerHeight = this.$el.querySelector('.accordion-content')
        .offsetHeight
      if (this.active) {
        this.maxHeight = '0px'
      } else {
        this.maxHeight = containerHeight + 32 + 'px'
      }
      this.active = !this.active
    }
  },
  computed: {
    styleObject: function() {
        return {
        '--background-color-hover': this.hoverColor
        }
    },
    styleIcon: function() {
        return {
        '--color-icon': this.iconColor
        }
    },
    styleTitle: function() {
        return {
        '--color-title': this.titleColor
        }
    }
  }
}
</script>

<style lang="scss">
    $fa-font-path : "~@fortawesome/fontawesome-free-webfonts/webfonts";
    @import "~@fortawesome/fontawesome-free-webfonts/scss/fontawesome.scss";
    @import "~@fortawesome/fontawesome-free-webfonts/scss/fa-solid.scss";
    @import "~@fortawesome/fontawesome-free-webfonts/scss/fa-regular.scss";
    @import "~@fortawesome/fontawesome-free-webfonts/scss/fa-brands.scss";
</style>

<style>
*{
   font-family:'Montserrat Regular';
}
/* #app {
  margin-top: 50px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  width: 360px;
  border: 1px solid #2e3553;
} */

.accordion {
  width: 100%;
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  overflow: hidden;
  background-color: #2e3553;
  cursor: pointer;
}
.accordion .accordion-header {
  box-sizing: border-box;
  padding: 10px;
  width: 95%;
  display: flex;
  align-items: center;
  justify-content: space-between;
  /* border-bottom: 1px solid #2e3553; */
  color: #fff;
  transition: all 0.3s ease;
}

.accordion-header .nextbss-bar-chart:hover {
  color: aqua;
}

.accordion .accordion-header .fa-angle-down {
  font-size: 20px;
  transition: all 0.3s ease;
  transform: rotate(180deg);
  right: 10%;
  top: 0px;
}

.accordion .accordion-header:hover {
  width: 95%;
  /* background-color: #d05d1c; */
  background-color: var(--background-color-hover);
  border-top-right-radius: 30px;
  border-bottom-right-radius: 30px;
  /* color: #2e3553 !important; */
}

.accordion .accordion-header:active,
.accordion .accordion-header:focus {
  width: 95%;
  /* background-color: #d05d1c; */
  border-top-right-radius: 30px;
  border-bottom-right-radius: 30px;
}

.accordion.disabled .accordion-header i {
  /* color: #d05d1c; */
  color: var(--color-icon);
}

.accordion.disabled .accordion-header span {
  /* color: #d05d1c; */
  color: var(--color-title);
}

.accordion-title {
  left: 20%;
  position: absolute;
  -webkit-transition: all 0.5s ease;
  -moz-transition: all 0.5s ease;
  -o-transition: all 0.5s ease;
  transition: all 0.5s ease;
}
.accordion .accordion-body {
  text-align: start;
  box-sizing: border-box;
  padding: 10px 16px;
  transition: all 0.3s ease;
  color: #ffffff;
  /* border-bottom: 1px solid #2e3553; */
  font-size: 14px;
  cursor: default;
}
.accordion .accordion-body .accordion-content {
  display: flex;
  flex-direction: column;
}

.accordion.disabled {
  /* background-color: #2e3553; */
}
.accordion.disabled .accordion-header {
  border-bottom: none;
  color: #ffffff;
}
.accordion.disabled .accordion-header i {
  transform: rotate(0deg);
}
.accordion.disabled .accordion-body {
  pointer-events: none;
  padding: 0;
  margin-left: 16px;
  opacity: 0;
  max-height: 0px;
  transform: translateY(-20px);
}

#wrapper.toggled .accordion-title {
  -webkit-transition: all 0.5s ease;
  -moz-transition: all 0.5s ease;
  -o-transition: all 0.5s ease;
  transition: all 0.5s ease;
  display: none;
}
</style>
