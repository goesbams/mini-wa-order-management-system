# Order Management System via WhatsApp

This system integrates WhatsApp as the main channel for customer orders and manages the entire order process, from product selection to payment and delivery, leveraging various external services (AI, catalogs, payment gateways, delivery services).

## Flow Overview

1. **Customer Initiates Order via WhatsApp:**
   - Customer sends a message via WhatsApp.
   - WhatsApp triggers the AI system to analyze the message (using NLP/AI) to identify order intent and display a generated menu or prompt.

2. **Display Integrated Catalog:**
   - AI determines whether to show the internal catalog or the client's (pharmacy, retail, etc.) integrated catalog.
   - Customer selects items and specifies quantities.

3. **Check Item Availability:**
   - WhatsApp confirms item availability (e.g., stock quantity) from the internal or client’s catalog.
   - Customer is informed whether the items are available for order.

4. **Order Confirmation & Payment Method Selection:**
   - Customer confirms order details (items and quantities).
   - Customer is prompted to choose a payment method (via WhatsApp interface).
   
5. **Payment Gateway Integration:**
   - Payment method selection triggers WhatsApp to call the appropriate payment gateway (Midtrans, Xendit, Doku).
   - WhatsApp generates payment information (QRIS, VA, etc.), and this is sent to the customer.
   
6. **Customer Makes Payment:**
   - Customer proceeds with payment via the selected method (QRIS, Virtual Account, etc.).
   - Customer shares payment confirmation with WhatsApp.

7. **Delivery Hailing:**
   - After payment is confirmed, WhatsApp triggers the delivery service (e.g., Gojek, Grab, Indrive, Maxim) to deliver the items.
   - Customer is informed of the delivery status (e.g., "Driver on the way").

8. **Order Completion and Status Update:**
   - Upon successful delivery, WhatsApp triggers the system to update the order status as "Completed."
   - The customer receives a final confirmation via WhatsApp that the order has been completed.

## Sequence Diagram

```plantuml
@startuml
actor Customer
participant WhatsApp as WA
participant AI as AI
participant Catalog as Catalog
participant OrderMgmt as "Order Management"
participant PaymentGateway as PG
participant DeliveryService as DS

Customer -> WA: Send Order Request
WA -> AI: Analyze Order Message
AI -> WA: Display Generated Menu / Prompt
WA -> Catalog: Request Catalog (Internal or Client)
Catalog -> WA: Return Catalog Items
WA -> Customer: Display Catalog and Availability
Customer -> WA: Confirm Items & Quantity
WA -> OrderMgmt: Trigger Internal Order
OrderMgmt -> WA: Order Details Confirmed

Customer -> WA: Choose Payment Method
WA -> PG: Trigger Payment Gateway (Midtrans, Xendit, Doku)
PG -> WA: Generate Payment Details (QRIS, VA, etc.)
WA -> Customer: Send Payment Details
Customer -> WA: Confirm Payment
WA -> PG: Verify Payment Confirmation
PG -> WA: Payment Successful
WA -> DS: Trigger Delivery (Gojek/Grab/Indrive/Maxim)
DS -> WA: Delivery Confirmation
WA -> Customer: Delivery Status (Driver on the way)

DS -> WA: Confirm Delivery Completed
WA -> OrderMgmt: Update Order Status to "Completed"
WA -> Customer: Order Completed Notification

@enduml
```

![Order Flow Diagram](./wa-order-management-system.png)
