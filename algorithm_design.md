# 5. Algorithm Design / Pseudocode

This document outlines core algorithmic logic and pseudocode implementations for essential **PawPet** features before writing production source code.

## Algorithm 1: Reminder Dispatcher & Status Evaluator

**Purpose:** Runs periodically (e.g., via background cron every 15 minutes) to find pending reminders due within the notification window, dispatch alerts, and update reminder statuses.

### Pseudocode

```text
FUNCTION ProcessPendingReminders():
    currentTime = GET_CURRENT_TIMESTAMP()
    notificationWindowEnd = currentTime + INTERVAL(15 MINUTES)

    // Step 1: Query due reminders
    dueReminders = DB_QUERY(
        "SELECT r.*, u.email, u.device_token, p.name AS pet_name 
         FROM reminders r
         JOIN pets p ON r.pet_id = p.id
         JOIN users u ON p.owner_id = u.id
         WHERE r.status = 'PENDING' 
           AND r.due_date <= :notificationWindowEnd"
    )

    // Step 2: Dispatch notifications
    FOR EACH reminder IN dueReminders DO:
        TRY:
            notificationPayload = {
                title: "PawPet Health Reminder: " + reminder.pet_name,
                message: "Reminder for " + reminder.pet_name + ": " + reminder.title,
                dueDate: reminder.due_date
            }

            IF reminder.device_token IS NOT NULL THEN:
                SEND_PUSH_NOTIFICATION(reminder.device_token, notificationPayload)
            END IF

            SEND_EMAIL_NOTIFICATION(reminder.email, notificationPayload)

            // Step 3: Update reminder status
            DB_EXECUTE(
                "UPDATE reminders SET status = 'SENT', updated_at = :currentTime WHERE id = :id",
                { id: reminder.id, currentTime: currentTime }
            )

        CATCH Exception error:
            LOG_ERROR("Failed to send reminder ID: " + reminder.id, error)
        END TRY
    END FOR
END FUNCTION
```

## Algorithm 2: Vaccination Schedule Due-Date Calculator

**Purpose:** Automatically calculates next booster due date based on vaccine type, pet age, and previous administration date.

### Pseudocode

```text
FUNCTION CalculateNextVaccineDueDate(petAgeMonths, vaccineType, lastAdministeredDate):
    DEFAULT boosterIntervalMonths = 12 // Standard 1-year booster

    SWITCH vaccineType:
        CASE "RABIES":
            IF petAgeMonths < 12 THEN:
                boosterIntervalMonths = 12 // Initial booster at 1 year
            ELSE:
                boosterIntervalMonths = 36 // 3-year rabies cycle
            END IF
        CASE "DHPP":
            boosterIntervalMonths = 12
        CASE "BORDETELLA":
            boosterIntervalMonths = 6  // High risk 6-month cycle
    END SWITCH

    nextDueDate = ADD_MONTHS(lastAdministeredDate, boosterIntervalMonths)
    RETURN nextDueDate
END FUNCTION
```

## Algorithm 3: Overdue Status Aggregator

**Purpose:** Determines if a pet profile requires visual urgency badges on the UI dashboard.

### Pseudocode

```text
FUNCTION EvaluatePetHealthAlertStatus(petId):
    currentDate = GET_CURRENT_DATE()
    
    overdueCount = DB_QUERY(
        "SELECT COUNT(*) FROM reminders 
         WHERE pet_id = :petId AND due_date < :currentDate AND status = 'PENDING'",
        { petId: petId, currentDate: currentDate }
    )

    IF overdueCount > 0 THEN:
        RETURN { alertLevel: "HIGH", badgeColor: "RED", overdueItems: overdueCount }
    ELSE:
        RETURN { alertLevel: "NORMAL", badgeColor: "GREEN", overdueItems: 0 }
    END IF
END FUNCTION
```
