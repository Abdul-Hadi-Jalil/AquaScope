# Extensibility model

New integrations follow stable contracts:

- A source configuration describes requests and destinations.
- An authentication implementation handles the provider-specific exchange.
- An API client handles transport and response capture.
- A transformation module maps source payloads into canonical structures.
- Validation rules verify required fields, ranges, uniqueness, and completeness.

This design keeps shared orchestration unchanged when a new provider is introduced.
