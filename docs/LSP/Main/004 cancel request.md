# Cancel Request

Canceling a request

- method: ‘$/cancelRequest’
- params: CancelParams defined as follows:

```typescript
interface CancelParams {
  /**
   * The request id to cancel.
   */
  id: integer | string;
}
```
