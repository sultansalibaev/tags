<template>
    <div class="badges">
        <span
            v-for="i in 15"
            :key="i"
            class="badge"
        >{{ i }}</span>
        <span
            class="badge"
        ></span>
    </div>


</template>

<script>

export default {
    name: 'App',
    // methods: {
    //     updateOverflowBadge() {
    //         const container = document.getElementById('badge-container');
    //         const badges = Array.from(container.getElementsByClassName('badge'));
    //         let totalWidth = 0;
    //         let hiddenCount = 0;
    //         const containerWidth = container.clientWidth;
    //         const overflowBadge = badges[badges.length - 1]; // Предполагается, что overflow-badge - последний в списке
    //         overflowBadge.style.display = 'none'; // Скрываем для измерения

    //         // Предварительно измеряем ширину overflow-badge
    //         overflowBadge.style.display = 'inline-block';
    //         const overflowBadgeWidth = overflowBadge.offsetWidth;
    //         overflowBadge.style.display = 'none'; // Скрываем снова

    //         badges.forEach((badge, index) => {
    //             if (index !== badges.length - 1) { // Игнорируем overflow-badge в расчёте
    //                 totalWidth += badge.offsetWidth + 5; // Добавляем margin-right
    //                 if (totalWidth + overflowBadgeWidth > containerWidth) {
    //                     hiddenCount++;
    //                     badge.style.display = 'none';
    //                 } else {
    //                     badge.style.display = 'inline-block';
    //                 }
    //             }
    //         });

    //         if (hiddenCount > 0) {
    //             overflowBadge.textContent = `+${hiddenCount}`;
    //             overflowBadge.style.display = 'inline-block';
    //         } else {
    //             overflowBadge.style.display = 'none';
    //         }
    //     },
    // },
    // mounted() {
    //     function updateOverflowBadge() {
    //         const container = document.getElementById('badge-container');
    //         const badges = Array.from(container.getElementsByClassName('badge'));
    //         let totalWidth = 0;
    //         let overflowWidth = 0;
    //         let hiddenCount = 0;
    //         const containerWidth = container.clientWidth;
    //         const overflowBadge = badges[badges.length - 1]; // Предполагается, что overflow-badge - последний в списке
    //         overflowBadge.style.display = 'none'; // Скрываем overflow-badge для корректного расчёта ширины

    //         badges.forEach((badge, index) => {
    //             if (index !== badges.length - 1) { // Игнорируем overflow-badge в расчёте
    //                 totalWidth += badge.offsetWidth + 5; // Добавляем margin-right, если он есть
    //                 if (totalWidth > containerWidth) {
    //                     hiddenCount++;
    //                     badge.style.display = 'none';
    //                     overflowWidth += badge.offsetWidth + 5; // Учитываем скрытые теги
    //                 } else {
    //                     badge.style.display = 'inline-block';
    //                 }
    //             }
    //         });

    //         if (hiddenCount > 0) {
    //             overflowBadge.textContent = `+${hiddenCount}`;
    //             overflowBadge.style.display = 'inline-block';
    //             // Устанавливаем ширину overflow-badge если контейнер не может вместить все теги
    //             if (totalWidth + overflowBadge.offsetWidth > containerWidth) {
    //             overflowBadge.style.width = `${containerWidth - (totalWidth - overflowWidth)}px`;
    //             } else {
    //             overflowBadge.style.width = 'auto';
    //             }
    //         }
    //     }

    //     // Run on initial load and on window resize
    //     window.addEventListener('load', updateOverflowBadge);
    //     window.addEventListener('resize', updateOverflowBadge);
    // },
    mounted() {
        /*

        function updateOverflowBadge() {
            const container = document.getElementById('badge-container');
            const badges = Array.from(container.getElementsByClassName('badge'));
            let totalWidth = 0;
            let hiddenCount = 0;
            const containerWidth = container.clientWidth;
            const overflowBadge = badges[badges.length - 1]; // Предполагается, что overflow-badge - последний в списке
            overflowBadge.style.display = 'none'; // Скрываем для измерения

            // Предварительно измеряем ширину overflow-badge
            overflowBadge.style.display = 'inline-block';
            const overflowBadgeWidth = overflowBadge.offsetWidth;
            overflowBadge.style.display = 'none'; // Скрываем снова

            badges.forEach((badge, index) => {
                if (index !== badges.length - 1) { // Игнорируем overflow-badge в расчёте
                    totalWidth += badge.offsetWidth + 5; // Добавляем margin-right
                    if (totalWidth + overflowBadgeWidth > containerWidth) {
                        hiddenCount++;
                        badge.style.display = 'none';
                    } else {
                        badge.style.display = 'inline-block';
                    }
                }
            });

            if (hiddenCount > 0) {
                overflowBadge.textContent = `+${hiddenCount}`;
                overflowBadge.style.display = 'inline-block';
            } else {
                overflowBadge.style.display = 'none';
            }
        }

        // Run on initial load and on window resize
        window.addEventListener('load', updateOverflowBadge);
        window.addEventListener('resize', updateOverflowBadge);

        */

        function updateOverflowBadge() {
            const container = document.querySelector('.badges');
            const badges = Array.from(container.querySelectorAll('.badge'));
            let totalWidth = 0;
            let hiddenCount = 0;
            const overflowBadge = badges[badges.length - 1];
            overflowBadge.textContent = `+${hiddenCount}`;
            overflowBadge.style.display = 'inline-block';
            const overflowBadgeWidth = overflowBadge.offsetWidth; 
            overflowBadge.style.position = 'absolute';
            overflowBadge.style.pointerEvents = 'none';
            overflowBadge.style.opacity = '0';

            const containerWidth = container.clientWidth;

            const gap = 8;
            badges.slice(0, -1).forEach((badge) => {
                if (totalWidth + badge.offsetWidth + (gap * 2) + overflowBadgeWidth < containerWidth) {
                    totalWidth += badge.offsetWidth + gap;
                    // badge.style.display = 'inline-block';
                    badge.style.position = 'static';
                    badge.style.pointerEvents = 'default';
                    badge.style.opacity = '1';
                } else {
                    badge.style.position = 'absolute';
                    badge.style.pointerEvents = 'none';
                    badge.style.opacity = '0';
                    hiddenCount++;
                    
                    overflowBadge.textContent = `+${hiddenCount}`;
                    overflowBadge.style.position = 'static';
                    overflowBadge.style.pointerEvents = 'default';
                    overflowBadge.style.opacity = '1';
                }
            });
        }

        window.addEventListener('load', updateOverflowBadge);
        window.addEventListener('resize', updateOverflowBadge);




        /*

        function updateOverflowBadge() {
            const container = document.getElementById('badge-container');
            const badges = Array.from(container.getElementsByClassName('badge'));
            let totalWidth = 0;
            let hiddenCount = 0;
            const overflowBadge = badges[badges.length - 1]; // Предполагается, что overflow-badge - последний в списке
            overflowBadge.style.display = 'inline-block'; // Показываем, чтобы замерить ширину
            const overflowBadgeWidth = overflowBadge.offsetWidth; // Ширина элемента overflow-badge
            overflowBadge.style.display = 'none'; // Скрываем обратно, чтобы не мешал вычислениям

            const containerWidth = container.clientWidth;
            let indexLastVisibleBadge = 0; // Индекс последнего видимого тега

            badges.slice(0, -1).forEach((badge, index) => {
                const margin = 5; // Предполагаемый margin-right у тегов
                if (totalWidth + badge.offsetWidth + margin + overflowBadgeWidth <= containerWidth) {
                    totalWidth += badge.offsetWidth + margin;
                    badge.style.display = 'inline-block';
                    indexLastVisibleBadge = index; // Обновляем индекс последнего видимого тега
                } else {
                    hiddenCount++;
                }
            });

            if (hiddenCount > 0) {
                // Скрываем все теги после последнего видимого
                badges.slice(indexLastVisibleBadge + 1, -1).forEach(badge => {
                badge.style.display = 'none';
                });
                // Обновляем текст overflow-badge и показываем его
                overflowBadge.textContent = `+${hiddenCount}`;
                overflowBadge.style.display = 'inline-block';
            } else {
                overflowBadge.style.display = 'none';
            }
        }

        // Запуск при загрузке и изменении размера окна
        window.addEventListener('load', updateOverflowBadge);
        window.addEventListener('resize', updateOverflowBadge);

        */
    },
}

</script>

<style>
body {
    background-color: rgb(38, 38, 38);
}
.badges {
    @apply flex m-5 gap-2 truncate;
}
.badge {
    @apply py-1 px-2.5 rounded-xl bg-slate-600 text-white;
}
</style>
  