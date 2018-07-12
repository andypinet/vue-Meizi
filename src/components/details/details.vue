<template>
    <transition name="fade">
        <div v-show="showFlag" class="details">
            <div
            >
                <header class="header">
                    <header class="bar bar-nav" @click="hide">
                        <div class="pull-left">
                            <span class="iconfont icon-left"></span>
                        </div>
                        <div class="title">{{detailsData.publishedAt || time | formatDate}}</div>
                    </header>
                </header>
                <v-scroll-view          
                    ref="content">
                    <v-day :data="detailsData" ref="day"></v-day>
                </v-scroll-view>
            </div>
        </div>
    </transition>
</template>
<script>
    import { formatDate } from '../../common/js/date';
    import BScroll from 'better-scroll';
    import vScrollView from '../scroll-view/scroll-view';
    import vDay from '../day/day.vue';
    export default {
        name: 'v-details',
        props: {
            time: {
                type: String
            },
            detailsData: {
                type: Object
            }
        },
        data() {
            return {
                showFlag: false
            };
        },
        created() {
        },
        methods: {
            show() {
                this.showFlag = true;
                setTimeout(() => {
                    if (!this.scroll) {
                        this.scroll = new BScroll(this.$refs.content.$el, {
                            click: true
                        });
                    } else {
                        this.scroll.refresh();
                    }
                    this.scroll.scrollTo(0, 0);
                    this.$refs.day.clearStyle();
                }, 0);
            },
            hide() {
                this.showFlag = false;
            }
        },
        filters: {
            formatDate(time) {
                let date = new Date(time);
                return formatDate(date, 'yyyy-MM-dd');
            }
        },
        components: {
            vDay,
            vScrollView
        }
    };
</script>


<style lang="stylus" rel="stylesheet/stylus">
    @import './details.styl';      
</style>