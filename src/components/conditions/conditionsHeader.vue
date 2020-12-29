<template>
  <div class="conditions">
    <div class="conditions__header">
      <img :src="require( `@/assets/logo.png`)" width="16" height="16" alt="Vue"/>
      <!-- <p>{{ displaySettings.subType }}</p> -->
      <!-- <p v-if=""></p> -->
      <div class="decorativeCircleLeft"></div>
    </div>
    <div class="conditions__title">
      <!-- <p>{{ displaySettings.type }}</p> -->
      <p>
        <select v-model="conditions_data"> <!-- v-model="conditions__titles_selected" -->
          <option v-for="conditions__title of conditions__titles"
          :key="conditions__title">  <!-- :value="conditions__title" -->
          {{ conditions__title }}
          </option>
        </select>
      </p>
    </div>
    <conditionsBodyFollowers />
    <!-- <conditionsBodyFollowers v-if="this.conditions_data === 'followers'" />
    <conditionsBodyLikes v-else-if="this.conditions_data === 'likes'" />
    <conditionsBodyEtc v-else-if="this.conditions_data === 'etc'" /> -->
    <!-- <component v-else>Error</component> -->
    <!-- <component :is="this.conditionsBodyFollowers"></component> -->
  </div>
</template>

<script>
import conditionsBodyFollowers from './conditionsBodyFollowers.vue';
// import conditionsBodyLikesFake from './conditionsBodyLikesFake.vue';
// import conditionsBodyEtcFake from './conditionsBodyEtcFake.vue';

export default {
  name: 'conditionsHeader',
  components: {
    // conditionsBodyFollowers: () => import('./conditionsBodyFollowers.vue'),
    // conditionsBodyLikes: () => import('./conditionsBodyFollowers.vue'),
    // conditionsBodyEtc: () => import('./conditionsBodyFollowers.vue'),
    conditionsBodyFollowers,
    // conditionsBodyLikesFake,
    // conditionsBodyEtcFake,
  },
  data() {
    return {
      component: '',
      conditions_data: '',
      conditions__titles: [
        'followers',
        'likes',
        'etc',
      ],
    };
  },
  beforeUpdate() {
    console.log(this.conditions_data);
  },
  methods: {
    componentChecker() {
      if (this.conditions_data === 'followers') {
        // console.log(componentChecker());
        return this.component === conditionsBodyFollowers;
      }
      return undefined;
    },
  },
};

</script>

<style lang='scss'>
  .conditions {
    display: flex;
    flex-direction: column;
    min-width: 225px;
    max-width: 225px;
    min-height: 275px;
    margin: 12px;
    background-color: #ffffff;
    /* background: linear-gradient( #bae7d3 0px, #bae7d3 10px, #ffffff 10px, #ffffff 100%); */
    border-radius: 6px;
    border: 1px solid #41b883;
    box-shadow: 3px 3px 3px #dddddd;
    /* overflow: hidden; */
  }

  .conditions__header {
    position: relative;
    display: flex;
    align-items: center;
    width: 100%;
    min-height: 34px;
    background-color: #bae7d3;
    border-radius: 5px 5px 0 0;
      p {
        padding: 0 10px 0 0;
      }
      p:first-letter {
        text-transform: capitalize;
      }
      img {
        margin: 0 6px;
      }
  }

  .conditions__title {
    display: flex;
    align-items: center;
    width: 100%;
    min-height: 34px;
    border: 1px solid #d1d1d1;
    border-style: solid none;
      p {
        padding: 0 10px;
        color: #818181;
        font-size: 9px;
      }
      p:first-letter {
        text-transform: capitalize;
      }
  }

  .decorativeCircleLeft {
    /* z-index: 999;
    clear: both;
    overflow: visible; */
    position: absolute;
    left: -5px;
    height: 10px;
    width: 10px;
    border-radius: 50%;
    border: 1px solid #41b883;
    background-color: #ffffff;
  }
</style>
