# Super Rewards Forex Software

Source code for the Super Rewards Forex Software developed by the Forex Robot Easy Team. 

Forex Robot Easy is not the official developer of this product. This code is provided as a sample and can work as described in the product. For detailed reviews and trading results of this product, please visit [Forex Robot Easy](https://forexroboteasy.com/forex-robot-review/super-rewards-forex-software-review-a-professional-traders-perspective/). To find the official developer of this product, please use MQL5.

## Description

The Super Rewards Forex Software is an Expert Advisor (EA) that automatically trades in the Forex market based on a specific trading strategy. The code provided demonstrates how the EA opens and closes trades based on certain criteria.

## Required Libraries

The following libraries are necessary for the proper functioning of the code:

- Trade.mqh
- PositionInfo.mqh

## Constants

The code defines the following constants:

- `RISK_TO_REWARD_RATIO`: The risk-to-reward ratio for calculating the risk amount.
- `MAX_TRADE_COUNT`: The maximum number of trades allowed.

## Variables

The code initializes the following variables:

- `trade`: An instance of the `CTrade` class for executing trades.
- `positionInfo`: An instance of the `CPositionInfo` class for retrieving position information.

## Functions

### `CalculateRiskAmount`

This function calculates the risk amount based on the current account balance and the risk-to-reward ratio.

```cpp
double CalculateRiskAmount(double accountBalance, int riskRewardRatio)
{
    return (accountBalance * riskRewardRatio) / 100;
}
```

### `OpenTrade`

This function opens a trade with the specified trade direction, lot size, and stop loss.

```cpp
void OpenTrade(double lotSize, double stopLoss, ENUM_ORDER_TYPE tradeType)
{
    double accountBalance = AccountInfoDouble(ACCOUNT_BALANCE);
    double riskAmount = CalculateRiskAmount(accountBalance, RISK_TO_REWARD_RATIO);
    
    if (positionInfo.Total() < MAX_TRADE_COUNT)
    {
        double tradeVolume = NormalizeDouble(lotSize * riskAmount / stopLoss, 2);
        
        trade.Sell(tradeVolume, NULL, stopLoss, 0, NULL);
        trade.Buy(tradeVolume, NULL, stopLoss, 0, NULL);
    }
}
```

### `CloseAllTrades`

This function closes all open trades.

```cpp
void CloseAllTrades()
{
    for (int i = positionInfo.Total(); i >= 0; i--)
    {
        trade.PositionSelect(i);
        trade.PositionClose();
    }
}
```

### `OnTick`

This is the entry point of the EA. It checks if there are any open trades. If there are no open trades, it opens new trades. If there are open trades, it closes them.

```cpp
void OnTick()
{
    if (positionInfo.Total() == 0)
    {
        OpenTrade(0.01, 100, ORDER_TYPE_BUY);
        OpenTrade(0.02, 200, ORDER_TYPE_SELL);
        OpenTrade(0.03, 300, ORDER_TYPE_BUY);
        OpenTrade(0.04, 400, ORDER_TYPE_SELL);
        OpenTrade(0.05, 500, ORDER_TYPE_BUY);
    }
    else
    {
        CloseAllTrades();
    }
}
```

## Conclusion

The Super Rewards Forex Software is an automated trading solution that opens and closes trades based on a specific trading strategy. The code provided demonstrates how the EA opens trades with specified trade directions, lot sizes, and stop losses. It also includes functions to calculate the risk amount and close all open trades. For detailed reviews and trading results of this product, please visit [Forex Robot Easy](https://forexroboteasy.com/forex-robot-review/super-rewards-forex-software-review-a-professional-traders-perspective/).
