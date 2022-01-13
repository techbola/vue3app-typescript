<template>
  <div class="job-list">
    <p>Ordered by {{ order }}</p>
    <transition-group name="list" tag="ul">
      <li v-for="job in orderedJobs" :key="job.id">
        <h2>{{ job.title }} in {{ job.location }}</h2>
        <div class="salary">
          <p>&#8358; {{ job.salary.toLocaleString() }}</p>
        </div>
        <div class="description">
          <p>
            Lorem ipsum dolor sit amet consectetur adipisicing elit. Quia
            inventore, ipsa earum repellendus rem ipsum, non pariatur, magnam
            enim reprehenderit commodi dolor eius eveniet odio dolores iusto
            neque doloremque suscipit.
          </p>
        </div>
      </li>
    </transition-group>
  </div>
</template>

<script lang="ts">
import Job from "@/types/Job";
import OrderTerm from "@/types/OrderTerm";
import { computed, defineComponent, PropType } from "vue";

export default defineComponent({
  props: {
    jobs: {
      required: true,
      type: Array as PropType<Job[]>,
    },
    order: {
      required: true,
      type: String as PropType<OrderTerm>,
    },
  },
  setup(props) {
    const orderedJobs = computed(() => {
      return [...props.jobs].sort((a: Job, b: Job) => {
        return a[props.order] > b[props.order] ? 1 : -1;
      });
    });

    return { orderedJobs };
  },
});
</script>

<style lang="scss" scoped>
.job-list {
  max-width: 960px;
  margin: 40px auto;

  ul {
    padding: 0;
  }
  li {
    list-style-type: none;
    background: white;
    padding: 16px;
    margin: 16px 0;
    border-radius: 4px;
  }
  h2 {
    margin: 0 0 10px;
    text-transform: capitalize;
  }
}
.salary {
  display: flex;

  img {
    width: 30px;
  }
  p {
    color: #17bf66;
    font-weight: bold;
    margin: 10px 4px;
  }
}
.list-move {
  transition: all 1s;
}
</style>
