<template>
  <div id="rectangles">
    <ul v-for="(rectangle, index) in rectangles" :key="index">
      <li>
        <input
          type="checkbox"
          :checked="rectangle.isActive"
          @input="check($event.target.checked, index)"
        />
        {{rectangle}}
      </li>
    </ul>
  </div>
</template>
<script>
export default {
  el: "#rectangles",
  name: "Rectangles",
  data: function() {
    return {};
  },
  props: ["rectangles"],
  methods: {
    check: function(value, key) {
      let index = key;
      let checked = value;
      console.log(index, checked);
      this.$emit("check", [index, checked]);
    }
  }
};
</script>