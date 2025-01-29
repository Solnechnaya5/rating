<template>
  <div class="rating-row">
  <div class="rating-text">
  <img class="google-img" src="../assets/imgs/google.svg" alt="google icon" />
  <h3>{{ title }}</h3>
    </div>
  <div class="rating-data">
      <div class="rating-data__contaner">
        <span class="rating-num">{{ rating }} / 5</span>
        <div class="rating-stars">
          <svg
            v-for="index in 5"
            :key="index"
            class="star"
            :class="{ 'filled': index <= rating }"
            width="26.235840"
            height="25.049896"
            viewBox="0 0 26.2358 25.0499"
            fill="none"
            xmlns="http://www.w3.org/2000/svg"
          >
            <defs />
            <path
              id="Star 5"
              d="M8.94 7.2C8.79 7.49 8.51 7.7 8.18 7.74L0.85 8.81C0.03 8.93 -0.3 9.94 0.3 10.51L5.6 15.69C5.84 15.92 5.95 16.25 5.89 16.57L4.64 23.87C4.5 24.69 5.36 25.31 6.09 24.93L12.65 21.48C12.94 21.33 13.29 21.33 13.58 21.48L20.14 24.93C20.87 25.31 21.73 24.69 21.59 23.87L20.33 16.57C20.28 16.25 20.39 15.92 20.62 15.69L25.93 10.51C26.52 9.94 26.19 8.93 25.37 8.81L18.04 7.74C17.72 7.7 17.43 7.49 17.29 7.2L14.01 0.55C13.64 -0.19 12.58 -0.19 12.22 0.55L8.94 7.2ZM10.73 8.08C10.29 8.97 9.45 9.58 8.47 9.72L3.14 10.5L7 14.25C7.71 14.94 8.03 15.94 7.86 16.91L6.95 22.21L11.72 19.71C12.59 19.25 13.63 19.25 14.51 19.71L19.27 22.21L18.36 16.91C18.2 15.94 18.52 14.94 19.23 14.25L23.08 10.5L17.75 9.72C16.78 9.58 15.93 8.97 15.5 8.08L13.11 3.25L10.73 8.08Z"
              :fill="index <= rating ? '#FCC141' : 'none'"
              stroke="#FCC141"
            />
          </svg>
        </div>
      </div>
        <span class="reviews-num">({{ reviewsCount }} Відгуки)</span>
      
  </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

interface RatingData {
  rate: number;
  reviewsCount: number;
}

export default defineComponent({
  props: {
    title: {
      type: String,
      required: false,
      default: "Відгуки наших клієнтів у Google", 
    },
  },
  data() {
    return {
      rating: 0 as number,
      reviewsCount: 0 as number,
    };
  },
  mounted() {
    this.fetchRatingData();
  },
  methods: {
    async fetchRatingData(): Promise<void> {
      try {
        const response = await fetch(
          'https://679894bcbe2191d708b0218a.mockapi.io/api/rate/rating'
        );
        const data: RatingData[] = await response.json();

        const randomIndex = Math.floor(Math.random() * data.length);
        const randomRating = data[randomIndex];

        this.rating = randomRating.rate >= 5 ? 5 : randomRating.rate;
        this.reviewsCount = randomRating.reviewsCount;
      } catch (error) {
        console.error('Error fetching rating data:', error);
      }
    },
  },
});
</script>

<style scoped>

.rating-row{
  display: flex;
  align-items: center;
  height: inherit;
}
.rating-data{
  display: flex;
  align-items: center;
}
.rating-data__contaner{
  display: flex;
}
.rating-text{
  display: flex;
  align-items: center;
  margin-right: 60px;
}
.google-img{
  width: 40px;
  height: 40px;
  margin-right: 20.8px;
}
.rating-text h3{
color: rgb(57, 65, 85);
font-size: 20px;
font-weight: 500;
line-height: 30px;
text-align: left;
}
.rating-stars {
  display: flex;
  margin-right: 20px;
}

.star {
margin-right: 6px;
}.star:last-child{
  margin-right: 0;
}

.star.filled {
  fill: #fcc141; 
}

.rating-info {
  display: flex;
}
.rating-num{
color: rgb(57, 65, 85);
font-family: 'Greenwich';
font-size: 36px;
font-weight: 500;
line-height: 44px;
margin-right: 20px;
}
.reviews-num{
  color: rgb(121, 133, 149);
font-size: 14px;
font-weight: 400;
line-height: 22px;
letter-spacing: 0%;
text-align: left;
}
@media(max-width: 1199px){
    .rating-row{
      flex-direction: column;
    }
    .rating-data{
      margin-top: 10px;
    }
    .rating-num{
      font-size: 24px;
font-weight: 500;
line-height: 32px;
    }
  }
  @media(max-width: 576px){
    .rating-data{
      width: 100%;
  flex-direction: column;
  align-items: start;
  margin-bottom: 6px;
}
  }
</style>
