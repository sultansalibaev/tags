<template>
    <div
        class="badges"
        :class="{
            'flex-wrap': outsideTagIndex === undefined
        }"
        ref="badges"
    >
        <span
            v-for="(badge, i) in badges"
            :key="i"
            class="badge"
            :class="{
                'hidden-badge': i >= outsideTagIndex && outsideTagIndex != null
            }"
        >{{ badge?.name }}</span>
        <span
            class="badge cursor-pointer hide-badge-btn"
            :class="{
                'hidden-badge': outsideTagIndex === null,
            }"
            @click="toggleMore"
        >
            <template v-if="outsideTagIndex === undefined">hide</template>
            <template v-else>{{ `+ ${hiddenBadgesCount} tag` }}</template>
        </span>
    </div>
</template>

<script>

export default {
    name: 'v-badges',
    props: {
        badges: {
            type: Array,
            required: true,
        },
    },
    data: () => ({
        outsideTagIndex: null,
    }),
    methods: {
        toggleMore() {
            this.outsideTagIndex = this.outsideTagIndex === undefined ? null : undefined;

            if (this.outsideTagIndex === null) this.updateOverflowBadge();
        },
        getContainerGap() {
            return Number(
                window.getComputedStyle(
                    this.$refs.badges
                )?.gap?.replace(/\D/g, '')
            );
        },
        updateOverflowBadge() {
            if (this.outsideTagIndex === undefined) return;

            const container = this.$refs.badges;
            const badges = container.children;

            const containerWidth = container.clientWidth;
            const gap = this.getContainerGap() | 8;
            const overflowBadgeWidth = badges[badges.length - 1].offsetWidth;

            let totalWidth = 0;

            for (let i = 0; i < badges.length - 1; i++) {
                const badge = badges?.[i];
                if (totalWidth + badge.offsetWidth + gap + overflowBadgeWidth < containerWidth) {
                    totalWidth += badge.offsetWidth + gap;
                } else {
                    this.outsideTagIndex = i;
                    return;
                }
            }

            this.outsideTagIndex = null;
        },
    },
    computed: {
        hiddenBadgesCount() {
            return this.badges?.length - this.outsideTagIndex;
        }
    },
    mounted() {
        this.updateOverflowBadge()
        window.addEventListener('resize', this.updateOverflowBadge);
    },
    beforeUnmount() {
        window.removeEventListener('resize', this.updateOverflowBadge);
    },
}

</script>

<style>
.badges {
    @apply flex m-5 gap-2 truncate relative;
}
.badge {
    @apply py-1 px-2.5 rounded-xl bg-slate-600 text-white;
}
.hidden-badge {
    @apply absolute !opacity-0 pointer-events-none;
}
.hide-badge-btn:not(:hover) {
    @apply opacity-60;
}
.hide-badge-btn:not(.hidden-badge) {
    @apply transition-opacity;
}

</style>
  