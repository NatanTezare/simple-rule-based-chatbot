# Building a Reasoning and Inferencing Engine for a Student Academic Advisor

## Introduction
This repository contains a Knowledge-Based System (KBS) designed to act as an intelligent academic advisor. It evaluates student performance metrics, attendance data, and administrative records to output actionable academic recommendations.

## Problem Statement
University advisors must parse multiple streams of data (GPA, attendance, fee statuses, disciplinary records) to accurately determine a student's academic standing, scholarship eligibility, and graduation status. Manual evaluation is time-consuming and prone to human error. This system automates that process using strict logical inferencing.

## Knowledge Base
The system represents knowledge using a dynamically generated `knowledge_base.json` file. It maps logical conditions directly to academic outcomes.

## Rules Implemented
1. **Scholarship:** IF GPA > 3.5 AND Attendance > 80% AND No Disciplinary Cases $\rightarrow$ Eligible for Scholarship
2. **Graduation:** IF GPA > 3.0 AND Completed Prerequisite Courses AND No Outstanding Fees $\rightarrow$ Eligible for Graduation
3. **Probation:** IF GPA < 3.0 $\rightarrow$ Academic Probation
4. **Registration:** IF Outstanding Fees $\rightarrow$ Registration Blocked
5. **Dean's List:** IF GPA > 3.5 AND Attendance > 80% $\rightarrow$ Dean's List Candidate

## Reasoning Method Used
This system implements **Forward Chaining** as its primary reasoning method. It extracts a set of factual truths from raw student data, iterates through the knowledge base, and triggers any rule where the conditions are fully met (data-driven reasoning). 

**Bonus Feature:** The system also includes a **Backward Chaining** module that allows the system to start with a specific goal (e.g., "Eligible for Graduation") and work backward to determine if the student possesses the required facts to fulfill that specific goal.

## Forward Chaining vs. Backward Chaining Comparison (Bonus Feature)

As part of the bonus implementation, this system evaluates student data using both Forward (Data-Driven) and Backward (Goal-Driven) chaining. 

### Conclusion Verification
When tested against identical student profiles, both the Forward Chaining and Backward Chaining engines produced the **exact same conclusions**. This verifies that our Knowledge-Based System is logically sound and consistent. 

### Execution Differences
- **Forward Chaining** proved highly efficient for universal profiling. By starting with raw metrics (e.g., GPA, attendance), it successfully mapped out multiple simultaneous conclusions (e.g., determining a student is concurrently a Dean's List Candidate, Eligible for Scholarship, and Eligible for Graduation) in a single processing pass.
- **Backward Chaining** proved superior for targeted verification. When the system was given a specific goal query (e.g., verifying if a blocked senior can graduate), the engine selectively checked only the sub-conditions required for that rule, ignoring irrelevant rules like the Dean's List criteria.

## How to Run the Program
1. Clone the repository and navigate to the project directory.
2. Open the directory within VS Code.
3. Launch the `reasoning_engine.ipynb` notebook.
4. Execute the cell. The system will automatically generate the JSON knowledge base and process the three sample profiles.

## Sample Inputs and Outputs
**Input:** GPA = 3.8, Attendance = 90%, No Disciplinary Cases, Completed Prerequisites, No Outstanding Fees
**Output (Forward Chaining Explanation Facility):**
- ✓ Eligible for Scholarship because: No Disciplinary Cases, Attendance > 80%, GPA > 3.5
- ✓ Eligible for Graduation because: No Outstanding Fees, Completed Prerequisite Courses, GPA > 3.0
- ✓ Dean's List Candidate because: Attendance > 80%, GPA > 3.5

## Screenshots
Screenshots demonstrating the system processing three distinct test profiles are available in the `/screenshots/` directory.