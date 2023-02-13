<template>
  <div />
</template>

<script>
export default {
  name: 'IndexPage',
  middleware: [
    function ({ redirect, app }) {
      redirect('/auth/login')
    },
  ],
}
</script>
