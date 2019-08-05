<template>
    <div class="v-w-calendar">
        <div class="v-w-calendar__wrapper">

            <div class="title__wrapper">
                <button class="pre btn"
                        @click="pre"
                        :disabled="showWeekNumber===0"><  前の週</button>

                <p class="current-week">{{currentMonth}}</p>

                <button class="next btn"
                        @click="next"
                        :disabled="showWeekNumber===(showWeek-1)">次の週  ></button>
            </div>

            <div class="week__wrapper">
                <div class="week-day" v-for="item in showCalendar">
                    <p class="text">{{item.dayOfWeek}}</p>
                    <p class="num">{{item.day}}</p>
                    <div v-if="!item.active" class="mark">ー</div>
                    <div v-else class="mark active"></div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    import CalendarService from '../Service/CalendarService'

    export default {
        name: 'weekly-calendar',

        data() {
            return {
                calendar: new CalendarService(),
                weekly: [],
                showWeekNumber: 0
            }
        },

        created() {
            this.weekly = this.calendar.getWeeklyMoment(this.showWeek)
        },

        computed: {
            showCalendar() {
                return this.weekly[this.showWeekNumber]
            },
            currentMonth() {
                return this.showCalendar[0].today
            }
        },

        props: {
            //表示する週
            showWeek: {
                type: Number,
                default: 10
            }
        },

        methods: {
            next() {
                this.showWeekNumber++
            },
            pre() {
                this.showWeekNumber--
            },
            getWeekly() {
                return this.weekly
            },

        }
    }
</script>

<style lang="scss">
    @import "../style/style.scss";

    .v-w-calendar {
        &__wrapper {
            .title__wrapper {
                display: flex;
                justify-content: space-between;
                align-items: center;

                .btn{
                    outline: 0;
                    box-shadow: none;
                }

                //前の週
                .pre {
                }

                .current-week {
                    margin-bottom: 0;
                }

                //次の週
                .next {
                }

            }
            //カレンダー部分
            .week__wrapper {
                display: flex;
                justify-content: space-between;
                align-items: center;
                padding-left: 24px;
                padding-right: 24px;
                margin-top: 24px;
                margin-bottom: 24px;

                .week-day {
                    .mark {
                        width: 20px;
                        height: 20px;
                        text-align: center;
                        color: #a7a39a;
                        background-color: unset;
                    }
                    .mark.active {
                        border: 2px solid red;
                        border-radius: 50%;
                    }
                }
            }
        }
    }

</style>