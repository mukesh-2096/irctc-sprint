# IRCTC Problem Discovery — Part A

## Summary

* Total problems documented: 3 Given Problems
* Platform explored: irctc.co.in (live platform)
* Devices used: Desktop Chrome and Mobile Chrome

---

# Problem 1: Tatkal Booking Crashes at 10:00 AM [Given]

## Category:

Performance / Scalability / UX

## What is broken:

The IRCTC Tatkal booking system becomes extremely slow or crashes exactly at 10:00 AM when Tatkal booking opens. Users experience page freezes, session timeouts, CAPTCHA resets, delayed OTPs, and failed payments during the highest traffic window.

## Affected users:

Daily Tatkal passengers across India, especially users from Tier 2 and Tier 3 cities who rely heavily on train travel. Approximately 20–40 lakh users attempt Tatkal booking during the 9:58 AM–10:05 AM window.

## Frequency:

Occurs daily at 10:00 AM during Tatkal booking hours. This is a long-standing recurring issue.

## Current flow — step by step:

1. User opens IRCTC around 9:50 AM and logs into their account.
2. User searches for trains and selects the required train.
3. User chooses “Tatkal” quota before 10:00 AM.
4. Passenger details are filled and the user waits near the payment step.
5. At exactly 10:00 AM, the user clicks “Book Now”.
6. The page freezes and continuously shows a loading spinner.
7. No queue status or progress message is displayed.
8. After 15–45 seconds, the page either crashes, logs the user out, or throws an HTTP 502/server error.
9. User refreshes the page and discovers that the Tatkal quota is already full or waitlisted.

## Where exactly it breaks:

Step 6–8. The backend infrastructure cannot handle massive concurrent requests at 10:00 AM. The system also fails to provide meaningful feedback or queue management during overload.

---

# Problem 2: Search Filters Do Not Work Reliably [Given]

## Category:

UX / Information Architecture

## What is broken:

Train search filters such as class type, quota, seat availability, and departure timing behave inconsistently. Filters sometimes reset automatically or display incorrect train results.

## Affected users:

All IRCTC users searching for trains. Senior citizens and first-time users are especially affected because they depend on filters to simplify train selection.

## Frequency:

Occurs intermittently, especially during high traffic periods. Estimated failure rate is around 30–40% during repeated searches.

## Current flow — step by step:

1. User opens the train search page on IRCTC.
2. User enters source station, destination station, and journey date.
3. Search results display multiple trains.
4. User applies filters such as “Sleeper Class”, “Available Seats”, or “Morning Departure”.
5. The page reloads after applying filters.
6. Some trains shown still contain waitlist seats instead of available seats.
7. User clicks a train and notices that the displayed availability does not match the filter.
8. User navigates back to search results.
9. Previously selected filters are reset automatically.
10. User must reapply filters manually again.

## Where exactly it breaks:

Step 5–9. The filter state is not preserved properly, and cached data causes mismatched train availability information.

---

# Problem 3: Seat Selection Resets Randomly [Given]

## Category:

Mobile / UX / State Management

## What is broken:

During seat selection, users choose a preferred berth, but the selection resets or changes automatically when moving to the next booking step.

## Affected users:

Families, elderly passengers, women travelers, and users requiring specific berth preferences. Mobile users face this issue more frequently.

## Frequency:

Occurs in around 15–25% of booking sessions, especially on mobile browsers and slower networks.

## Current flow — step by step:

1. User searches and selects a train.
2. User proceeds to the seat selection page.
3. The seat map loads showing available and occupied seats.
4. User selects a preferred berth, such as a lower berth.
5. The selected berth is highlighted successfully.
6. User clicks “Proceed” to continue booking.
7. Passenger details page opens.
8. The selected berth changes to “Auto” or another seat number.
9. User navigates back to reselect the berth.
10. Previously selected seat may already appear unavailable.

## Where exactly it breaks:

Step 6–8. The seat selection state is not transferred properly between booking steps. Mobile page re-rendering and weak state persistence contribute to the issue.
