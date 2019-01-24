<template>
    <div>
        <p>{{ response }}</p>

        <canvas id="myChart"></canvas>

    </div>
</template>


<script>

    import Chart from 'chart.js';

    export default{
        data () {
            return {
                response: [],
                error: [],
                index: []
            }
        },
        mounted() {
            this.$http.get('http://35.234.145.51/hello').then(response => {
                this.response = response.data.input;
                for(let a = 0; a < this.response.length; a++){
                    this.index.push(a);
                }


                var ctx = document.getElementById("myChart").getContext('2d');
                new Chart(ctx, {
                    type: 'line',
                    data: {
                        labels: this.index,
                        datasets: [{
                            label: 'Values',
                            data: this.response,
                            backgroundColor: [
                                'rgba(255, 99, 132, 0.2)',
                                'rgba(54, 162, 235, 0.2)',
                                'rgba(255, 206, 86, 0.2)',
                                'rgba(75, 192, 192, 0.2)',
                                'rgba(153, 102, 255, 0.2)',
                                'rgba(255, 159, 64, 0.2)'
                            ],
                            borderColor: [
                                'rgba(255,99,132,1)',
                                'rgba(54, 162, 235, 1)',
                                'rgba(255, 206, 86, 1)',
                                'rgba(75, 192, 192, 1)',
                                'rgba(153, 102, 255, 1)',
                                'rgba(255, 159, 64, 1)'
                            ],
                            borderWidth: 1
                        }]
                    },
                    options: {
                        scales: {
                            yAxes: [{
                                ticks: {
                                    beginAtZero: true
                                }
                            }]
                        }
                    }
                });
            });
        }
    }
</script>

<style scoped>
    canvas{
        height: 10%;
        width: 10%;
    }
</style>