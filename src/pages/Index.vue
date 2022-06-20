
<template>
<div>
    <nav class="navbar navbar-expand-lg navbar-dark bg">
      <div class="container-fluid">
        <a class="navbar-brand" href="#">CricZone</a>
      </div>
    </nav>
    <div class="nav">
        <div class="nav-item">Hello</div>
        <div class="nav-item">Hello</div>
        <div class="nav-item">Hello</div>
        <div class="nav-item">Hello</div>
    </div>
  <div class="container">
    <div>
      <h1> Posts </h1>
      <div class="row">
      <div class="col-9">
          <Carousel :per-page="1" :paginationSize="8" :autoplay="true" :loop="true" :autoplayTimeOut="1000" :autoplayHoverPause="true" paginationColor="#efefef" paginationPosition="bottom-overlay" paginationActiveColor="#ff4500" :navigationEnabled="true">
            <Slide v-for="{ node } in $static.posts.edges" :key="node.featuredImage.node.id">

              <div>
                <div class="image-caption">
                  <h5 class="card-title">{{node.title}}</h5>
                  <div class="fw-light text-start"><i class="bi bi-calendar-day"></i> {{date(node.date)}}</div>
                </div>
                <img :src="node.featuredImage.node.link" :alt="node.featuredImage.node.altText" id="slide-img" class="card-img-top">
              </div>

            </Slide>
          </Carousel>
          <br>
          <div class="row row-cols-2">
            <div v-for="{ node } in $static.posts.edges" :key="node.id">
                  <img :src="node.featuredImage.node.link" class="card-img-top" :alt="node.featuredImage.node.altText">
                  <figcaption v-html="node.featuredImage.node.caption" class="text-end fst-italic"></figcaption>
                  <div class="card-body">
                    <div class="title-card">
                    <h5 class="card-title">{{node.title}}</h5>
                    <div class="fw-light text-start"><i class="bi bi-calendar-day"></i> {{date(node.date)}}</div>
                    </div>
                    <br>
                    <div class="card-text"><span v-html="node.excerpt">...</span></div>
                  </div>
            </div>
          </div>
        </div>

        <div class="col-3">
          <div>
          </div>
        </div>
      </div>
    </div>
  </div>
</div>
</template>


<static-query>
{
  posts {
    edges {
      node {
        featuredImage {
          node {
            link
            altText
            caption
          }
        }
        excerpt
        date
        content
        title
        id
      }
    }
  }
}

</static-query>


<script>
import { Carousel , Slide } from 'vue-carousel';

export default {
  components: {
    Carousel,
    Slide
  },
  metaInfo: {
    title: 'Hello, world!'
  },
  methods:{
    date(string){
      let arr = string.split('T')
      return Date(arr[0]).slice(4,15)
    }
  }
}

</script>

<style>
@import url("https://cdn.jsdelivr.net/npm/bootstrap-icons@1.8.3/font/bootstrap-icons.css");
.card-img-top:hover{
  transform: scale(1.02);
}
.image-caption:hover {
  color:orangered;
}

.title-card:hover {
  color:orangered;
}

.home-links a {
  margin-right: 1rem;
}

.image-caption{
  transform: translate(5%,20%);
  color:white;
  width:70%;
  height:5%;
  position:absolute;
  z-index: 9;
  padding: 3px;
}
#slide-img{
    float: left;
    width:  100%;
    height: 100%;
    object-fit: cover;
}
.VueCarousel-slide{
  max-height:25%;
}
.VueCarousel-wrapper{
  max-height:450px;
}
.bg{
  background-color: black;
}
.navbar{
  min-height: 140px;
  max-height: 140px;
}
.nav-item{
  margin:1% 2%;
}
.nav{
  background-color: orangered;
  color:white;
}

</style>
