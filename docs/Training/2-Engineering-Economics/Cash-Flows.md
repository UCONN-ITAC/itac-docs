# Cash Flows

When we recommend that a facility install new equipment or modify a process, we are asking them to spend money today in exchange for savings in the future. Engineering economics provides the framework for evaluating whether that trade is worthwhile.

## What is a Cash Flow?

A cash flow is money moving into or out of an organization at a specific point in time. Cash flows are the foundation of all financial analysis.

- **Cash inflows** (positive) include revenue, savings, rebates, and tax credits.

- **Cash outflows** (negative) include equipment purchases, installation costs, maintenance expenses, and operating costs.

We represent cash flows on a timeline where year 0 is the present (when the investment decision is made) and subsequent years represent the future.

!!! example

    A lighting retrofit costs $25,000 to install, qualifies for a $5,000 utility rebate, and saves $8,000 per year in electricity costs.

    | Year | Cash Flow | Description |
    |------|-----------|-------------|
    | 0 | -$25,000 | Implementation cost |
    | 0 | +$5,000 | Utility rebate |
    | 1 | +$8,000 | Annual savings |
    | 2 | +$8,000 | Annual savings |
    | 3 | +$8,000 | Annual savings |
    | ... | ... | ... |

    The net cash flow at year 0 is -$20,000 (the $25,000 cost offset by the $5,000 rebate).

## Elements of an ITAC Recommendation

Every assessment recommendation involves some combination of the following cash flow elements:

### Implementation Cost (Year 0 Outflow)

This is the total cost to implement the recommendation, including equipment, materials, labor, engineering, and any other expenses required to complete the project. This is always a negative cash flow at year 0.

### Tax Credits and Incentives (Year 0 Inflow)

Utility rebates, tax credits, and other incentives reduce the effective cost of a project. These are positive cash flows that offset the implementation cost. For simplicity, we typically assume these are received at year 0, though in practice some incentives may be paid after project completion or spread across multiple years.

$$\text{Net Implementation Cost} = \text{Implementation Cost} - \text{Tax Credits and Incentives}$$

### Annual Savings

The recurring benefit from reduced energy consumption, lower demand charges, avoided maintenance, or other operational improvements. This is a positive cash flow that repeats each year over the life of the measure.

### Recurring Costs

Some measures introduce new ongoing expenses: maintenance contracts, replacement parts, consumables, or increased costs in one area that partially offset savings in another. These are subtracted from annual savings to determine the net annual cash flow.

$$\text{Net Annual Cash Flow} = \text{Annual Savings} - \text{Recurring Costs}$$

!!! example

    A compressed air system optimization costs $45,000 to implement and qualifies for a $7,500 rebate. It saves $18,000 annually in electricity but requires a $2,000 annual maintenance contract.

    | Element | Cash Flow |
    |---------|-----------|
    | Implementation Cost | -$45,000 |
    | Utility Rebate | +$7,500 |
    | **Net Year 0** | **-$37,500** |
    | Annual Savings | +$18,000 |
    | Recurring Costs | -$2,000 |
    | **Net Annual** | **+$16,000** |

## Cash Flow Timing Matters

The timing of cash flows affects their economic value. A dollar received today is more valuable than a dollar received next year, even ignoring inflation, because today's dollar can be invested to earn a return. This concept, called the time value of money, is explored in the next page.

For now, the key point is that we carefully distinguish between:

- **Year 0 cash flows:** Immediate costs and benefits
- **Annual cash flows:** Recurring benefits and costs that continue into the future

This distinction becomes important when we evaluate projects using metrics like net present value and payback period.
