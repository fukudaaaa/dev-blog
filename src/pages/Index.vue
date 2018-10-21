<template>
  <Layout>
    <g-image alt="Example image" src="~/favicon.png" width="135" />
    <h1>Hello, world!</h1>
    <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Pariatur excepturi labore tempore expedita, et iste tenetur suscipit explicabo! Dolores, aperiam non officia eos quod asperiores</p>
    <ul>
      <li v-for="edge in $page.allPost.edges" :key="edge.node._id">
        <router-link :to="edge.node.path">{{ edge.node.title }}</router-link>
      </li>
    </ul>
  </Layout>
</template>

<page-query>
query Home ($page: Int) {
  allPost (perPage: 10, page: $page) @paginate {
    pageInfo {
      totalPages
      currentPage
    }
    edges {
      node {
        _id
        title
        path
        content
      }
    }
  }
}
</page-query>

<script>
import { Pager } from 'gridsome'
export default {
  created() {
    console.log(this.$page)
  },
  components: {
    Pager
  }
}
</script>
