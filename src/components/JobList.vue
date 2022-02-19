<template>
    <div class="job-list">
        <p> Ordered by: {{ order }}</p>
        <transition-group name="jobs-liist" tag="ul">
            <li v-for="job in orderedJobs" :key="job.id">
                <h2>{{ job.title }} in {{ job.location }}</h2>
                <div class="salary">
                    <p>$ {{ job.salary }}</p>
                </div>

                <div class="description">
                    <p class="">
                        Lorem ipsum dolor sit amet consectetur, adipisicing elit. Provident 
                        voluptate ea atque deleniti rerum a necessitatibus corrupti quas nemo 
                        consectetur eveniet delectus illum explicabo quo dicta possimus quaerat, 
                        nesciunt distinctio!
                    </p>
                </div>
            </li>
        </transition-group>
    </div>
</template>

<script lang="ts">

import type Job from '@/types/Job';
import type OrderTerm from '@/types/OrderTerm';
import { computed, defineComponent, reactive, toRefs, type PropType } from 'vue';

export default defineComponent({
    name: "JobList",
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
    setup (props) {

        const orderedJobs = computed( () => {
            return [...props.jobs].sort( (a: Job, b: Job) => {
                return a[props.order] > b[props.order] ? 1 : -1;
            });
        });

        return { orderedJobs }
    }
});
</script>

<style scoped>
.job-list {
    max-width: 960px;
    margin: 40px auto;
}

.job-list ul {
    padding: 0;
}

.job-list li {
    list-style-type: none;
    background: white;
    padding: 16px;
    margin: 16px 0;
    border-radius: 4px;
}

.job-list h2 {
    margin: 0 0 10px;
    text-transform: capitalize;
}

.salary {
    display: flex;
    color: blueviolet;
    font-weight: 700;
}

.jobs-liist-move {
    transition: all 400ms;
}
</style>