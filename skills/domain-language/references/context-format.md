# Glossary format

Use the project's existing vocabulary source and formatting first. A particular
filename does not establish how many domains the application contains.

## Minimal glossary

```markdown
# Ordering vocabulary

Terms used by the order acceptance and fulfillment flows.

**Order:** A customer's request to buy items, from placement through fulfillment
or cancellation.
Avoid "transaction" when it would confuse the order with a payment event.

**Shipment:** A group of items dispatched together. One order may have several
shipments.

**Cancellation:** Ending the unfulfilled part of an order according to its
current lifecycle rules.
```

These definitions are examples, not universal business rules. Check definitions
against the actual product and distinguish current from proposed behavior.

## Define useful terms

- Define what the concept is and the distinction the reader needs.
- Include lifecycle or ownership detail when essential to its meaning.
- Add avoided synonyms only when they prevent ambiguity in this context.
- Exclude generic programming vocabulary unless the project gives it a special meaning.
- Keep implementation proposals and scratch notes outside the glossary.

## Several contexts

Add a context map only when separate vocabularies or ownership boundaries are
demonstrated and readers need to navigate them. Name each context, its source
document, and the relevant relationship.

For example, Ordering can own order acceptance while Billing owns invoices.
Document the actual integration and terminology boundary rather than creating
a map solely because those words occur in the code.

Link to the existing documents at their real project paths. Do not create a
second glossary or infer architecture from absent map files.
