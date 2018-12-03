<template>
  <transition
    name="dialog-fade"
    @after-enter="afterEnter"
    @after-leave="afterLeave">
    <div
      class="el-dialog__wrapper"
      v-show="visible"
      @click.self="handleWrapperClick">
      <div
        role="dialog"
        aria-modal="true"
        :aria-label="title || 'dialog'"
        class="el-dialog"
        :class="[{'el-dialog--center': center }, customClass]"
        ref="dialog"
        :style="dialogStyle">
        <div
          class="el-dialog__header"
          :style="headerStyle">
          <slot name="title">
            <span class="el-dialog__title">{{ title }}</span>
          </slot>
          <button
            type="button"
            class="el-dialog__headerbtn"
            aria-label="Close"
            v-if="showClose"
            @click="handleClose">
            <i class="el-dialog__close el-icon el-icon-close"/>
          </button>
        </div>
        <div
          class="el-dialog__body"
          v-if="rendered"
          :style="bodyStyle">
          <slot/>
        </div>
        <div
          class="el-dialog__footer"
          v-if="$slots.footer">
          <slot name="footer"/>
        </div>
      </div>
    </div>
  </transition>
</template>

<script>
import Popup from 'element-ui/src/utils/popup'
import Migrating from 'element-ui/src/mixins/migrating'
import emitter from 'element-ui/src/mixins/emitter'

export default {
  name: 'ThSidebar',
  mixins: [Popup, emitter, Migrating],
  props: {
    title: {
      type: String,
      default: ''
    },
    modal: {
      type: Boolean,
      default: true
    },
    modalAppendToBody: {
      type: Boolean,
      default: true
    },
    appendToBody: {
      type: Boolean,
      default: false
    },
    lockScroll: {
      type: Boolean,
      default: true
    },
    closeOnClickModal: {
      type: Boolean,
      default: true
    },
    closeOnPressEscape: {
      type: Boolean,
      default: true
    },
    showClose: {
      type: Boolean,
      default: true
    },
    width: {
      type: String,
      default: '360px'
    },
    customClass: {
      type: String,
      default: ''
    },
    top: {
      type: String,
      default: '0px'
    },
    bottom: {
      type: String,
      default: '0px'
    },
    beforeClose: {
      type: Function,
      default: undefined
    },
    center: {
      type: Boolean,
      default: false
    },
    hideTitle: {
      type: Boolean,
      default: false
    },
    padding: {
      type: String,
      default: '0'
    },
    position: {
      type: String,
      default: 'right',
      validator (v) {
        // make sure it's either left or right
        return ['left', 'right'].indexOf(v) > -1
      }
    }
  },
  data () {
    return {
      closed: false
    }
  },
  watch: {
    visible (val) {
      if (val) {
        this.closed = false
        this.$emit('open')
        this.$el.addEventListener('scroll', this.updatePopper)
        this.$nextTick(() => {
          this.$refs.dialog.scrollTop = 0
        })
        if (this.appendToBody) {
          document.body.appendChild(this.$el)
        }
      } else {
        this.$el.removeEventListener('scroll', this.updatePopper)
        if (!this.closed) this.$emit('close')
      }
    }
  },
  computed: {
    dialogStyle () {
      let style = {
        width: this.width,
        marginTop: this.top,
        marginBottom: this.bottom
      }

      // align on left or right viewport edge based on prop
      if (this.position === 'left') {
        style.left = 0
      } else {
        style.right = 0
      }

      return style
    },
    bodyStyle () {
      return {
        padding: this.padding
      }
    },
    headerStyle () {
      if (this.hideTitle) { return { display: 'none' } } else { return {} }
    }
  },
  methods: {
    getMigratingConfig () {
      return {
        props: {
          'size': 'size is removed.'
        }
      }
    },
    handleWrapperClick () {
      if (!this.closeOnClickModal) return
      this.handleClose()
    },
    handleClose () {
      if (typeof this.beforeClose === 'function') {
        this.beforeClose(this.hide)
      } else {
        this.hide()
      }
    },
    hide (cancel) {
      if (cancel !== false) {
        this.$emit('update:visible', false)
        this.$emit('close')
        this.closed = true
      }
    },
    updatePopper () {
      this.broadcast('ElSelectDropdown', 'updatePopper')
      this.broadcast('ElDropdownMenu', 'updatePopper')
    },
    afterEnter () {
      this.$emit('opened')
    },
    afterLeave () {
      this.$emit('closed')
    }
  },
  mounted () {
    if (this.visible) {
      this.rendered = true
      this.open()
      if (this.appendToBody) {
        document.body.appendChild(this.$el)
      }
    }
  },
  destroyed () {
    // if appendToBody is true, remove DOM node after destroy
    if (this.appendToBody && this.$el && this.$el.parentNode) {
      this.$el.parentNode.removeChild(this.$el)
    }
  }
}
</script>

<style scoped>
.el-dialog {
  position: fixed;
  top: 0;
  bottom: 0;
  display: flex;
  flex-direction: column;
}

.el-dialog__header {
  flex: 0 0 auto;
}

.el-dialog__body {
  flex: 1 1 auto;
  overflow: auto;
}

.el-dialog__footer {
  flex: 0 0 auto;
  padding: 0;
}
</style>
