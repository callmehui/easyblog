<template>
  <div class="article-item novel-item">
    <router-link :to="`/chapterdetail?id=${novel.id}`">
      <a class="title align-center">{{novel.name}}</a>
    </router-link>
    <div class="sub-info flex-center">
      <div class="item">
        <Icon type="UserOutlined" />
        <span class="text">{{novel.author}}</span>
      </div>
      <div class="item">
        <c-icon type="icon-clock" />
        <span class="text">
          {{ formatDate(novel.publishTime, true) }}
        </span>
      </div>
      <div class="item" v-if="novel.viewCount > 0">
        <c-icon type="icon-antd-fire" />
        <span class="text">{{novel.viewCount}}</span>
      </div>
    </div>
    <div class="introduce" v-html="marked(novel.summary)"></div>
    <div class="view-content">
      <router-link :to="`/chapterdetail?id=${novel.id}`">
        查看全文 &gt;
      </router-link>
    </div>
  </div>
</template>

<script>
import Icon from './Icon'
import { formatDate } from '../assets/js/tools'

const renderer = new marked.Renderer()
marked.setOptions({
  renderer: renderer,
  gfm: true,
  pedantic: false,
  sanitize: false,
  tables: true,
  breaks: true,
  smartLists: true,
  smartypants: false,
  highlight: function(code){
    return hljs.highlightAuto(code).value;
  }
})

export default {
  components: {
    'c-icon': Icon
  },
  props: {
    novel: {
      type: Object,
      required: true
    }
  },
  methods: {
    formatDate,
    marked
  },
}
</script>

<style lang="scss" scoped>
.article-item {
  width: 100%;
  background-color: #fff;
  margin-bottom: 1rem;
  padding: 1rem 1rem;
  border-radius: .25rem;
  .title {
    font-size: 1.3rem;
    display: block;
    margin-bottom: .5rem;
  }
  .sub-info {
    display: flex;
    align-items: center;
    padding-bottom: .5rem;
    .reprint {
      color: #74cf59;
      margin-right: 2rem;
      padding: .25rem .5rem;
      background-color: #eaf9e3;
    }
    .orginal {
      color: #ca0c16;
      background-color: #f9ecec;
    }
    .item {
      font-size: 1rem;
      color: #999999;
      margin-right: 2rem;
      padding-right: 0;
      .text {
        font-size: .9rem;
        margin-left: .5rem;
      }
    }
    .tag {
      color: rgba(204, 51, 51, .6);
      .text {
        margin-left: 0rem;
      }
    }
  }
  .introduce {
    color: #333333;
    font-size: 1rem;
    padding: .5rem 0 1rem;
    img{
      width:100% ;
      border-radius:5px;
      border:1px solid #f0f0f0;
      max-width:1000px !important;
      display: block;
      margin:8px  auto ;
    }
  }
  .view-content {
    display: flex;
    flex-direction: row-reverse;
    margin-right: 2rem;
  }
  & /deep/ pre{
    display: block;
    background-color: #283646;
    padding: .5rem !important;
    overflow-y: auto;
    font-weight: 300;
    font-family: Menlo, monospace;
    border-radius: .3rem;
  }
  & /deep/ pre > code{
    border:0px !important;
    background-color: #283646 !important;
    color:#FFF;
  }
  & /deep/ code {
    color: #c7254e;
    background-color: #f9f2f4;
    border-radius: 4px;
    font-size: 12px;
    padding-left: 5px;
    padding-right: 5px;
    margin: 0px 3px;
    width: calc(100% - 10px);
    box-sizing: border-box;
  }
}

.novel-item {
  .align-center {
    text-align: center;
  }
  .flex-center {
    justify-content: center;
  }
}
</style>
