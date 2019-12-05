<template>
    <div class="outer"
         @mousedown.self.stop.prevent="resize"
         :style="{width, height, top: posX, left: posY}"
    >
        {{slot}}
    </div>
</template>

<script>
  export default {
    name: 'BlockNode',
  };
</script>

<style scoped>
    .outer {
        width: 200px;
        height: 200px;
        position: absolute;
        padding: .2em;
        background: #000;
        z-index: 100;
        border-radius: 3px;
    }

    .outer:hover {
        cursor: se-resize;
    }
</style>