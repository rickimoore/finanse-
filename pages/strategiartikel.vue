<template>
    <div>
        <div class="container">
            <h1>strategiartikel</h1>
            <div class="entry" v-for="(item, $index) in entries" :key="$index">
                <h1>{{item.fields.rubrik}}</h1>
                <p>{{item.fields.ingress}}</p>

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
    }

    .entry {
        padding: 5%;
        margin-bottom: 15px;
        background-color: #dbe1ec;
        border: 1px solid #959BA6;
    }

    ul {
        margin-top: 25px;
    }

    ul li {
        list-style-type: circle;
    }

</style>