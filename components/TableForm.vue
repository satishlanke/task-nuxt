<template>
  <div class="d-flex justify-content-center">
    <div class="mt-5">
      <form @submit="onSubmit">
        Rows : <input class="form-control" v-model="tableinfo.row" type="number" /> Cols :
        <input class="form-control" v-model="tableinfo.col" type="number" />
        <button class="btn  btn-success mt-4" type="submit">Submit</button>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  name: "TableForm",
  data() {
    return {
      tableinfo: {
        row: '',
        col: '',
      },
    };
  },
  methods: {
      onSubmit (e) {
      e.preventDefault()

      // console.log(newTask)
      this.$emit('submittabledata', this.tableinfo)
    }
  }
};
</script>