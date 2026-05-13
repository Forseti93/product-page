# Shopify Dynamic Checkout (Buy Now) Button

The Dynamic Checkout Button (often called the "Buy Now" button) is a specialized Shopify component that allows customers to skip the cart and go directly to checkout using accelerated payment methods (Shop Pay, Apple Pay, PayPal, etc.).

## 1. Implementation Pattern

The button **must** be rendered using the `payment_button` filter on a `form` object within a product form.

```liquid
{%- form 'product', product -%}
  {{ form | payment_button }}
{%- endform -%}
```

> [!IMPORTANT]
> The specific button shown (e.g., Apple Pay vs. PayPal) is determined dynamically by Shopify based on the customer's device, browser, and payment history.

## 2. Modern Styling (CSS Variables)

Shopify renders these buttons inside a **closed Shadow DOM**, meaning traditional CSS selectors cannot reach the internal elements. The only officially supported way to style these is via **CSS Custom Properties** applied to the custom element.

```css
shopify-accelerated-checkout,
shopify-accelerated-checkout-cart {
  /* Dimensions */
  --shopify-accelerated-checkout-button-block-size: 50px;   /* Height */
  --shopify-accelerated-checkout-button-inline-size: 100%; /* Width */
  
  /* Appearance */
  --shopify-accelerated-checkout-button-border-radius: 4px;
  
  /* Layout (Cart only) */
  --shopify-accelerated-checkout-cart-button-margin-block: 8px;
}
```

## 3. Critical Compatibility Warnings

> [!CAUTION]
> **Data Loss Risk**: Dynamic checkout buttons **DO NOT** support:
> - **Line Item Properties**: Any data from `name="properties[...]"` inputs will be ignored.
> - **Cart Attributes**: Metadata intended for the cart object will be bypassed.
> 
> **Solution**: If your block includes custom text inputs or file uploads, you **must disable** the Dynamic Checkout button for that product to ensure data is captured correctly.

## 4. Best Practices

1. **Avoid Layout Shift (CLS)**: These buttons load asynchronously. Always wrap them in a container with a minimum height to prevent the page from "jumping" when the button appears.
   ```css
   .product-form__buttons { min-height: 50px; }
   ```
2. **Conditional Rendering**: Always wrap the button in an `if product.available` check.
3. **No Overlays**: Never place invisible elements or "click-jacking" overlays on top of the button. This can cause payment providers (like Apple Pay) to reject the transaction for security reasons.
4. **Ajax Drawers**: These buttons are not recommended for Ajax-powered drawers. They require complex re-initialization and often fail to sync with the current variant correctly.

## 5. CSS Selector Reference

| Selector | Usage |
| :--- | :--- |
| `shopify-accelerated-checkout` | Target for CSS variables (Product Page). |
| `shopify-accelerated-checkout-cart` | Target for CSS variables (Cart Page). |
| `.shopify-payment-button` | Outer wrapper for margin and positioning. |
| `.shopify-payment-button__button--unbranded` | Fallback "Buy it now" button (when no accelerated method is found). |
