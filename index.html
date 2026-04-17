import { useState, useMemo } from "react";

const PRODUCTS = [
  { id: 1, series: "AI眼镜", name: "1300W E08骑行款", costCNY: 280, sku: "E08-1300W", packageDim: "20.3×8.5×5.5cm", packageWeight: 0.24, outerDim: "44.5×42.5×29.5cm", outerWeight: 12.19, unitsPerCarton: 50, suggestedPrice: 129.99 },
  { id: 2, series: "AI眼镜", name: "800W E09", costCNY: 132, sku: "E09-800W", packageDim: "20.3×8.5×5.5cm", packageWeight: 0.24, outerDim: "44.5×42.5×29.5cm", outerWeight: 12.19, unitsPerCarton: 50, suggestedPrice: 79.99 },
  { id: 3, series: "AI眼镜", name: "E05C 变色款", costCNY: 85, sku: "E05C-COLOR", packageDim: "20.3×8.5×5.5cm", packageWeight: 0.24, outerDim: "44.5×42.5×29.5cm", outerWeight: 12.19, unitsPerCarton: 50, suggestedPrice: 49.99 },
];

const TABS = [
  { key: "profit", label: "售价利润核算", icon: "💰" },
  { key: "ops", label: "运营规划", icon: "📋" },
  { key: "inventory", label: "备货规划", icon: "📦" },
  { key: "sensitivity", label: "价格敏感度", icon: "📊" },
  { key: "logistics", label: "物流成本对比", icon: "🚢" },
  { key: "fees", label: "FBA费用明细", icon: "🏷️" },
];

function getFBAFee(shippingWeightOz, priceUSD) {
  const band = priceUSD < 10 ? 0 : priceUSD <= 50 ? 1 : 2;
  // Large Standard 8+ to 12 oz (product is ~8.5oz)
  const rates = [3.38, 4.20, 4.46];
  return rates[band];
}

function getReferralFee(price) {
  // Electronics: 8% of sale price
  return price * 0.08;
}

