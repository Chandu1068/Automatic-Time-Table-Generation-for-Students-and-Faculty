# Automatic-Time-Table-Generation-for-Students-and-Faculty
**Automatic Time Table Generation for Students and Faculty**

A zero-dependency, browser-based web application that automatically generates a complete, clash-free college timetable for all sections and faculty members. This tool uses a smart heuristic algorithm to solve complex scheduling constraints and produce an optimized, faculty-friendly schedule.


**Features**

Zero-Dependency: The entire application is a single index.html file. It runs 100% in the browser with no backend, database, or setup required.

Step-by-Step Wizard: An easy-to-use 4-step interface guides the user through data entry.

Complex Constraint Handling:

Maps subjects and faculty to specific sections.

Manages multi-period blocks (e.g., 2 or 3 consecutive periods for labs).

Enforces hard constraints for lab-specific time slots.

Ensures the total weekly period count for each section is met perfectly.

Smart Scheduling Engine:

Uses a "best-fit" cost-based heuristic algorithm, not just random placement.

Finds the most optimal schedule, not just the first one that works.

Faculty-Friendly Optimization (Soft Constraints):

The algorithm actively avoids scheduling faculty for 4 or more consecutive periods.

It intelligently penalizes schedules that place a faculty member in classes immediately before and after the lunch break.

Clash-Free Guarantee (Hard Constraints):

Ensures no faculty member is assigned to two different sections at the same time.

Ensures no section has two different classes scheduled at the same time.

Ensures no lab (as a shared resource) is used by two different sections at the same time.

Dual Output: Generates two sets of timetables:

Section Timetables: A complete weekly schedule for each individual section.

Faculty Timetables: A complete weekly schedule for each individual faculty member, showing their assigned classes and total workload.

Print-Ready: A built-in "Print" button formats all generated timetables cleanly for printing.

**How to Use**

No installation is needed!

Clone this repository or download the index.html file.

Open the index.html file in any modern web browser (like Chrome, Firefox, or Edge).

Follow the 4-step process:

Step 1: Enter the number of sections and subjects for each year.

Step 2: Provide the names for all subjects, faculty, and sections.

Step 3: For each section, allocate subjects and faculty, specifying the number of classes per week and how many periods are consecutive (e.g., a lab might be 1 "class" of 3 "consecutive" periods).

Step 4: Click "Generate Timetable". The result will appear in seconds.

**How It Works: The Scheduling Engine**

The core of this project is the JavaScript-based scheduling engine (generateTimetables and calculatePlacementCost functions). It solves this complex constraint-satisfaction problem using a heuristic search with a cost-based "best-fit" algorithm.

1) Prioritization: The engine sorts all classes to be scheduled, placing high-constraint tasks (like 3-period labs) first.

2) Best-Fit Search: For each class, it does not just find the first available slot. Instead, it iterates through every possible empty slot in the week and calculates a "penalty score" for that placement.

3)Penalty Calculation:

  ->  Infinity Penalty (Hard Constraint): A slot is given an infinite penalty if it violates a hard rule (e.g., the teacher is busy, the section is busy, or it's a lab in the wrong slot).

  ->  High Penalty (Soft Constraint): A slot gets a high penalty (e.g., +10) if placing a class there creates a 4-period or 5-period block for the assigned faculty.

  ->  Medium Penalty (Soft Constraint): A slot gets a medium penalty (e.g., +5) if it schedules the faculty right before and right after the lunch break.

  ->  Low Penalty (Soft Constraint): A slot gets a low penalty (e.g., +1) if it creates a 3-period block.

  ->  Zero Penalty: An ideal slot that causes no issues.

4) Placement: The algorithm places the class in the slot with the lowest total penalty score. This ensures that it always makes the most optimal, faculty-friendly choice available.

5) Iteration: The process is repeated hundreds of times (runGeneratorWithRetries) with a small amount of randomness to find a valid solution even for highly complex schedules.

**Contributing**

Contributions are welcome! If you have ideas for new features or find a bug, please feel free to fork the repository, make your changes, and submit a pull request.

1) Fork the Project

2) Create your Feature Branch (git checkout -b feature/AmazingFeature)

3) Commit your Changes (git commit -m 'Add some AmazingFeature')

4) Push to the Branch (git push origin feature/AmazingFeature)

5) Open a Pull Request
