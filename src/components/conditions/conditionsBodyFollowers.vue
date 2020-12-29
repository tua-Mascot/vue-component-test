<template>
   <div class="conditions__mBody">
      <div class="mBody__options">
        <div class="dropdown__content">
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
      <div class="mBody__values">
         <div class="values__opt" v-for="(element, index) of elements" :key="index"> <!-- key id -->
          <button :disabled="elements.length === 1" @click="removeElement(index)"
          :style="{opacity: elements.length > 1 ? 1 : 0}">&times;</button>
          <input v-model="element.condition.value" />
          <div class="decorativeCircleRight"></div>
        </div>
        <div class="values__addBtn">
            <button @click="addValue()">+ Add value</button>
            <div class="decorativeCircleRight"></div>
        </div>
      </div>
    </div>
    <div class="conditions__bottom">
      <div class="bottom__title">
        <p>Followers count is</p>
      </div>
      <div class="bottom__wrap">
        <div class="bottom__totalValue">
          <p>5000 or <br><span>{{ checkingSelected }}</span></p>
        </div>
        <div class="decorativeCircleRight"></div>
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
      firstOnFailSaver: null,
      selected: 'Greater',
    };
  },
  mounted() {
    this.firstOnFailSaver = JSON.parse(JSON.stringify(this.elements[0]));
  },
  computed: {
    checkingSelected() {
      if (this.selected === 'Greater') {
        console.log(1);
        return 'less';
      }
      console.log(2);
      return 'greater';
    },
    // checkingConditionsTitle() {
    //   // TODO
    //   if (this.displaySettings.type === 'followers') {
    //     return `Followers count is${<span class='dropdown'>Greater
    //     <div class='dropdown__content'>
    //     <span>Greater</span><span>Less</span>
    //     </div>
    //     </span>}than`;
    //   }
    //   return 'Err';
    // },

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
    lastItemElements() {
      return this.elements[this.elements.length - 1];
    },
  },
  watch: {
    elements: {
      deep: true,
      handler(newElements) {
        if (newElements.length === 1) {
          this.elements[0].onFail = this.firstOnFailSaver;
          console.log(this.elements);
        }
      },
    },
  },
};
</script>

<style lang='scss'>
 .conditions__mBody {
    display: flex;
    width: 100%;
    height: 100%;
    min-height: 34px;
  }

  .mBody__options {
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

  .dropdown__content {
    position: absolute;
      select {
        width: 50px;
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

  .mBody__values {
    display: flex;
    align-items: center;
    flex-direction: column;
    width: 35%;
    min-height: 34px;
  }

  .values__opt {
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

  .values__addBtn {
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

  .conditions__bottom {
    display: flex;
    width: 100%;
    min-height: 34px;
    margin-top: auto;
    border: 1px #d1d1d1;
    border-style: dashed none none none;
  }

  .bottom__title {
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

  .bottom__wrap {
    position: relative;
    width: 35%;
  }

  .bottom__totalValue {
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

  .decorativeCircleRight {
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