export default function App() {
  const [tab, setTab] = useState("profit");
  const [exchangeRate, setExchangeRate] = useState(7.25);
  const [logisticsCostPerKg, setLogisticsCostPerKg] = useState(24);
  const [airFreightCost, setAirFreightCost] = useState(38);
  const [seaFreightCost, setSeaFreightCost] = useState(12);
  const [adROAS, setAdROAS] = useState(4.0);
  const [adSpendPct, setAdSpendPct] = useState(15);
  const [prices, setPrices] = useState({ 1: 129.99, 2: 79.99, 3: 49.99 });
  const [airQty, setAirQty] = useState({ 1: 100, 2: 100, 3: 200 });
  const [seaQty, setSeaQty] = useState({ 1: 500, 2: 500, 3: 1000 });

  const fuelSurcharge = 0.035; // 3.5% starting April 17, 2026
  const storageFeePerCuFt = 0.78; // Jan-Sep
  const storageQ4PerCuFt = 2.40; // Oct-Dec
  const unitVolumeCuFt = (20.3 * 8.5 * 5.5) / 28316.85; // cm³ to cubic feet
  const inboundPlacementFee = 0.30; // average for large standard

  const calculations = useMemo(() => {
    return PRODUCTS.map(p => {
      const price = prices[p.id];
      const costUSD = p.costCNY / exchangeRate;
      const logisticsPerUnit = (p.packageWeight * logisticsCostPerKg) / exchangeRate;
      const airLogisticsPerUnit = (p.packageWeight * airFreightCost) / exchangeRate;
      const seaLogisticsPerUnit = (p.packageWeight * seaFreightCost) / exchangeRate;
      const avgLogisticsPerUnit = logisticsPerUnit;

      const fbaFee = getFBAFee(p.packageWeight * 35.274, price);
      const fbaWithFuel = fbaFee * (1 + fuelSurcharge);
      const referralFee = getReferralFee(price);
      const monthlyStorage = unitVolumeCuFt * storageFeePerCuFt;
      const storageFor2Months = monthlyStorage * 2;

      const totalAmazonFees = fbaWithFuel + referralFee + inboundPlacementFee + storageFor2Months;
      const adCostPerUnit = price / adROAS;
      const totalCost = costUSD + avgLogisticsPerUnit + totalAmazonFees + adCostPerUnit;
      const profit = price - totalCost;
      const profitMargin = (profit / price) * 100;
      const breakEvenPrice = totalCost / (1 - 0);

      return {
        ...p,
        price,
        costUSD: costUSD.toFixed(2),
        logisticsPerUnit: avgLogisticsPerUnit.toFixed(2),
        airLogistics: airLogisticsPerUnit.toFixed(2),
        seaLogistics: seaLogisticsPerUnit.toFixed(2),
        fbaFee: fbaFee.toFixed(2),
        fbaWithFuel: fbaWithFuel.toFixed(2),
        referralFee: referralFee.toFixed(2),
        monthlyStorage: monthlyStorage.toFixed(2),
        inboundPlacement: inboundPlacementFee.toFixed(2),
        totalAmazonFees: totalAmazonFees.toFixed(2),
        adCostPerUnit: adCostPerUnit.toFixed(2),
        totalCost: totalCost.toFixed(2),
        profit: profit.toFixed(2),
        profitMargin: profitMargin.toFixed(1),
      };
    });
  }, [prices, exchangeRate, logisticsCostPerKg, airFreightCost, seaFreightCost, adROAS]);

  const sensitivityData = useMemo(() => {
    return PRODUCTS.map(p => {
      const costUSD = p.costCNY / exchangeRate;
      const logisticsPerUnit = (p.packageWeight * logisticsCostPerKg) / exchangeRate;
      const pricePoints = [];
      const basePrice = prices[p.id];
      for (let pct = -30; pct <= 30; pct += 10) {
        const testPrice = basePrice * (1 + pct / 100);
        const fba = getFBAFee(p.packageWeight * 35.274, testPrice) * (1 + fuelSurcharge);
        const ref = getReferralFee(testPrice);
        const storage = unitVolumeCuFt * storageFeePerCuFt * 2;
        const adCost = testPrice / adROAS;
        const total = costUSD + logisticsPerUnit + fba + ref + inboundPlacementFee + storage + adCost;
        const profit = testPrice - total;
        pricePoints.push({
          pct,
          price: testPrice.toFixed(2),
          profit: profit.toFixed(2),
          margin: ((profit / testPrice) * 100).toFixed(1),
          dailySalesEst: Math.max(1, Math.round(10 * (1 - pct / 100))),
        });
      }
      return { product: p, pricePoints };
    });
  }, [prices, exchangeRate, logisticsCostPerKg, adROAS]);

  return (
    <div style={{ fontFamily: "'DM Sans', 'Noto Sans SC', sans-serif", background: "#0a0e17", color: "#e2e8f0", minHeight: "100vh", padding: "0" }}>
      <link href="https://fonts.googleapis.com/css2?family=DM+Sans:wght@400;500;600;700&family=Noto+Sans+SC:wght@400;500;700&family=JetBrains+Mono:wght@400;500&display=swap" rel="stylesheet" />
      
      {/* Header */}
      <div style={{ background: "linear-gradient(135deg, #0f172a 0%, #1e293b 50%, #0f172a 100%)", borderBottom: "1px solid #1e3a5f", padding: "24px 28px" }}>
        <div style={{ display: "flex", justifyContent: "space-between", alignItems: "center", flexWrap: "wrap", gap: 12 }}>
          <div>
            <h1 style={{ fontSize: 22, fontWeight: 700, color: "#f1f5f9", margin: 0, letterSpacing: "-0.5px" }}>
              <span style={{ color: "#38bdf8" }}>Amazon US</span> · AI智能眼镜 FBA运营全案
            </h1>
            <p style={{ color: "#64748b", fontSize: 12, margin: "4px 0 0", fontFamily: "'JetBrains Mono', monospace" }}>
              更新时间: 2026年4月17日 · 数据基于2026年亚马逊最新费率（含4/17燃油附加费）
            </p>
          </div>
          <div style={{ display: "flex", gap: 8, flexWrap: "wrap" }}>
            {[
              { label: "汇率 USD/CNY", value: exchangeRate, set: setExchangeRate, step: 0.01 },
              { label: "头程均价 ¥/kg", value: logisticsCostPerKg, set: setLogisticsCostPerKg, step: 1 },
              { label: "广告ROAS", value: adROAS, set: setAdROAS, step: 0.1 },
            ].map((p, i) => (
              <div key={i} style={{ background: "#1e293b", border: "1px solid #334155", borderRadius: 8, padding: "6px 10px", display: "flex", flexDirection: "column", gap: 2 }}>
                <span style={{ fontSize: 10, color: "#94a3b8", fontWeight: 500 }}>{p.label}</span>
                <input
                  type="number"
                  value={p.value}
                  onChange={e => p.set(Number(e.target.value))}
                  step={p.step}
                  style={{ background: "transparent", border: "none", color: "#38bdf8", fontSize: 16, fontWeight: 700, fontFamily: "'JetBrains Mono'", width: 70, outline: "none" }}
                />
              </div>
            ))}
          </div>
        </div>
      </div>

      {/* Tabs */}
      <div style={{ display: "flex", gap: 0, borderBottom: "1px solid #1e3a5f", background: "#0d1424", overflowX: "auto", scrollbarWidth: "none" }}>
        {TABS.map(t => (
          <button
            key={t.key}
            onClick={() => setTab(t.key)}
            style={{
              padding: "12px 18px",
              background: tab === t.key ? "#1e293b" : "transparent",
              color: tab === t.key ? "#38bdf8" : "#64748b",
              border: "none",
              borderBottom: tab === t.key ? "2px solid #38bdf8" : "2px solid transparent",
              cursor: "pointer",
              fontSize: 13,
              fontWeight: 600,
              fontFamily: "'DM Sans', 'Noto Sans SC'",
              whiteSpace: "nowrap",
              transition: "all 0.2s",
            }}
          >
            {t.icon} {t.label}
          </button>
        ))}
      </div>

      {/* Content */}
      <div style={{ padding: "20px 24px", maxWidth: 1400, margin: "0 auto" }}>
        {tab === "profit" && <ProfitTab calculations={calculations} prices={prices} setPrices={setPrices} exchangeRate={exchangeRate} adROAS={adROAS} />}
        {tab === "ops" && <OpsTab calculations={calculations} adROAS={adROAS} adSpendPct={adSpendPct} setAdSpendPct={setAdSpendPct} prices={prices} />}
        {tab === "inventory" && <InventoryTab products={PRODUCTS} airQty={airQty} setAirQty={setAirQty} seaQty={seaQty} setSeaQty={setSeaQty} exchangeRate={exchangeRate} airFreightCost={airFreightCost} setAirFreightCost={setAirFreightCost} seaFreightCost={seaFreightCost} setSeaFreightCost={setSeaFreightCost} />}
        {tab === "sensitivity" && <SensitivityTab data={sensitivityData} />}
        {tab === "logistics" && <LogisticsTab products={PRODUCTS} exchangeRate={exchangeRate} airFreightCost={airFreightCost} setAirFreightCost={setAirFreightCost} seaFreightCost={seaFreightCost} setSeaFreightCost={setSeaFreightCost} />}
        {tab === "fees" && <FeesTab calculations={calculations} />}
      </div>
    </div>
  );
}

