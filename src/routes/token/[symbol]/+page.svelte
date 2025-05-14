<script lang="ts">
  import { page } from '$app/stores';

  let symbol = $page.params.symbol;
  
  // Placeholder data - replace with real data
  const tokenData = {
    price: "$0.0234",
    priceChange: "+12.5%",
    marketCap: "$12.8M",
    volume24h: "$1.2M",
    volume24hChange: "+15.3%",
    holders: "2,451",
    holdersChange: "+5.2%",
    liquidity: "$890K",
    liquidityChange: "+3.1%",
    supply: {
      total: "1,000,000,000",
      circulating: "750,000,000",
      burned: "250,000,000"
    }
  };
</script>

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
          <h1 class="app-title">{symbol}</h1>
        </div>
        <div class="market-cap-pill">
          <span class="market-cap-label">Market Cap</span>
          <span class="market-cap-value">{tokenData.marketCap}</span>
        </div>
      </div>
    </div>
  </header>

  <div class="content-wrapper">
    <div class="token-container">
      <div class="token-header">
        <div class="token-info">
          <div class="token-image-large">
            {symbol.slice(0, 2).toUpperCase()}
          </div>
          <div class="token-name">
            {symbol}
          </div>
          <div class="token-symbol">
            {symbol.toUpperCase()}
          </div>
        </div>
      </div>
      <div class="token-grid">
        <!-- Price Card -->
        <div class="info-card">
          <div class="info-card-header">
            <h2>Price</h2>
            <span class={tokenData.priceChange.startsWith('+') ? 'positive-change' : 'negative-change'}>
              {tokenData.priceChange}
            </span>
          </div>
          <div class="info-card-value">{tokenData.price}</div>
        </div>

        <!-- Volume Card -->
        <div class="info-card">
          <div class="info-card-header">
            <h2>24h Volume</h2>
            <span class="positive-change">{tokenData.volume24hChange}</span>
          </div>
          <div class="info-card-value">{tokenData.volume24h}</div>
        </div>

        <!-- Holders Card -->
        <div class="info-card">
          <div class="info-card-header">
            <h2>Holders</h2>
            <span class="positive-change">{tokenData.holdersChange}</span>
          </div>
          <div class="info-card-value">{tokenData.holders}</div>
        </div>

        <!-- Liquidity Card -->
        <div class="info-card">
          <div class="info-card-header">
            <h2>Liquidity</h2>
            <span class="positive-change">{tokenData.liquidityChange}</span>
          </div>
          <div class="info-card-value">{tokenData.liquidity}</div>
        </div>

        <!-- Supply Info Card -->
        <div class="info-card wide">
          <div class="info-card-header">
            <h2>Token Supply</h2>
          </div>
          <div class="supply-grid">
            <div class="supply-item">
              <div class="supply-label">Total Supply</div>
              <div class="supply-value">{tokenData.supply.total}</div>
            </div>
            <div class="supply-item">
              <div class="supply-label">Circulating Supply</div>
              <div class="supply-value">{tokenData.supply.circulating}</div>
            </div>
            <div class="supply-item">
              <div class="supply-label">Burned Tokens</div>
              <div class="supply-value">{tokenData.supply.burned}</div>
            </div>
          </div>
        </div>

        <!-- Links Card -->
        <div class="info-card wide links-card">
          <div class="info-card-header">
            <h2>Links</h2>
          </div>
          <div class="links-grid">
            <a href="https://beview.app/{symbol}" target="_blank" rel="noopener noreferrer" class="link-item">
              <svg width="20" height="20" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                <path d="M12 2C6.48 2 2 6.48 2 12s4.48 10 10 10 10-4.48 10-10S17.52 2 12 2zM8.5 8.5A3.5 3.5 0 0112 5a3.5 3.5 0 110 7 3.5 3.5 0 01-3.5-3.5zM12 19c-2.9 0-5.44-1.56-6.83-3.88.03-2.27 4.55-3.51 6.83-3.51s6.8 1.24 6.83 3.51C17.44 17.44 14.9 19 12 19z" fill="currentColor"/>
              </svg>
              <span>Official Website</span>
            </a>
            <a href="https://twitter.com/BeViewApp" target="_blank" rel="noopener noreferrer" class="link-item">
              <svg width="20" height="20" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                <path d="M18.244 2.25h3.308l-7.227 8.26 8.502 11.24H16.17l-5.214-6.817L4.99 21.75H1.68l7.73-8.835L1.254 2.25H8.08l4.713 6.231zm-1.161 17.52h1.833L7.084 4.126H5.117z" fill="currentColor"/>
              </svg>
              <span>Twitter Community</span>
            </a>
            <a href="https://www.dextools.io/app/en/ether/pair-explorer/{symbol}" target="_blank" rel="noopener noreferrer" class="link-item">
              <svg width="20" height="20" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                <path d="M12 2C6.48 2 2 6.48 2 12s4.48 10 10 10 10-4.48 10-10S17.52 2 12 2zm-1.07 14.826L6.93 12.83l1.414-1.414 2.586 2.586 5.656-5.657 1.415 1.414-7.071 7.071z" fill="currentColor"/>
              </svg>
              <span>View on DEXTools</span>
            </a>
          </div>
        </div>
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

  .header-left {
    display: flex;
    align-items: center;
    gap: 12px;
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

  .app-title {
    font-family: 'OpenRunde', ui-sans-serif, system-ui, -apple-system, Arial, Helvetica, sans-serif;
    font-size: 24px;
    font-weight: 700;
    color: rgb(17, 17, 17);
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

  .token-container {
    padding-top: 84px;
    padding-bottom: 72px;
  }

  .token-header {
    text-align: center;
    margin-bottom: 32px;
    padding: 32px;
    background: #ffffff;
    border-radius: 24px;
    border: 1px solid rgba(0, 0, 0, 0.08);
    box-shadow: 0 1px 3px rgba(0, 0, 0, 0.08), 0 1px 2px rgba(0, 0, 0, 0.04);
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
  }

  .token-info {
    display: flex;
    flex-direction: column;
    align-items: center;
    text-align: center;
    width: 100%;
  }

  .token-image-large {
    width: 96px;
    height: 96px;
    border-radius: 50%;
    background: linear-gradient(135deg, #22c55e 0%, #16a34a 100%);
    display: flex;
    align-items: center;
    justify-content: center;
    color: white;
    font-weight: 700;
    font-size: 32px;
    box-shadow: 0 8px 16px rgba(34, 197, 94, 0.2);
    margin-bottom: 20px;
  }

  .token-name {
    font-size: 32px;
    font-weight: 700;
    color: #111111;
    margin: 0;
    letter-spacing: -0.5px;
    line-height: 1.2;
    text-align: center;
    width: 100%;
  }

  .token-symbol {
    font-size: 18px;
    color: #666666;
    font-weight: 500;
    margin-top: 8px;
    line-height: 1;
    text-align: center;
    width: 100%;
    display: block;
  }

  .token-grid {
    display: grid;
    grid-template-columns: repeat(4, minmax(0, 1fr));
    gap: 24px;
    margin-top: 16px;
  }

  .info-card {
    background: #ffffff;
    border-radius: 16px;
    padding: 24px;
    border: 1px solid rgba(0, 0, 0, 0.08);
    box-shadow: 0 1px 3px rgba(0, 0, 0, 0.08), 0 1px 2px rgba(0, 0, 0, 0.04);
    display: flex;
    flex-direction: column;
    height: 100%;
    min-height: 140px;
  }

  .info-card.large {
    grid-column: span 2;
    display: flex;
    flex-direction: column;
    padding: 32px;
  }

  .info-card.large .info-card-header {
    display: flex;
    align-items: center;
    gap: 16px;
    margin-bottom: 24px;
  }

  .token-image {
    width: 48px;
    height: 48px;
    border-radius: 50%;
    background: linear-gradient(135deg, #22c55e 0%, #16a34a 100%);
    display: flex;
    align-items: center;
    justify-content: center;
    color: white;
    font-weight: 600;
    font-size: 20px;
    box-shadow: 0 4px 6px rgba(34, 197, 94, 0.2);
  }

  .price-content {
    flex-grow: 1;
  }

  .price-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 8px;
  }

  .info-card.large .info-card-value {
    font-size: 48px;
    font-weight: 700;
    background: linear-gradient(135deg, #111111 0%, #333333 100%);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    letter-spacing: -1px;
  }

  .positive-change {
    color: #22c55e;
    font-weight: 600;
    font-size: 14px;
    background: rgba(34, 197, 94, 0.1);
    padding: 6px 12px;
    border-radius: 100px;
  }

  .negative-change {
    color: #ef4444;
    font-weight: 600;
    font-size: 14px;
    background: rgba(239, 68, 68, 0.1);
    padding: 6px 12px;
    border-radius: 100px;
  }

  .info-card.wide {
    grid-column: span 4;
    min-height: auto;
  }

  .info-card-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 16px;
  }

  .info-card-header h2 {
    font-size: 14px;
    color: rgb(85, 85, 85);
    margin: 0;
    font-weight: 600;
  }

  .info-card-value {
    font-size: 32px;
    font-weight: 700;
    color: rgb(17, 17, 17);
    letter-spacing: -0.5px;
    margin-top: auto;
  }

  .supply-grid {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 32px;
    margin-top: 24px;
    padding: 8px 0;
  }

  .supply-item {
    text-align: center;
  }

  .supply-label {
    font-size: 14px;
    color: rgb(85, 85, 85);
    margin-bottom: 4px;
    font-weight: 500;
  }

  .supply-value {
    font-size: 18px;
    font-weight: 600;
    color: rgb(17, 17, 17);
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
    .token-grid {
      grid-template-columns: repeat(2, minmax(0, 1fr));
      gap: 20px;
    }

    .info-card.wide {
      grid-column: span 2;
    }
  }

  @media (max-width: 768px) {
    .content-wrapper {
      padding: 0 12px;
    }

    .app-header {
      padding: 12px 0;
    }

    .app-title {
      font-size: 20px;
    }

    .market-cap-pill {
      padding: 4px 12px;
      font-size: 13px;
    }

    .token-container {
      padding-top: 24px;
    }

    .token-header {
      padding: 24px;
      margin-bottom: 24px;
    }

    .token-image-large {
      width: 72px;
      height: 72px;
      font-size: 24px;
    }

    .token-name {
      font-size: 24px;
    }

    .token-symbol {
      font-size: 16px;
    }

    .info-card {
      padding: 20px;
    }

    .info-card-value {
      font-size: 28px;
    }

    .supply-grid {
      grid-template-columns: 1fr;
      gap: 16px;
    }

    .app-footer {
      padding: 12px 0;
    }

    .copyright {
      font-size: 13px;
    }

    .links-grid {
      grid-template-columns: 1fr;
      gap: 12px;
    }

    .link-item {
      padding: 14px 16px;
      justify-content: center;
    }
  }

  @media (max-width: 480px) {
    .token-grid {
      grid-template-columns: 1fr;
      gap: 16px;
    }

    .info-card.large,
    .info-card.wide {
      grid-column: span 1;
    }

    .supply-grid {
      grid-template-columns: 1fr;
      gap: 24px;
    }

    .info-card {
      min-height: 120px;
    }
  }

  .links-card {
    margin-top: 16px;
    min-height: auto;
    padding: 24px;
  }

  .links-grid {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 20px;
    margin-top: 12px;
  }

  .link-item {
    display: flex;
    align-items: center;
    gap: 10px;
    padding: 14px 20px;
    background: #ffffff;
    border-radius: 16px;
    color: #111111;
    text-decoration: none;
    font-weight: 600;
    font-size: 15px;
    transition: all 0.2s ease;
    border: 1px solid rgba(0, 0, 0, 0.08);
    box-shadow: 0 1px 2px rgba(0, 0, 0, 0.04);
  }

  .link-item:hover {
    background: #22c55e;
    color: #ffffff;
    transform: translateY(-1px);
    box-shadow: 0 4px 6px rgba(34, 197, 94, 0.15);
    border-color: #22c55e;
  }

  .link-item svg {
    flex-shrink: 0;
    width: 18px;
    height: 18px;
  }
</style> 