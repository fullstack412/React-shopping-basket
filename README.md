# react-basket

Shopping basket integrated to Crystallize

## Usage

```
yarn add @crystallize/react-basket
```

**In your app root**

```
import { BasketProvider } from '@crystallize/react-basket';

const basketOptions = {
  freeShippingMinimumPurchaseAmount: 600
};

export default () => (
  <BasketProvider {...basketOptions}>
    <YourApp />
  </BasketProvider>
);
```

**Where you consume it**

```
import { BasketConsumer } from '@crystallize/react-basket';

export default () => (
  <BasketConsumer>
    {({ state, actions }) => (
      <button onClick={() => actions.addItem({ sku: 'product-sku-1', price: 99, quantity: 1 })}>
        {state.totalQuantity
          ? `Your basket (${state.totalQuantity} items, ${state.totalPrice},-)`
          : 'Your basket is empty'}
      </button>
    )}
  </BasketConsumer>
);
```

## State

The state object contains:

* items (array of the product items in the basket)
* totalPrice (the total price of the basket items)
* totalPriceMinusDiscount (total price minus discount (if applied))
* totalToPay (total price - discount + shipping)
* totalQuantity (the total items including quantity)
* freeShipping (if free shipping has been granted)
* remainingUntilFreeShippingApplies (the minimum amount required for free shipping)

## Actions

* empty (empty the basket)
* addItem (add an item)
* removeItem (remove an item)
* incrementQuantityItem (incremenet the quantity for a given item)
* decrementQuantityItem (decremenet the quantity for a given item)
* parseBasketItem (takes a product and a variant model and returns a valid basket item)
