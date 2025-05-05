<template>
  <div class="article-search-wrapper">
    <div class="container">
      <h1>Article Search</h1>
      <input
        type="text"
        v-model="searchTerm"
        placeholder="Search articles..."
        class="search-box form-control"
      />
      
      <div class="row justify-content-between gy-4 gx-4">
        <div v-for="(article, index) in filteredArticles" :key="index" class="col-xl-6 col-md-6 col-12 article">
          <h2 v-html="highlightText(article.title)"></h2>
          <p v-html="highlightText(article.content)"></p>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
  import { ref, computed } from 'vue'

  const searchTerm = ref('')

  const articles = [
    {
      title: 'Vue.js Introduction',
      content: 'Vue.js is a progressive JavaScript framework for building user interfaces.'
    },
    {
      title: 'React vs Vue',
      content: 'Both React and Vue are popular JavaScript frameworks for frontend development.'
    },
    {
      title: 'Why Choose Vue?',
      content: 'Vue offers a simpler learning curve and better integration capabilities.'
    },
    {
      title: 'JavaScript Fundamentals',
      content: 'Understanding variables, functions, and loops is key to mastering JavaScript.'
    },
    {
      title: 'CSS Grid Layout',
      content: 'CSS Grid allows developers to create complex responsive layouts easily.'
    },
    {
      title: 'Flexbox in Depth',
      content: 'Flexbox is ideal for one-dimensional layouts like navbars and columns.'
    },
    {
      title: 'Building with Vite',
      content: 'Vite provides fast build times and a modern development environment for Vue and React.'
    },
    {
      title: 'Single Page Applications',
      content: 'SPAs improve user experience by loading content dynamically without refreshing.'
    },
    {
      title: 'Understanding Props in Vue',
      content: 'Props are used to pass data from a parent component to a child component.'
    },
    {
      title: 'Vue Lifecycle Hooks',
      content: 'Vue lifecycle hooks let you run code at specific stages of a component’s life.'
    }
  ]

  const filteredArticles = computed(() => {
    if (!searchTerm.value) return articles
    const term = searchTerm.value.toLowerCase()
    return articles.filter(
      (article) =>
        article.title.toLowerCase().includes(term) ||
        article.content.toLowerCase().includes(term)
    )
  })

  function highlightText(text) {
    if (!searchTerm.value) return text
    const pattern = new RegExp(`(${searchTerm.value})`, 'gi')
    return text.replace(pattern, '<mark>$1</mark>')
  }
</script>

<style>
  .article-search-wrapper {
    height: 100%;
    width: 100%;
    background-color: #dddddd5c;
    position: relative;
  }
  .container {
    border-radius: 10px;
    font-family: Arial, sans-serif;
    padding-top: 3rem;
    padding-bottom: 3rem;
  }
  .row{
    width: 100%;
    margin: 0 auto;
  }

  h1{
    margin-top: 0px;
    font-size: 46px;
    font-weight: 700;
  }

  h2{
    font-size: 30px;
    font-weight: 600;
  }
  p{
    font-size: 20px;
    margin-bottom: 0px;
  }
  .search-box {
    width: 100%;
    padding: 12px;
    margin-bottom: 1.5rem;
    font-size: 18px;
  }
  .form-control:focus{
    box-shadow: unset !important;
  }

  .article {
    width: 49%;
    text-align: left;
    background-color: #ffffff;
    padding: 1rem;
    border-radius: 10px;
    box-shadow: 0px 0px 15px 0px rgba(0, 0, 0, 10%);
  }

  mark {
    background-color: yellow;
    padding: unset;
  }

  @media(max-width: 575px){
    .article{
      width: unset;
    }
    h1{
      font-size: 40px;
    }

    h2{
      font-size: 26px;
    }
    p{
      font-size: 18px;
    }
  }
</style>
