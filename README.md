# Railway Ticket Management System

A DSA mini project that simulates railway ticket booking, cancellation and waiting-list management. Every data structure is implemented from scratch in JavaScript, with no built-in `Map`, `Set` or queue classes used for the core logic.

**Live demo:** https://your-project-name.vercel.app
**Repository:** https://github.com/pavankrishnanjj/S3-DSA-Mini-Project

## Features

- Book a ticket on one of three sample trains
- Automatic seat allocation, with a waiting list once a train is full
- Search a booking by its 10-digit PNR
- Cancel a ticket by PNR, with automatic promotion of the first waiting passenger
- Restore the most recently cancelled booking
- View all bookings, sorted by name, age or PNR
- Live seat map and waiting list for every train
- Activity log of every booking, cancellation and promotion

## Data structures used

| Feature | Data structure | Why |
|---|---|---|
| PNR lookup, insert, delete | Hash table with separate chaining | Average O(1) access by PNR |
| Waiting list per train | Singly linked list queue (head and tail pointers) | First come, first served, with O(1) enqueue and dequeue |
| Cancelled bookings | Stack | The latest cancellation is restored first (LIFO) |
| Seat map per train | Array | Index = seat number, `null` means free |
| Sorted bookings table | Merge sort | Stable, O(n log n) sorting by any field |

## Time complexity

| Operation | Complexity |
|---|---|
| Search by PNR | O(1) average, O(n) worst case |
| Book a ticket (seat available) | O(c), where c is the train capacity (linear scan of the seat array) |
| Book a ticket (train full) | O(1) enqueue to the waiting list |
| Cancel a confirmed ticket | O(1) hash delete + O(1) dequeue of the next waiting passenger |
| Cancel a waiting-list ticket | O(w), where w is the waiting list length |
| Restore last cancelled booking | O(1) stack pop + booking cost |
| Sort all bookings | O(n log n) |

## How the booking flow works

1. A booking gets a unique random 10-digit PNR and is stored in the hash table.
2. The seat array of the chosen train is scanned for the first free seat. If one is found, the status is `CNF` (confirmed).
3. If no seat is free, the PNR joins the train's waiting list queue with status `WL`.
4. When a confirmed ticket is cancelled, its seat is freed and the front of the waiting list is dequeued and given that seat.
5. Cancelled bookings are pushed onto a stack so they can be restored later.

## Project structure

```
S3-DSA-Mini-Project/
├── index.html   # UI, styles and all logic in a single file
└── README.md
```

## Run locally

No installation or build step is needed.

1. Clone the repository:
   ```
   git clone https://github.com/pavankrishnanjj/S3-DSA-Mini-Project.git
   ```
2. Open `index.html` in any modern browser.

## Deployment

The project is a static site hosted on Vercel and deployed automatically from the `main` branch of this repository. Every `git push` triggers a new deployment.

## Limitations and future improvements

- Data lives in memory and resets when the page is refreshed (add `localStorage` or a backend database for persistence)
- Only confirmed and waiting statuses are supported (an RAC status could be added)
- A priority queue could be used to model Tatkal or senior-citizen quotas
- Seat classes and fares (Sleeper, 3AC, 2AC) could be added per train
- A graph of stations with shortest-path search (Dijkstra) could be added for route planning

## Author

Pavan Krishnan J
