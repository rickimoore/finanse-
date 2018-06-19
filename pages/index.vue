<template>
  <div>
    <div class="container">
      <div class="entry" v-for="(item, $index) in entries" :key="$index">
        <h1>{{item.fields.namn}}</h1>
        <p>{{item.fields.isinKod}}</p>
        <span>{{item.fields.marknadsplats}}</span>
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
        'content_type': 'bolag'
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

</style>
