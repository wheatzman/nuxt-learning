<template>
    <div>
        <p class="mb-10">
            Take a look at my github projects
        </p>
        <section v-if="pending">Loading ...</section>
        <section v-else-if="error">Something went wrong... please try again</section>
        <section v-else>
            <ul class="grid grid-cols-1 gap-4">
                <li v-for="project in projects" :key="project.id" class="border border-gray- 200 rounded-sm p-4 hover:bg-gray-100 font-mono">
                    <a :href="project.html_url" target="_blank">
                        <div class="flex items-center justify-between text-sm">
                            <div class="font-semibold">
                                {{ project.name }}
                            </div>
                            <div>
                                {{ project.stargazers_count }} ★
                            </div>
                        </div>
                        <p class="text-sm">
                            {{ project.description }}
                        </p>
                    </a>
                </li>
            </ul>
        </section>
    </div>
</template>

<script setup>
const {error, pending, data} = await useFetch('https://api.github.com/users/wheatzman/repos');

const projects = computed(
    () => data.value.filter(project => project.description)
        .sort((a, b) => b.stargazers_count - a.stargazers_count)
);
</script>