<template>
  <div class="conditions">
    <div class="conditions__header">
      <img :src="require( `@/assets/logo.png`)" width="16" height="16" alt="Vue"/>
      <p>Conditions</p>
      <!-- <p @titleData="titleDataValue">{{ titleDataValue }}</p> // TODO -->
      <div class="decorative-circle--left"></div>
    </div>
    <div class="conditions__title">
      <p>
        <select v-model="conditionsData">
          <option v-for="conditionsTitle of conditionsTitles"
          :key="conditionsTitle">
          {{ conditionsTitle }}
          </option>
        </select>
      </p>
    </div>
    <conditionsBodyFollowers />
    <component v-if="component" :is="conditionsBodyFollowers"></component>
  </div>
</template>

<script>
import conditionsBodyFollowers from './conditionsBodyFollowers.vue';

export default {
  name: 'conditionsHeader',
  components: {
    conditionsBodyFollowers,
  },
  data() {
    return {
      component: null,
      conditionsData: 'Followers',
      conditionsTitles: [
        'Followers',
        'Likes',
        'Etc',
      ],
    };
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
    box-shadow: 3px 3px 3px #cfcfcf;
    /* overflow: hidden; */
      &__header {
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

      &__title {
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
          select {
            padding-left: 2px;
            width: 64px;
            font-size: 14px;
            border: none;
            -webkit-appearance: none;
            -moz-appearance: none;
            appearance: none;
            cursor: pointer;
              &:focus {
                background-color: #bae7d3
              }
          }
          select:first-letter {
            text-transform: capitalize;
          }
      }
  }

  .decorative-circle--left {
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
