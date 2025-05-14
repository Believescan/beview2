<script lang="ts">
  import { page } from '$app/stores';

  type Category = 'new-tokens' | 'top-market-cap' | 'top-gainers';
  let category = $page.params.category as Category;

  interface TokenMetadataInfo {
    mintAuthority?: string;
    freezeAuthority?: string;
  }

  interface TokenMetadata {
    address: string;
    name: string;
    symbol: string;
    icon?: string;
    decimals: number;
    price?: number;
    volume24h?: number;
    marketCap?: number;
    marketCapRank?: number;
    priceChange24h?: number;
    supply?: string;
    holder?: number;
    creator?: string;
    createTx?: string;
    createdTime?: number;
    firstMintTx?: string;
    firstMintTime?: number;
    metadata?: TokenMetadataInfo;
  }

  // Helper functions for formatting values
  function formatPrice(price?: number): string {
    if (!price) return '$0.00';
    return new Intl.NumberFormat('en-US', {
      style: 'currency',
      currency: 'USD',
      minimumFractionDigits: 2,
      maximumFractionDigits: 6
    }).format(price);
  }

  function formatLargeNumber(num?: number): string {
    if (!num) return '0';
    if (num >= 1e9) return (num / 1e9).toFixed(2) + 'B';
    if (num >= 1e6) return (num / 1e6).toFixed(2) + 'M';
    if (num >= 1e3) return (num / 1e3).toFixed(2) + 'K';
    return num.toFixed(2);
  }

  function formatPercentage(change?: number): string {
    if (!change) return '0%';
    return (change > 0 ? '+' : '') + change.toFixed(2) + '%';
  }

  function formatHolders(holders?: number): string {
    if (!holders) return '0';
    return new Intl.NumberFormat('en-US').format(holders);
  }

  // Extended placeholder data based on category
  const tokenData = {
    'new-tokens': {
      title: 'New Tokens',
      tokens: [
        {
          address: '0x123...abc',
          name: 'NewToken1',
          symbol: 'NT1',
          decimals: 18,
          price: 0.50,
          priceChange24h: 15,
          marketCap: 2500000,
          volume24h: 450000,
          holder: 1245,
          createdTime: Date.now() - 86400000 // 24h ago
        },
        {
          address: '0x456...def',
          name: 'NewToken2',
          symbol: 'NT2',
          decimals: 18,
          price: 1.20,
          priceChange24h: 8,
          marketCap: 3100000,
          volume24h: 680000,
          holder: 2130,
          createdTime: Date.now() - 172800000 // 48h ago
        },
        {
          address: '0x789...ghi',
          name: 'NewToken3',
          symbol: 'NT3',
          decimals: 18,
          price: 0.75,
          priceChange24h: 12,
          marketCap: 1800000,
          volume24h: 320000,
          holder: 956,
          createdTime: Date.now() - 259200000 // 72h ago
        }
      ] as TokenMetadata[]
    },
    'top-market-cap': {
      title: 'Top by Market Cap',
      tokens: [
        {
          address: '0xabc...123',
          name: 'TopToken1',
          symbol: 'TT1',
          decimals: 18,
          price: 2.50,
          priceChange24h: 5,
          marketCap: 1200000000,
          volume24h: 45000000,
          holder: 25678,
          marketCapRank: 1
        },
        {
          address: '0xdef...456',
          name: 'TopToken2',
          symbol: 'TT2',
          decimals: 18,
          price: 1.80,
          priceChange24h: 3,
          marketCap: 800000000,
          volume24h: 28000000,
          holder: 18934,
          marketCapRank: 2
        },
        {
          address: '0xghi...789',
          name: 'TopToken3',
          symbol: 'TT3',
          decimals: 18,
          price: 3.20,
          priceChange24h: 7,
          marketCap: 600000000,
          volume24h: 15000000,
          holder: 12456,
          marketCapRank: 3
        }
      ] as TokenMetadata[]
    },
    'top-gainers': {
      title: 'Top Gainers',
      tokens: [
        {
          address: '0xjkl...012',
          name: 'Gainer1',
          symbol: 'GN1',
          decimals: 18,
          price: 1.20,
          priceChange24h: 45,
          marketCap: 8500000,
          volume24h: 2100000,
          holder: 3456
        },
        {
          address: '0xmno...345',
          name: 'Gainer2',
          symbol: 'GN2',
          decimals: 18,
          price: 0.90,
          priceChange24h: 38,
          marketCap: 6200000,
          volume24h: 1800000,
          holder: 2789
        },
        {
          address: '0xpqr...678',
          name: 'Gainer3',
          symbol: 'GN3',
          decimals: 18,
          price: 2.10,
          priceChange24h: 32,
          marketCap: 12400000,
          volume24h: 3500000,
          holder: 5678
        }
      ] as TokenMetadata[]
    }
  };

  const currentData = tokenData[category] || tokenData['new-tokens'];
</script>

<svelte:head>
  <title>BeView | Believe Token Dashboard</title>
</svelte:head>

