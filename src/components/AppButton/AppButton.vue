<!-- SPDX-License-Identifier: GPL-3.0-or-later
License: GNU GPLv3 or later. See the license file in the project root for more information.
Copyright © 2021 - present Aleksey Hoffman. All rights reserved.
-->

<template>
  <v-tooltip bottom>
    <template #activator="{on}">
      <v-btn
        :value="value"
        :icon="!!icon && type === 'icon'"
        :small="small"
        :class="buttonClass"
        :disabled="isDisabled"
        v-on="on"
        @click="onClickHandler"
      >
        <v-icon
          v-if="icon"
          :class="iconClass"
          :size="iconSize"
        >
          {{icon}}
        </v-icon>
        <slot />
      </v-btn>
    </template>
    <span>{{tooltip}}</span>
  </v-tooltip>
</template>

<script>
export default {
  props: {
    onClick: {
      type: Function,
      default: () => ({}),
    },
    type: {
      type: String,
      default: 'icon', // 'icon' | 'button'
    },
    icon: {
      type: String,
      default: '',
    },
    iconSize: {
      type: String,
      default: '20px',
    },
    iconClass: {
      type: [String, Object],
      default: '',
    },
    buttonClass: {
      type: [String, Object],
      default: '',
    },
    tooltip: {
      type: String,
      default: '',
    },
    isDisabled: {
      type: Boolean,
      default: false,
    },
    value: {
      type: String,
      default: '',
    },
    small: {
      type: Boolean,
      default: false,
    },
  },
  emits: ['click'],
  methods: {
    onClickHandler () {
      if (this.onClick) {
        this.onClick()
      }
      this.$emit('click')
    },
  },
}
</script>