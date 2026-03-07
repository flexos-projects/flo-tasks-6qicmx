---
id: "project-organisation"
title: "Project Organisation"
type: "feature"
status: "draft"
priority: "P1"
description: "Enable users to group tasks into projects with custom attributes and track progress."
tags: ["projects", "task-management", "organisation"]
createdAt: "2026-03-07"
updatedAt: "2026-03-07"
---

---
id: project-organisation
title: Project Organisation
type: feature
status: draft
description: Enable users to group tasks into projects with custom attributes and track progress.
tags:
  - projects
  - task-management
  - organisation
relatesTo: []
---

### Overview
This feature introduces project management capabilities to flo-tasks, allowing users to group related tasks into distinct projects. Each project will have a set of attributes including a name, description, status, and a customizable color. Project progress will be automatically calculated based on the completion status of its constituent tasks. Users will also be able to assign team members to projects, facilitating better collaboration and visibility.

### User Stories
*   **As a project manager,** I want to create a new project with a name, description, status, and color, so I can organize related tasks effectively.
*   **As a project manager,** I want to assign existing tasks to a project, so all relevant work is grouped together.
*   **As a project manager,** I want to view a project's overall progress percentage, calculated from its tasks, so I can quickly understand its current state.
*   **As a project manager,** I want to assign team members to a project, so everyone involved knows their responsibilities and can easily access project-related information.
*   **As a team member,** I want to see which project each of my tasks belongs to, so I can prioritize my work within the broader project context.
*   **As a team member,** I want to filter my tasks by project, so I can focus on specific project deliverables.
*   **As a project manager,** I want to edit a project's details (name, description, status, color, members), so I can keep project information up-to-date.
*   **As a project manager,** I want to archive or delete a project, so I can manage my list of active projects.

### Requirements

<flex_block type="requirements">
#### Functional Requirements
*   **F1: Project Creation:** Users must be able to create a new project with the following attributes:
    *   Name (required, string, max 100 chars)
    *   Description (optional, string, max 500 chars)
    *   Status (dropdown: Not Started, In Progress, Completed, On Hold, Cancelled) - default to 'Not Started'.
    *   Color (color picker: selection from a predefined palette or hex code input)
    *   Team Members (multi-select from existing flo-tasks users)
*   **F2: Task-Project Assignment:** Users must be able to assign one or more tasks to a project.
    *   A task can belong to only one project at a time.
    *   Tasks can be unassigned from a project.
*   **F3: Project Progress Calculation:** The system must automatically calculate a project's progress percentage.
    *   `Progress = (Number of Completed Tasks / Total Number of Tasks in Project) * 100`.
    *   If a project has no tasks, its progress should be 0%.
*   **F4: Project Viewing:** Users must be able to:
    *   View a list of all projects, displaying their name, status, color, and progress.
    *   View detailed project information, including name, description, status, color, assigned members, and a list of associated tasks.
*   **F5: Project Editing:** Users with appropriate permissions must be able to edit all attributes of an existing project (name, description, status, color, team members).
*   **F6: Project Filtering/Sorting:** Users must be able to filter tasks by project and sort projects by name, status, or progress.
*   **F7: Project Deletion/Archiving:** Users with appropriate permissions must be able to delete or archive a project.
    *   Archiving moves the project to an 'Archived' state, hiding it from default views but retaining its data.
    *   Deleting permanently removes the project and unassigns all associated tasks from it.
</flex_block>

<flex_block type="requirements">
#### Non-Functional Requirements
*   **NFR1: Performance:** Project progress calculation should not introduce noticeable latency when viewing projects or updating task statuses.
*   **NFR2: Usability:** The user interface for creating, editing, and viewing projects and assigning tasks should be intuitive and easy to use.
*   **NFR3: Security:** Only authorized users (e.g., project creators, assigned project managers) should be able to edit or delete projects. Team members can view assigned projects and tasks.
</flex_block>

### Acceptance Criteria

*   **AC1: Project Creation:**
    *   Given I am on the "Create Project" screen, when I fill in all required fields and click "Save", then a new project is created with the specified details.
    *   Given I am on the "Create Project" screen, when I omit the project name, then an error message is displayed, and the project is not created.
    *   Given I create a project with no tasks, then its progress percentage is displayed as 0%.
*   **AC2: Task Assignment:**
    *   Given I have a task and a project, when I assign the task to the project, then the task's details reflect its project assignment, and the project's task list includes the task.
    *   Given I have a task assigned to Project A, when I try to assign it to Project B, then the task is moved from Project A to Project B.
*   **AC3: Progress Calculation:**
    *   Given a project has 5 tasks, and 2 of them are marked as "completed", then the project's progress percentage is displayed as 40%.
    *   Given a project has 10 tasks, and all 10 are marked as "completed", then the project's progress percentage is displayed as 100%.
    *   Given a project has no tasks, then its progress percentage is displayed as 0%.
*   **AC4: Project Viewing:**
    *   Given I navigate to the "Projects List" page, then I see a list of all active projects, each showing its name, status, color, and progress percentage.
    *   Given I click on a project from the list, then I am taken to the project's detail page, showing its full description, assigned members, and a list of its tasks.
*   **AC5: Project Editing:**
    *   Given I am an authorized user, when I edit a project's name, description, status, color, or assigned members, then the changes are saved and reflected across the application.
*   **AC6: Project Deletion/Archiving:**
    *   Given I am an authorized user, when I choose to archive a project, then it disappears from the active projects list but can be found in an "Archived Projects" view.
    *   Given I am an authorized user, when I choose to delete a project, then a confirmation dialog appears, and upon confirmation, the project is permanently removed, and its associated tasks are unassigned.

### Edge Cases

*   **No tasks in a project:** Project progress should be 0%.
*   **All tasks completed in a project:** Project progress should be 100%.
*   **Project with only one task:** Progress calculated correctly (0% or 100% depending on task status).
*   **No team members assigned to a project:** The team members section should indicate no members or be empty, not break the display.
*   **Attempting to assign a task to a non-existent project:** Prevented by UI (e.g., dropdown selection).
*   **Deleting a user who is a project member:** The user should be removed from the project's member list. If the user was the project creator, ownership might need to be transferred or the project remains creator-less.
*   **Project name duplication:** Allow multiple projects to have the same name, as they will be uniquely identified by an internal ID.
*   **Exceeding character limits:** Input fields for name and description should enforce max length on both client and server sides.
*   **Permissioning for editing/deleting:** Only specific roles (e.g., project creator, designated project manager) should be able to perform these actions.
*   **Archiving/Deleting a project with active tasks:** Tasks associated with an archived project remain assigned to that project but the project is hidden from default views. Tasks associated with a deleted project are unassigned from that project.

### Dependencies
*   **Task Management Core:** Existing functionality for creating, viewing, editing, and completing tasks.
*   **User Management:** Ability to manage users and roles within flo-tasks, especially for assigning team members to projects.
*   **UI Component Library:** Reusable components for dropdowns, color pickers, multi-selects, etc.