const Card = ({ title, children, accent = "#38bdf8" }) => (
  <div style={{ background: "#111827", border: "1px solid #1e3a5f", borderRadius: 12, padding: "18px 20px", marginBottom: 16 }}>
    {title && <h3 style={{ fontSize: 15, fontWeight: 700, color: accent, margin: "0 0 14px", borderLeft: `3px solid ${accent}`, paddingLeft: 10 }}>{title}</h3>}
    {children}
  </div>
);

const Table = ({ headers, rows, highlightCol }) => (
  <div style={{ overflowX: "auto" }}>
    <table style={{ width: "100%", borderCollapse: "collapse", fontSize: 13 }}>
      <thead>
        <tr>
          {headers.map((h, i) => (
            <th key={i} style={{ padding: "8px 10px", textAlign: i === 0 ? "left" : "right", color: "#94a3b8", fontWeight: 600, borderBottom: "1px solid #1e3a5f", whiteSpace: "nowrap", fontSize: 12 }}>{h}</th>
          ))}
        </tr>
      </thead>
      <tbody>
        {rows.map((row, ri) => (
          <tr key={ri} style={{ borderBottom: "1px solid #1e293b" }}>
            {row.map((cell, ci) => (
              <td key={ci} style={{
                padding: "9px 10px",
                textAlign: ci === 0 ? "left" : "right",
                fontFamily: ci > 0 ? "'JetBrains Mono'" : undefined,
                fontSize: ci > 0 ? 13 : 13,
                color: ci === highlightCol ? (parseFloat(cell) >= 0 ? "#4ade80" : "#f87171") : "#cbd5e1",
                fontWeight: ci === highlightCol ? 700 : 400,
                whiteSpace: "nowrap",
              }}>{cell}</td>
            ))}
          </tr>
        ))}
      </tbody>
    </table>
  </div>
);

const InputCell = ({ value, onChange, prefix = "$", width = 80 }) => (
  <div style={{ display: "inline-flex", alignItems: "center", background: "#1e293b", border: "1px solid #334155", borderRadius: 6, padding: "3px 8px" }}>
    <span style={{ color: "#64748b", fontSize: 12, marginRight: 2 }}>{prefix}</span>
    <input
      type="number"
      value={value}
      onChange={e => onChange(Number(e.target.value))}
      style={{ background: "transparent", border: "none", color: "#f1f5f9", fontSize: 14, fontFamily: "'JetBrains Mono'", width, outline: "none" }}
    />
  </div>
);

