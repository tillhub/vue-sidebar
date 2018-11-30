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
     * @param {string} p - padding value
     */
    updatePadding (p) {
      this.$nextTick(() => {
        console.log('padding:', p, this.$refs.dialog.childNodes)
        console.log('childNode[1]:', this.$refs.dialog.childNodes[1])
        this.$refs.dialog.childNodes[1].style.padding = p
        console.log('childNode[1]:', this.$refs.dialog.childNodes[1])
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
