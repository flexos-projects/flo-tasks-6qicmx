---
id: "team-collaboration-v1"
title: "Team Collaboration"
type: "feature"
status: "draft"
priority: "P1"
description: "Enable users to invite team members, assign roles, comment on tasks, and receive in-app notifications."
tags: ["collaboration", "team", "invitations", "roles", "notifications", "comments"]
createdAt: "2026-03-07"
updatedAt: "2026-03-07"
---

---
id: team-collaboration-v1
title: Team Collaboration
type: feature
status: draft
description: Enable users to invite team members, assign roles, comment on tasks, and receive in-app notifications.
tags:
  - collaboration
  - team
  - invitations
  - roles
  - notifications
  - comments
relatesTo: []
createdAt: 2023-10-27T10:00:00Z
updatedAt: 2023-10-27T10:00:00Z
---

# Team Collaboration

## Overview
This feature introduces essential team collaboration capabilities to flo-tasks, allowing users to build and manage teams effectively. It will enable users to invite colleagues, define their access levels through roles, facilitate communication directly on tasks via comments, and ensure team members stay informed through real-time in-app notifications for relevant events.

## User Stories
*   As a team owner, I want to invite new members to my workspace by email so they can collaborate on tasks.
*   As a team owner, I want to assign different roles (Owner, Admin, Member) to team members so I can control their access and permissions within the workspace.
*   As a team member, I want to comment on tasks so I can provide updates, ask questions, or offer feedback directly where the work happens.
*   As a team member, I want to receive in-app notifications when I am mentioned in a comment so I don't miss important direct communication.
*   As a team member, I want to receive in-app notifications when a task I'm assigned to or following changes status so I stay informed about progress and critical updates.

## Requirements
<flex_block type="requirements">
*   **Team Invitation:** Users with 'Owner' or 'Admin' roles must be able to invite new members to their workspace via email address.
*   **Role Management:** The system must support at least three distinct roles: Owner, Admin, and Member, each with defined permissions.
*   **Task Commenting:** Users must be able to add text-based comments to individual tasks.
*   **@Mentions:** The commenting system must support `@mentioning` other team members within comments, triggering a notification.
*   **In-app Notifications:** The system must provide an in-app notification center or feed.
*   **Notification Triggers:** Notifications must be triggered for `@mentions` and for changes in task status (e.g., assigned, unassigned, due date changed, completed, re-opened).
*   **Access Control:** Permissions for creating, editing, and deleting tasks, and managing team members must be enforced based on assigned roles.
</flex_block>

## Acceptance Criteria

### Team Invitation
*   An 'Owner' or 'Admin' can access an "Invite Members" interface.
*   The interface allows entering one or more valid email addresses.
*   Upon invitation, an email is sent to the provided address with a link to join the team.
*   The invited user appears in the team's member list with a 'Pending' status until they accept the invitation.
*   If the invited email is already a flo-tasks user, they are prompted to join the team directly upon accepting the invite.
*   If the invited email is not a flo-tasks user, they are prompted to create an account before joining the team.
*   'Owners' and 'Admins' can resend or revoke pending invitations.

### Role Management
*   Roles available are: Owner, Admin, Member.
*   **Owner:** Can invite/remove members, assign/change all roles (except transfer primary ownership to another user), create/edit/delete all tasks, manage workspace settings.
*   **Admin:** Can invite/remove members, assign/change 'Admin' and 'Member' roles, create/edit/delete all tasks.
*   **Member:** Can create their own tasks, edit/delete their own tasks, comment on any task, view all tasks in the workspace.
*   An 'Owner' can change the role of any 'Admin' or 'Member'.
*   An 'Admin' can change the role of any 'Member'.
*   A user cannot change their own role.
*   The primary 'Owner' role cannot be removed or demoted by an 'Admin'.

### Task Commenting
*   A dedicated section for comments is visible on the task detail view.
*   Users can type and submit comments, which are displayed chronologically.
*   Each comment shows the author's name and a timestamp.
*   The comment input field supports `@mentioning` team members by typing `@` followed by their name/username, displaying a suggestion list.
*   Submitting a comment with an `@mention` successfully sends an in-app notification to the mentioned user(s).

### In-app Notifications
*   A notification icon (e.g., bell) is visible in the application's header.
*   A badge counter on the notification icon indicates the number of unread notifications.
*   Clicking the notification icon opens a notification feed or panel.
*   Each notification entry clearly states the event (e.g., "[User] mentioned you in [Task Name]", "[Task Name] status changed to [New Status]").
*   Clicking a notification navigates the user directly to the relevant task or comment.
*   Notifications are cleared from the 'unread' count upon viewing the notification feed or navigating to the associated item.

## Edge Cases
*   **Inviting Existing User:** If an invited user already has a flo-tasks account, they should be prompted to join the team directly without creating a new account.
*   **Invalid Email:** The invitation system should validate email formats and provide appropriate error messages for invalid inputs.
*   **Team Ownership Transfer:** What happens if the sole 'Owner' leaves the team or wishes to transfer ownership? (Requires a dedicated workflow).
*   **Deleting a Member:** When a member is removed, their comments remain, attributed to their name, possibly marked as 'Former Member'. Their assigned tasks need to be unassigned or reassigned.
*   **User Without Team:** A new user who creates an account without an invitation starts with their own private workspace (or is prompted to create one).
*   **Mentions of Non-Existent Users:** If a user attempts to `@mention` a non-existent or invalid user, the system should indicate the mention is invalid and not send a notification.
*   **Maximum Team Members:** Consider limits if applicable (e.g., for free tiers).
*   **Offline Experience:** How notifications are handled if a user is offline when an event occurs (queued and delivered upon reconnection).

## Dependencies
*   **User Authentication & Authorization System:** Core user accounts and permissions are required.
*   **Email Sending Service:** For sending invitation emails.
*   **Task Management Core Features:** Existing functionality for creating, editing, assigning, and changing the status of tasks.
*   **Real-time Communication Infrastructure:** For immediate delivery of in-app notifications (e.g., WebSockets for push notifications).