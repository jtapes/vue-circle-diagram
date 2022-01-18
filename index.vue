<template>
    <div class="circle">
        <div
            v-for="item in circle(items)"
            :key="JSON.stringify(item)"
            :style="{
              backgroundColor: item.color, 
              transform: `rotate(${item.rotate}deg) skewY(${item.skewY}deg)}`
            }"
            class="sector"></div>
    </div>
</template>

<script>
    export default {
        name: "VCircle",
        props: {
            items: {
                type: Array,
                required: true
            }
        },

        methods: {
            circle(items) {
                const sectorDeg = 3.6
                let rotateSum = 0
                let result = []
                items.map(el => {
                    for(let i = el.progress; i > 0; i = i - 25) {
                        const percent = i >= 25 ? 25 : i
                        result.push({rotate: rotateSum * sectorDeg, skewY: 90 + (sectorDeg * percent), color: el.color})
                        rotateSum += percent
                    }
                })
                return result
            }
        }
    }
</script>

<style lang="scss" scoped>
    .circle {
        width: 300px;
        height: 300px;
        overflow: hidden;
        border-radius: 50%;
        position: relative;

        &:after {
            content: '';
            position: absolute;
            width: 80%;
            height: 80%;
            background: #fff;
            border-radius: 50%;
            top: 50%;
            left: 50%;
            transform: translateY(-50%) translateX(-50%);
        }
    }

    .sector {
        width: 50%;
        height: 50%;
        position: absolute;
        left: 50%;
        top: 0;
        transform-origin: left bottom;
    }
</style>
