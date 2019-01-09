<template>
    <div>
        <ul :class="containerClassProp">
            <li @click="handler(currentPage-1)" :class="prevButtonClassProp" v-if="prevPageUrl">
                <a href="javascript:void(0)" :class="numberClassProp">{{prevButtonTextProp}}</a></li>
            <li v-for="(number,i) in (numbers)" @click="handler(number==='...' ? i+1 : number)"
                :class="{[numberButtonClassProp]:true,[activeClassProp]:isCurrent(number)}">
                <a href="javascript:void(0)" :class="numberClassProp">{{number}}</a>
            </li>
            <li @click="handler(currentPage+1)" :class="nextButtonClassProp" v-if="nextPageUrl">
                <a href="javascript:void(0)" :class="numberClassProp">{{nextButtonTextProp}}</a></li>
        </ul>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                prevPageUrl: null,
                nextPageUrl: null,
                currentPage: 1,
                numbers: []
            }
        },
        props: {
            data: {
                required: true
            },
            containerClass: {
                default: 'pagination'
            },
            prevButtonClass: {
                default: 'page-item'
            },
            prevButtonText: {
                default: 'Prev'
            },
            nextButtonClass: {
                default: 'page-item'
            },
            nextButtonText: {
                default: 'Next'
            },
            numberButtonClass: {
                default: 'page-item'
            },
            numberClass: {
                default: 'page-link'
            },
            activeClass: {
                default: 'active'
            },
            numbersCountForShow: {
                default: 2
            },
            changePage: {
                required:true
            },
            options: {}
        },
        computed: {
            containerClassProp: function () {
                if (this.options && this.options.containerClass) {
                    return this.options.containerClass;
                }
                return this.containerClass;
            },
            prevButtonClassProp: function () {
                if (this.options && this.options.prevButtonClass) {
                    return this.options.prevButtonClass;
                }
                return this.prevButtonClass;
            },
            prevButtonTextProp: function () {
                if (this.options && this.options.prevButtonText) {
                    return this.options.prevButtonText;
                }
                return this.prevButtonText;
            },
            nextButtonClassProp: function () {
                if (this.options && this.options.nextButtonClass) {
                    return this.options.nextButtonClass;
                }
                return this.nextButtonClass;
            },
            nextButtonTextProp: function () {
                if (this.options && this.options.nextButtonText) {
                    return this.options.nextButtonText;
                }
                return this.nextButtonText;
            },
            numberButtonClassProp: function () {
                if (this.options && this.options.numberButtonClass) {
                    return this.options.numberButtonClass;
                }
                return this.numberButtonClass;
            },
            numberClassProp: function () {
                if (this.options && this.options.numberClass) {
                    return this.options.numberClass;
                }
                return this.numberClass;
            },
            numbersCountForShowProp: function () {
                if (this.options && this.options.numbersCountForShow) {
                    return this.options.numbersCountForShow;
                }
                return this.numbersCountForShow;
            },
            activeClassProp: function () {
                if (this.options && this.options.activeClass) {
                    return this.options.activeClass;
                }
                return this.activeClass;
            }
        },
        watch: {
            data: {
                deep: true,
                handler() {
                    console.log(this.numbersCountForShowProp);
                    let current = this.data.current_page,
                        last = this.data.last_page,
                        delta = parseInt(this.numbersCountForShowProp),
                        left = current - delta,
                        right = current + delta + 1,
                        range = [],
                        rangeWithDots = [],
                        l;
                    for (let i = 1; i <= last; i++) {
                        if (i == 1 || i == last || i >= left && i < right) {
                            range.push(i);
                        }
                    }
                    for (let i of range) {
                        if (l) {
                            if (i - l === 2) {
                                rangeWithDots.push(l + 1);
                            } else if (i - l !== 1) {
                                rangeWithDots.push('...');
                            }
                        }
                        rangeWithDots.push(i);
                        l = i;
                    }
                    this.numbers = rangeWithDots;
                    this.currentPage = this.data.current_page;
                    this.nextPageUrl = this.data.next_page_url;
                    this.prevPageUrl = this.data.prev_page_url;
                }
            },
        },
        methods: {
            handler(page) {
                console.log(page);
                this.changePage(page);
            },
            isCurrent(page) {
                if (this.currentPage === page) {
                    return true;
                }
                return false;
            }
        }
    }
</script>
