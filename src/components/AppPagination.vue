<template>
<div>
    <ul class="pagination js-pagination">
        <li class="pagination__item js-page" v-for="(pageNum, key) in pages" :key="key">
            <a href="#" class="pagination__link js-page-number" @click.prevent="paginate(pageNum)">{{ pageNum }}</a>
        </li>
    </ul>
</div>
</template>

<script>
export default {
    name: 'AppPagination',
    model: {
        prop: 'page',
        event: 'paginate',
    },
    props: ['page', 'count', 'perPage'],
    computed: {
        pages() {
            return Math.ceil(this.count / this.perPage);
        },  
    },
    methods: {
        paginate(page) {
            this.$emit('paginate', page);
        },
    },
}
</script>