# Engineering Economics

## Introduction

When we recommend that a facility install new equipment or modify a process, we are asking them to spend money today in exchange for savings in the future. Engineering economics provides the framework for evaluating whether that trade is worthwhile. 

## Part 1: Cash Flows

A cash flow is money moving into or out of an organization at a specific point in time. Cash flows are the foundation of all financial analysis.

- **Cash inflows** (positive) include revenue, savings, rebates, and tax credits.

- **Cash outflows** (negative) include equipment purchases, installation costs, maintenance expenses, and operating costs.

We represent cash flows on a timeline where year 0 is the present (when the investment decision is made) and subsequent years represent the future.

**Example:** A lighting retrofit costs $25,000 to install, qualifies for a $5,000 utility rebate, and saves $8,000 per year in electricity costs.

| Year | Cash Flow | Description |
|------|-----------|-------------|
| 0 | -$25,000 | Implementation cost |
| 0 | +$5,000 | Utility rebate |
| 1 | +$8,000 | Annual savings |
| 2 | +$8,000 | Annual savings |
| 3 | +$8,000 | Annual savings |
| ... | ... | ... |

The net cash flow at year 0 is -$20,000 (the $25,000 cost offset by the $5,000 rebate).

### Elements of an ITAC Recommendation

Every assessment recommendation involves some combination of the following cash flow elements:

**Implementation Cost (Year 0 Outflow)**

This is the total cost to implement the recommendation, including equipment, materials, labor, engineering, and any other expenses required to complete the project. This is always a negative cash flow at year 0.

**Tax Credits and Incentives (Year 0 Inflow)**

Utility rebates, tax credits, and other incentives reduce the effective cost of a project. These are positive cash flows that offset the implementation cost. For simplicity, we typically assume these are received at year 0, though in practice some incentives may be paid after project completion or spread across multiple years.

$$\text{Net Implementation Cost} = \text{Implementation Cost} - \text{Tax Credits and Incentives}$$

**Annual Savings**

The recurring benefit from reduced energy consumption, lower demand charges, avoided maintenance, or other operational improvements. This is a positive cash flow that repeats each year over the life of the measure.

**Recurring Costs**

Some measures introduce new ongoing expenses: maintenance contracts, replacement parts, consumables, or increased costs in one area that partially offset savings in another. These are subtracted from annual savings to determine the net annual cash flow.

$$\text{Net Annual Cash Flow} = \text{Annual Savings} - \text{Recurring Costs}$$

**Example:** A compressed air system optimization costs $45,000 to implement and qualifies for a $7,500 rebate. It saves $18,000 annually in electricity but requires a $2,000 annual maintenance contract.

| Element | Cash Flow |
|---------|-----------|
| Implementation Cost | -$45,000 |
| Utility Rebate | +$7,500 |
| **Net Year 0** | **-$37,500** |
| Annual Savings | +$18,000 |
| Recurring Costs | -$2,000 |
| **Net Annual** | **+$16,000** |

## Part 2: The Time Value of Money

### Why This Matters for Energy Engineers

When you present a recommendation to a plant manager, they may approve it themselves. But larger projects go to finance departments, CFOs, and executive teams for approval. These decision-makers think in terms of discount rates, present values, and NPV. They compare your energy project against every other use of company capital: new production equipment, facility expansions, acquisitions, or simply leaving money in the bank.

If you cannot speak their language, you cannot effectively advocate for your recommendations. Understanding discounting does not mean you need to perform complex financial analysis. It means you understand how your simple payback figures translate into the metrics executives actually use to make decisions.

### Why Timing Matters

A dollar today is worth more than a dollar next year. This is not just because of inflation. Even in a world with no inflation, a dollar today can be invested to earn a return, making it worth more than a dollar received later.

This concept, called the time value of money, is fundamental to engineering economics. It means we cannot simply add up cash flows from different time periods without adjustment.

### Future Value

If you invest money today at an interest rate, it grows over time. The future value tells you what a present amount will be worth at some point in the future.

$$FV = PV(1 + i)^n$$

Where:

