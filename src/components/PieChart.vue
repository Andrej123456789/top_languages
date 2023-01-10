<template>
    <Pie id="my-chart-id" :options="chartOptions" :data="chartData"></Pie>
</template>

<script lang="ts">
import { Pie } from 'vue-chartjs'

import {
    Chart as ChartJS,
    Title,
    Tooltip,
    Legend,
    ArcElement,
    CategoryScale,
} from 'chart.js'

ChartJS.register(Title, Tooltip, Legend, ArcElement, CategoryScale)

/* ----------------------------------- */

function CalculatePercentage(num: number) {
    const number_of_repos = 17;

    return (num / number_of_repos) * 100;
}

var languages = new Map<String, [number, String]>();

languages.set("VB.NET", [CalculatePercentage(1), "#945db7"]);
languages.set("Python", [CalculatePercentage(1), "#3572a5"]);
languages.set("HTML", [CalculatePercentage(2), "#e34c26"]);
languages.set("Java", [CalculatePercentage(1), "#b07219"]);
languages.set("Rust", [CalculatePercentage(3), "#dea584"]);
languages.set("Assembly", [CalculatePercentage(1), "#6e4c13"]);
languages.set("C++", [CalculatePercentage(1), "#f34b7d"]);
languages.set("C", [CalculatePercentage(2), "#555555"]);
languages.set("Dart", [CalculatePercentage(2), "#00b4ab"]);
languages.set("Vue", [CalculatePercentage(1), "#41b883"]);
languages.set("Without language", [CalculatePercentage(1), "gray"])

const mapArray = Array.from(languages);
mapArray.sort((a, b) => b[1][0] - a[1][0]);
const sortedMap = new Map(mapArray);

const firstStrings = Array.from(sortedMap.entries()).map(
    ([key, _value]) => key
);
const numbers = Array.from(sortedMap.entries()).map(
    ([_key, value]) => value[0]
);
const secondStrings = Array.from(sortedMap.entries()).map(
    ([_key, value]) => value[1]
);

let numbers_two = [];

for (let index = 0; index < numbers.length; index++) {
    const element = numbers[index];

    numbers_two.push((Math.round(element * 100) / 100).toString() + "%");
}

/* ----------------------------------- */

export default {
    name: 'PieChart',
    components: { Pie },
    data() {
        return {
            chartData: {
                labels: firstStrings,
                datasets: [
                    {
                        data: numbers,
                        backgroundColor: secondStrings,
                    },
                ],
            },
            chartOptions: {
                responsive: true,
                tooltips: {
                    callbacks: {
                        label: function (tooltipItems: any, data: any) {
                            return (
                                data.labels[tooltipItems.index] +
                                " : " +
                                (
                                    Math.round(
                                        data.datasets[tooltipItems.datasetIndex].data[
                                        tooltipItems.index
                                        ] * 100
                                    ) / 100
                                ).toString() +
                                " %"
                            );
                        },
                    },
                },
            }
        }
    }
}
</script>
