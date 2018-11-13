<template>
  <q-page class="flex flex-center">
    <div class="row justify-center items-stretch q-pt-md q-ml-lg q-pb-xl" >
      <div class="col-md-4 col-sm-10" v-for="blog in blogs" :key ="blog.id">
      <q-card @click.native="cardClick(blog)" style="width: 90%;" class="q-mb-xl">
        <q-card-media>
          <img :src="blog.images[0].path" style="height: 200px;">
        </q-card-media>
        <q-card-title>
          {{blog.title}}
        </q-card-title>
        <q-card-main>
          <p>{{blog.content}}</p>
        </q-card-main>
        <q-card-separator />
      </q-card>
      </div>
    </div>
  </q-page>
</template>

<style>
</style>

<script>
import axios from 'axios'
export default {
  name: 'PageIndex',
  data () {
    return {
      blogs: []
    }
  },
  methods: {
    cardClick (blog) {
      this.$router.push({name: 'Create', params: {blog: blog}})
    }
  },
  mounted () {
    axios('/statics/mock/blogs.json')
      .then((res) => {
        this.blogs = res.data
        window.localStorage.setItem('blogs', JSON.stringify(this.blogs))
      })
      .catch()
    this.blogs = JSON.parse(window.localStorage.getItem('blogs'))
    console.log(this.blogs)
  }
}
</script>
