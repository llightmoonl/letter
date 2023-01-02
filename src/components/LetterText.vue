<template>
  <div class = "container">
    <h1 class = "post__title">{{dataJson.title}}</h1>
    <div class="post__information">
      <div class="post__item author">{{dataJson.author}}</div>
      <div class = "post__item date">{{dataJson.date}}</div>
    </div>
    <div class = "post__text">
      <p class = "text__item" v-for = "item in dataJson.text" :key="item">{{item}}</p>
    </div>
  </div>
</template>
<script>

export default {
  name: 'LetterText',
  props: ['dataJson'],

}
</script>
