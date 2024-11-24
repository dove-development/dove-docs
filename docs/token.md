# Token
The DOVE token is the ownership unit of the Dove DAO, which exercises full control over the Dove protocol. It was launched on 24 November 2024.

## Supply
The initial supply of DOVE is 1,000,000. It follows a simple distribution:

- 33% to shareholders (team members and initial investors)
- 67% to the community, split at a DAO-set ratio among Vault and Savings rewards
<div style="max-width: 400px; margin: 0 auto;">
  <canvas id="doveAllocationChart"></canvas>
</div>

<script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
<script>
(function() {
    var ctx = document.getElementById('doveAllocationChart').getContext('2d');
    var data = [670000, 330000];
    var totalSum = data.reduce((a, b) => a + b, 0);
    var percentages = data.map(value => ((value / totalSum) * 100).toFixed(2));
    var doveAllocationChart = new Chart(ctx, {
        type: 'pie',
        data: {
            labels: ['Community', 'Shareholders'],
            datasets: [{
                data: data,
                backgroundColor: ['#36A2EB', '#4BC0C0'],
                borderWidth: 1
            }]
        },
        options: {
            responsive: true,
            devicePixelRatio: 2.5,
            plugins: {
                tooltip: {
                    callbacks: {
                        label: (context) => {
                                var label = context.label || '';
                                if (label) {
                                    label += ': ';
                                }
                                var value = context.raw;
                                var percentage = percentages[context.dataIndex];
                                label += value.toLocaleString() + ' (' + percentage + '%)';
                                return label;
                            }
                    }
                },
                legend: {
                    position: 'top',
                    labels: {
                        color: 'rgba(226, 228, 233, 0.82)'
                    }
                },
                title: {
                    display: true,
                    text: 'DOVE Allocation',
                    color: 'rgba(226, 228, 233, 0.82)'
                }
            }
        }
    });
})();
</script>

## Release Schedule
DOVE token distribution follows a linear vesting schedule over a 1-year period, with a 30-day warmup period. The release schedule is fixed at protocol creation and cannot be changed by governance.

- Launch (2024-11-24): The protocol is made live, with a circulating supply of 0 DOVE and an initial release rate of 0 DOVE/day.
- Warmup period (2024-11-24 to 2024-12-24): The release rate increases linearly.
- Linear vesting period (2024-12-24 to 2025-11-24): The release rate stabilizes at its maximum of 2,867.14 DOVE/day.
- Vesting completion (2025-11-24): Total circulation reaches 1,000,000 DOVE, and distribution ends.

<div style="max-width: 600px; margin: 0 auto;">
  <canvas id="doveSupplyChart"></canvas>
</div>
<script>
(function() {
    var ctx = document.getElementById('doveSupplyChart').getContext('2d');
    var currentDate = '2025-03-15';
    var l = 365, w = 30, s = 1000000, m = 2857.14285714285;
    var doveSupplyChart = new Chart(ctx, {
        type: 'line',
        data: {
            datasets: [{
                label: 'Total Supply',
                data: Array.from({length: 396}, function(_, i) {
                    var date = new Date(2024, 11, 24);
                    date.setDate(date.getDate() + i);
                    var x = i;
                    var y;
                    if (x < 0) {
                        y = 0;
                    } else if (x >= l) {
                        y = 1000000;
                    } else if (x < w) {
                        y = (m / (2 * w)) * Math.pow(x, 2);
                    } else {
                        y = (0.5 * w * m) + ((x - w) * m);
                    }
                    return {
                        x: date.toISOString().split('T')[0],
                        y: Math.round(y)
                    };
                }),
                fill: true,
                backgroundColor: 'rgba(54, 162, 235, 0.2)',
                borderColor: 'rgba(54, 162, 235, 1)',
                borderWidth: 1,
                pointRadius: 0
            }]
        },
        options: {
            responsive: true,
            devicePixelRatio: 2.5,
            scales: {
                x: {
                    type: 'category',
                    title: {
                        display: true,
                        text: 'Date',
                        color: 'rgba(226, 228, 233, 0.82)'
                    },
                    ticks: {
                        color: 'rgba(226, 228, 233, 0.82)',
                        maxTicksLimit: 4
                    }
                },
                y: {
                    title: {
                        display: true,
                        text: 'Total Supply',
                        color: 'rgba(226, 228, 233, 0.82)'
                    },
                    ticks: {
                        color: 'rgba(226, 228, 233, 0.82)'
                    },
                    beginAtZero: true
                }
            },
            plugins: {
                legend: {
                    display: false
                },
                title: {
                    display: true,
                    text: 'DOVE Supply',
                    color: 'rgba(226, 228, 233, 0.82)'
                },
                tooltip: {
                    mode: 'index',
                    intersect: false,
                },
                annotation: {
                    annotations: {
                        line1: {
                            type: 'line',
                            xMin: currentDate,
                            xMax: currentDate,
                            borderColor: 'red',
                            borderWidth: 2,
                        }
                    }
                }
            },
            hover: {
                mode: 'index',
                intersect: false
            }
        }
    });
})();
</script>

## Surplus Auction
The System Surplus is the total profit generated by the Dove protocol. It consists of the interest and liquidation fees collected from Vaults, minus the interest paid out to users who stake DVD in Savings.

When the System Surplus exceeds a Surplus Limit set by governance, the protocol initiates a Surplus Auction. During this process, the protocol uses the excess Surplus to buy back DOVE tokens from the open market and burn them to remove them from circulation.

The Surplus Auction provides deflationary pressure to the DOVE supply and rewards token holders for the success of the protocol.

## Deficit Auction
In rare circumstances, such as extreme market volatility, the Dove protocol may experience a high number of Vault liquidations where the liquidated collateral is insufficient to cover the Vaults' outstanding obligations to the protocol. This situation can result in a System Deficit. If the System Deficit surpasses a Deficit Limit set by governance, the protocol triggers a Deficit Auction.

During this auction, the protocol mints new DOVE tokens and sells them on the open market in exchange for DVD, which is then used to recapitalize the system and ensure the protocol remains solvent. Deficit Auctions are the only scenario in which the protocol will mint DOVE tokens beyond the initial supply allocation.

To date, the Dove protocol has never encountered a situation that required a Deficit Auction, but this mechanism exists as a safety net to guarantee the protocol's long-term stability and solvency.