function ProfitTab({ calculations, prices, setPrices, exchangeRate, adROAS }) {
  return (
    <>
      <Card title="📐 产品基础参数">
        <Table
          headers={["产品名称", "采购成本(¥)", "采购成本($)", "包装尺寸", "单件重量(kg)", "外箱规格", "外箱重量(kg)", "装箱数/箱"]}
          rows={PRODUCTS.map(p => [
            p.name,
            `¥${p.costCNY}`,
            `$${(p.costCNY / exchangeRate).toFixed(2)}`,
            p.packageDim,
            p.packageWeight.toString(),
            p.outerDim,
            p.outerWeight.toString(),
            p.unitsPerCarton.toString(),
          ])}
        />
      </Card>

      <Card title="💵 售价设置（可修改）">
        <div style={{ display: "flex", gap: 20, flexWrap: "wrap" }}>
          {PRODUCTS.map(p => (
            <div key={p.id} style={{ display: "flex", flexDirection: "column", gap: 4 }}>
              <span style={{ color: "#94a3b8", fontSize: 12 }}>{p.name}</span>
              <InputCell value={prices[p.id]} onChange={v => setPrices(prev => ({ ...prev, [p.id]: v }))} />
            </div>
          ))}
        </div>
      </Card>

      <Card title="🧮 利润核算明细（单位: USD）">
        <Table
          headers={["费用项目", calculations[0].name, calculations[1].name, calculations[2].name]}
          highlightCol={-1}
          rows={[
            ["售价", `$${calculations[0].price}`, `$${calculations[1].price}`, `$${calculations[2].price}`],
            ["采购成本", `$${calculations[0].costUSD}`, `$${calculations[1].costUSD}`, `$${calculations[2].costUSD}`],
            ["头程物流(均价)", `$${calculations[0].logisticsPerUnit}`, `$${calculations[1].logisticsPerUnit}`, `$${calculations[2].logisticsPerUnit}`],
            ["FBA配送费(含燃油)", `$${calculations[0].fbaWithFuel}`, `$${calculations[1].fbaWithFuel}`, `$${calculations[2].fbaWithFuel}`],
            ["平台佣金(8%)", `$${calculations[0].referralFee}`, `$${calculations[1].referralFee}`, `$${calculations[2].referralFee}`],
            ["入仓配置费", `$${calculations[0].inboundPlacement}`, `$${calculations[1].inboundPlacement}`, `$${calculations[2].inboundPlacement}`],
            ["仓储费(2个月)", `$${calculations[0].monthlyStorage}`, `$${calculations[1].monthlyStorage}`, `$${calculations[2].monthlyStorage}`],
            ["亚马逊费用小计", `$${calculations[0].totalAmazonFees}`, `$${calculations[1].totalAmazonFees}`, `$${calculations[2].totalAmazonFees}`],
            [`广告费(ROAS=${adROAS})`, `$${calculations[0].adCostPerUnit}`, `$${calculations[1].adCostPerUnit}`, `$${calculations[2].adCostPerUnit}`],
            ["总成本", `$${calculations[0].totalCost}`, `$${calculations[1].totalCost}`, `$${calculations[2].totalCost}`],
          ]}
        />
        <div style={{ marginTop: 12, borderTop: "2px solid #1e3a5f", paddingTop: 12 }}>
          <Table
            headers={["指标", calculations[0].name, calculations[1].name, calculations[2].name]}
            highlightCol={-1}
            rows={[
              [
                "单件利润",
                ...(calculations.map(c => {
                  const val = parseFloat(c.profit);
                  return <span style={{ color: val >= 0 ? "#4ade80" : "#f87171", fontWeight: 700, fontFamily: "'JetBrains Mono'" }}>${c.profit}</span>;
                }))
              ],
              [
                "利润率",
                ...(calculations.map(c => {
                  const val = parseFloat(c.profitMargin);
                  return <span style={{ color: val >= 0 ? "#4ade80" : "#f87171", fontWeight: 700, fontFamily: "'JetBrains Mono'" }}>{c.profitMargin}%</span>;
                }))
              ],
            ]}
          />
        </div>
      </Card>

      <Card title="📝 费率说明">
        <div style={{ fontSize: 12, color: "#94a3b8", lineHeight: 1.8 }}>
          <p>• <b style={{ color: "#cbd5e1" }}>平台佣金</b>: 电子品类8%（2026年费率不变）</p>
          <p>• <b style={{ color: "#cbd5e1" }}>FBA配送费</b>: Large Standard 8-12oz档位 + 3.5%燃油附加费（2026年4月17日起生效）</p>
          <p>• <b style={{ color: "#cbd5e1" }}>入仓配置费</b>: Large Standard单一仓库发货$0.30/件（使用Amazon-optimized分仓可免除）</p>
          <p>• <b style={{ color: "#cbd5e1" }}>仓储费</b>: 标准尺寸$0.78/立方英尺/月（1-9月），$2.40/立方英尺/月（10-12月）</p>
          <p>• <b style={{ color: "#cbd5e1" }}>广告费</b>: 按ROAS={adROAS}计算，即每产生${adROAS}销售额花费$1广告费</p>
          <p>• <b style={{ color: "#f59e0b" }}>注意</b>: AI眼镜含锂电池，可能需要危险品(Hazmat)审核，DG品类FBA费用更高约$0.80/件</p>
        </div>
      </Card>
    </>
  );
}

