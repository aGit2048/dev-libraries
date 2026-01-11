<template>
    <div ref="chartDom" :style="style"></div>
</template>

<script setup lang="ts">
    import { ref, onMounted, computed } from "vue";
    import * as echarts from "echarts"

    const chartDom = ref()

    onMounted(()=>{
        initChart()
    })
    const style =  computed(()=>({
        width: props.width,
        height: props.height
    }))

    const props = defineProps({
        width: {
            type: String,
            default: "100%"
        },
        height: {
            type: String,
            default: "100%"
        },
        option: {
            type: Object,
            default: ()=> ({
                    xAxis: {
                        type: 'category',
                        data: ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun']
                    },
                    yAxis: {
                        type: 'value'
                    },
                    series: [
                        {
                            data: [150, 230, 224, 218, 135, 147, 260],
                            type: 'line'
                        }
                    ]
            })
        }
    })
    function initChart() {
        var chart = echarts.init(chartDom.value)
        chart.setOption(props.option);
        window.addEventListener("resize", ()=>{
            chart.resize();
        })
    }

</script>