<template>
    <v-badges
        class="mx-0 mt-12"
        :badges="badges"
    />
    <v-badges
        class="mx-0 mt-4"
        :badges="[
            { name: 'tag' },
            { name: 'offline' },
            { name: 'online' },
            { name: 'new' },
            { name: 'project' },
            { name: 'old' },
            { name: 'course' },
            { name: 'card' },
            { name: 'module' },
        ]"
    />
    <v-badges
        class="mx-0 mt-4"
        :badges="[
            { name: 'project' },
            { name: 'old' },
            { name: 'online' },
            { name: 'new' },
            { name: 'card' },
            { name: 'tag' },
            { name: 'module' },
            { name: 'course' },
            { name: 'offline' },
        ]"
    />
</template>

<script>
import VBadges from "@/components/VBadges.vue"

export default {
    name: 'App',
    components: {
        VBadges,
    },
    data: () => ({
        badges: [
            { name: 'new' },
            { name: 'online' },
            { name: 'tag' },
            { name: 'offline' },
            { name: 'old' },
            { name: 'card' },
            { name: 'course' },
            { name: 'module' },
            { name: 'project' }
        ]
    }),
}

</script>

<style>
body {
    background-color: rgb(38, 38, 38);
}
</style>
  