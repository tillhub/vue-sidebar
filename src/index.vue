<!--<template lang="pug">-->
<!--</template>-->

<script>
import Dialog from 'element-ui/lib/dialog'

/**
 * This component extends the ElementUI Dialog component and positions it to the right side of the viewport as a
 * sidebar. Provides additional options, such as `showTitle` and `padding`
 */
export default {
  extends: Dialog,
  props: {
    top: {
      type: String,
      default: '0px'
    },
    showTitle: {
      type: Boolean,
      default: true
    },
    padding: {
      type: String,
      default: '0'
    }
  },
  mounted () {
    console.log('REF', this.$refs)
    this.updatePadding(this.padding)
    this.setShowTitle(this.showTitle)
  },
  methods: {
    /**
     * Updates the padding of the dialog body
     * @param {string} [p] - padding value
     */
    updatePadding (p) {
      // wrap it in $nextTick as classList of child is not available on mounted() yet
      this.$nextTick(() => {
        console.log('padding:', p)
        // find dialog body and update its padding
        for (const childNode of this.$refs.dialog.childNodes) {
          console.log(`padding checking ${childNode}'s classList: ${JSON.stringify(childNode.classList)}`)
          if (childNode.classList && childNode.classList.contains('el-dialog__body')) {
            childNode.style.padding = p
            return
          }
        }
        console.warn('updatePadding: body was not updated! (DOM not ready?)')
      })
    },
    /**
     * Adds or removes a class to the dialog header that set's its display to `none`, depending on the provided boolean.
     * @param {boolean} b - whether to show the dialog title or not
     */
    setShowTitle (b) {
      console.log('showTitle:', b)
      const headerClasses = this.$refs.dialog.childNodes[0].classList
      b ? headerClasses.remove('__hide_header') : headerClasses.add('__hide_header')
    }
  },
  watch: {
    showTitle: (nVal) => this.setShowTitle(nVal),
    padding: (nVal) => this.updatePadding(nVal)
  }
}
</script>

<style scoped>
.el-dialog {
  margin-bottom: 0;
  position: fixed;
  top: 0;
  bottom: 0;
  right: 0;
  width: 360px;
  display: flex;
  flex-direction: column;
}

.__hide_header {
  display: none;
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
}
</style>