function OpsTab({ calculations, adROAS, adSpendPct, setAdSpendPct, prices }) {
  const phases = [
    { phase: "第一阶段", period: "第1-2月", goal: "产品上架 · 积累评论", adBudget: "每SKU $20-30/天", strategy: "自动广告为主，精准长尾词手动广告", targetACoS: "40-50%", dailySales: "3-5单/SKU" },
    { phase: "第二阶段", period: "第3-4月", goal: "推排名 · 稳定出单", adBudget: "每SKU $40-60/天", strategy: "扩展手动广告，商品定位广告，品牌视频广告", targetACoS: "25-35%", dailySales: "8-15单/SKU" },
    { phase: "第三阶段", period: "第5-6月", goal: "盈利优化 · 规模扩张", adBudget: "每SKU $50-80/天", strategy: "优化ACoS，增加品牌广告占比，防御性广告", targetACoS: "15-25%", dailySales: "15-30单/SKU" },
  ];

  return (
    <>
      <Card title="📅 运营阶段规划（6个月周期）">
        <div style={{ display: "grid", gridTemplateColumns: "repeat(auto-fit, minmax(300px, 1fr))", gap: 16 }}>
          {phases.map((p, i) => (
            <div key={i} style={{ background: "#0d1424", border: "1px solid #1e3a5f", borderRadius: 10, padding: 16 }}>
              <div style={{ display: "flex", justifyContent: "space-between", marginBottom: 8 }}>
                <span style={{ color: "#38bdf8", fontWeight: 700, fontSize: 15 }}>{p.phase}</span>
                <span style={{ color: "#64748b", fontSize: 12, fontFamily: "'JetBrains Mono'" }}>{p.period}</span>
              </div>
              <div style={{ fontSize: 13, color: "#e2e8f0", fontWeight: 600, marginBottom: 10 }}>{p.goal}</div>
              {[
                ["广告预算", p.adBudget],
                ["广告策略", p.strategy],
                ["目标ACoS", p.targetACoS],
                ["日均销量", p.dailySales],
              ].map(([k, v], j) => (
                <div key={j} style={{ display: "flex", justifyContent: "space-between", padding: "5px 0", borderBottom: "1px solid #1e293b", fontSize: 12 }}>
                  <span style={{ color: "#94a3b8" }}>{k}</span>
                  <span style={{ color: "#cbd5e1", fontFamily: j < 2 ? undefined : "'JetBrains Mono'" }}>{v}</span>
                </div>
              ))}
            </div>
          ))}
        </div>
      </Card>

      <Card title="💡 广告费用月度预估（3个SKU合计）">
        <Table
          headers={["月份", "日均广告花费", "月广告总额", "预估月销量", "预估月销售额", "ACoS", "ROAS"]}
          rows={[
            ["第1月", "$75/天", "$2,250", "300件", `$${(300 * 86.66).toFixed(0)}`, "35-45%", "2.2-2.9"],
            ["第2月", "$120/天", "$3,600", "600件", `$${(600 * 86.66).toFixed(0)}`, "30-40%", "2.5-3.3"],
            ["第3月", "$150/天", "$4,500", "900件", `$${(900 * 86.66).toFixed(0)}`, "25-30%", "3.3-4.0"],
            ["第4月", "$180/天", "$5,400", "1,200件", `$${(1200 * 86.66).toFixed(0)}`, "20-28%", "3.6-5.0"],
            ["第5月", "$200/天", "$6,000", "1,500件", `$${(1500 * 86.66).toFixed(0)}`, "15-25%", "4.0-6.7"],
            ["第6月", "$210/天", "$6,300", "1,800件", `$${(1800 * 86.66).toFixed(0)}`, "12-20%", "5.0-8.3"],
          ]}
        />
      </Card>

      <Card title="🎯 关键运营动作清单">
        <div style={{ fontSize: 12, color: "#94a3b8", lineHeight: 2.0 }}>
          {[
            "Listing优化: 主图6+1视频, A+页面, 5点描述含核心关键词",
            "上架前准备: 品牌备案(Brand Registry), UPC码, 锂电池安全测试报告(UN38.3)",
            "评论积累: Vine计划(每SKU最多30个), Request a Review, 产品插卡引导",
            "定价策略: 上架初期低价引流(coupon/promotion), 稳定后逐步提价至目标价位",
            "库存管理: 保持28天以上库存(避免Low Inventory Level Fee), IPI指标>400",
            "竞品监控: 每周分析竞品价格、评论、广告位变化",
            "合规要点: FCC认证, 锂电池标识, 产品责任保险(>$10K月销需要)",
          ].map((item, i) => (
            <p key={i} style={{ margin: "4px 0" }}>
              <span style={{ color: "#38bdf8", marginRight: 6 }}>▸</span>
              <span style={{ color: "#cbd5e1" }}>{item.split(":")[0]}:</span> {item.split(":").slice(1).join(":")}
            </p>
          ))}
        </div>
      </Card>
    </>
  );
}

