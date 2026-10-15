# Vaccination Tracker

A Python command-line program that helps medical facilities and their clients
track multi-dose vaccination courses. It calculates when the next dose is due,
alerts staff to due and overdue doses, and issues a completion certificate when
a course is finished.

Built for PROG211 Object-Oriented Programming 1 (Health domain: Vaccination Tracker).

## How to run

Requires Python 3.8 or later. No external libraries are needed.

```
python main.py          # interactive menu
python main.py --demo   # scripted demonstration with sample data
```

## Project structure

| File | Purpose |
|------|---------|
| `vaccine.py` | `Vaccine` class: name and dosing schedule |
| `client.py` | `Client` class: a person's doses, next due date and alerts |
| `certificate.py` | `Certificate` class: issued when a course is complete |
| `registry.py` | Dictionary of all clients plus add/display/alert functions |
| `main.py` | Menu and demo |

## OOP concepts used

- **Classes and objects:** `Vaccine`, `Client` and `Certificate`. A `Client` holds a `Vaccine` object and creates a `Certificate` object when the final dose is recorded.
- **Data structure:** a dictionary (`registry.clients`) storing `Client` objects with the client ID as the key.
- **Tuples:** each vaccine schedule (e.g. `(0, 30, 180)`) and the dose dates on a certificate are tuples, because they must not change.
- **Instance methods:** `record_dose()`, `next_due_date()`, `check_alert()`, `display_info()`, `display_certificate()`.
- **Class methods:** `Vaccine.from_preset()`, `Vaccine.available_presets()`, `Client.generate_id()`, `Certificate.total_issued()`.
- **Static methods:** `Vaccine.add_days()`, `Client.validate_birth_year()`.

## Alignment with Digital Public Goods (DPG) standards

**Open source.** The full source code is public on GitHub so any facility can use, study and improve it.

**Privacy-respecting.** Vaccination records are health information, so the system stores no names, phone numbers, national ID numbers or exact dates of birth. Each client is identified by a generated code (e.g. `CL-0001`), with only initials and birth year kept for staff to confirm identity. The facility keeps the link between the code and the real person in its own secure records.

**Inclusive and accessible.** The program runs in a plain text terminal on any computer with Python, needs no internet connection and no paid software, which suits low-resource settings. Alerts use plain-language words (COMPLETE, OVERDUE, DUE TODAY, DUE SOON, UPCOMING) rather than colours or symbols, so they work with screen readers and on any display.

**Modular and reusable.** Each class lives in its own file. Vaccine schedules are data, not hard-coded logic, so a facility can add a new vaccine by adding one line to `Vaccine.PRESETS`. The classes can be reused in a larger system, such as a web or SMS reminder service.

## Example usage

Output from `python main.py --demo` (dates are relative to the day it is run):

```
=== DEMO: alerts ===
Vaccination alerts for 2026-10-15
----------------------------------------------
CL-0001 (Hepatitis B): COMPLETE - certificate VC-0001
CL-0002 (Hepatitis B): OVERDUE - dose 2 was due 2026-10-10 (5 day(s) late)
CL-0003 (Hepatitis B): DUE SOON - dose 2 on 2026-10-20 (in 5 day(s))
CL-0004 (Yellow Fever): COMPLETE - certificate VC-0002

=== DEMO: certificate ===
==============================================
        VACCINATION COMPLETION CERTIFICATE
==============================================
  Certificate ID : VC-0001
  Client ID      : CL-0001
  Vaccine        : Hepatitis B
  Dose 1         : 2026-03-29
  Dose 2         : 2026-04-28
  Dose 3         : 2026-09-25
  Completed on   : 2026-09-25
==============================================
```

Interactive example (recording a dose):

```
Choose an option: 2
Client ID: CL-0003
Date of dose (YYYY-MM-DD, blank = today): 2026-10-20
Dose 2 of 3 recorded for CL-0003 on 2026-10-20.
```

## Limitations and future work

- Data is kept in memory and is lost when the program closes; saving to a file is a natural next step.
- Alerts are shown on screen; a future version could send SMS reminders using the client code only.
- Schedules should be checked against the facility's national immunization guidelines.
