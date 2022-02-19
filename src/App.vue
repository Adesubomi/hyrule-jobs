<template>
  <div class="app">
    <header>
      <button @click="handleClick('location')">Order by location</button>
      <button @click="handleClick('title')">Order by title</button>
      <button @click="handleClick('salary')">Order by salary</button>

      <div>
          <br />
          <h2>Available Jobs</h2>
      </div>
    </header>
    <JobList :jobs="jobs" :order="order" />
  </div>
</template>


<script lang="ts">
import { defineComponent, reactive, toRefs, ref } from "vue";
import type Job from "./types/Job";
import type OrderTerm from "./types/OrderTerm";
import JobList from "./components/JobList.vue";

export default defineComponent({
  name: "App",
  components: { JobList },
  setup() {

    const name = ref("Daniel");
    const age = ref<number|string>(25);

    const jobs = ref<Job[]>([
      { title: "Software Engineer", location: "Zurich", salary: 1500, id: 'id-1' },
      { title: "Quarryman", location: "Zurich", salary: 2500, id: 'id-2' },
      { title: "Flute player", location: "Zurich", salary: 32500, id: 'id-3' },
      { title: "prison guard", location: "Zurich", salary: 3700, id: 'id-4' },
      { title: "Fisherman", location: "Zurich", salary: 400, id: 'id-5' },
    ]);

    const order = ref<OrderTerm>('title');

    const handleClick = (term: OrderTerm) => {
      order.value = term;
    };

    return {
      name, age, jobs, order, handleClick
    };
  },

  methods: {
    changeName(name: string) {
      this.name = name;
    },

    changeAge(age: string|number) {
      this.age = age;
    }
  }
});
</script>

<style>
header {
  text-align: center;
}

header .order {
  margin-top: 20px;
}

button {
  margin: 0 10px;
  color: #1195c9;
  border: 3px solid #2295c9;
  background: #d5f0ff;
  padding: 8px 16px;
  border-radius: 4px;
  cursor: pointer;
  font-weight: bold;
}

</style>
