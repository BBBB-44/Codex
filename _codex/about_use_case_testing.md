---
---

# Use Case Testing Strategy

## Overview

Use case testing focuses on validating real user behaviors instead of isolated units of logic. The objective is to ensure that critical user journeys function correctly under realistic conditions, including navigation, asynchronous operations, and partial failures.

This document outlines a modern approach to use case testing using Playwright, model-based testing, and controlled chaos techniques.

---

## 1. End-to-End Use Case Testing with Playwright

### Rationale

End-to-end (E2E) testing validates complete user flows in a real browser environment. Playwright is currently one of the most effective tools for this purpose due to its reliability, speed, and native support for modern web features.

### Example Scenario

A typical test should reflect a real user journey:

```ts
test('user search + back navigation', async ({ page }) => {
  await page.goto('/')

  await page.fill('[data-test=search-input]', 'Montreal')
  await page.click('[data-test=search-button]')

  await page.click('[data-test=event-card]:nth-child(1)')

  await page.goBack()

  await expect(page.locator('[data-test=search-input]')).toHaveValue('Montreal')
})
````

### Key Principles

* Focus on **critical user paths**
* Use **stable selectors** (`data-test`)
* Validate **state persistence**, especially with navigation (e.g., back button)

---

## 2. Model-Based Testing

### Rationale

Model-based testing validates application behavior against a defined state model. Instead of manually writing all scenarios, the system generates test paths automatically.

### Application States

Example states for an event-based application:

* Home
* Search Results
* Event Modal
* Back Navigation

### User Actions

Define all possible user interactions:

* `search`
* `click event`
* `back`
* `change filters`
* `scroll`

### Implementation with fast-check

```ts
fc.assert(
  fc.property(userActionsArbitrary, async (actions) => {
    const model = new Model()
    const realApp = new AppDriver(page)

    for (const action of actions) {
      model.apply(action)
      await realApp.apply(action)

      expect(realApp.state()).toEqual(model.state)
    }
  })
)
```

### Benefits

* Explores **unexpected user paths**
* Detects **state inconsistencies**
* Reduces reliance on manually written scenarios

---

## 3. Controlled Chaos Testing

### Rationale

Many bugs arise from unstable conditions such as latency, race conditions, and partial reloads. These issues are rarely caught by deterministic tests.

### Techniques with Playwright

Simulate adverse conditions:

* Network throttling
* Delayed API responses
* Interrupted requests
* Mobile environments

### Example

```ts
await page.route('**/api/events', route => {
  setTimeout(() => route.continue(), 2000)
})
```

### Objective

Force the application into unstable states to identify failure points.

---

## 4. Fuzz Testing User Journeys

### Concept

Fuzz testing involves generating random sequences of user actions over extended sessions.

### Example Behavior

Simulated users may:

* Scroll
* Open modals
* Change filters
* Navigate back
* Refresh the page

These sequences typically span **50 to 200 actions**.

### Expected Outcome

* If the application fails → a bug is detected
* If it remains stable → confidence increases in resilience

---

## 5. Testable Application Design

### Common Issue

Failures during navigation (e.g., back button) often indicate flawed state management.

### Root Causes

* State not stored in the URL
* Non-idempotent state transitions
* Hidden state within components

### Best Practices

* Use **query parameters** (e.g., `?location=mtl`)
* Ensure **idempotent state**
* Avoid **implicit or hidden state**
* Maintain **synchronization between UI and URL**

---

## 6. Practical Testing Strategy

### Recommended Weekly Plan

* Implement **5 critical Playwright scenarios**
* Add **1 model-based random test** using fast-check
* Simulate **slow network conditions**
* Systematically test **back navigation behavior**

---

## 7. Real-World Perspective

Complete test coverage is not achievable. The goal is to maximize confidence by focusing on:

* Critical user flows
* Intelligent randomness
* Failure-prone conditions

This approach distinguishes fragile systems from robust, production-ready applications.

---

## 8. Fuzzy Testing Scope (Event Aggregator)

### Core Use Cases to Validate

* A user can **add an event**
* A user can **modify an event**
* A user can **delete an event**

These actions should be included in both deterministic and fuzz-generated scenarios to ensure consistency and reliability.

---

## Conclusion

A solid use case testing strategy combines:

* Deterministic E2E scenarios
* Model-based exploration
* Controlled chaos engineering
* Fuzz testing

The objective is not exhaustive testing, but **high confidence in real-world behavior under diverse conditions**.

```
```
