<template>
  <div :class="`h-[1px] my-4 ${classes}`">

  </div>
</template>

<script>
export default {
  props: {
    classes: {
      type: String,
      default: 'mx-4 bg-teal-600 dark:bg-teal-100/25'
    }
  }
}
</script>