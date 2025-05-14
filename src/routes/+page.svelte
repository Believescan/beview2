<script lang="ts">
  import { onMount } from 'svelte';
  import Chart from 'chart.js/auto';

  // Placeholder data - will be replaced with real data later
  const newTokens = [
    { name: 'NewToken1', symbol: 'NT1', price: '$0.50', change: '+15%' },
    { name: 'NewToken2', symbol: 'NT2', price: '$1.20', change: '+8%' },
    { name: 'NewToken3', symbol: 'NT3', price: '$0.75', change: '+12%' },
    { name: 'NewToken4', symbol: 'NT4', price: '$0.90', change: '+5%' },
    { name: 'NewToken5', symbol: 'NT5', price: '$1.50', change: '+10%' }
  ];

  const topTokens = [
    { name: 'TopToken1', symbol: 'TT1', marketCap: '$1.2B', price: '$2.50' },
    { name: 'TopToken2', symbol: 'TT2', marketCap: '$800M', price: '$1.80' },
    { name: 'TopToken3', symbol: 'TT3', marketCap: '$600M', price: '$3.20' },
    { name: 'TopToken4', symbol: 'TT4', marketCap: '$450M', price: '$1.20' },
    { name: 'TopToken5', symbol: 'TT5', marketCap: '$300M', price: '$0.90' }
  ];

  const topGainers = [
    { name: 'Gainer1', symbol: 'GN1', change: '+45%', price: '$1.20' },
    { name: 'Gainer2', symbol: 'GN2', change: '+38%', price: '$0.90' },
    { name: 'Gainer3', symbol: 'GN3', change: '+32%', price: '$2.10' },
    { name: 'Gainer4', symbol: 'GN4', change: '+28%', price: '$1.50' },
    { name: 'Gainer5', symbol: 'GN5', change: '+25%', price: '$0.75' }
  ];

  const stats = [
    { title: 'Total Tokens', value: '2,451', change: '+12%' },
    { title: 'Market Volume', value: '$1.2M', change: '+8%' },
    { title: '24h Transactions', value: '45,231', change: '+15%' }
  ];

  // Chart data
  const chartData = {
    labels: ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun'],
    datasets: [{
      label: 'Tokens Created',
      data: [12, 19, 15, 25, 22, 30, 28],
      backgroundColor: 'rgba(34, 197, 94, 0.2)',
      borderColor: '#22c55e',
      borderWidth: 2,
      borderRadius: 5,
      maxBarThickness: 50
    }]
  };

  let chart: Chart;

  onMount(() => {
    const canvas = document.getElementById('tokenChart') as HTMLCanvasElement;
    if (canvas) {
      const ctx = canvas.getContext('2d');
      if (ctx) {
        chart = new Chart(ctx, {
          type: 'bar',
          data: chartData,
          options: {
            responsive: true,
            maintainAspectRatio: false,
            plugins: {
              legend: {
                display: false
              },
              title: {
                display: true,
                text: 'Daily Token Creation',
                font: {
                  size: 16,
                  weight: 'bold'
                },
                padding: 20
              }
            },
            scales: {
              y: {
                beginAtZero: true,
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
      }
    }
  });
</script>

<div class="app-container">
  <header class="app-header">
    <div class="content-wrapper">
      <div class="header-content">
        <h1 class="app-title">BeView</h1>
        <div class="market-cap-pill">
          <span class="market-cap-label">Market Cap</span>
          <span class="market-cap-value">$12.8M</span>
        </div>
      </div>
    </div>
  </header>

  <div class="content-wrapper">
    <div class="dashboard-container">
      <div class="stats-grid">
        {#each stats as stat}
          <div class="stat-card">
            <div class="stat-content">
              <h3 class="stat-title">{stat.title}</h3>
              <div class="stat-value">{stat.value}</div>
              <div class="stat-change positive-change">{stat.change} from last week</div>
            </div>
          </div>
        {/each}
      </div>
      
      <div class="dashboard-grid">
        <div class="card">
          <div class="card-header">
            <h2 class="card-title">New Tokens</h2>
            <a href="/tokens/new-tokens" class="button">View All</a>
          </div>
          <ul class="token-list">
            {#each newTokens as token}
              <a href="/token/{token.symbol}" class="token-item">
                <div class="token-info">
                  <div class="token-image">{token.symbol[0]}</div>
                  <div class="token-text">
                    <div class="token-name">{token.name}</div>
                    <div class="token-symbol">{token.symbol}</div>
                  </div>
                </div>
                <div class="token-metrics">
                  <span class="token-price">{token.price}</span>
                  <span class="positive-change">{token.change}</span>
                </div>
              </a>
            {/each}
          </ul>
        </div>

        <div class="card">
          <div class="card-header">
            <h2 class="card-title">Top by Market Cap</h2>
            <a href="/tokens/top-market-cap" class="button">View All</a>
          </div>
          <ul class="token-list">
            {#each topTokens as token}
              <a href="/token/{token.symbol}" class="token-item">
                <div class="token-info">
                  <div class="token-image">{token.symbol[0]}</div>
                  <div class="token-text">
                    <div class="token-name">{token.name}</div>
                    <div class="token-symbol">{token.symbol}</div>
                  </div>
                </div>
                <div class="token-metrics">
                  <span class="token-price">{token.price}</span>
                  <span class="market-cap">{token.marketCap}</span>
                </div>
              </a>
            {/each}
          </ul>
        </div>

        <div class="card">
          <div class="card-header">
            <h2 class="card-title">Top Gainers</h2>
            <a href="/tokens/top-gainers" class="button">View All</a>
          </div>
          <ul class="token-list">
            {#each topGainers as token}
              <a href="/token/{token.symbol}" class="token-item">
                <div class="token-info">
                  <div class="token-image">{token.symbol[0]}</div>
                  <div class="token-text">
                    <div class="token-name">{token.name}</div>
                    <div class="token-symbol">{token.symbol}</div>
                  </div>
                </div>
                <div class="token-metrics">
                  <span class="token-price">{token.price}</span>
                  <span class="positive-change">{token.change}</span>
                </div>
              </a>
            {/each}
          </ul>
        </div>
      </div>

      <div class="card chart-card">
        <canvas id="tokenChart"></canvas>
      </div>
    </div>
  </div>

  <footer class="app-footer">
    <div class="content-wrapper">
      <div class="footer-content">
        <div class="copyright">© 2025 BeView.app. All rights reserved.</div>
        <a href="https://twitter.com/BeViewApp" target="_blank" rel="noopener noreferrer" class="social-link">
          <svg width="20" height="20" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
            <path d="M18.244 2.25h3.308l-7.227 8.26 8.502 11.24H16.17l-5.214-6.817L4.99 21.75H1.68l7.73-8.835L1.254 2.25H8.08l4.713 6.231zm-1.161 17.52h1.833L7.084 4.126H5.117z" fill="currentColor"/>
          </svg>
        </a>
      </div>
    </div>
  </footer>
</div>

<style>
  @font-face {
    font-family: 'OpenRunde';
    src: url('/fonts/OpenRunde-Regular.woff2') format('woff2'),
         url('/fonts/OpenRunde-Regular.woff') format('woff');
    font-weight: 400;
    font-style: normal;
    font-display: swap;
  }

  @font-face {
    font-family: 'OpenRunde';
    src: url('/fonts/OpenRunde-Medium.woff2') format('woff2'),
         url('/fonts/OpenRunde-Medium.woff') format('woff');
    font-weight: 500;
    font-style: normal;
    font-display: swap;
  }

  @font-face {
    font-family: 'OpenRunde';
    src: url('/fonts/OpenRunde-Semibold.woff2') format('woff2'),
         url('/fonts/OpenRunde-Semibold.woff') format('woff');
    font-weight: 600;
    font-style: normal;
    font-display: swap;
  }

  @font-face {
    font-family: 'OpenRunde';
    src: url('/fonts/OpenRunde-Bold.woff2') format('woff2'),
         url('/fonts/OpenRunde-Bold.woff') format('woff');
    font-weight: 700;
    font-style: normal;
    font-display: swap;
  }

  :global(body) {
    margin: 0;
    padding: 0;
    transition: background-color 0.3s, color 0.3s;
    background: var(--background, #fafafa);
    color: var(--text-dark, #1a1a1a);
    min-height: 100vh;
    font-family: 'OpenRunde', ui-sans-serif, system-ui, -apple-system, Arial, Helvetica, sans-serif;
    font-size: 16px;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
  }

  :global(body.dark-theme) {
    --background: #111111;
    --card-background: #1a1a1a;
    --text-dark: #ffffff;
    --text-muted: #a0a0a0;
    --border-color: #2a2a2a;
  }

  .app-container {
    padding: 0;
    display: flex;
    flex-direction: column;
    min-height: 100vh;
  }

  .content-wrapper {
    max-width: 1400px;
    width: 100%;
    margin: 0 auto;
    padding: 0 16px;
  }

  .app-header {
    background: var(--card-background, #ffffff);
    backdrop-filter: blur(10px);
    -webkit-backdrop-filter: blur(10px);
    border: none;
    padding: 16px 0;
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    width: 100%;
    z-index: 100;
    box-shadow: 0 1px 0 rgba(0, 0, 0, 0.05);
  }

  .header-content {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }

  .app-title {
    font-family: 'OpenRunde', ui-sans-serif, system-ui, -apple-system, Arial, Helvetica, sans-serif;
    font-size: 24px;
    font-weight: 700;
    color: var(--text-dark);
    margin: 0;
    letter-spacing: -0.5px;
  }

  .market-cap-pill {
    background: #22c55e;
    color: #ffffff;
    padding: 6px 16px;
    border-radius: 50px;
    font-size: 14px;
    font-weight: 600;
    display: flex;
    gap: 8px;
    align-items: center;
    box-shadow: 0 2px 4px rgba(34, 197, 94, 0.2);
  }

  .market-cap-label {
    opacity: 0.9;
    font-size: 13px;
    letter-spacing: 0.3px;
    font-weight: 600;
  }

  .market-cap-value {
    font-weight: 600;
    letter-spacing: -0.3px;
  }

  .token-list {
    list-style: none;
    padding: 0 8px 0 0;
    margin: -16px 0;
    max-height: 400px;
    overflow-y: auto;
  }

  .token-item {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 16px;
    border-radius: 16px;
    background: #ffffff;
    border: 1px solid rgba(0, 0, 0, 0.08);
    margin: 16px 0;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.05), 0 1px 3px rgba(0, 0, 0, 0.05);
    text-decoration: none;
    transition: transform 0.2s ease, box-shadow 0.2s ease;
  }

  .token-item:hover {
    transform: translateY(-1px);
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.07), 0 2px 4px rgba(0, 0, 0, 0.05);
  }

  .token-info {
    display: flex;
    align-items: center;
    gap: 12px;
    min-width: 0;
  }

  .token-image {
    width: 32px;
    height: 32px;
    border-radius: 50%;
    background: #f3f4f6;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 12px;
    color: #6b7280;
    font-weight: 600;
    border: 1px solid rgba(0, 0, 0, 0.04);
  }

  .token-text {
    display: flex;
    flex-direction: column;
    gap: 2px;
    min-width: 0;
    align-items: flex-start;
  }

  .token-name {
    font-weight: 600;
    color: rgb(17, 17, 17);
    letter-spacing: -0.3px;
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
    line-height: 1.2;
    padding: 0;
    margin: 0;
  }

  .token-symbol {
    color: rgb(153, 153, 153);
    font-size: 14px;
    line-height: 1.2;
    padding: 0;
    margin: 0;
    font-weight: 500;
  }

  .token-metrics {
    display: flex;
    align-items: flex-end;
    flex-direction: column;
    gap: 2px;
    min-width: 100px;
    text-align: right;
  }

  .token-price {
    font-weight: 600;
    color: rgb(17, 17, 17);
    letter-spacing: -0.3px;
  }

  .positive-change {
    color: #22c55e;
    font-weight: 700;
  }

  .market-cap {
    color: var(--text-muted, #64748b);
    font-size: 0.9em;
  }

  .dashboard-grid {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 16px;
    margin-bottom: 24px;
  }

  .card-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 16px;
  }

  .card-title {
    font-size: 18px;
    font-weight: 700;
    color: rgb(17, 17, 17);
    margin: 0;
    letter-spacing: -0.5px;
  }

  .button {
    background: #22c55e;
    border: none;
    padding: 8px 16px;
    border-radius: 50px;
    font-weight: 700;
    color: #ffffff;
    cursor: pointer;
    transition: all 0.2s ease;
    font-size: 14px;
    letter-spacing: 0.3px;
    box-shadow: 0 2px 4px rgba(34, 197, 94, 0.2);
    text-decoration: none;
  }

  .button:hover {
    transform: translateY(-1px);
    box-shadow: 0 4px 6px rgba(34, 197, 94, 0.25);
  }

  .chart-card {
    min-height: 400px;
    position: relative;
  }

  @media (max-width: 1024px) {
    .dashboard-grid {
      grid-template-columns: repeat(2, 1fr);
    }

    .stats-grid {
      grid-template-columns: repeat(2, 1fr);
    }
  }

  @media (max-width: 768px) {
    .content-wrapper {
      padding: 0 12px;
    }

    .dashboard-grid {
      grid-template-columns: 1fr;
    }

    .stats-grid {
      grid-template-columns: 1fr;
    }

    .card {
      padding: 20px;
    }

    .chart-card {
      min-height: 300px;
    }

    .token-metrics {
      min-width: 85px;
    }

    .app-header {
      padding: 12px 0;
    }

    .market-cap-pill {
      padding: 4px 12px;
      font-size: 13px;
    }

    .app-title {
      font-size: 20px;
    }

    .stat-card {
      padding-top: 20px;
    }

    .stat-change {
      display: none;
    }
  }

  @media (max-width: 480px) {
    .token-item {
      padding: 14px;
    }

    .token-image {
      width: 28px;
      height: 28px;
      font-size: 11px;
    }

    .token-info {
      gap: 10px;
    }

    .token-name {
      font-size: 14px;
    }

    .token-symbol {
      font-size: 13px;
    }

    .token-price {
      font-size: 14px;
    }

    .positive-change {
      font-size: 13px;
    }

    .market-cap {
      font-size: 13px;
    }
  }

  .dashboard-container {
    padding-top: 84px;
    padding-bottom: 72px;
  }

  .stats-grid {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 16px;
    margin-bottom: 24px;
  }

  .card, .stat-card, .chart-card {
    background: #ffffff;
    border-radius: 24px;
    padding: 24px;
    border: 1px solid rgba(0, 0, 0, 0.08);
    box-shadow: 0 1px 3px rgba(0, 0, 0, 0.08), 0 1px 2px rgba(0, 0, 0, 0.04);
  }

  :global(body.dark-theme) .card,
  :global(body.dark-theme) .stat-card,
  :global(body.dark-theme) .chart-card {
    background: var(--card-background, #1a1a1a);
    border-color: rgba(255, 255, 255, 0.1);
    box-shadow: 0 1px 3px rgba(0, 0, 0, 0.2), 0 1px 2px rgba(0, 0, 0, 0.1);
  }

  .stat-card {
    position: relative;
    padding-top: 32px;
    display: flex;
    flex-direction: column;
  }

  .stat-content {
    display: flex;
    flex-direction: column;
    gap: 4px;
  }

  .stat-change {
    position: absolute;
    top: 24px;
    right: 24px;
    font-size: 14px;
    font-weight: 600;
  }

  .stat-title {
    font-size: 14px;
    color: rgb(85, 85, 85);
    margin: 0 0 8px 0;
    font-weight: 600;
  }

  .stat-value {
    font-size: 28px;
    font-weight: 600;
    color: rgb(17, 17, 17);
    letter-spacing: -0.5px;
  }

  .card {
    padding-right: 16px;
  }

  .token-list::-webkit-scrollbar {
    width: 6px;
  }

  .token-list::-webkit-scrollbar-track {
    background: transparent;
  }

  .token-list::-webkit-scrollbar-thumb {
    background-color: rgba(0, 0, 0, 0.1);
    border-radius: 20px;
  }

  .app-footer {
    margin-top: auto;
    padding: 16px 0;
    border-top: 1px solid rgba(0, 0, 0, 0.08);
    background: #ffffff;
    width: 100%;
    position: fixed;
    bottom: 0;
    left: 0;
    right: 0;
    z-index: 100;
    box-shadow: 0 -1px 0 rgba(0, 0, 0, 0.05);
  }

  .footer-content {
    display: flex;
    justify-content: space-between;
    align-items: center;
    height: 24px;
  }

  .copyright {
    color: rgb(85, 85, 85);
    font-size: 14px;
    font-weight: 500;
  }

  .social-link {
    color: rgb(85, 85, 85);
    transition: color 0.2s ease;
    display: flex;
    align-items: center;
  }

  .social-link:hover {
    color: #22c55e;
  }

  @media (max-width: 768px) {
    .app-footer {
      padding: 20px 0;
    }

    .copyright {
      font-size: 13px;
    }
  }
</style>
