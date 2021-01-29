<template>
   <div class="conditions__m-body">
      <div class="conditions__m-body-options">
        <div class="conditions__m-body-options-dropdown">
          <p>
            Followers count <br> is
            <select v-model="selected">
              <option>Greater</option>
              <option>Less</option>
            </select>
            than
          </p>
        </div>
      </div>
      <div class="conditions__m-body-values">
         <div class="conditions__m-body-values-opt"
         v-for="(element, index) of elements" :key="index">
          <button :disabled="elements.length === 1" @click="removeElement(index)"
          :style="{opacity: elements.length > 1 ? 1 : 0}">&times;</button>
          <input v-model="element.condition.value" />
          <div class="decorative-circle--right"></div>
        </div>
        <div class="conditions__m-body-values-add-btn">
            <button @click="addValue">+ Add value</button>
            <div class="decorative-circle--right"></div>
        </div>
      </div>
    </div>
    <div class="conditions__bottom">
      <div class="conditions__bottom-title">
        <p>Followers count is</p>
      </div>
      <div class="conditions__bottom-total-value--bottom-wrap">
        <div class="conditions__bottom-total-value">
          <p>5000 or <br><span>{{ checkingSelected }}</span></p>
        </div>
        <div class="decorative-circle--right"></div>
      </div>
    </div>
</template>

<script>
export default {
  name: 'conditionsBodyFollowers',
  data() {
    return {
      displaySettings: {
        subType: 'condition',
        type: 'followers',
      },
      elements: [
        {
          type: 'rule',
          condition: {
            entity: 'contact',
            field: 'followers',
            operand: 'lt',
            value: 5000,
          },
          onFail: {
            action: 'goto',
            target: '5e26e98027b2c58a70085d4e',
          },
          onMatch: {
            action: 'goto',
            target: '5e26e98027b2c58a70085d4f',
          },
        },
      ],
      selected: 'Greater',
      firstOnFailSaver: null,
    };
  },

  mounted() {
    this.firstOnFailSaver = JSON.parse(JSON.stringify(this.elements[0]));
  },

  computed: {
    checkingSelected() {
      if (this.selected === 'Greater') {
        return 'less';
      }
      return 'greater';
    },
    lastItemElements() {
      return this.elements[this.elements.length - 1];
    },
  },

  methods: {
    addValue() {
      const newValue = JSON.parse(JSON.stringify(this.lastItemElements));
      newValue.onMatch = null;
      this.elements[this.elements.length - 1].onFail = 'fallthrough';
      this.elements.push(newValue);
    },
    removeElement(index) {
      this.elements.splice(index, 1);
    },
    // titleData() {
    //   this.$emit('displaySubType', this.displaySettings.subType);
    // }, // TODO ?
  },

  watch: {
    elements: {
      deep: true,
      handler(newElements) {
        if (newElements.length === 1) {
          this.elements[0].onFail = this.firstOnFailSaver;
        }
      },
    },
  },
};
</script>

<style lang='scss'>
  .conditions {
    &__m-body {
      display: flex;
      width: 100%;
      height: 100%;
      min-height: 34px;
    }
    &__m-body-options {
      display: flex;
      align-items: center;
      width: 65%;
      min-height: 34px;
      border: 1px #d1d1d1;
      border-style: none dashed none none;
        p {
          padding: 0 10px;
          color: #818181;
        }
    }
    &__m-body-options-dropdown {
      position: absolute;
        select {
          width: 52px;
          padding-left: 1px;
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
    }
    &__m-body-values {
      display: flex;
      align-items: center;
      flex-direction: column;
      width: 35%;
      min-height: 34px;
    }
    &__m-body-values-opt {
      position: relative;
      display: flex;
      width: 100%;
      min-height: 34px;
      border: 1px #d1d1d1;
      border-style: none none dashed none;
        input {
          color: #41b883;
          width: 80%;
          min-height: 34px;
          padding: 0 0 0 5px;
          border: none;
          outline: none;
          font-size: 12px;
            &:focus {
              text-decoration: underline;
            }
        }
        button {
          width: 20%;
          border: none;
          background: none;
        }
    }
    &__m-body-values-add-btn {
      position: relative;
      width: 100%;
      min-height: 34px;
      margin-top: auto;
      /* border: 1px #d1d1d1;
      border-style: none none none dashed; */
        button {
          color: #41b883;
          width: 100%;
          min-height: 34px;
          border: none;
          background: none;
          font-size: 12px;
        }
    }

    &__bottom {
      display: flex;
      width: 100%;
      min-height: 34px;
      margin-top: auto;
      border: 1px #d1d1d1;
      border-style: dashed none none none;
    }

    &__bottom-title {
      display: flex;
      align-items: center;
      width: 65%;
      min-height: 34px;
      border: 1px #d1d1d1;
      border-style: none dashed none none;
        p {
          padding: 0 10px;
          color: #818181;
        }
    }

    &__bottom-total-value--bottom-wrap {
      position: relative;
      width: 35%;
    }

    &__bottom-total-value {
      display: flex;
      align-items: center;
      margin: 0;
      /* width: 35%; */
      min-height: 34px;
        p {
          color: #b84141;
          padding-left: 4px;
        }
    }
  }

  .decorative-circle--right {
    position: absolute;
    top: 12px;
    left: 73px;
    height: 10px;
    width: 10px;
    border-radius: 50%;
    border: 1px solid #41b883;
    background-color: #ffffff;
  }
</style>
