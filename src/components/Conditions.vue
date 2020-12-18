<template>
  <div class="component">
    <div class="component__header">
      <p>Conditions</p>
    </div>
    <div class="component__title">
      <p> > Followers</p>
    </div>
    <div class="component__mBody">
      <div class="mBody__options"></div>
      <div class="mBody__values"></div>
    </div>
    <div class="component__bottom">
      <div class="bottom__title"></div>
      <div class="bottom__totalValue"></div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String,
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss">
.component {
  min-width: 300px;
  min-height: 300px;
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
}

.component__title {
  display: flex;
  align-items: center;
  width: 100%;
  min-height: 34px;
  border-bottom: 1px solid #818181;
  p {
      padding: 0 10px;
      color: #818181;
      font-size: 10px;
    }
}

</style>