function InventoryTab({ products, airQty, setAirQty, seaQty, setSeaQty, exchangeRate, airFreightCost, setAirFreightCost, seaFreightCost, setSeaFreightCost }) {
  const airDays = 7;
  const seaDays = 35;
  const fbaReceiveDays = 5;

  const totalWeight = (qty, p) => (qty * p.packageWeight).toFixed(1);
  const totalCartons = (qty, p) => Math.ceil(qty / p.unitsPerCarton);
  const logisticsCost = (qty, p, rate) => ((qty * p.packageWeight * rate) / exchangeRate).toFixed(2);

  return (
    <>
      <Card title="✈️ 头程物流费率设置（可修改）">
        <div style={{ display: "flex", gap: 20, flexWrap: "wrap", marginBottom: 10 }}>
          <div style={{ display: "flex", flexDirection: "column", gap: 4 }}>
            <span style={{ color: "#94a3b8", fontSize: 12 }}>空运红单 ¥/kg</span>
            <InputCell value={airFreightCost} onChange={setAirFreightCost} prefix="¥" />
          </div>
          <div style={{ display: "flex", flexDirection: "column", gap: 4 }}>
            <span style={{ color: "#94a3b8", fontSize: 12 }}>海运 ¥/kg</span>
            <InputCell value={seaFreightCost} onChange={setSeaFreightCost} prefix="¥" />
          </div>
        </div>
      </Card>

      <Card title="✈️ 第一批·空运红单备货计划">
        <p style={{ color: "#f59e0b", fontSize: 12, marginBottom: 12 }}>预计到仓时间: {airDays}天运输 + {fbaReceiveDays}天入仓 = 约12天</p>
        <div style={{ display: "flex", gap: 16, flexWrap: "wrap", marginBottom: 12 }}>
          {products.map(p => (
            <div key={p.id} style={{ display: "flex", flexDirection: "column", gap: 4 }}>
              <span style={{ color: "#94a3b8", fontSize: 12 }}>{p.name} 数量</span>
              <InputCell value={airQty[p.id]} onChange={v => setAirQty(prev => ({ ...prev, [p.id]: v }))} prefix="" width={60} />
            </div>
          ))}
        </div>
        <Table
          headers={["产品", "数量", "箱数", "总重量(kg)", "物流费($)", "采购金额(¥)", "采购金额($)", "总投入($)"]}
          rows={products.map(p => {
            const qty = airQty[p.id];
            const freight = logisticsCost(qty, p, airFreightCost);
            const purchaseCNY = qty * p.costCNY;
            const purchaseUSD = (purchaseCNY / exchangeRate).toFixed(2);
            return [
              p.name,
              qty.toString(),
              totalCartons(qty, p).toString(),
              totalWeight(qty, p),
              `$${freight}`,
              `¥${purchaseCNY.toLocaleString()}`,
              `$${purchaseUSD}`,
              `$${(parseFloat(freight) + parseFloat(purchaseUSD)).toFixed(2)}`,
            ];
          }).concat([
            (() => {
              const totals = products.reduce((acc, p) => {
                const qty = airQty[p.id];
                const freight = parseFloat(logisticsCost(qty, p, airFreightCost));
                const purchaseUSD = (qty * p.costCNY) / exchangeRate;
                return { qty: acc.qty + qty, cartons: acc.cartons + totalCartons(qty, p), weight: acc.weight + qty * p.packageWeight, freight: acc.freight + freight, cny: acc.cny + qty * p.costCNY, usd: acc.usd + purchaseUSD };
              }, { qty: 0, cartons: 0, weight: 0, freight: 0, cny: 0, usd: 0 });
              return ["合计", totals.qty.toString(), totals.cartons.toString(), totals.weight.toFixed(1), `$${totals.freight.toFixed(2)}`, `¥${totals.cny.toLocaleString()}`, `$${totals.usd.toFixed(2)}`, `$${(totals.freight + totals.usd).toFixed(2)}`];
            })()
          ])}
        />
      </Card>

      <Card title="🚢 第一批·海运备货计划">
        <p style={{ color: "#38bdf8", fontSize: 12, marginBottom: 12 }}>预计到仓时间: {seaDays}天运输 + {fbaReceiveDays}天入仓 = 约40天</p>
        <div style={{ display: "flex", gap: 16, flexWrap: "wrap", marginBottom: 12 }}>
          {products.map(p => (
            <div key={p.id} style={{ display: "flex", flexDirection: "column", gap: 4 }}>
              <span style={{ color: "#94a3b8", fontSize: 12 }}>{p.name} 数量</span>
              <InputCell value={seaQty[p.id]} onChange={v => setSeaQty(prev => ({ ...prev, [p.id]: v }))} prefix="" width={60} />
            </div>
          ))}
        </div>
        <Table
          headers={["产品", "数量", "箱数", "总重量(kg)", "物流费($)", "采购金额(¥)", "采购金额($)", "总投入($)"]}
          rows={products.map(p => {
            const qty = seaQty[p.id];
            const freight = logisticsCost(qty, p, seaFreightCost);
            const purchaseCNY = qty * p.costCNY;
            const purchaseUSD = (purchaseCNY / exchangeRate).toFixed(2);
            return [
              p.name,
              qty.toString(),
              totalCartons(qty, p).toString(),
              totalWeight(qty, p),
              `$${freight}`,
              `¥${purchaseCNY.toLocaleString()}`,
              `$${purchaseUSD}`,
              `$${(parseFloat(freight) + parseFloat(purchaseUSD)).toFixed(2)}`,
            ];
          }).concat([
            (() => {
              const totals = products.reduce((acc, p) => {
                const qty = seaQty[p.id];
                const freight = parseFloat(logisticsCost(qty, p, seaFreightCost));
                const purchaseUSD = (qty * p.costCNY) / exchangeRate;
                return { qty: acc.qty + qty, cartons: acc.cartons + totalCartons(qty, p), weight: acc.weight + qty * p.packageWeight, freight: acc.freight + freight, cny: acc.cny + qty * p.costCNY, usd: acc.usd + purchaseUSD };
              }, { qty: 0, cartons: 0, weight: 0, freight: 0, cny: 0, usd: 0 });
              return ["合计", totals.qty.toString(), totals.cartons.toString(), totals.weight.toFixed(1), `$${totals.freight.toFixed(2)}`, `¥${totals.cny.toLocaleString()}`, `$${totals.usd.toFixed(2)}`, `$${(totals.freight + totals.usd).toFixed(2)}`];
            })()
          ])}
        />
      </Card>

      <Card title="📊 备货时间线">
        <div style={{ fontSize: 12, color: "#94a3b8", lineHeight: 2.2 }}>
          {[
            { time: "D0", event: "下单采购 + 工厂备货", note: "预计5-7天生产周期" },
            { time: "D7", event: "空运红单发货", note: `${airQty[1]+airQty[2]+airQty[3]}件，约${airDays}天到美国` },
            { time: "D7", event: "海运同步发货", note: `${seaQty[1]+seaQty[2]+seaQty[3]}件，约${seaDays}天到美国` },
            { time: "D14", event: "空运货物到达FBA仓库", note: "开始入仓上架流程" },
            { time: "D19", event: "空运货物上架可售", note: "开启广告，开始销售" },
            { time: "D42", event: "海运货物到达FBA仓库", note: "空运库存应仍有余量" },
            { time: "D47", event: "海运货物上架可售", note: "库存充足，加大广告投放" },
          ].map((item, i) => (
            <div key={i} style={{ display: "flex", gap: 16, alignItems: "flex-start" }}>
              <span style={{ color: "#38bdf8", fontFamily: "'JetBrains Mono'", fontWeight: 700, minWidth: 40 }}>{item.time}</span>
              <span style={{ color: "#e2e8f0", fontWeight: 600, minWidth: 180 }}>{item.event}</span>
              <span style={{ color: "#64748b" }}>{item.note}</span>
            </div>
          ))}
        </div>
      </Card>
    </>
  );
}

