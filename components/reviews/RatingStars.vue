<template>
  <div class="ratings__stars d-flex">
    <span
      v-for="(star, index) in ratings"
      :key="star.rating"
      class="ratings__star text-center"
    >
      <i
        :class="starBinder(index, star.rating)"
        class="d-block"
        @mouseout="hovered = hovered.filter(each => each !== index)"
        @mouseover="hovered = [...hovered, index]"
        @click="$store.commit('reviews/setChosen', star.rating)"
      />
      <span
        :class="textColorBinder(star.rating)"
        class="text-center ratings__star-text"
      >{{ star.text }}</span>
    </span>
  </div>
</template>

<script>
export default {
  data () {
    return {
      ratings: [
        { rating: 1, text: 'Awful' },
        { rating: 2, text: 'Not great' },
        { rating: 3, text: 'Okay' },
        { rating: 4, text: 'Pretty good' },
        { rating: 5, text: 'Fantastic!' }
      ],
      hovered: []
    }
  },
  methods: {
    starBinder (index, rating) {
      if (
        this.hovered.includes(index) ||
        this.hovered[0] >= index ||
        this.$store.state.reviews.chosen >= rating
      ) {
        return 'fas fa-star ratings__star-is-chosen'
      } else {
        return 'far fa-star'
      }
    },
    textColorBinder (rating) {
      return this.$store.state.reviews.chosen === rating && 'bold text-purple'
    }
  }
}
</script>

<style lang="scss"></style>
