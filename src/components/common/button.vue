<template>
  <Button :class="glass" :icon="icon" v-if="inPermission" @click="$emit('click')">{{text}}</Button>
</template>
<script>
export default {
  props: ['glass', 'icon', 'permission', 'text', 'isSuper'],
  computed: {
    inPermission() {
      if (typeof this.$store.state.User.permissions === 'undefined') {
        return false;
      }
      if (this.isSuper && !this.$store.state.User.is_super) {
        return false;
      }
      if (this.$store.state.User.is_super) {
        return true;
      }
      let permissions = this.$store.state.User.permissions;
      return typeof permissions[this.permission] !== 'undefined';
    }
  }
};
</script>