function SensitivityTab({ data }) {
  return (
    <>
      {data.map((d, i) => (
        <Card key={i} title={`📊 ${d.product.name} · 价格敏感度分析`}>
          <Table
            headers={["价格变动", "售价($)", "单件利润($)", "利润率(%)", "预估日销量"]}
            highlightCol={2}
            rows={d.pricePoints.map(pp => [
              `${pp.pct > 0 ? "+" : ""}${pp.pct}%`,
              `$${pp.price}`,
              `$${pp.profit}`,
              `${pp.margin}%`,
              `${pp.dailySalesEst}件/天`,
            ])}
          />
          <div style={{ marginTop: 12, display: "flex", gap: 4, height: 80, alignItems: "flex-end" }}>
            {d.pricePoints.map((pp, j) => {
              const val = parseFloat(pp.margin);
              const h = Math.max(5, Math.min(70, (val + 10) * 2));
              return (
                <div key={j} style={{ flex: 1, display: "flex", flexDirection: "column", alignItems: "center", gap: 2 }}>
                  <span style={{ fontSize: 9, color: val >= 0 ? "#4ade80" : "#f87171", fontFamily: "'JetBrains Mono'" }}>{pp.margin}%</span>
                  <div style={{ width: "80%", height: h, background: val >= 0 ? `linear-gradient(180deg, #4ade80, #166534)` : `linear-gradient(180deg, #f87171, #991b1b)`, borderRadius: "3px 3px 0 0" }} />
                  <span style={{ fontSize: 9, color: "#64748b" }}>{pp.pct > 0 ? "+" : ""}{pp.pct}%</span>
                </div>
              );
            })}
          </div>
        </Card>
      ))}

      <Card title="🔑 定价建议">
        <div style={{ fontSize: 12, color: "#94a3b8", lineHeight: 2.0 }}>
          <p><span style={{ color: "#4ade80" }}>▸</span> <b style={{ color: "#cbd5e1" }}>E08骑行款($129.99)</b>: 利润空间充足，可适当做coupon引流，建议售价区间$109-$149</p>
          <p><span style={{ color: "#4ade80" }}>▸</span> <b style={{ color: "#cbd5e1" }}>E09($79.99)</b>: 中等利润率，建议稳定在$69-$89区间，兼顾竞争力与利润</p>
          <p><span style={{ color: "#f59e0b" }}>▸</span> <b style={{ color: "#cbd5e1" }}>E05C变色款($49.99)</b>: 利润率较低，提价空间有限，重点控制广告ACoS和物流成本</p>
        </div>
      </Card>
    </>
  );
}

function LogisticsTab({ products, exchangeRate, airFreightCost, setAirFreightCost, seaFreightCost, setSeaFreightCost }) {
  return (
    <>
      <Card title="🚀 头程物流方式对比">
        <Table
          headers={["对比项", "空运红单 ✈️", "海运 🚢", "空派(空运+卡派)"]}
          rows={[
            ["单价(¥/kg)", `¥${airFreightCost}`, `¥${seaFreightCost}`, "¥20-26"],
            ["时效(门到门)", "5-7天", "30-40天", "10-15天"],
            ["单件物流费($)", `$${((0.24 * airFreightCost) / exchangeRate).toFixed(2)}`, `$${((0.24 * seaFreightCost) / exchangeRate).toFixed(2)}`, `$${((0.24 * 23) / exchangeRate).toFixed(2)}`],
            ["适合场景", "紧急补货/首批小量", "大批量备货", "中等批量/常规补货"],
            ["最低起运量", "无限制", "1CBM起", "100kg起"],
            ["风险", "成本高", "时间长/可能延误", "性价比较高"],
          ]}
        />
      </Card>

      <Card title="📦 单件物流成本对比（按产品）">
        <Table
          headers={["产品", "重量(kg)", "空运费($)", "海运费($)", "差额($)", "100件差额($)"]}
          rows={products.map(p => {
            const airCost = (p.packageWeight * airFreightCost) / exchangeRate;
            const seaCost = (p.packageWeight * seaFreightCost) / exchangeRate;
            const diff = airCost - seaCost;
            return [
              p.name,
              p.packageWeight.toString(),
              `$${airCost.toFixed(2)}`,
              `$${seaCost.toFixed(2)}`,
              `$${diff.toFixed(2)}`,
              `$${(diff * 100).toFixed(2)}`,
            ];
          })}
        />
      </Card>

      <Card title="📐 外箱物流数据">
        <Table
          headers={["参数", "数值"]}
          rows={[
            ["外箱尺寸", "44.5 × 42.5 × 29.5 cm"],
            ["外箱重量", "12.19 kg"],
            ["装箱数", "50件/箱"],
            ["单箱体积", `${(44.5 * 42.5 * 29.5 / 1000000).toFixed(4)} CBM`],
            ["体积重(÷5000)", `${(44.5 * 42.5 * 29.5 / 5000).toFixed(1)} kg`],
            ["实际重量", "12.19 kg"],
            ["计费重量", `${Math.max(12.19, 44.5 * 42.5 * 29.5 / 5000).toFixed(1)} kg`],
            ["空运整箱费用", `¥${(Math.max(12.19, 44.5 * 42.5 * 29.5 / 5000) * airFreightCost).toFixed(0)} → $${(Math.max(12.19, 44.5 * 42.5 * 29.5 / 5000) * airFreightCost / exchangeRate).toFixed(2)}`],
            ["海运整箱费用", `¥${(12.19 * seaFreightCost).toFixed(0)} → $${(12.19 * seaFreightCost / exchangeRate).toFixed(2)}`],
          ]}
        />
        <p style={{ fontSize: 11, color: "#f59e0b", marginTop: 8 }}>⚠️ 空运按体积重与实际重量取大值计费; 海运按实际重量或体积(CBM)计费</p>
      </Card>
    </>
  );
}

