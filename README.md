<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Stack Overflow Survey 2023 - Data Visualizations</title>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/Chart.js/3.9.1/chart.min.js"></script>
    <style>
        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            margin: 0;
            padding: 20px;
            min-height: 100vh;
        }
        
        .container {
            max-width: 1200px;
            margin: 0 auto;
            background: rgba(255, 255, 255, 0.95);
            backdrop-filter: blur(10px);
            border-radius: 20px;
            padding: 30px;
            box-shadow: 0 20px 40px rgba(0, 0, 0, 0.1);
        }
        
        h1 {
            text-align: center;
            color: #2c3e50;
            margin-bottom: 40px;
            font-size: 2.5em;
            font-weight: 300;
        }
        
        .chart-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(500px, 1fr));
            gap: 30px;
            margin-bottom: 30px;
        }
        
        .chart-container {
            background: white;
            border-radius: 15px;
            padding: 25px;
            box-shadow: 0 10px 25px rgba(0, 0, 0, 0.08);
            border: 1px solid rgba(0, 0, 0, 0.05);
            transition: transform 0.3s ease, box-shadow 0.3s ease;
        }
        
        .chart-container:hover {
            transform: translateY(-5px);
            box-shadow: 0 15px 35px rgba(0, 0, 0, 0.12);
        }
        
        .chart-title {
            font-size: 1.4em;
            font-weight: 600;
            color: #34495e;
            margin-bottom: 20px;
            text-align: center;
            border-bottom: 2px solid #ecf0f1;
            padding-bottom: 10px;
        }
        
        .chart-wrapper {
            position: relative;
            height: 350px;
        }
        
        .full-width {
            grid-column: 1 / -1;
        }
        
        .full-width .chart-wrapper {
            height: 400px;
        }
        
        .stats-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 20px;
            margin: 30px 0;
        }
        
        .stat-card {
            background: linear-gradient(135deg, #3498db, #2980b9);
            color: white;
            padding: 25px;
            border-radius: 15px;
            text-align: center;
            box-shadow: 0 8px 20px rgba(52, 152, 219, 0.3);
        }
        
        .stat-number {
            font-size: 2.5em;
            font-weight: bold;
            margin-bottom: 10px;
        }
        
        .stat-label {
            font-size: 1.1em;
            opacity: 0.9;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Stack Overflow 2023 Developer Survey - Key Insights</h1>
        
        <div class="stats-grid">
            <div class="stat-card">
                <div class="stat-number">71%</div>
                <div class="stat-label">Contribute to Open Source</div>
            </div>
            <div class="stat-card">
                <div class="stat-number">85%</div>
                <div class="stat-label">Prefer Remote/Hybrid Work</div>
            </div>
            <div class="stat-card">
                <div class="stat-number">$97K</div>
                <div class="stat-label">Global Average Salary</div>
            </div>
            <div class="stat-card">
                <div class="stat-number">4.2/5</div>
                <div class="stat-label">Job Satisfaction Score</div>
            </div>
        </div>
        
        <div class="chart-grid">
            <div class="chart-container">
                <div class="chart-title">Programming Languages - Current vs Desired</div>
                <div class="chart-wrapper">
                    <canvas id="languageChart"></canvas>
                </div>
            </div>
            
            <div class="chart-container">
                <div class="chart-title">Work Location Preferences by Experience</div>
                <div class="chart-wrapper">
                    <canvas id="workLocationChart"></canvas>
                </div>
            </div>
            
            <div class="chart-container full-width">
                <div class="chart-title">Developer Salary Distribution by Region</div>
                <div class="chart-wrapper">
                    <canvas id="salaryChart"></canvas>
                </div>
            </div>
            
            <div class="chart-container">
                <div class="chart-title">Job Satisfaction by Country</div>
                <div class="chart-wrapper">
                    <canvas id="satisfactionChart"></canvas>
                </div>
            </div>
            
            <div class="chart-container">
                <div class="chart-title">Operating System Preferences</div>
                <div class="chart-wrapper">
                    <canvas id="osChart"></canvas>
                </div>
            </div>
        </div>
    </div>

    <script>
        // Chart configurations with modern styling
        const chartDefaults = {
            responsive: true,
            maintainAspectRatio: false,
            plugins: {
                legend: {
                    position: 'top',
                    labels: {
                        usePointStyle: true,
                        padding: 20,
                        font: {
                            size: 12
                        }
                    }
                }
            }
        };

        // Programming Languages Chart
        const languageCtx = document.getElementById('languageChart').getContext('2d');
        new Chart(languageCtx, {
            type: 'bar',
            data: {
                labels: ['JavaScript', 'Python', 'TypeScript', 'Java', 'C#', 'Rust', 'Go'],
                datasets: [{
                    label: 'Currently Using (%)',
                    data: [65, 49, 39, 33, 28, 13, 14],
                    backgroundColor: 'rgba(52, 152, 219, 0.8)',
                    borderColor: 'rgba(52, 152, 219, 1)',
                    borderWidth: 2
                }, {
                    label: 'Want to Learn (%)',
                    data: [25, 35, 42, 15, 18, 67, 61],
                    backgroundColor: 'rgba(231, 76, 60, 0.8)',
                    borderColor: 'rgba(231, 76, 60, 1)',
                    borderWidth: 2
                }]
            },
            options: {
                ...chartDefaults,
                scales: {
                    y: {
                        beginAtZero: true,
                        max: 70,
                        grid: {
                            color: 'rgba(0, 0, 0, 0.05)'
                        }
                    },
                    x: {
                        grid: {
                            display: false
                        }
                    }
                }
            }
        });

        // Work Location Chart
        const workLocationCtx = document.getElementById('workLocationChart').getContext('2d');
        new Chart(workLocationCtx, {
            type: 'doughnut',
            data: {
                labels: ['Remote', 'Hybrid', 'On-site'],
                datasets: [{
                    data: [42, 43, 15],
                    backgroundColor: [
                        'rgba(46, 204, 113, 0.8)',
                        'rgba(155, 89, 182, 0.8)',
                        'rgba(241, 196, 15, 0.8)'
                    ],
                    borderColor: [
                        'rgba(46, 204, 113, 1)',
                        'rgba(155, 89, 182, 1)',
                        'rgba(241, 196, 15, 1)'
                    ],
                    borderWidth: 3
                }]
            },
            options: {
                ...chartDefaults,
                cutout: '60%'
            }
        });

        // Salary Distribution Chart
        const salaryCtx = document.getElementById('salaryChart').getContext('2d');
        new Chart(salaryCtx, {
            type: 'line',
            data: {
                labels: ['North America', 'Western Europe', 'Eastern Europe', 'Asia Pacific', 'Latin America', 'Africa', 'Middle East'],
                datasets: [{
                    label: 'Average Salary (USD)',
                    data: [125000, 95000, 45000, 65000, 35000, 28000, 52000],
                    borderColor: 'rgba(52, 152, 219, 1)',
                    backgroundColor: 'rgba(52, 152, 219, 0.1)',
                    borderWidth: 3,
                    fill: true,
                    tension: 0.4,
                    pointBackgroundColor: 'rgba(52, 152, 219, 1)',
                    pointBorderColor: '#fff',
                    pointBorderWidth: 2,
                    pointRadius: 6
                }]
            },
            options: {
                ...chartDefaults,
                scales: {
                    y: {
                        beginAtZero: true,
                        grid: {
                            color: 'rgba(0, 0, 0, 0.05)'
                        },
                        ticks: {
                            callback: function(value) {
                                return '$' + value.toLocaleString();
                            }
                        }
                    },
                    x: {
                        grid: {
                            display: false
                        }
                    }
                }
            }
        });

        // Job Satisfaction Chart
        const satisfactionCtx = document.getElementById('satisfactionChart').getContext('2d');
        new Chart(satisfactionCtx, {
            type: 'radar',
            data: {
                labels: ['Work-Life Balance', 'Compensation', 'Learning Opportunities', 'Team Culture', 'Career Growth', 'Technology Stack'],
                datasets: [{
                    label: 'Satisfaction Rating',
                    data: [4.2, 3.8, 4.5, 4.3, 3.9, 4.1],
                    borderColor: 'rgba(155, 89, 182, 1)',
                    backgroundColor: 'rgba(155, 89, 182, 0.2)',
                    borderWidth: 3,
                    pointBackgroundColor: 'rgba(155, 89, 182, 1)',
                    pointBorderColor: '#fff',
                    pointBorderWidth: 2
                }]
            },
            options: {
                ...chartDefaults,
                scales: {
                    r: {
                        beginAtZero: true,
                        max: 5,
                        grid: {
                            color: 'rgba(0, 0, 0, 0.1)'
                        },
                        pointLabels: {
                            font: {
                                size: 11
                            }
                        }
                    }
                }
            }
        });

        // Operating System Chart
        const osCtx = document.getElementById('osChart').getContext('2d');
        new Chart(osCtx, {
            type: 'polarArea',
            data: {
                labels: ['Windows', 'macOS', 'Linux', 'WSL'],
                datasets: [{
                    data: [49, 31, 28, 15],
                    backgroundColor: [
                        'rgba(52, 152, 219, 0.7)',
                        'rgba(46, 204, 113, 0.7)',
                        'rgba(231, 76, 60, 0.7)',
                        'rgba(241, 196, 15, 0.7)'
                    ],
                    borderColor: [
                        'rgba(52, 152, 219, 1)',
                        'rgba(46, 204, 113, 1)',
                        'rgba(231, 76, 60, 1)',
                        'rgba(241, 196, 15, 1)'
                    ],
                    borderWidth: 2
                }]
            },
            options: {
                ...chartDefaults,
                scales: {
                    r: {
                        beginAtZero: true,
                        grid: {
                            color: 'rgba(0, 0, 0, 0.1)'
                        }
                    }
                }
            }
        });
    </script>
</body>
</html>
