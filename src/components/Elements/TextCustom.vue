<template>
    <div class="text"
        @click.self="changeText"
         @dragstart="() => {return false}"
         @mousedown="moveTo"

    >
        {{text}}
        <div class="redactor" :class="{active : showRedactor}">
            <textarea  name="" id="" cols="30" rows="10" v-model="text"></textarea>
            <button class="clear" @click="cancel">Cancel</button>
            <button type="submit" class="save" @click="saveText">Save</button>
        </div>
    </div>
</template>

<script>
  export default {
    name: 'Text',
    data() {
      return {
        text: 'Lorem ipsum dolor sit amet, consectetur adipisicing elit. Enim in iste quia tenetur.',
        textPrevious: '',
        showRedactor: false
      }
    },
    methods: {
      changeText() {
        this.textPrevious = this.text;
        this.showRedactor = true;

      },
      saveText() {
        this.showRedactor = false;
      },
      cancel() {
        this.text = this.textPrevious;
        this.showRedactor = false;
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
          // Console.log(self.posX, x, shiftX);
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
    }
  };
</script>

<style scoped>
    .text {
        position: absolute;
        top: 0;
        left: 0;
        color: red;
        width: 300px;
        height: 20px

    }

    .redactor {
        display: none;
    }

    .active {
        display: flex;
    }
</style>