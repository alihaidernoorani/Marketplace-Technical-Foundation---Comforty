**Marketplace Technical Foundation - Comforty**

---

### 1. System Architecture Overview

#### High-Level Diagram:
```
[Frontend (Next.js)]
  |
[Sanity CMS] ---------> [Product Data API]
  |
[Third-Party API] -----> [Shipment Tracking API]
  |
[Payment Gateway]
```

#### Components and Roles:
- **Frontend (Next.js):** User interface for browsing products, adding to cart, and checking out.
- **Sanity CMS:** Backend for managing product, customer, and order data.
- **Product Data API:** Fetches product listings and details from Sanity CMS.
- **Third-Party APIs:** Handles shipment tracking and other integrations.
- **Payment Gateway:** Securely processes transactions.

---

### 2. Key Workflows

#### Workflow 1: User Registration
1. User signs up via the frontend.
2. User data is sent to Sanity CMS through an API request.
3. Sanity CMS stores the user information and sends a confirmation response.

#### Workflow 2: Product Browsing
1. User visits the marketplace to browse products.
2. Frontend requests product data from the Product Data API (powered by Sanity CMS).
3. Products are displayed dynamically on the frontend.

#### Workflow 3: Order Placement
1. User adds products to the cart and proceeds to checkout.
2. Frontend sends order details to Sanity CMS via an API.
3. Payment is processed through the Payment Gateway.
4. Order status and payment confirmation are recorded in Sanity CMS.

#### Workflow 4: Shipment Tracking
1. Order details are updated with a shipment tracking ID via a third-party API.
2. User can view real-time shipment status on their order page.

---

### 3. API Endpoints

| Endpoint          | Method | Purpose                                   | Payload/Response                                    |
|-------------------|--------|-------------------------------------------|---------------------------------------------------|
| `/products`       | GET    | Fetch all available products              | Response: `{ id, name, price, image, stock }`     |
| `/orders`         | POST   | Create a new order                        | Payload: `{ customerId, products, totalPrice }`   |
| `/shipment`       | GET    | Track order shipment status               | Response: `{ shipmentId, orderId, status }`      |

---

### 4. Sanity Schemas

#### Product Schema:
```javascript
export default {
  name: 'product',
  type: 'document',
  fields: [
    { name: 'name', type: 'string', title: 'Product Name' },
    { name: 'price', type: 'number', title: 'Price' },
    { name: 'image', type: 'image', title: 'Product Image' },
    { name: 'stock', type: 'number', title: 'Stock Level' },
  ]
};
```

#### Order Schema:
```javascript
export default {
  name: 'order',
  type: 'document',
  fields: [
    { name: 'orderId', type: 'string', title: 'Order ID' },
    { name: 'customerId', type: 'reference', to: [{ type: 'customer' }], title: 'Customer ID' },
    { name: 'products', type: 'array', of: [{ type: 'reference', to: [{ type: 'product' }] }], title: 'Products' },
    { name: 'totalPrice', type: 'number', title: 'Total Price' },
    { name: 'paymentMethod', type: 'string', title: 'Payment Method' },
    { name: 'status', type: 'string', title: 'Status' },
  ]
};
```

#### Customer Schema:
```javascript
export default {
  name: 'customer',
  type: 'document',
  fields: [
    { name: 'customerId', type: 'string', title: 'Customer ID' },
    { name: 'name', type: 'string', title: 'Name' },
    { name: 'email', type: 'string', title: 'Email' },
    { name: 'number', type: 'string', title: 'Phone Number' },
    { name: 'address', type: 'string', title: 'Address' },
  ]
};
```

#### Delivery Zone Schema:
```javascript
export default {
  name: 'deliveryZone',
  type: 'document',
  fields: [
    { name: 'zoneName', type: 'string', title: 'Zone Name' },
    { name: 'address', type: 'string', title: 'Address' },
    { name: 'number', type: 'string', title: 'Contact Number' },
  ]
};
```

---

### 5. Technical Roadmap

1. **Week 1:** Define technical requirements and finalize system architecture.
2. **Week 2:** Develop and test Sanity CMS schemas and API integrations.
3. **Week 3:** Implement frontend design and connect to APIs.
4. **Week 4:** Perform end-to-end testing and refine the user experience.
5. **Launch:** Deploy the marketplace and monitor for feedback.



