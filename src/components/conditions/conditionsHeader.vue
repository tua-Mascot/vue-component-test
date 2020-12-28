<template>
  <div class="conditions">
    <div class="conditions__header">
      <img :src="require( `@/assets/logo.png`)" width="16" height="16" alt="Vue"/>
      <p>{{ displaySettings.subType }}</p>
      <div class="decorativeCircleLeft"></div>
    </div>
    <div class="conditions__title">
      <p>{{ displaySettings.type }}</p>
    </div>
    <conditionsBody />
  </div>
</template>

<script>
import conditionsBody from './conditionsBody.vue';

export default {
  name: 'conditionsHeader',
  components: {
    conditionsBody,
  },
};
// export default {
//   name: 'conditions',
//   data() {
//     return {
//       displaySettings: {
//         subType: 'condition',
//         type: 'followers',
//       },
//       elements: [
//         {
//           type: 'rule',
//           condition: {
//             entity: 'contact',
//             field: 'followers',
//             operand: 'lt',
//             value: 5000,
//           },
//           onFail: {
//             action: 'goto',
//             target: '5e26e98027b2c58a70085d4e',
//           },
//           onMatch: {
//             action: 'goto',
//             target: '5e26e98027b2c58a70085d4f',
//           },
//         },
//       ],
//       firstOnFailSaver: null,
//       selected: '',
//     };
//   },
//   mounted() {
//     this.firstOnFailSaver = JSON.parse(JSON.stringify(this.elements[0]));
//   },
//   computed: {
//     checkingConditionsTitle() {
//       // TODO
//       if (this.displaySettings.type === 'followers') {
//         return `Followers count is${<span class='dropdown'>Greater
//         <div class='dropdown__content'>
//         <span>Greater</span><span>Less</span>
//         </div>
//         </span>}than`;
//       }
//       return 'Err';
//     },
//     lastItemElements() {
//       return this.elements[this.elements.length - 1];
//     },
//   },
//   methods: {
//     addValue() {
//       const newValue = JSON.parse(JSON.stringify(this.lastItemElements));
//       newValue.onMatch = null;
//       this.elements[this.elements.length - 1].onFail = 'fallthrough';
//       this.elements.push(newValue);
//     },
//     removeElement(index) {
//       this.elements.splice(index, 1);
//       // this.$delete(this.elements, index); ?????
//     },
//   },
//   watch: {
//     elements: {
//       deep: true,
//       handler(newElements) {
//         if (newElements.length === 1) {
//           this.elements[0].onFail = this.firstOnFailSaver;
//           console.log(this.elements);
//         }
//       },
//     },
//   },
// };
</script>

<!-- Add "scoped" attribute to limit CSS to this conditions only -->
<style lang='scss'>
  .conditions {
    display: flex;
    flex-direction: column;
    min-width: 225px;
    max-width: 225px;
    min-height: 275px;
    margin: 12px;
    background-color: #ffffff;
    border-radius: 6px;
    border: 1px solid #41b883;
    box-shadow: 3px 3px 3px #dddddd;
    /* overflow-y: hidden; */
    overflow: hidden;
  }

  .conditions__header {
    position: relative;
    display: flex;
    align-items: center;
    width: 100%;
    min-height: 34px;
    /* max-height: 42px; */
    background-color: #bae7d3;
    /* border-radius: 4px 4px 0 0; */
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
