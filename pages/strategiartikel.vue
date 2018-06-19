<template>
    <div>
        <div class="container">
            <div class="entry" v-for="(item, $index) in entries" :key="$index">
                <div class="company--info row">
                    <span style="color: red; margin-right: 25px">{{item.fields.artikeltyp}}</span>
                    <div class="company" v-if="item.fields.analyseratBolag">
                        <div class="row">
                            <div class="image--container">
                                <img class="logo" v-if="item.fields.analyseratBolag.fields.bolagslogotyp" :src="item.fields.analyseratBolag.fields.bolagslogotyp.fields.file.url" alt="">
                            </div>
                            <p>{{item.fields.analyseratBolag.fields.namn}}</p>
                        </div>
                    </div>
                </div>
                <div class="row">
                    <div class="entry--image" v-if="item.fields.image">
                        <div class="image" :style="'background-image: url(' + item.fields.image.fields.file.url + ')'"></div>
                    </div>
                    <div class="entry--content">
                        <h1>{{item.fields.rubrik}}</h1>
                        <p>{{item.fields.ingress}}</p>
                    </div>
                </div>

                <ul v-if="item.fields.bullets">
                    <li v-for="bullet in item.fields.bullets">{{bullet}}</li>
                </ul>
            </div>
        </div>
    </div>
</template>

<script>
  import {createClient} from '~/plugins/contentful.js'

  const client = createClient()

  export default {
    asyncData ({env}) {
      return Promise.all([
        client.getEntries({
          'content_type': 'strategiartikel', 'include': 10
        })
      ]).then(([entries]) => {
        return {
          entries: entries.items,
        }
      }).catch(console.error)
    }
  }
</script>

<style>

    .container {
        margin-top: 50px;
        padding-bottom: 100px;
    }

    .row {
        width: 100%;
        display: flex;
        flex-direction: row;
    }

    .entry {
        padding: 5%;
        margin-bottom: 15px;
        background-color: #dbe1ec;
        border: 1px solid #959BA6;
    }

    .company--info {
        margin-bottom: 25px;
    }

    ul {
        margin-top: 25px;
    }

    ul li {
        list-style-type: circle;
    }
    .image--container{
        margin-right: 15px;
    }

    .company .logo {
        width: 85px;
    }

    .entry--image .image {
        width: 100px;
        height: 100px;
        margin-right: 15px;
        background-size: cover;
        background-position: center;
    }

</style>