<template>
  <div>
    <p>{{ age }}</p>
    <p>{{ person.age }}</p>
  </div>
</template>

<script lang="ts">
import { Vue, Component, Watch } from "vue-property-decorator";

interface Person {
  name: string;
  age: number;
}

@Component
export default class WatchTest extends Vue {
  private age = 37;
  private person: Person = {
    name: "mark",
    age: 37
  };
  private name = "mark";

  @Watch("age")
  onAgeChange(newVal: number, oldVal: number) {
    console.log(newVal, oldVal);
  }

  @Watch("person")
  onPersonChange(newVal: Person, oldVal: Person) {
    console.log("onPersonChange", newVal, oldVal);
  }

  @Watch("person", { deep: true })
  onPersonChangeDeep(newVal: Person, oldVal: Person) {
    console.log("onPersonChangeDeep", newVal, oldVal);
  }

  @Watch("name", { immediate: true })
  onNameChange(newVal: string, oldVal: string) {
    console.log("onNameChange", newVal, oldVal);
  }

  created() {
    console.log("created");
  }

  mounted() {
    console.log("mounted");
    this.person = { name: "mark", age: 37 };
  }
}
</script>