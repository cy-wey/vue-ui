<template>
  <div>
    <div class=" gulu-tabs">
      <div class=" gulu-tabs-nav" ref="container">
        <div class=" gulu-tabs-nav-item" v-for="(t,index) in titles" :key="index"
             @click="select(t)"
             :ref="el => {if (t === selected) selectedItem = el}"
             :class="{selected: t===selected}"
        >{{ t }}
        </div>
        <div class="gulu-tabs-nav-indicator" ref="indicator"></div>
      </div>
      <div class=" gulu-tabs-content">
        <component :is="current" :key="current.props.title"/>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import Tab from './Tab.vue'
import {
  ref,
  computed,
  onMounted,
  watchEffect
} from 'vue'

export default {
  props: {
    selected: {
      type: String
    }
  },
  name: "Tabs",
  setup(props, context) {
    const selectedItem = ref<HTMLDivElement>([])
    const indicator = ref<HTMLDivElement>(null)
    const container = ref<HTMLDivElement>(null)
    onMounted(() => {
      watchEffect(() => {
        const {width} = selectedItem.value.getBoundingClientRect()
        indicator.value.style.width = width + 'px'
        const {left: left1} = container.value.getBoundingClientRect()
        const {left: left2} = selectedItem.value.getBoundingClientRect()
        const left = left2 - left1
        indicator.value.style.left = left + 'px'
      })
    })
    const defaults = context.slots.default()
    defaults.forEach((tag) => {
      if (tag.type.name !== Tab.name) {
        throw new Error('Tabs 的子标签必需是 Tab')
      }
    })
    const titles = defaults.map((tag) => {
      return tag.props.title
    })
    const select = (title: string) => {
      context.emit('update:selected', title)
    }
    const current = computed(() => {
      return defaults.find(tag => tag.props.title === props.selected)
    })
    return {
      current,
      defaults,
      titles,
      select,
      selectedItem,
      indicator,
      container
    }
  }
}
</script>

<style lang="scss">
$blue: #40a9ff;
$color: #333;
$border-color: #d9d9d9;

.gulu-tabs {
  &-nav {
    display: flex;
    color: $color;
    border-bottom: 1px solid $border-color;
    position: relative;

    &-item {
      padding: 8px 0;
      margin: 0 16px;
      cursor: pointer;

      &:first-child {
        margin-left: 0;
      }

      &.selected {
        color: $blue;
      }
    }

    &-indicator {
      position: absolute;
      height: 3px;
      background: $blue;
      left: 0;
      bottom: -1px;
      width: 100px;
      transition: all 250ms;
    }
  }

  &-content {
    padding: 8px 0;
  }
}
</style>