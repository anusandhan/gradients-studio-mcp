# Security

This repository holds documentation and client configuration for the hosted Gradients Studio MCP server (`https://www.gradients.studio/mcp`). It contains no server code and no secrets.

## Reporting a vulnerability

Email hello@gradients.studio with a description and, if you can, steps to reproduce. Please don't open a public issue for a security problem. You'll get a reply within 3 working days.

## Keys

API keys are optional and only needed for sized exports. Never commit a key: clients read it from an environment variable or their own secret store, and the configs here use a placeholder.
