Technical Report – Don’t Forget
NFC-Based Reminder System with Power Apps and Power Automate
1. Introduction
This document is the final technical report for the Don’t Forget project, developed within the scope of the Project Planning and Management course of the 1st year of the Entrepreneurship programme at ISCTE – Instituto Universitário de Lisboa, 2nd semester of 2023/2024.

The project consists of a cross-platform low-code solution designed to help users ensure that essential items are not forgotten when leaving home. The system integrates a Power Apps application, Power Automate automation flows, an NFC sensor simulator, and data persistence through Dataverse and Excel tables.

The team, composed of seven members, applied the SCRUM methodology across four sprints, with task management supported by Jira.

2. Context and Objectives
Don’t Forget was conceived to address a concrete daily need: verifying that all essential objects — such as a laptop, calculator, wallet, or keys — are carried by the user. The developed solution allows users to:

Create an account and authenticate in the application;

Manage customisable lists of objects;

Associate NFC tags with each item;

Consult reading history;

Receive automatic notifications when an object is not detected.

The project followed an iterative and incremental approach, with four sprints that progressively refined the application, automation flows, and hardware simulation.

3. System Architecture
The system architecture is based on four main components:

Component	Description
Power Apps	User interface for account creation, list management, NFC tag association, and reading history.
Power Automate	Automation flow that processes NFC readings, updates tables, triggers notifications, and resets states.
NFC Sensor Simulator	Emulates hardware behaviour by sending HTTP requests with reading data.
Dataverse / Excel	Data persistence: lists, items, reading history, and user accounts.
The high-level flow is as follows:

The simulator sends an HTTP request with the NFC tag data;

Power Automate identifies the tag and updates the reading history;

The flow checks whether any items remain unread;

If so, it retrieves the user’s email and sends a notification via Outlook;

The flow waits 30 seconds and resets the reading states;

The system is ready for the next cycle.

4. Development Methodology
The team adopted the SCRUM methodology, with four distinct sprints:

Sprint 1 and 2 (initial phases) – Establishment of the product foundation: usability, hardware operation, tag recognition, and error reduction.

Sprint 3 (22/03 – 05/05) – Focus on application programming (account creation, password recovery, reading history), hardware configuration, and notification implementation. The user story “Add tag” was moved to the following sprint.

Sprint 4 (06/05 – 19/05) – Finalisation and full testing. Interface polishing, security and language improvements, hardware assembly, bug fixing, and preparation of the final presentation.

Task distribution was carried out according to each member’s degree and skills. Daily meetings took place weekly via WhatsApp, complemented by sprint reviews and retrospectives.

5. Technical Implementation
5.1 Power Apps – Main Screens
Home Screen: logo, options to create an account, log in, and recover password.

Dashboard: access to list management, profile, reading history, settings, and quick list creation.

List Management: creation, editing, search, activation/deactivation, and deletion of lists.

Reading History: chronological record of NFC readings with date and time.

Expansion Screen: installation guide, terms and conditions, FAQs, and notifications.

5.2 Power Automate – Flow Logic
The flow consists of eleven sequential steps:

Request – Receives data via HTTP from the simulator;

Tag reception – Identifies the item in the table;

Reading timestamp addition – Registers the reading in the history table;

State update – Item marked as L1 (read);

State listing – Checks for items N1/N2/N3 (not read);

Condition – Checks whether any objects remain unread;

Condition True (part 1) – Retrieves the email list via Dataverse;

Condition True (part 2) – Sends notification email via Outlook;

Condition False – Performs no action, continues the flow;

Delay – 30-second delay for stabilisation;

Reset – Resets reading states to not read.

5.3 Hardware Simulator
The NFC sensor simulator continuously attempts to detect a tag. If no tag is detected, it keeps trying; if a tag is detected, it sends the data to the URL configured in Power Automate. The configuration file simulacao_leitor_NFC.json accompanies the project.

6. Results and Demonstration
The final product meets all defined requirements:

Functional application with account creation, login, and password recovery;

Complete management of lists and items with NFC tag association;

Reading history with date and time;

Operational automation flow with email notifications;

Configured and integrated hardware simulator.

Demonstration video link:
https://youtu.be/m0EsdiDIDmU
Delivered files:

DontForget.msapp – Power Apps application export;

flow_definition.json – Power Automate flow definition;

simulacao_leitor_NFC.json – NFC simulator configuration;

Architecture diagrams and flowcharts.

7. Team Contributions
Name	Technical Contribution	Management Contribution
Ilie Iftime	Hardware implementation, Power Apps corrections, application development	Product Owner
Rafael Tavares	Simulator features, Jira planning support, logo creation	Scrum Master
Sara Pereira	Power Apps application development	—
Carolina Sousa	Reports	—
Patrícia Silva	D1 and D4 reports, sprint planning/update in Jira	—
David Ferreira	Reports	—
Martim Sargo	Did not perform or attend classes	Did not perform or attend classes
8. Final Assessment
The SCRUM methodology proved suitable for the interdisciplinary nature of the project, enabling rapid identification of obstacles and incremental delivery of value. The Jira tool facilitated backlog management and task coordination.

The developed product exceeded the team’s initial expectations, meeting the client’s requirements and providing the members involved with technical and methodological skills relevant to future projects.

Group work benefited from the diversity of skills, although the absence of one member placed additional pressure on the others. Overall, the experience was positive, combining learning in project development with the practical application of an agile methodology.

9. Repository Structure
text
/powerapps/
    DontForget.msapp
/powerautomate/
    flow_definition.json
/simulator/
    simulacao_leitor_NFC.json
/docs/
    architecture_diagrams/
    screenshots/
README.md
10. Installation and Usage
Power Apps:

Import the .msapp file;

Configure connections to Dataverse or Excel;

Publish and run the application.

Power Automate:

Import the flow JSON;

Update connections (Excel, Dataverse, Outlook);

Set the HTTP trigger URL in the NFC simulator.

Simulator:

Load the JSON configuration;

Set the correct HTTP endpoint;

Run the simulation to send NFC readings.

Document prepared for academic purposes – ISCTE, Project Planning and Management, 2nd Semester 2023/2024.

