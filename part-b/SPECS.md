# IRCTC Design Sprint — Part B Feature Specifications

---

# Feature Spec 1: Tatkal Virtual Queue System

## Problem Statement

IRCTC servers crash during Tatkal booking at 10:00 AM because millions of users attempt booking simultaneously. Users receive no queue feedback and sessions frequently fail.

## Proposed Solution

Introduce a virtual queue system that assigns queue positions before Tatkal booking begins. Users can track live progress and receive a timed booking window.

## Technical Implementation

### Backend

* Redis queue management
* WebSocket support for live updates
* Session-token validation

### Frontend

* Live queue counter
* Countdown timer
* Auto-filled passenger details

### API Changes

* POST `/tatkal/join-queue`
* GET `/tatkal/queue-status`

## Success Metrics

* Server crash rate reduced below 5%
* Tatkal booking success increased from 40% → 70%

## Constraints

* Must support low-speed internet users
* Railway APIs may still become bottlenecks

---

# Feature Spec 2: Persistent Smart Search Filters

## Problem Statement

Train search filters reset frequently and display incorrect results, increasing search time and confusion.

## Proposed Solution

Persist filters using session storage and apply server-side validation for accurate results.

## Technical Implementation

### Frontend

* SessionStorage/localStorage persistence
* Real-time filter chips

### Backend

* Server-side filter verification
* Cached search optimization

### API Changes

* GET `/trains/search?filters=`

## Success Metrics

* Reduce repeated filter actions by 80%
* Faster train discovery experience

## Constraints

* Live train availability changes rapidly

---

# Feature Spec 3: Persistent Seat Selection

## Problem Statement

Seat selections reset during booking, especially on mobile devices.

## Proposed Solution

Store selected seat state throughout booking and lock temporary selections for short durations.

## Technical Implementation

### Frontend

* React state persistence
* Mobile-friendly seat map

### Backend

* Temporary seat-lock service

### API Changes

* POST `/seat/lock`
* POST `/seat/confirm`

## Success Metrics

* Reduce seat reset complaints by 75%

## Constraints

* High concurrent seat updates

---

# Feature Spec 4: Waitlist Prediction & Notification System

## Problem Statement

Users with waitlisted tickets do not know confirmation probability or receive proactive updates.

## Proposed Solution

Provide waitlist confirmation prediction percentages and automatic notifications.

## Technical Implementation

### Backend

* Historical booking analysis
* Notification service integration

### Frontend

* WL prediction card
* Push/SMS alerts

### API Changes

* GET `/wl/prediction`

## Success Metrics

* Reduce manual PNR checks
* Increase user confidence

## Constraints

* Prediction accuracy may vary during festivals

---

# Feature Spec 5: Mobile Booking Experience Redesign

## Problem Statement

The mobile booking experience is cluttered and difficult to navigate.

## Proposed Solution

Redesign mobile forms with step-based booking flow and optimized layouts.

## Technical Implementation

### Frontend

* Mobile-first responsive redesign
* Multi-step forms

### Backend

* Minimal backend changes required

## Success Metrics

* Reduce booking abandonment rate
* Faster mobile booking completion

## Constraints

* Must support older Android devices

---

# Feature Spec 6: Simplified Refund & TDR Assistant

## Problem Statement

The refund and TDR process is confusing and difficult for normal users.

## Proposed Solution

Introduce guided refund filing with simplified explanations and progress tracking.

## Technical Implementation

### Frontend

* Step-by-step refund assistant
* Refund progress tracker

### Backend

* Refund status APIs
* Ticket eligibility checker

### API Changes

* GET `/refund/status`
* POST `/tdr/create`

## Success Metrics

* Reduce refund support complaints
* Improve refund tracking transparency

## Constraints

* Railway refund rules are complex
