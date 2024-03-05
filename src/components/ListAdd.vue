<template>
  <div div>
    <v-textarea
      outline
      v-model="memo"
      label="Write To do List"
      value=""
    ></v-textarea>
    <v-btn v-if="mode === 'add'" @click="listAdd">Add List</v-btn>
    <v-btn v-else @click="listEdit">Edit List</v-btn>
  </div>
</template>

<script>
import { eventBus } from '../main'

export default {
  data() {
    return {
      memo: '',
      index: null,
      mode: 'add',
    }
  },
  created() {
    eventBus.$on('listEdit', (memo, index) => {
      this.memo = memo;
      this.index = index;
      this.mode = 'edit';
    });
  },
  methods: {
    listAdd() {
      if(this.memo === '') {
        alert('Write To do List');
      } else {
        this.$emit('listAdd', this.memo);
        this.memo = '';
      }
    },
    listEdit() {
      if(this.memo === '') {
        alert('Write To do List');
      } else {
        this.$emit('listEdit', this.memo, this.index);
        this.memo = '';
        this.mode = 'add';
      }
    }
  }
}
</script>

<style>

</style>