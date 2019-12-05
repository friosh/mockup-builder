<template>
    <div class="outer"
         @mousedown.self.stop.prevent="resize"
         :style="{width, height, top: posX, left: posY}"
    >

        <div class="inner"
             :disabled="disabled"
             @click.right.prevent.stop="disabled =!disabled"
             @dragstart="() => {return false}"
             @mousedown="moveTo"
        >
        </div>
    </div>
</template>

<script>
  let Console = console;

  export default {
    name: 'Rectangle',
    data() {
      return {
        width: '100px',
        height: '100px',
        disabled: true,
        content: 'jo',
        posX: "5px",
        posY: "5px"
      }
    },
    methods: {
      changeSize: function() {
        this.$data.width = this.width == '300px' ? '100px' : '300px';
      },
      moveTo(e) {
        let self = this;
        let shiftX = e.clientX - this.$el.getBoundingClientRect().left;
        let shiftY = e.clientY - this.$el.getBoundingClientRect().top;

        // move(e.pageX, e.pageY);
        document.body.append(self.$el);

        function move(x, y) {
          self.posY = x - shiftX + 'px';
          self.posX = y - shiftY + 'px';
          Console.log(self.posX, x, shiftX);
        }

        function onMouseMove(e) {
          move(e.pageX, e.pageY);
        }

        document.addEventListener('mousemove', onMouseMove);
        self.$el.onmouseup = function() {
          document.removeEventListener('mousemove', onMouseMove);
          self.onmouseup = null;
        }
      },
      resize: function(e) {
        const el = {
          top: e.target.offsetTop,
          left: e.target.offsetLeft
        };
        Console.log(el);

        function move(w, h, context) {
            context.width = w - el.left  + 'px';
            context.height = h - el.top + 'px';
        }

        function onMouseMove(e) {
          move(e.pageX, e.pageY, this);
        }

        let callback = onMouseMove.bind(this);
        // let callback = onMouseMove;

        document.addEventListener('mousemove', callback);
        document.onmouseup = function() {
          document.removeEventListener('mousemove', callback);
        }
      }
    }
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

    .inner {
        position: absolute;
        top:.2em;
        left: .2em;
        background: #ccc;
        width: calc(100% - 1.4em);
        height: calc(100% - 1.4em);
        z-index: 1100;
        padding: .5em;
        border-radius: 3px;
    }

    .inner:hover {
        cursor: default;
    }

    .inner[disabled] {
        color: #000;
        background: #666;
    }
</style>