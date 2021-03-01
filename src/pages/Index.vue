<template>
  <Layout>

    <!-- Learn how to use images here: https://gridsome.org/docs/images -->
    <!-- <g-image alt="Example image" src="~/favicon.png" width="135" /> -->

    <!-- Page Header -->
    <!-- static/img下的图片 -->
    <!-- <header class="masthead" style="background-image: url('/img/home-bg.jpg')"> -->
    <!-- backgroundImage: `url(http://localhost:1337${generalNode.cover.url})` -->
    <header
      class="masthead"
      :style="{
        backgroundImage: `url(${GRIDSOME_API_URL + generalNode.cover.url})`
      }">
      <div class="overlay"></div>
      <div class="container">
        <div class="row">
          <div class="col-lg-8 col-md-10 mx-auto">
            <div class="site-heading">
              <h1>{{ generalNode.title }}</h1>
              <span class="subheading">{{ generalNode.subtitle }}</span>
            </div>
          </div>
        </div>
      </div>
    </header>

    <!-- Main Content -->
    <div class="container">
      <div class="row">
        <div class="col-lg-8 col-md-10 mx-auto">
          <div class="post-preview" v-for="edge in $page.posts.edges" :key="edge.node.id">
            <g-link :to="'/post/' + edge.node.id">
              <h2 class="post-title">
                {{ edge.node.title }}
              </h2>
              <!-- 副标题 -->
              <!-- <h3 class="post-subtitle">
                暂无
              </h3> -->
            </g-link>
            <p class="post-meta">Posted by
              <a href="#">Wan Peng</a>
              on {{ edge.node.created_at }}</p>
            <p>
              <span v-for="tag in edge.node.tags" :key="tag.id">
                <!-- <a href="">{{ tag.name }}</a> -->
                <g-link :to="'/tag/' + tag.id">{{ tag.name }}</g-link>
                &nbsp;&nbsp;
              </span>
            </p>
            <hr>
          </div>
          <!-- Pager -->
          <!-- gridsome自带的分页组件，通过posts别名拿到页面信息 -->
          <Pager :info="$page.posts.pageInfo"/>
          <!-- <div class="clearfix">
            <a class="btn btn-primary float-right" href="#">Older Posts &rarr;</a>
          </div> -->
        </div>
      </div>
    </div>
  </Layout>
</template>

<page-query>
query($page: Int) {
  posts: allStrapiPost(perPage: 3, page: $page) @paginate {
    pageInfo {
      totalPages
      currentPage
    }
    edges {
      node {
        id
        title
        content
        tags {
          id
          name
        }
        created_at
        published_at
      }
    }
  }

  general: allStrapiGeneral {
    edges {
      node {
        id
        title
        subtitle
        cover {
          id
          width
          url
        }
      }
    }
  }
}
</page-query>

<script>
import { Pager } from 'gridsome'

export default {
  metaInfo: {
    title: '我的博客'
  },
  name: 'HomePage',
  components: {
    Pager
  },
  computed: {
    // 通过计算属性拿到Strapi的单节点（简写使用）
    generalNode () {
      return this.$page.general.edges[0].node
    }
  }
}
</script>

<style>
</style>
