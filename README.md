# NAGIISIP — Message Channel Demo

A front-end demo that reimagines the Message Channel pattern from the ITP103 midterm lab exam as an SMS/iMessage-style chat app. Each conversation in the app stands in for one of the five Enterprise Integration Patterns built with Apache Camel and an embedded Apache ActiveMQ broker.

**Group SILANGAN | 3 IT-A**

## What this is

The original lab exam implements five EIP patterns in Java using Apache Camel routes and a JMS broker. This demo takes that same set of patterns and visualizes them as a messenger app: each channel in the sidebar is one queue from the project, the "you" side is the producer, and the auto-reply side is the consumer. Sending a message plays out the same exchange the Java routes perform, just as a chat bubble instead of a log line.

## Patterns covered

| Channel | Queue | Pattern | Producer → Consumer |
|---|---|---|---|
| Message Channel | `customer.registrations` | Task 1 | Web App → Back-end System |
| Content-Based Router | `registrations.inbound` | Task 2 | Registration Source → Router |
| Aggregator | `orders.parts` | Task 3 | Order · Payment · Shipping → Aggregator |
| Message Translator | `legacy.customers.xml` → `crm.customers.json` | Task 4 | Legacy XML System → Translator |
| Dead Letter Channel + Retry | `crm.delivery` → `crm.errors` → `crm.parkinglot` | Task 5 | Retry Route → Target CRM |

Type a message in any channel to see it: the Content-Based Router checks for a Philippine location and routes local vs. international, the Aggregator counts parts toward a completed order, the Translator turns a simple XML-style tag into JSON, and the Dead Letter Channel simulates delivery attempts up to the point a message lands in the parking lot.

## Running it

This is a single self-contained HTML file — no build step, no server, no dependencies to install.

1. Download `nagiisip-message-channel.html`.
2. Open it directly in any modern browser (double-click, or drag it into a browser window).

## Design

The interface deliberately avoids the usual grey-and-blue iMessage look. The dominant palette is a warm sunrise yellow, with royal blue reserved for sent messages and key accents. Layout follows a standard two-pane messenger: a channel list on the left, and an active thread with a composer on the right. On narrower screens the layout collapses to a single pane with a back button, the same way a phone messaging app would.

## Relationship to the main lab exam

This is a companion piece to the Java implementation, not a replacement for it. The actual routing, aggregation, translation, and retry logic run in Apache Camel against the embedded ActiveMQ broker, as documented in the main project. This demo is meant to make those five patterns easier to explain and walk through visually.