- $FV$ = Future Value
- $PV$ = Present Value (amount today)
- $i$ = Interest rate per period (as a decimal)
- $n$ = Number of periods

**Example:** You invest $1,000 today at 8% annual interest. What is it worth in 5 years?

$$FV = \$1{,}000(1 + 0.08)^5 = \$1{,}000(1.469) = \$1{,}469$$

### Present Value

Present value works in reverse. It tells you what a future amount is worth today. This process is called discounting.

$$PV = \frac{FV}{(1 + i)^n}$$

**Example:** You will receive $1,469 in 5 years. At an 8% discount rate, what is that worth today?

$$PV = \frac{\$1{,}469}{(1 + 0.08)^5} = \frac{\$1{,}469}{1.469} = \$1{,}000$$

### The Discount Rate

The discount rate reflects the opportunity cost of capital. If a company can earn 10% on its typical investments, then a dollar next year is only worth about $0.91 today (because $0.91 invested at 10% grows to $1.00 in one year).

Different organizations use different discount rates based on their cost of capital, risk tolerance, and alternative investment opportunities. Higher discount rates make future cash flows worth less in present terms, which favors projects with quick returns.

## Part 3: Net Present Value

### Combining Cash Flows Across Time

Net Present Value (NPV) converts all cash flows to their present value and sums them. This allows us to compare the total value created by an investment in today's dollars.

$$NPV = \sum_{t=0}^{n} \frac{CF_t}{(1 + i)^t}$$

Where:

- $CF_t$ = Cash flow at time $t$
- $i$ = Discount rate
- $n$ = Number of periods
- $t$ = Time period (0, 1, 2, ...)

Note that cash flows at year 0 are not discounted (dividing by $(1+i)^0 = 1$).

### Interpreting NPV

- **NPV > 0**: The project creates value. It returns more than the discount rate.
- **NPV = 0**: The project breaks even at the discount rate.
- **NPV < 0**: The project destroys value. It returns less than the discount rate.

**Example:** A motor replacement costs $5,000 (no incentives) and saves $1,500 per year for 5 years. Using a 10% discount rate:

| Year | Cash Flow | Discount Factor | Present Value |
|------|-----------|-----------------|---------------|
| 0 | -$5,000 | 1.000 | -$5,000 |
| 1 | +$1,500 | 0.909 | +$1,364 |
| 2 | +$1,500 | 0.826 | +$1,239 |
| 3 | +$1,500 | 0.751 | +$1,127 |
| 4 | +$1,500 | 0.683 | +$1,025 |
| 5 | +$1,500 | 0.621 | +$931 |
| **Total** | | | **+$686** |

