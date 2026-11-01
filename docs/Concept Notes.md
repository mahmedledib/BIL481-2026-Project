KidsCode  
Arjen Tüysüz  
Mohamed Ahmed Ledib

## **1\. Project Name**

KidsCode

## **2\. Short Description**

KidsCode is a global, multi-lingual learning platform designed to teach K-12 students programming through interactive Blockly and Python puzzles. What sets KidsCode apart is its aggressive optimization for low-bandwidth use and a deep structural focus on empowering schools, parents, and teachers. Hosted entirely online using Cloudflare Workers and D1, it seamlessly supports both Left-To-Right (LTR) and Right-To-Left (RTL) layouts so children worldwide can learn in their native languages. The platform manages complex user relationships and organizes its curriculum strictly into a Course \> Lesson \> Level \> Stop hierarchy.

## **3\. Requirements**

R1: Implement full internationalization (i18n) with dynamic switching between Left-To-Right (LTR) and Right-To-Left (RTL) UI layouts. Specifically, ensure that the code editor direction follows the chosen programming language, not the site language (e.g., an RTL programming language results in an RTL code editor even on an LTR site).  
R2: Structure all educational content into a strict, fixed hierarchy (Course \> Lesson \> Level \> Stop) and enforce server-side validation to refuse access or data retrieval for locked content.  
R3: Integrate Blockly for drag-and-drop visual programming for beginners, and provide a Python text editor environment for advanced coding puzzles.  
R4: Execute user code securely on the client-side using WebAssembly (Pyodide) in the browser's main thread to minimize server load.  
R5: Implement a behavior-based grading system on a 0-100 scale that continuously updates and persistently stores the highest score achieved for each Stop.  
R6: Deploy the platform and backend API using Cloudflare Workers for fast serverless execution, utilizing Cloudflare D1 (Serverless SQL) to store curriculum data and progress tracking.  
R7: Optimize frontend payload size using plain TypeScript with no framework, employing heavy lazy-loading for assets like Pyodide to support low-bandwidth environments.  
R8: Implement Role-Based Access Control (RBAC) accommodating distinct Student, Parent, Teacher, Manager, and Admin accounts.  
R9: Implement an authentication flow where Parents log in using a phone number and password, allowing Students to select their individual profiles under the active parent session.  
R10: Allow a single class/cohort to have multiple assigned users in the Teacher role (e.g., main teacher and secondary/co-teachers).

## **4\. Simple Pseudocode for Implementation Parts**

function loadStop(courseId, lessonId, levelId, stopId, siteLanguage, programmingLanguage):  
    siteLayoutDirection \= getLanguageDirection(siteLanguage)  
    applySiteLayout(siteLayoutDirection) // code editor follows the programming language, not the site: applyEditorLayout(getLanguageDirection(programmingLanguage))  
    stopData \= fetchFromD1Worker(courseId, lessonId, levelId, stopId) // Worker API  
    if stopData.isLocked:  
        return displayError("Course/Stop is locked.")  
    if stopData.format \== "blockly":  
        renderBlocklyInterface(stopData)  
    else:  
        renderPythonInterface(stopData) // lazy-loads Pyodide only here  
function executeCode(userCode, languageType):  
    if languageType \== "blockly":  
        pythonCode \= convertBlocklyToPython(userCode)  
    else:  
        pythonCode \= userCode  
    result \= runInSecureSandbox(pythonCode)  
    score \= calculateBehaviorScore(result, currentStop)  
    saveHighestScore(currentStop.id, score) // keeps best score  
    return validateResult(result, currentStop.expectedOutput)

## **5\. Sample Views**

Student Dashboard: Displays enrolled Courses, current Lesson progress, and accessible Levels/Stops in a visually engaging interface. Unreached content is visibly locked.  
Teacher/Parent Dashboard: Displays linked student metrics, showing completion rates, best scores (0-100), and identifying specific Stops where students are struggling. Secondary teachers share the same view for their assigned cohorts.  
Admin/Manager Console: Interface for managing user role assignments, assigning co-teachers to classes, creating new Courses/Lessons, and monitoring platform-wide metrics.  
Puzzle Workspace (The "Stop"): Features the block library or Python editor, central workspace, and execution terminal. The general UI dynamically flips sides based on the site's RTL/LTR language setting, while the code editor orientation specifically locks to the chosen programming language.  
Login View: A dual-step screen where the Parent first logs in with a phone number and password, followed by a profile-selection screen where the Student clicks their avatar to begin learning.

## **6\. Sample Design Information**

Frontend Architecture: Plain TypeScript with no framework to minimize payload size. The platform is strictly online-only; there is no offline mode and no offline saving for workspace drafts. To preserve bandwidth, the WebAssembly runtime (Pyodide) is heavily lazy-loaded and will only be fetched when a student explicitly opens a Python-based Stop.  
Backend & API: Cloudflare Workers to handle user authentication (including parent phone/password logins), role-based routing, server-side progression validation, and low-latency API calls directly from the edge.  
Database: Cloudflare D1 (Serverless SQLite) to store the RBAC model (Users, Roles) and Content hierarchy. The architecture will use a single global database without sharding, as the 10 GB limit is sufficient for storing scores, metadata, and many-to-many teacher/class relationships.  
Code Execution Sandbox: Client-side execution using WebAssembly (Pyodide) to run Python code directly in the browser's main thread (no Web Workers will be used).  
Curriculum Structure & Flexibility: Educational content strictly adheres to the Course \> Lesson \> Level \> Stop progression with no open-ended "playground" areas. However, the database design remains flexible to ensure teacher-generated content (e.g., custom Stops or localized puzzles) can be seamlessly integrated in the future without requiring major architectural changes.

## **7\. Scenarios**

Scenario 1: Content Progression & Validation  
User: Parent and Student.  
Goal: Access and complete the next Python puzzle.  
Steps: The parent logs in on a tablet using their phone number and password (R9). The student selects their profile and attempts to access a future lesson, but the server explicitly refuses the request (R2). They navigate to their current Python Stop instead (R3). The platform lazy-loads Pyodide to save bandwidth (R7). The student writes Python code, which is executed securely on their local machine's main thread (R4).  
Outcome: The system evaluates their behavioral approach and updates their profile with a new best score of 85, replacing their previous 70 (R5).  
Scenario 2: RTL Interface Switch with Programming Language Check  
User: Arabic-speaking Student learning an LTR programming language.  
Goal: Complete a Blockly puzzle in their native language.  
Steps: The student selects Arabic for the site language. The platform dynamically mirrors the general UI (dashboard, instructions, block library placement) to an RTL layout. However, because the selected programming language is LTR, the code editor remains LTR (R1). The student solves the puzzle using visual blocks (R3).  
Outcome: The student experiences a fully localized, native navigation interface while the code editor keeps the orientation of the chosen programming language (R1), powered by a lightweight plain TypeScript frontend (R7).  
Scenario 3: Role & Content Management  
User: Manager, Main Teacher, and Secondary Teacher.  
Goal: Assign a new course and monitor classroom performance.  
Steps: A Manager uses the admin console to assign a newly created Course to a specific class (R8) and assigns a secondary teacher to help moderate (R10). Both the main and secondary teachers log into their dashboards (R8).  
Outcome: Both teachers view shared metrics showing exactly which Stop a specific student is stuck on, while the D1 database and Workers API handle the data routing seamlessly on the edge (R6).