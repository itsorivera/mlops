# Deployment Strategies and Patterns

When deploying ML models, the goal is to minimize risk through **Gradual Ramp-up**, **Monitoring**, and the ability to **Rollback**.

### 1. Common Deployment Use Cases

- **New Product**: Offering a capability not previously available.
- **Automating/Assisting Humans**: Replacing or helping with a task previously done by people (e.g., factory inspection).
- **Replacing ML Systems**: Upgrading an existing ML implementation with a better version.

### 2. Deployment Patterns

- **Shadow Mode**:
  - The model runs in parallel with humans or old systems.
  - Outputs are logged but **not used** for decisions.
  - Used to verify accuracy safely before full deployment.
- **Canary Deployment**:
  - Roll out to a **small fraction** of traffic (e.g., 5%).
  - Enables early detection of failures with minimal impact.
  - Traffic is ramped up only after confirming reliability.
- **Blue-Green Deployment**:
  - Two environments: **Blue** (Current Production) and **Green** (New Version).
  - A router switches 100% of traffic from Blue to Green.
  - Allows **instant rollback** by switching back to Blue if errors occur.

### 3. Degrees of Automation (Human-in-the-Loop)

Deployment exists on a spectrum rather than being binary:

1.  **Human-only**: No AI involved.
2.  **Shadow Mode**: Parallel data gathering (no impact).
3.  **AI Assistance**: AI highlights regions or provides info (UX-critical), but humans decide.
4.  **Partial Automation**: AI decides when **confident**; sends **uncertain** cases to a human. Human feedback can be used for retraining.
5.  **Full Automation**: AI makes every decision (typical for large-scale consumer apps).

### 4. Key Takeaway

For many industrial and specialized applications, the best design point is a **Human-in-the-loop** system (Assistance or Partial Automation), rather than jumping straight to full automation.
