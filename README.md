<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>🍕 Pizza Sales Analytics – Project README</title>
  <style>
    :root{
      --bg:#0b0f14; --panel:#101620; --ink:#e8f0fe; --muted:#98a2b3; --accent:#ff6b00; --accent2:#ffd166; --card:#0f172a; --ok:#22c55e; --warn:#f59e0b; --danger:#ef4444;
      --mono: ui-monospace, SFMono-Regular, Menlo, Monaco, Consolas, "Liberation Mono", "Courier New", monospace;
      --sans: Inter, ui-sans-serif, system-ui, -apple-system, Segoe UI, Roboto, Ubuntu, Cantarell, Noto Sans, "Helvetica Neue", Arial, "Apple Color Emoji", "Segoe UI Emoji";
    }
    html,body{background:var(--bg); color:var(--ink); font-family:var(--sans); line-height:1.6;}
    .wrap{max-width:1080px; margin:40px auto; padding:0 20px;}
    header{display:flex; align-items:center; gap:16px; margin-bottom:18px;}
    header .logo{font-size:40px;}
    h1{font-size: clamp(28px,4vw,44px); margin: 0; letter-spacing:.3px;}
    .sub{color:var(--muted); margin-top:4px}
    .badges{display:flex; flex-wrap:wrap; gap:10px; margin:18px 0 8px}
    .badge{font-size:12px; padding:6px 10px; background:#0e1726; color:#dbeafe; border:1px solid #1f2937; border-radius:999px}
    nav{background:var(--panel); border:1px solid #1e293b; border-radius:14px; padding:14px; margin:20px 0 30px}
    nav a{color:#c7d2fe; text-decoration:none; margin-right:14px}
    section{background:var(--panel); border:1px solid #1e293b; border-radius:16px; padding:22px; margin:18px 0}
    h2{margin:0 0 8px; font-size: clamp(20px,3vw,28px)}
    p{margin:10px 0}
    .grid{display:grid; gap:16px}
    .grid.cols-2{grid-template-columns:repeat(auto-fit,minmax(260px,1fr))}
    code, pre{font-family:var(--mono)}
    pre{background:#0b1220; border:1px solid #1f2937; padding:14px; border-radius:12px; overflow:auto}
    .kpi{display:grid; grid-template-columns:repeat(2,1fr); gap:10px}
    .kpi div{background:#0b1220; border:1px solid #1f2937; border-radius:12px; padding:12px}
    .kpi .val{font-size:22px; font-weight:700}
    .callout{border-left:4px solid var(--accent); padding:10px 14px; background:#0e1726; color:#f8fafc; border-radius:8px}
    .imgbox{background:#0b1220; border:1px dashed #334155; border-radius:12px; padding:18px; text-align:center; color:#94a3b8}
    .steps{counter-reset: step}
    .steps li{counter-increment: step}
    .steps li::marker{content: counter(step) ".  "}
    footer{color:#94a3b8; font-size:12px; text-align:center; margin:24px 0}
    a.btn{display:inline-block; background:var(--accent); color:#0b0f14; padding:10px 14px; border-radius:10px; text-decoration:none; font-weight:700}
    .table{width:100%; border-collapse:collapse;}
    .table th,.table td{border-bottom:1px solid #243043; padding:10px; text-align:left}
    .pill{display:inline-block; padding:4px 10px; border-radius:999px; font-size:12px; border:1px solid #374151; background:#0b1220}
  </style>
</head>
<body>
  <div class="wrap">
    <header>
      <div class="logo">🍕</div>
      <div>
        <h1>Pizza Sales Analytics</h1>
        <div class="sub">SQL • Power BI • Excel • Python – end‑to‑end data analysis and dashboarding project</div>
        <div class="badges">
          <span class="badge">SQL</span>
          <span class="badge">Power BI</span>
          <span class="badge">Excel</span>
          <span class="badge">Python</span>
          <span class="badge">Open Source</span>
        </div>
      </div>
    </header>

    <nav>
      <a href="#overview">Overview</a>
      <a href="#dataset">Dataset</a>
      <a href="#schema">Schema</a>
      <a href="#kpi">KPIs</a>
      <a href="#sql">Core SQL</a>
      <a href="#dashboard">Dashboard</a>
      <a href="#setup">Setup</a>
      <a href="#credits">Credits</a>
    </nav>

    <section id="overview">
      <h2>Overview</h2>
      <p>This repository analyzes pizza shop transactions to uncover sales trends, top‑performing products, and customer behavior. The project covers the full analytics workflow—data cleaning with SQL/Python, KPI computation, and interactive visualizations in Power BI/Excel.</p>
      <div class="kpi">
        <div>
          <div class="label">Total Revenue</div>
          <div class="val">$1.2M</div>
          <small class="muted">Sample value – computed in model</small>
        </div>
        <div>
          <div class="label">Total Orders</div>
          <div class="val">24,890</div>
        </div>
        <div>
          <div class="label">Avg. Order Value</div>
          <div class="val">$48.23</div>
        </div>
        <div>
          <div class="label">Top Category</div>
          <div class="val">Classic</div>
        </div>
      </div>
    </section>

    <section id="dataset">
      <h2>Dataset</h2>
      <div class="grid cols-2">
        <div>
          <p><strong>Files</strong></p>
          <ul>
            <li><code>orders.csv</code> – order header (order_id, order_time, customer_id, channel)</li>
            <li><code>order_details.csv</code> – line items (order_id, pizza_id, qty, unit_price)</li>
            <li><code>pizzas.csv</code> – pizza_id, name, size, category</li>
            <li><code>customers.csv</code> – customer_id, city, state</li>
          </ul>
        </div>
        <div>
          <table class="table">
            <thead><tr><th>Column</th><th>Type</th><th>Notes</th></tr></thead>
            <tbody>
              <tr><td>order_time</td><td>timestamp</td><td>Used for time‑series and seasonality</td></tr>
              <tr><td>category</td><td>text</td><td class="pill">Classic / Veggie / Supreme / Chicken</td></tr>
              <tr><td>size</td><td>text</td><td class="pill">S / M / L / XL</td></tr>
              <tr><td>unit_price</td><td>numeric</td><td>Currency USD</td></tr>
            </tbody>
          </table>
        </div>
      </div>
      <div class="callout"><strong>Tip:</strong> Replace CSVs with your own data or connect to a database; the SQL below is ANSI‑compliant.</div>
    </section>

    <section id="schema">
      <h2>Relational Schema</h2>
      <pre><code>orders(order_id PK, order_time, customer_id, channel)
order_details(order_id FK, line_id PK, pizza_id FK, qty, unit_price)
pizzas(pizza_id PK, name, size, category)
customers(customer_id PK, city, state)
      </code></pre>
      <p>Revenue is calculated as <code>qty * unit_price</code> at the line level.</p>
    </section>

    <section id="kpi">
      <h2>Key Metrics (KPIs)</h2>
      <ul>
        <li><span class="pill">Total Revenue</span>: sum of line revenue</li>
        <li><span class="pill">Total Orders</span>: distinct orders</li>
        <li><span class="pill">Average Order Value (AOV)</span>: revenue / orders</li>
        <li><span class="pill">Orders by Hour/Weekday/Month</span></li>
        <li><span class="pill">Top 5 Pizzas</span> by revenue & quantity</li>
        <li><span class="pill">Category & Size Mix</span></li>
        <li><span class="pill">Repeat Rate</span> (if customer_id exists)</li>
      </ul>
    </section>

    <section id="sql">
      <h2>Core SQL Queries</h2>

      <h3>1) Revenue, Orders, AOV</h3>
      <pre><code>WITH line AS (
  SELECT od.order_id,
         od.qty * od.unit_price AS revenue
  FROM order_details od
)
SELECT SUM(revenue)            AS total_revenue,
       COUNT(DISTINCT order_id) AS total_orders,
       ROUND(SUM(revenue) * 1.0 / COUNT(DISTINCT order_id), 2) AS aov
FROM line;
      </code></pre>

      <h3>2) Top 5 Pizzas by Revenue</h3>
      <pre><code>SELECT p.name,
       SUM(od.qty * od.unit_price) AS revenue,
       SUM(od.qty)                 AS quantity
FROM order_details od
JOIN pizzas p ON p.pizza_id = od.pizza_id
GROUP BY p.name
ORDER BY revenue DESC
FETCH FIRST 5 ROWS ONLY; -- use LIMIT 5 for MySQL/Postgres
      </code></pre>

      <h3>3) Sales by Category & Size</h3>
      <pre><code>SELECT p.category, p.size,
       SUM(od.qty * od.unit_price) AS revenue
FROM order_details od
JOIN pizzas p ON p.pizza_id = od.pizza_id
GROUP BY p.category, p.size
ORDER BY revenue DESC;
      </code></pre>

      <h3>4) Hourly / Weekly Seasonality</h3>
      <pre><code>SELECT EXTRACT(HOUR   FROM o.order_time) AS hr,
       EXTRACT(DOW    FROM o.order_time) AS dow,  -- use DATEPART(dw, ...) on SQL Server
       COUNT(DISTINCT o.order_id)        AS orders
FROM orders o
GROUP BY hr, dow
ORDER BY hr, dow;
      </code></pre>

      <h3>5) Repeat Customers</h3>
      <pre><code>WITH firsts AS (
  SELECT customer_id,
         MIN(order_time) AS first_order
  FROM orders
  GROUP BY customer_id
)
SELECT CASE WHEN o.order_time &gt; f.first_order THEN 'Repeat' ELSE 'First' END AS segment,
       COUNT(DISTINCT o.order_id) AS orders
FROM orders o
JOIN firsts f USING(customer_id)
GROUP BY segment;
      </code></pre>
    </section>

    <section id="dashboard">
      <h2>Dashboards</h2>
      <div class="grid cols-2">
        <div class="imgbox">Add screenshot: <code>./assets/powerbi_dashboard.png</code></div>
        <div class="imgbox">Add screenshot: <code>./assets/excel_dashboard.png</code></div>
      </div>
      <p>
        Suggested visuals: <span class="pill">Revenue trend</span> • <span class="pill">Orders by weekday/hour</span> • <span class="pill">Category & size tree/stack</span> • <span class="pill">Top products</span> • <span class="pill">AOV</span>
      </p>
    </section>

    <section id="setup">
      <h2>Setup & Repro</h2>
      <ol class="steps">
        <li>Clone the repo: <code>git clone https://github.com/&lt;your-username&gt;/pizza-sales-analytics.git</code></li>
        <li>Place CSVs in <code>./data/</code> or configure DB connection string in <code>config/.env</code>.</li>
        <li>Run SQL scripts in <code>sql/</code> to create tables and load data (or use Power Query in Excel).</li>
        <li>Open <code>dashboard/PizzaSales.pbix</code> in Power BI Desktop (or Excel dashboard file).</li>
        <li>Export static images to <code>assets/</code> and update paths in this README.</li>
      </ol>

      <h3>Optional: Python Quickstart</h3>
      <pre><code>pip install pandas sqlalchemy matplotlib

# example extract
import pandas as pd
orders = pd.read_csv('data/orders.csv', parse_dates=['order_time'])
lines  = pd.read_csv('data/order_details.csv')
rev = (lines.assign(revenue=lambda d: d.qty * d.unit_price)
             .groupby([])['revenue'].sum())
print(rev)
      </code></pre>
    </section>

    <section id="credits">
      <h2>Credits</h2>
      <p>Built by &lt;your name&gt;. Feel free to use this HTML README as a template—just replace sample values, screenshots, and repository links.</p>
      <a class="btn" href="#top">⬆ Back to top</a>
    </section>

    <footer>
      <p>© 2025 Pizza Sales Analytics • MIT License</p>
    </footer>
  </div>
</body>
</html>
