<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Crypto Guide</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      margin: 0; padding: 0;
      background: #f5f7fa; color: #333;
    }
    header {
      background-color: #2d2d72; color: white;
      padding: 20px 0;
      text-align: center;
    }
    nav {
      background: #4446a1;
      padding: 15px;
      text-align: center;
    }
    nav a {
      color: white;
      margin: 0 15px;
      text-decoration: none;
      font-weight: bold;
    }
    nav a:hover {color: #ffcc00;}
    main {
      max-width: 960px;
      margin: 20px auto;
      padding: 0 20px;
    }
    section {
      margin-bottom: 40px;
      background: white;
      padding: 20px;
      border-radius: 6px;
      box-shadow: 0 2px 5px rgba(0,0,0,0.1);
    }
    h1, h2 {color: #2d2d72;}
    footer {
      text-align: center;
      padding: 15px;
      background: #2d2d72;
      color: white;
      margin-top: 40px;
    }
    #price-ticker {
      background: #22294d;
      color: white;
      padding: 10px;
      font-size: 1.1em;
      overflow-x: auto;
      white-space: nowrap;
      margin-bottom: 20px;
      border-radius: 6px;
    }
    #price-ticker span {
      margin-right: 30px;
    }
    #newsletter input[type="email"] {
      padding: 10px;
      width: 250px;
      border: 1px solid #ccc;
      border-radius: 4px;
    }
    #newsletter button {
      padding: 10px 20px;
      border: none;
      background-color: #2d2d72;
      color: white;
      font-weight: bold;
      border-radius: 4px;
      cursor: pointer;
      margin-left: 10px;
    }
    #newsletter button:hover {
      background-color: #4446a1;
    }
    .faq-item {
      margin-bottom: 10px;
    }
    .faq-question {
      background: #eee;
      padding: 10px;
      cursor: pointer;
      font-weight: bold;
      border-radius: 4px;
    }
    .faq-answer {
      max-height: 0;
      overflow: hidden;
      transition: max-height 0.3s ease;
      background: #f9f9f9;
      padding: 0 10px;
      border-left: 2px solid #2d2d72;
      border-radius: 0 4px 4px 0;
    }
    .faq-answer.open {
      max-height: 200px;
      padding: 10px;
    }
    #social-links a {
      margin: 0 10px;
      color: #2d2d72;
      text-decoration: none;
      font-size: 1.4em;
    }
    #social-links a:hover {
      color: #ffcc00;
    }
  </style>
</head>
<body>
  <header>
    <h1>Crypto Guide</h1>
    <p>Your beginner to advanced cryptocurrency resource</p>
  </header>
  <nav>
    <a href="#beginner">Beginner's Guide</a>
    <a href="#buy-sell">How to Buy & Sell</a>
    <a href="#news">Market News</a>
    <a href="#security">Security Tips</a>
    <a href="#faqs">FAQs</a>
  </nav>
  <main>
    <div id="price-ticker" aria-label="Real-time Cryptocurrency Prices" role="region">
      Loading prices...
    </div>
    <section id="beginner">
      <h2>Beginner's Guide</h2>
      <p>Cryptocurrency is digital money secured by cryptography and powered by blockchain technology. Learn the basics of how cryptocurrencies work, common terms, and how to start your journey.</p>
    </section>
    <section id="buy-sell">
      <h2>How to Buy and Sell Crypto</h2>
      <p>Set up a digital wallet, choose a trusted exchange like Coinbase or Binance, and learn the steps to purchase and trade cryptocurrencies safely and efficiently.</p>
    </section>
    <section id="news">
      <h2>Market News & Updates</h2>
      <p>Stay informed about the latest developments, price trends, and major events that impact the cryptocurrency markets worldwide.</p>
    </section>
    <section id="security">
      <h2>Security & Safety Tips</h2>
      <p>Protect your investments by understanding wallet security, recognizing phishing scams, and practicing safe transaction habits.</p>
    </section>
    <section id="faqs">
      <h2>Frequently Asked Questions</h2>
      <div class="faq-item">
        <div class="faq-question">What is a cryptocurrency?</div>
        <div class="faq-answer">Cryptocurrency is a type of digital or virtual currency that uses cryptography for security and operates on decentralized technology called blockchain.</div>
      </div>
      <div class="faq-item">
        <div class="faq-question">How do I buy cryptocurrency safely?</div>
        <div class="faq-answer">Use trusted exchanges, enable two-factor authentication, and store your crypto in secure wallets to buy safely.</div>
      </div>
      <div class="faq-item">
        <div class="faq-question">What are the risks of investing in crypto?</div>
        <div class="faq-answer">Risks include market volatility, security vulnerabilities, regulation changes, and potential scams.</div>
      </div>
    </section>
    <section id="newsletter">
      <h2>Subscribe to Our Newsletter</h2>
      <form onsubmit="subscribeNewsletter(event)">
        <input type="email" id="email" placeholder="Enter your email" required />
        <button type="submit">Subscribe</button>
      </form>
      <p id="subscription-status"></p>
    </section>
    <section id="social-links" aria-label="Social Media Links" style="text-align:center; margin-top: 40px;">
      <a href="https://twitter.com" target="_blank" aria-label="Twitter">&#x1F426;</a>
      <a href="https://facebook.com" target="_blank" aria-label="Facebook">&#x1F465;</a>
      <a href="https://instagram.com" target="_blank" aria-label="Instagram">&#x1F4F7;</a>
    </section>
  </main>
  <footer>
    <p>© 2025 Crypto Guide. All rights reserved.</p>
  </footer>
  <script>
    // Fetch live prices from CoinGecko API
    async function fetchPrices() {
      const priceTicker = document.getElementById('price-ticker');
      try {
        const response = await fetch('https://api.coingecko.com/api/v3/simple/price?ids=bitcoin,ethereum,binancecoin,cardano&vs_currencies=usd');
        const data = await response.json();
        const prices = [];
        if (data.bitcoin) prices.push(`<span><strong>BTC</strong>: $${data.bitcoin.usd.toLocaleString()}</span>`);
        if (data.ethereum) prices.push(`<span><strong>ETH</strong>: $${data.ethereum.usd.toLocaleString()}</span>`);
        if (data.binancecoin) prices.push(`<span><strong>BNB</strong>: $${data.binancecoin.usd.toLocaleString()}</span>`);
        if (data.cardano) prices.push(`<span><strong>ADA</strong>: $${data.cardano.usd.toLocaleString()}</span>`);
        priceTicker.innerHTML = prices.join('');
      } catch (error) {
        priceTicker.textContent = 'Failed to load prices';
        console.error('Error fetching prices:', error);
      }
    }
    fetchPrices();
    setInterval(fetchPrices, 60000); // Refresh every 60 seconds
