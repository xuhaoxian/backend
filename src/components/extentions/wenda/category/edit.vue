<template>
  <div style="padding: 15px;">
    <Form
      v-width="400"
      mode="block"
      ref="form"
      :validOnChange="true"
      :showErrorTip="true"
      :rules="rules"
      :model="category"
    >
      <FormItem label="分类名" prop="name">
        <template v-slot:label>分类名</template>
        <input type="text" v-model="category.name" />
      </FormItem>
      <FormItem label="排序" prop="sort">
        <template v-slot:label>排序</template>
        <input type="number" v-model="category.sort" />
      </FormItem>
      <FormItem>
        <Button color="primary" @click="create">保存</Button>
      </FormItem>
    </Form>
  </div>
</template>
<script>
export default {
  props: ['id'],
  data() {
    return {
      category: {
        name: '',
        sort: 0
      },
      rules: {
        required: ['name', 'sort']
      }
    };
  },
  mounted() {
    R.Extentions.wenda.Category.Edit({ id: this.id }).then(res => {
      this.category = res.data.data;
    });
  },
  methods: {
    create() {
      let validResult = this.$refs.form.valid();
      if (validResult.result) {
        this.$emit('success', this.category);
      }
    }
  }
};
</script>