function FeesTab({ calculations }) {
  return (
    <>
      <Card title="🏷️ 2026年亚马逊FBA费用结构（4月17日更新）">
        <Table
          headers={["费用类型", "费率/金额", "计算方式", "备注"]}
          rows={[
            ["平台佣金(Referral Fee)", "8%", "售价 × 8%", "电子品类统一费率，2026年未调整"],
            ["FBA配送费", "$4.20/件", "Large Standard 8-12oz", "$10-$50价位档; >$50为$4.46"],
            ["燃油及物流附加费", "3.5%", "FBA配送费 × 3.5%", "2026年4月17日起生效，叠加计算"],
            ["入仓配置费", "$0.20-$0.40", "单一仓发货时收取", "使用Amazon优化分仓(5箱+)可免"],
            ["月度仓储费(1-9月)", "$0.78/立方英尺", "日均库存体积计算", "标准尺寸; Q4(10-12月)$2.40"],
            ["低库存费", "变动", "库存<28天供应量时", "按FNSKU级别计算"],
            ["超龄库存费(181天+)", "$0.50-$7.90/立方英尺", "库存超181天开始收取", "2026年新增456天+档位"],
            ["退货处理费", "变动", "退货率超品类阈值时", "低退货率产品不收取"],
            ["移除/废弃费", "$0.84+/件", "主动移除库存时", "2026年降低了轻小件费用"],
          ]}
        />
      </Card>

      <Card title="💲 三款产品FBA费用分解对比">
        <Table
          headers={["费用项", calculations[0].name, calculations[1].name, calculations[2].name]}
          rows={[
            ["售价", `$${calculations[0].price}`, `$${calculations[1].price}`, `$${calculations[2].price}`],
            ["佣金(8%)", `$${calculations[0].referralFee}`, `$${calculations[1].referralFee}`, `$${calculations[2].referralFee}`],
            ["FBA配送费(base)", `$${calculations[0].fbaFee}`, `$${calculations[1].fbaFee}`, `$${calculations[2].fbaFee}`],
            ["燃油附加(3.5%)", `$${(parseFloat(calculations[0].fbaFee) * 0.035).toFixed(2)}`, `$${(parseFloat(calculations[1].fbaFee) * 0.035).toFixed(2)}`, `$${(parseFloat(calculations[2].fbaFee) * 0.035).toFixed(2)}`],
            ["FBA配送费(含燃油)", `$${calculations[0].fbaWithFuel}`, `$${calculations[1].fbaWithFuel}`, `$${calculations[2].fbaWithFuel}`],
            ["入仓配置费", `$${calculations[0].inboundPlacement}`, `$${calculations[1].inboundPlacement}`, `$${calculations[2].inboundPlacement}`],
            ["仓储费(2月)", `$${calculations[0].monthlyStorage}`, `$${calculations[1].monthlyStorage}`, `$${calculations[2].monthlyStorage}`],
            ["亚马逊费用合计", `$${calculations[0].totalAmazonFees}`, `$${calculations[1].totalAmazonFees}`, `$${calculations[2].totalAmazonFees}`],
            ["占售价比例", `${(parseFloat(calculations[0].totalAmazonFees) / calculations[0].price * 100).toFixed(1)}%`, `${(parseFloat(calculations[1].totalAmazonFees) / calculations[1].price * 100).toFixed(1)}%`, `${(parseFloat(calculations[2].totalAmazonFees) / calculations[2].price * 100).toFixed(1)}%`],
          ]}
        />
      </Card>

      <Card title="📐 产品尺寸分级">
        <div style={{ fontSize: 12, color: "#94a3b8", lineHeight: 2.0 }}>
          <p><b style={{ color: "#38bdf8" }}>产品包装尺寸:</b> 20.3 × 8.5 × 5.5 cm = 7.99 × 3.35 × 2.17 英寸</p>
          <p><b style={{ color: "#38bdf8" }}>产品包装重量:</b> 0.24 kg = 0.53 lb = 8.47 oz</p>
          <p><b style={{ color: "#38bdf8" }}>FBA尺寸分级:</b> <span style={{ color: "#4ade80", fontWeight: 700 }}>Large Standard</span>（最短边2.17" > 0.75"，不符合Small Standard）</p>
          <p><b style={{ color: "#38bdf8" }}>重量档位:</b> 8+ to 12 oz 档位</p>
          <p><b style={{ color: "#38bdf8" }}>价格档位:</b> 根据售价分为 &lt;$10 / $10-$50 / &gt;$50 三档</p>
          <p style={{ color: "#f59e0b", marginTop: 8 }}>⚠️ AI眼镜含锂电池，可能被归类为危险品(Dangerous Goods)。DG品类FBA费用约高$0.55-$0.80/件。建议提前进行Hazmat审核。</p>
        </div>
      </Card>
    </>
  );
}
