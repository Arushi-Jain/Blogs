<template>
<div>
<div class = "row q-pt-md">
    <div class="col-1"/>
    <div class="col-10">
    <q-editor
        v-model="model"
        :readonly = "readonly"
        :toolbar="[
            ['bold', 'italic', 'strike', 'underline', 'subscript', 'superscript'],
            ['token', 'hr', 'link', 'custom_btn'],
            ['print', 'fullscreen'],
            ['undo', 'redo']
        ]"
        :fonts="{
            arial: 'Arial',
            arial_black: 'Arial Black',
            comic_sans: 'Comic Sans MS',
            courier_new: 'Courier New',
            impact: 'Impact',
            lucida_grande: 'Lucida Grande',
            times_new_roman: 'Times New Roman',
            verdana: 'Verdana'
        }"
        />
    </div>
    <div class="col-1"/>
</div>
    <div class= "row q-pt-sm">
        <div class="col-1"/>
        <div class = "col-8"><q-chips-input v-model="tags" placeholder="Type some hastags" /></div>
        <div class="col-1"/>
        <div class="col-2  q-pt-md">
            <q-btn
                color="primary"
                @click="clickMethod"
                :label = "readonly ? 'Edit' : 'Publish'"
                />
         </div>
    </div>
</div>
</template>

<script>
export default {
  data () {
    return {
      model: '',
      readonly: true,
      tags: [],
      title: '',
      content: ''
    }
  },
  mounted () {
    if (this.$route.params.blog !== undefined) {
      let blog = this.$route.params.blog
      console.log(this.$route.params.blog)
      this.model = `<h3>Header Title : ${blog.title}</h3><div>Normal text : ${blog.content}</div>`
    } else { this.model = `<h3>Header Title :${this.title}</h3><div>Normal text :${this.content}</div>` }
  },
  methods: {
    clickMethod () {
      if (!this.readonly) {
        let blogs = JSON.parse(window.localStorage.getItem('blogs'))
        console.log('model', this.model)
        let blog = {
          id: new Date(),
          title: 'Mytitle',
          content: 'my content',
          images: [{path: 'statics/blog2.jpg'}],
          tags: this.tags
        }
        blogs.splice(1, 0, blog)
        window.localStorage.setItem('blogs', JSON.stringify(blogs))
      }
      this.readonly = !this.readonly
      console.log(this.readonly)
    }
  }
}
</script>

<style>

</style>
