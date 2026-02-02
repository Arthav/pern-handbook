# Senior Concepts: System Design & Scaling

When your app hits 100k users.

## 1. Caching (Redis)
The database is the bottleneck. Cache expensive queries.
*   **Use Case**: Fetching user profile, product lists.
*   **Implementation**: Redis (Key-Value store).

```javascript
// Check cache first
const cached = await redis.get('product:123');
if (cached) return JSON.parse(cached);

// If miss, hit DB
const product = await db.query(...);
// Write to cache (expire in 1 hour)
await redis.set('product:123', JSON.stringify(product), 'EX', 3600);
```

## 2. Microservices (vs Monolith)
*   **Monolith**: All code in one repo/server. **KEEP IT THIS WAY** until you have a massive team.
*   **Microservices**: Auth service, billing service, shipping service. Complex to manage.

## 3. Database Scaling
*   **Vertical Scaling**: Buy a bigger server (RAM/CPU).
*   **Read Replicas**: One Writer DB, Multiple Reader DBs. Complex setup.
*   **Sharding**: Splitting data across servers (User IDs 1-1M on Server A, 1M-2M on Server B).

## 4. Message Queues (RabbitMQ / BullMQ)
Don't send emails synchronously in the API request. Put it in a queue.
1.  User registers.
2.  API adds "Send Email" job to Queue.
3.  API returns "Success".
4.  Worker process picks up job and sends email in background.
