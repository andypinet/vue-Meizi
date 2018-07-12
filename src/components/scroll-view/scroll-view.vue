<template>
    <div :style="comstyle">
        <slot></slot>
    </div>
</template>
<script>
export default {
    name: 'v-scroll-view',
    data() {
        return {
            comstyle: {
                height: `${window.innerHeight}px`
            }
        };
    }
};
</script>
<style>
</style>

