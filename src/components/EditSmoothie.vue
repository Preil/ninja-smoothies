<template>
  <div v-if="smoothie" class="edit-smoothie container">
    <h2>Edit Smoothie {{ this.$route.params.smoothie_slug }}</h2>
    <p>{{ this.smoothie.title }}</p>
    <p>{{ this.smoothie.slug }}</p>
  </div>
</template>

<script>
  import db from '@/firebase/init'

  export default {
    name: "EditSmoothie",
    data() {
      return {
        smoothie: null
      }
    },
    created() {
      let ref = db.collection('smoothies').where('slug', '==', this.$route.params.smoothie_slug)
      ref.get().then(snapshot => {
        snapshot.forEach(doc => {
          this.smoothie = doc.data()
          this.smoothie.id = doc.id
          console.log(this.smoothie)
        })
      })

    }
  }
</script>

<style scoped>

</style>
