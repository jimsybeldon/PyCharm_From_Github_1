**Before Inlining**

In this example, an over-engineered calculation breaks down a simple line item total into excessive intermediate variables, reducing readability.

```typescript
function calculateLineTotal(quantity: number, unitPrice: number): number {
    const basePrice = quantity * unitPrice;
    const standardDiscountRate = 0.10;
    const discountAmount = basePrice * standardDiscountRate;
    const priceAfterDiscount = basePrice - discountAmount;
    const salesTaxRate = 0.08;
    const taxAmount = priceAfterDiscount * salesTaxRate;
    const finalTotal = priceAfterDiscount + taxAmount;
    
    return finalTotal;
}

```

---

**Inlining Process**

Position the cursor on each intermediate variable, right-click, and select **Refactor → Inline Variable...** (or press `Cmd+Option+N` / `Ctrl+Alt+N` in IDEs like WebStorm, VS Code, or IntelliJ).

1. Inline `finalTotal` into the `return` statement.
2. Inline `taxAmount` and `priceAfterDiscount`.
3. Inline `discountAmount`, `standardDiscountRate`, and `salesTaxRate`.
4. Collapse the redundant mathematical operations into a single algebraic expression.

---

**After Inlining**

```typescript
function calculateLineTotal(quantity: number, unitPrice: number): number {
    return (quantity * unitPrice) * 0.90 * 1.08;
}

```

---

**Review of Structural Changes**

| Metric / Aspect | Before Inlining | After Inlining |
| --- | --- | --- |
| **Lines of Code (Body)** | 8 lines | 1 line |
| **Temporary Variables** | 7 variables allocated | 0 temporary variables |
| **Readability Focus** | Verbose step-by-step trace | Immediate high-level formula |
| **Estimated Accuracy** | $P = 0.99$ | $P = 0.99$ |