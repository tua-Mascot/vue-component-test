<template>
  <div class="component">
    <div class="component__header">
      <p>{{ displaySettings.subType }}</p>
    </div>
    <div class="component__title">
      <p>{{ displaySettings.type }}</p>
    </div>
    <div class="component__mBody">
      <div class="mBody__options">
        <p>{{ checkingComponentTitle }}</p>
      </div>
      <div class="mBody__values">
        <div class="values__opt" v-bind:key="element.condition.value" v-for="element of elements">
          <input type="text" v-bind:value="element.condition.value" />
        </div>
        <!-- this.elements[0].condition.value -->
        <!-- {{ dataChecker() }} -->
        <div class="values__addBtn">
            <button @click="addValue()">+ Add value</button>
        </div>
      </div>
    </div>
    <div class="component__bottom">
      <div class="bottom__title">
        <p>Follow is</p>
      </div>
      <div class="bottom__totalValue"></div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'conditions',
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
            action: 'fallthrough',
          },
          onMatch: {
            action: 'goto',
            target: '5e26e98027b2c58a1f',
          },
        },
        // {
        //   type: 'rule',
        //   condition: {
        //     entity: 'contact',
        //     field: 'followers',
        //     operand: 'lt',
        //     value: 10000,
        //   },
        //   onFail: {
        //     action: 'goto',
        //     target: '5e26e98027b2c58a2e',
        //   },
        //   onMatch: null,
        // },
      ],
      valueArr: [],
    };
  },
  computed: {
    checkingComponentTitle() {
      if (this.displaySettings.type === 'followers') {
        console.log(this.elements[0].condition.value);
        return 'Followers count is Greater than';
      }
      return 'Err';
    },
  },
  methods: {
    addValue() {
      const lastArrItem = this.elements.slice(-1);
      // const lastArrItem = [...this.elements];
      // const lastArrItem = this.elements[this.elements.length - 1];
      // console.log(lastArrItem);
      lastArrItem.onMatch = 'null';
      // lastArrItem.onFail = this.elements[this.elements.length - 1].onFail;
      // this.elements[this.elements.length - 1].onFail = this.elements[0].onFail;
      // this.elements[this.elements.length - 1].onFail.action = 'fallthrough';
      console.log(lastArrItem);
      console.log(this.elements);
      // eslint-disable-next-line vue/no-side-effects-in-computed-properties
      return this.elements.push(lastArrItem);
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss">
.component {
  min-width: 225px;
  max-width: 225px;
  min-height: 275px;
  margin: 12px;
  background-color: #ffffff;
  border-radius: 12px;
  box-shadow: 3px 3px 3px #dddddd;
}

.component__header {
  display: flex;
  align-items: center;
  width: 100%;
  min-height: 34px;
  /* max-height: 42px; */
  background-color: #16965a;
  color: #ffffff;
  border-radius: 12px 12px 0 0;
    p {
      padding: 0 10px;
    }
    p:first-letter {
      text-transform: capitalize;
    }
}

.component__title {
  display: flex;
  align-items: center;
  width: 100%;
  min-height: 34px;
  border-bottom: 1px solid #d1d1d1;
    p {
      padding: 0 10px;
      color: #818181;
      font-size: 9px;
    }
    p:first-letter {
      text-transform: capitalize;
    }
}

.component__mBody {
  display: flex;
  align-items: center;
  width: 100%;
  min-height: 34px;
}

.mBody__options {
  display: flex;
  align-items: center;
  width: 65%;
  min-height: 34px;
    p {
      padding: 0 10px;
      color: #818181;
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
  width: 100%;
  min-height: 34px;
  border: 1px #d1d1d1;
  border-style: none dashed dashed;
    input {
      width: 100%;
      min-height: 34px;
      border: none;
    }
}

.values__addBtn {
  width: 100%;
  min-height: 34px;
  border: 1px #d1d1d1;
  border-style: none dashed dashed;
    button {
      width: 100%;
      min-height: 34px;
      border: none;
    }
}

.component__bottom {
  display: flex;
  width: 100%;
  min-height: 34px;
}

.bottom__title {
  display: flex;
  align-items: center;
  width: 65%;
  min-height: 34px;
    p {
      padding: 0 10px;
      color: #818181;
    }
}

.bottom__totalValue {
  display: flex;
  align-items: center;
  width: 35%;
  min-height: 34px;
}
</style>
