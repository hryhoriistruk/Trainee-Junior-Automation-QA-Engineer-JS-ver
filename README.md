# aqa-inforce-hryhoriistruk

Automated tests (Cypress) for <https://automationintesting.online/>:
UI tests for the User App (room booking) and API tests for the Admin/User flows.

## Requirements
- Node.js 18+ and npm

## Setup
```bash
git clone https://github.com/<your-account>/aqa-inforce-hryhoriistruk.git
cd aqa-inforce-hryhoriistruk
npm install
```

## Run
```bash
npm test              # all specs, headless
npm run test:ui       # only UI tests   (cypress/e2e/user-spec.cy.js)
npm run test:api      # only API tests  (cypress/e2e/admin-spec.cy.js)
npm run cy:open       # interactive Cypress runner
```
Admin credentials (`admin` / `password`) and the API URL are set in `cypress.config.js` (`env`).

## Test cases
| What | File | Location |
|---|---|---|
| Manual test cases (UI + API) | `test-cases.txt` | repository root |
| UI automation (TC-UI-01…08) | `user-spec.cy.js` | `cypress/e2e/` |
| API automation (TC-API-01…07) | `admin-spec.cy.js` | `cypress/e2e/` |

## Structure
```
cypress/
  e2e/         user-spec.cy.js, admin-spec.cy.js
  fixtures/    room.json, booking.json
  support/     commands.js (custom commands), utils.js (data builders), e2e.js
test-cases.txt
cypress.config.js
package.json
```

## Notes
- Each spec creates its own room with a unique name via Admin API and deletes it afterwards,
  so tests are independent and don't pollute the shared demo site.
- Custom commands: `adminLogin`, `adminCreateRoom`, `adminUpdateRoom`, `adminDeleteRoom`,
  `adminGetBookings`, `userGetRooms`, `userBookRoom`, `userGetBookingSummary`,
  `selectDatesOnCalendar`, `fillBookingForm`.
- `cy.intercept` is used to wait for / assert `GET /api/booking/summary`, `POST /api/booking`
  (status 201 / 400) and `GET /api/room`.
- The demo site is shared and periodically reset – if a test flakes, simply re-run it.
