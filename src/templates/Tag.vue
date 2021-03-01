<template>
  <Layout>
    <!-- Page Header -->
    <!-- static/img下的图片 -->
    <header class="masthead" style="background-image: url('/img/home-bg.jpg')">
      <div class="overlay"></div>
      <div class="container">
        <div class="row">
          <div class="col-lg-8 col-md-10 mx-auto">
            <div class="site-heading">
              <h1>{{ $page.tag.name }}</h1>
              <span class="subheading">按相关标签分类的文章</span>
            </div>
          </div>
        </div>
      </div>
    </header>

    <!-- Main Content -->
    <div class="container">
      <div class="row">
        <div class="col-lg-8 col-md-10 mx-auto">
          <div class="post-preview" v-for="post in $page.tag.posts" :key="post.id">
            <g-link :to="'/post/' + post.id">
              <h2 class="post-title">
                {{ post.title }}
              </h2>
              <!-- 副标题 -->
              <!-- <h3 class="post-subtitle">
                暂无
              </h3> -->
            </g-link>
            <p class="post-meta">Posted by
              <a href="#">Wan Peng</a>
              on {{ post.created_at }}</p>
            <!-- <p>
              <span v-for="tag in edge.node.tags" :key="tag.id">
                <g-link :to="'/tag/' + tag.id">{{ tag.name }}</g-link>
                &nbsp;&nbsp;
              </span>
            </p> -->
            <hr>
          </div>
          <!-- Pager -->
          <!-- gridsome自带的分页组件，通过posts别名拿到页面信息 -->
          <!-- <Pager :info="$page.posts.pageInfo"/> -->
          <!-- <div class="clearfix">
            <a class="btn btn-primary float-right" href="#">Older Posts &rarr;</a>
          </div> -->
        </div>
      </div>
    </div>
  </Layout>
</template>

<page-query>
query ($id: ID!) {
  tag: strapiTag(id: $id) {
    id
    name
    posts {
      id
      title
      created_at
    }
  }
}
</page-query>

<script>
export default {
  name: 'TagPage',
  metaInfo () {
    return {
      title: `${this.$page.tag.name}的文章`
    }
  }
}
</script>

<style>

</style>