The NPV is +$686, meaning this project creates $686 of value (in today's dollars) above what could be earned by investing the $5,000 at the 10% discount rate.

## Part 4: Payback Periods

Payback period measures how long it takes to recover an initial investment. There are three versions of this metric, each with different assumptions about the time value of money.

### Simple Payback Period

Simple payback ignores the time value of money entirely. It divides the net initial investment by the annual net savings.

$$\text{Simple Payback} = \frac{\text{Implementation Cost} - \text{Incentives}}{\text{Annual Savings} - \text{Recurring Costs}}$$

**Example:** A VFD installation costs $12,000, qualifies for a $2,000 rebate, and saves $4,000 per year with no recurring costs.

$$\text{Simple Payback} = \frac{\$12{,}000 - \$2{,}000}{\$4{,}000} = \frac{\$10{,}000}{\$4{,}000} = 2.5 \text{ years}$$

Simple payback is easy to calculate and easy to communicate. However, it treats a dollar saved in year 1 the same as a dollar saved in year 10, which ignores economic reality.

**Important:** Simple payback assumes constant annual savings. When annual savings are constant, simple payback equals standard payback period (discussed below). The formula above is a shortcut that only works for even cash flows.

### Payback Period (Cumulative Cash Flow)

Standard payback period finds the point where cumulative cash flows become positive, but still does not discount future cash flows. This method handles varying annual cash flows, which simple payback cannot.

**When cash flows are constant**, payback period equals simple payback. You can use either method and get the same answer.

**When cash flows vary**, you must use the cumulative approach because the simple payback formula no longer applies.

**Example with varying cash flows:** A project costs $20,000 at year 0. Year 1 saves $5,000, year 2 saves $8,000, year 3 saves $10,000.

| Year | Cash Flow | Cumulative |
|------|-----------|------------|
| 0 | -$20,000 | -$20,000 |
| 1 | +$5,000 | -$15,000 |
| 2 | +$8,000 | -$7,000 |
| 3 | +$10,000 | +$3,000 |

Payback occurs between year 2 and year 3. Interpolating: $2 + \frac{\$7{,}000}{\$10{,}000} = 2.7$ years.

### Discounted Payback Period

Discounted payback finds when cumulative discounted cash flows become positive. This accounts for the time value of money.

**Example:** Same project as above, with a 10% discount rate.

| Year | Cash Flow | Discount Factor | PV | Cumulative PV |
|------|-----------|-----------------|-----|---------------|
| 0 | -$20,000 | 1.000 | -$20,000 | -$20,000 |
| 1 | +$5,000 | 0.909 | +$4,545 | -$15,455 |
| 2 | +$8,000 | 0.826 | +$6,608 | -$8,847 |
| 3 | +$10,000 | 0.751 | +$7,510 | -$1,337 |
| 4 | +$10,000 | 0.683 | +$6,830 | +$5,493 |

Discounted payback occurs between year 3 and year 4, longer than the undiscounted payback of 2.7 years. This reflects the reduced present value of future savings.

## Part 5: Why ITAC Uses Simple Payback

### Our Role in the Decision Process

ITAC conducts preliminary assessments to identify energy efficiency opportunities. We are not performing full financial analysis for capital budgeting decisions. Our recommendations are the starting point for a facility's internal evaluation, not the final word.

When a facility decides to pursue a recommendation, their finance team will conduct their own analysis using their specific discount rate, tax situation, depreciation schedules, and capital budgeting criteria. They have information we do not have access to: their cost of capital, their cash flow constraints, and their strategic priorities.

Simple payback is easy to calculate, easy to verify, and easy to communicate. A plant manager can look at our numbers, check the math, and immediately understand what we are claiming. This transparency builds trust in our analysis.

More sophisticated metrics require assumptions (discount rates, project lifetimes, escalation rates) that introduce uncertainty and potential disagreement. By using simple payback, we present the fundamental economics without imposing assumptions that may not match the facility's situation. Any assumption has potential to spark disagreement. By limiting assumptions, we limit potential disagreements. 

### When Simple Payback Works Well

For short-payback projects (under 2 years) with constant annual savings, simple payback is an excellent metric. The time value of money has minimal impact over short periods, and the calculation is straightforward.

Most ITAC recommendations fall into this category: lighting retrofits, motor replacements, compressed air leak repairs, insulation improvements, and similar measures. These projects have predictable, constant annual savings and relatively short payback periods.

### When Simple Payback Breaks Down

Simple payback becomes inadequate for large, complex projects with long time horizons and uneven cash flows. Examples include:

- **Battery storage systems** with savings that vary based on demand charge structures and time-of-use rates
- **Solar PV installations** with degrading output over 25+ year lifetimes and complex incentive structures
- **Geothermal systems** with high upfront costs, long lifetimes, and savings that depend on fuel price assumptions
- **Combined heat and power (CHP)** with multiple revenue streams and complex operating profiles

For these projects, the simple payback formula does not apply because annual cash flows are not constant. A 10-year simple payback tells you almost nothing about a solar installation where year 1 includes a large tax credit and years 2 through 25 show gradual panel degradation.

When we encounter these large projects, we may go a step further and calculate standard payback period or discounted payback period using out analysis software. These methods properly account for uneven cash flows and, in the case of DPP, the time value of money over long horizons where discounting significantly affects the analysis. However, we are not permitted to report these metrics in the ITAC database, so they live in the text of the costs and payback section, not in any summary tables. 