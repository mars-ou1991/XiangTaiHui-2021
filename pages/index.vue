<template>
  <div>加载中...</div>
</template>

<script>
export default {
  mounted() {
    const os = (function () {
      const ua = navigator.userAgent
      const isWindowsPhone = /(?:Windows Phone)/.test(ua)
      const isSymbian = /(?:SymbianOS)/.test(ua) || isWindowsPhone
      const isAndroid = /(?:Android)/.test(ua)
      const isFireFox = /(?:Firefox)/.test(ua)
      // eslint-disable-next-line no-unused-vars
      const isChrome = /(?:Chrome|CriOS)/.test(ua)
      const isTablet =
        /(?:iPad|PlayBook)/.test(ua) ||
        (isAndroid && !/(?:Mobile)/.test(ua)) ||
        (isFireFox && /(?:Tablet)/.test(ua))
      const isPhone = /(?:iPhone)/.test(ua) && !isTablet
      const isPc = !isPhone && !isAndroid && !isSymbian
      return {
        isTablet,
        isPhone,
        isAndroid,
        isPc
      }
    })()

    os.isPhone ? this.$router.push('/home-mobile') : this.$router.push('/home')
  }
}
</script>

<style lang="scss" scoped></style>