<div class="app-container">
  <header class="app-header">
    <div class="content-wrapper">
      <div class="header-content">
        <div class="header-left">
          <a href="/" class="back-button">
            <svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
              <path d="M15.41 7.41L14 6l-6 6 6 6 1.41-1.41L10.83 12l4.58-4.59z" fill="currentColor"/>
            </svg>
          </a>
          <h1 class="app-title">{currentData.title}</h1>
        </div>
      </div>
    </div>
  </header>

  <div class="content-wrapper">
    <div class="tokens-container">
      <div class="tokens-table">
        <div class="table-header">
          <div class="col-token">Token</div>
          <div class="col-price">Price</div>
          <div class="col-change">24h Change</div>
          <div class="col-market-cap">Market Cap</div>
          <div class="col-volume">Volume</div>
          <div class="col-holders">Holders</div>
        </div>
        {#each currentData.tokens as token}
          <a href="/token/{token.symbol}" class="table-row">
            <div class="col-token">
              <div class="token-info">
                <div class="token-image">{token.symbol.slice(0, 2)}</div>
                <div class="token-text">
                  <div class="token-name">{token.name}</div>
                  <div class="token-symbol">{token.symbol}</div>
                </div>
              </div>
            </div>
            <div class="col-price">{formatPrice(token.price)}</div>
            <div class="col-change">
              <span class={token.priceChange24h && token.priceChange24h > 0 ? 'positive-change' : 'negative-change'}>
                {formatPercentage(token.priceChange24h)}
              </span>
            </div>
            <div class="col-market-cap">${formatLargeNumber(token.marketCap)}</div>
            <div class="col-volume">${formatLargeNumber(token.volume24h)}</div>
            <div class="col-holders">{formatHolders(token.holder)}</div>
          </a>
        {/each}
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

  .tokens-container {
    padding-top: 84px;
    padding-bottom: 72px;
  }

  .tokens-table {
    background: #ffffff;
    border-radius: 24px;
    border: 1px solid rgba(0, 0, 0, 0.08);
    box-shadow: 0 1px 3px rgba(0, 0, 0, 0.08), 0 1px 2px rgba(0, 0, 0, 0.04);
    padding: 24px;
  }

  .table-header {
    display: grid;
    grid-template-columns: 2fr 1fr 1fr 1fr 1fr 1fr;
    gap: 16px;
    padding: 16px 24px;
    margin-bottom: 8px;
    font-weight: 600;
    color: #666666;
    font-size: 14px;
  }

  .table-row {
    display: grid;
    grid-template-columns: 2fr 1fr 1fr 1fr 1fr 1fr;
    gap: 16px;
    padding: 20px 24px;
    margin-bottom: 16px;
    text-decoration: none;
    color: inherit;
    background: #ffffff;
    border-radius: 16px;
    border: 1px solid rgba(0, 0, 0, 0.08);
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.05), 0 1px 3px rgba(0, 0, 0, 0.05);
    transition: transform 0.2s ease, box-shadow 0.2s ease;
    align-items: center;
  }

  .table-row:last-child {
    margin-bottom: 0;
  }

  .table-row:hover {
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
    width: 40px;
    height: 40px;
    border-radius: 50%;
    background: linear-gradient(135deg, #22c55e 0%, #16a34a 100%);
    display: flex;
    align-items: center;
    justify-content: center;
    color: white;
    font-weight: 600;
    font-size: 14px;
    box-shadow: 0 2px 4px rgba(34, 197, 94, 0.2);
  }

  .token-text {
    display: flex;
    flex-direction: column;
    gap: 2px;
    min-width: 0;
  }

  .token-name {
    font-weight: 600;
    color: #111111;
    margin: 0;
    padding: 0;
  }

  .token-symbol {
    color: #666666;
    font-size: 14px;
    margin: 0;
    padding: 0;
  }

  .col-price,
  .col-market-cap,
  .col-volume,
  .col-holders,
  .col-change {
    font-weight: 500;
    display: flex;
    align-items: center;
  }

  .positive-change,
  .negative-change {
    display: inline-flex;
    align-items: center;
    height: fit-content;
    font-size: 14px;
    font-weight: 600;
    padding: 6px 12px;
    border-radius: 100px;
  }

  .positive-change {
    color: #22c55e;
    background: rgba(34, 197, 94, 0.1);
  }

  .negative-change {
    color: #ef4444;
    background: rgba(239, 68, 68, 0.1);
  }

  .back-button {
    color: rgb(85, 85, 85);
    display: flex;
    align-items: center;
    padding: 8px;
    margin: -8px;
    border-radius: 50%;
    transition: background-color 0.2s ease;
  }

  .back-button:hover {
    background-color: rgba(0, 0, 0, 0.05);
  }

  .header-left {
    display: flex;
    align-items: center;
    gap: 12px;
  }

  .app-header {
    background: #ffffff;
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
    color: rgb(17, 17, 17);
    margin: 0;
    letter-spacing: -0.5px;
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

  @media (max-width: 1024px) {
    .table-header, .table-row {
      grid-template-columns: 2fr 1fr 1fr 1fr;
    }

    .col-volume, .col-holders {
      display: none;
    }
  }

  @media (max-width: 768px) {
    .table-header, .table-row {
      grid-template-columns: 2fr 1fr 1fr;
      padding: 16px 20px;
    }

    .col-market-cap {
      display: none;
    }

    .token-image {
      width: 32px;
      height: 32px;
      font-size: 12px;
    }

    .token-name {
      font-size: 14px;
    }

    .token-symbol {
      font-size: 13px;
    }

    .positive-change,
    .negative-change {
      font-size: 13px;
      padding: 4px 8px;
    }
  }

  @media (max-width: 480px) {
    .table-header, .table-row {
      grid-template-columns: 2fr 1fr;
      gap: 12px;
      padding: 14px 16px;
    }

    .col-change {
      display: none;
    }
  }
</style> 