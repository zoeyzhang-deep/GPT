# 代执行全名单（实操步骤）

> 目标：把你给的全部项目逐个算出 listing FDV。

## 一次性准备

1. 打开 `fdv_full_list.csv`（已预置全名单）。
2. 对每行按下述顺序补齐：`chain,ca,total_supply,dextools_pair_url,init_tx_hash,listing_price_usd,listing_fdv_usd,notes`。

## 每个项目的标准动作

1. CMC/CG 搜索 `symbol + project_name`，确认同名冲突后取正确 CA 与 total supply。
2. 打开 `https://www.dextools.io/app/pairs`，搜索 CA。
3. 在 Pancake 相关池子中，选 liquidity 最高的 pair。
4. 进入 pair 页面 -> Trade History -> 时间升序。
5. 找第一笔 `type = init` 的成交，记录 USD 价格与 tx hash。
6. 计算：`listing_fdv_usd = listing_price_usd * total_supply`。
7. 回填 CSV。

## 质检规则

- 同名 symbol（如 SENT、BREV）必须用 project_name 做二次确认。
- 若无 Pancake 池：`notes=No pancake pair`。
- 若有池但无 init：`notes=No init in visible trade history`。
- total supply 读不到：`notes=Supply unavailable on CMC/CG`。

## EVAA 对照样例

- CA: `0xaa036928c9c0df07d525b55ea8ee690bb5a628c1`
- Pair: `0x26deb24a2623cf54452ab5183e2c34551831d54d`
- init: `$2`
- total supply: `50,000,000`
- listing fdv: `100,000,000`

